# REST-API bloček

**Později bude upraveno, zatím jenom slouží jako záloha**

```javascript
const digitalInputsCount  = 0;
const analogInputsCount   = 0;

const sendWhenOptions = {
    trigger: 'Trigger',
    input_changed: 'Input changed'
};

// init inputs
let trigger = context.inputs.add('trigger', 'digital', 'Send trigger');

for (let d = 1; d <= digitalInputsCount; d++) {
    context.inputs.add('din' + d, 'digital', 'Digital input #' + d);
}

for (let a = 1; a <= analogInputsCount; a++) {
    context.inputs.add('ain' + a, 'analog', 'Analog input #' + a);
}

// init outputs
let response = context.outputs.add('response', 'message', 'Response', ['integer', 'string', 'string']);

// init config properties
context.configProperties.description = `
There is **2 variants for trigger** sending request:

* **Trigger** - sends request when *trigger* input changes from **false** to **true**
* **Input changed** - sends request immedietly or after **debounce time** when any of *din1* - *din${digitalInputsCount}* or *ain1* - *ain${analogInputsCount}* changes value

In **URL**, **Headers** and **Request body** fields you can use following *micro*template syntax:

* \`<% din1 %>\` - will be replaced with bool value of *din1* (**true** or **false**)
* \`<% ain4 %>\` - will be replaced with numberic value of *ain4* input
* \`<% din2?"yes":"no" %>\` - will be replaced with bool value of *din2* (**yes** or **no**)
* \`<% if (din3 == true) { %> "open": true <% } %>\` - inserts **"open": true** only if value of *din3* input is **true**

---
`;

let sendWhen = context.configProperties.add('sendWhen', 'string', 'Send when', sendWhenOptions.trigger, {
    options: [sendWhenOptions.trigger, sendWhenOptions.input_changed]
});
let sendDebounceTime = context.configProperties.add('sendDebounceTime', 'integer', 'Send debounce time (in ms)', 200, {
    min: 0,
    max: 60000
});
let url = context.configProperties.add('url', 'string', 'URL', 'http://example.com/');
let method = context.configProperties.add('method', 'string', 'Method', 'POST', {
    options: ['GET', 'POST', 'PUT', 'DELETE', 'HEAD', 'OPTIONS']
});
let headers = context.configProperties.add('headers', 'string', 'Headers (one per line)', '', {
    multiline: true
});
let body = context.configProperties.add('body', 'string', 'Request body', '', {
    multiline: true
});


// inspired by https://github.com/krasimir/absurd/blob/master/lib/processors/html/helpers/TemplateEngine.js
let TemplateEngine = (template, options) => {
    var re = /<%(.+?)%>/g, 
        reExp = /(^( )?(var|if|for|else|switch|case|break|{|}|;))(.*)?/g, 
        code = 'with(obj) { var r=[];\n', 
        cursor = 0, 
        result,
            match;
    var add = function(line, js?) {
        js? (code += line.match(reExp) ? line + '\n' : 'r.push(' + line + ');\n') :
            (code += line != '' ? 'r.push("' + line.replace(/"/g, '\\"') + '");\n' : '');
        return add;
    }
    while(match = re.exec(template)) {
        add(template.slice(cursor, match.index))(match[1], true);
        cursor = match.index + match[0].length;
    }
    add(template.substr(cursor, template.length - cursor));
    code = (code + 'return r.join(""); }').replace(/[\r\t\n]/g, ' ');
    try { result = new Function('obj', code).apply(options, [options]); }
    catch(err) { console.error("'" + err.message + "'", " in \n\nCode:\n", code, "\n"); }
    return result;
}

// main send request function
let sendRequest = () => {

    let data = {};

    for (let d = 1; d <= digitalInputsCount; d++) {
        data['din' + d] = context.inputs.get<DigitalInputConnector>('din' + d).value;
    }
    for (let a = 1; a <= analogInputsCount; a++) {
        data['ain' + a] = context.inputs.get<AnalogInputConnector>('ain' + a).value;
    }

    let newUrl = TemplateEngine(url.value, data);
    let newHeaders = TemplateEngine(headers.value, data);
    let newBody = TemplateEngine(body.value, data);

    console.warn(`Do ${method.value} request to ${newUrl} with headers:\n ${newHeaders} and body:\n ${newBody} `);

    let request: RequestDef = null;
    if (method.value == 'GET') {
        request = new GetRequest(newUrl);
    } else if (method.value == 'POST') {
        request = new PostRequest(newUrl);
    } else if (method.value == 'PUT') {
        request = new PutRequest(newUrl);
    } else if (method.value == 'DELETE') {
        request = new DeleteRequest(newUrl);
    } else if (method.value == 'HEAD') {
        request = new HeadRequest(newUrl);
    } else if (method.value == 'OPTIONS') {
        request = new OptionsRequest(newUrl);
    }

    request.headers = newHeaders;
    request.body = newBody;

    services.fetchService.fetch(request)
    .then((res: FetchResponse) => {
        const message = [200, JSON.stringify(res.headers), JSON.stringify(res.body)];
        response.send(message);
        console.info('Response [' + newUrl + ', ' + res.status + ']');
    }).catch((e: Error) => {
        console.error(e);
    });

};

trigger.listenEvent('valueChanged', () => {
    if (trigger.value && sendWhen.value == sendWhenOptions.trigger) {
        console.info('Now send! [trigger]');
        sendRequest();
    }
});

let debounceTimeout = null;

context.inputs.listenEvent('valueChanged', (event) => {
    if (event.target.name != 'trigger') {
        if (sendWhen.value == sendWhenOptions.input_changed) {
            if (sendDebounceTime.value == 0) {
                console.info('Now send! [input_changed]');
                sendRequest();
            } else {
                clearTimeout(debounceTimeout);
                debounceTimeout = setTimeout(() => {
                    console.info('Now send! [input_changed_debounced]');
                    sendRequest();
                }, sendDebounceTime.value)
            }
        }
    }
});
```

