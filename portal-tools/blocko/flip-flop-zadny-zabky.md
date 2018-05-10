# Flip-flop

```javascript
const digitalInputsCount  = 1;

const output = context.outputs.add('dout', 'digital', 'Digital output');

for (let d = 1; d <= digitalInputsCount; d++) {
    context.inputs.add('din' + d, 'digital', 'Digital input #' + d);
}

let storage: boolean = false;

context.inputs.listenEvent("valueChanged", function(e) {
    if (e.value) {
        storage = !storage;
        output.value = storage;
    }
});
```

