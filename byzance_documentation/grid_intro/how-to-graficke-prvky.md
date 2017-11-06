/\*

 \*

 \* Widget size profiles configuration

 \* 

 \*/

context.addSizeProfiles\(1,1,20,20\);



const input = context.inputs.add\("ain","analog", "Input"\);



/\*

 \*

 \* Widget kit label

 \* 

 \*/

var element = new WK.Element\(context\); 



/\*

 \* define style for this button

 \*/

element.style.background = "\#FFF";

element.style.x = '50%';                                 //  position on x axis - can be in % \(of element width\), or in pixels

element.style.y = '50%';                                 //  position on y axis - can be in % \(of element height\), or in pixels

element.style.width = '100%';                            //  width - can be in % \(of element width\), or in pixels

element.style.height = '100%';                           //  height - can be in % \(of element height\), or in pixels

element.style.originX = '0.5';                           //  origin on x axis, 0 - positioning from left border, 1 - positioning from right border

element.style.originY = '0.5';                           //  origin on y axis, 0 - positioning from top border, 1 - positioning from bottom border



/\*

 \*  Place label into root element of widget

 \*/

context.root.add\(element\);



let dataStorage = \[\];



for\(let i = 0; i &lt; 200; i++\) {

    dataStorage\[i\] = Math.random\(\) \* 100;

}





context.listenEvent\("render", function\(e\) {

    const render:WK.RenderContext = e.context;



    let max = null;

    for\(let i = 0; i &lt; dataStorage.length; i++\) {

        if \(!max \|\| max &lt; dataStorage\[i\]\) {

            max = dataStorage\[i\];

        }

    }



    if \(!max\) {

        max = 0;

    }



    const chartSize = 100;



    const chartPaddingX = 10;

    const chartPaddingY = 10;

    const chartX = 30 + chartPaddingX;

    const chartY = 10 + chartPaddingY;

    const chartWidth = context.root.visibleRect.size.width - chartX - chartPaddingX \* 2;

    const chartHeight = context.root.visibleRect.size.height - chartY - chartPaddingY \* 2;



    render.beginPath\(\);

    let first = true;

    for\(let i = Math.max\(dataStorage.length - chartSize, 0\), j = 0; i &lt; dataStorage.length; i++, j++\) {

        const x = chartX + \(j / chartSize\) \* chartWidth;

        const y = chartY + chartHeight - \(dataStorage\[i\] / max\) \* chartHeight;



        if \(first\) {

            render.moveTo\(x,y\);

        } else {

            render.lineTo\(x,y\);

        }



        first = false;

    }



    render.strokeStyle = "\#489fdf";

    render.stroke\(\);



    for\(let i = Math.max\(dataStorage.length - chartSize, 0\), j = 0; i &lt; dataStorage.length; i++, j++\) {

        const x = chartX + \(j / chartSize\) \* chartWidth;

        const y = chartY + chartHeight - \(dataStorage\[i\] / max\) \* chartHeight;



        render.beginPath\(\);

        render.arc\(x,y,2,0,2\*Math.PI\);

        render.closePath\(\);

        render.strokeStyle = "rgb\(255, 153, 0\)";

        render.stroke\(\);

        render.fillStyle = "rgba\(255, 153, 0, 0.5\)";

        render.fill\(\);

    }



    render.fillStyle = "\#000";



    render.fillText\(\(0\).toString\(\),3,chartY + chartHeight - 3\);

    render.fillText\(\(Math.round\(max\*10\)/10\).toString\(\),3,chartY + 13\);



    render.strokeStyle = "rgba\(0,0,0,0.5\)";



    render.beginPath\(\);

    render.moveTo\(chartX, chartY\);

    render.lineTo\(chartX + chartWidth, chartY\);

    render.stroke\(\);



    render.beginPath\(\);

    render.moveTo\(chartX, chartY + chartHeight\);

    render.lineTo\(chartX + chartWidth, chartY + chartHeight\);

    render.stroke\(\);



    for\(let i = Math.max\(dataStorage.length - chartSize, 0\), j = 0; i &lt; dataStorage.length; i+=10, j+=10\) {

        const x = chartX + \(j / chartSize\) \* chartWidth;



        render.beginPath\(\);

        render.strokeStyle = "rgba\(0,0,0,0.2\)";

        render.setLineDash\(\[5, 15\]\);

        render.moveTo\(x, chartY\);

        render.lineTo\(x, chartY + chartHeight\);

        render.stroke\(\);

    }

}\);



let changedInput = true;





setInterval\(function\(\) {

    //if \(changedInput\) {

        dataStorage.push\(input.value\);

        context.root.invalidate\(\);

        changedInput = false;

    //}

}, 1000\);





input.listenEvent\("valueChanged", function\(e\) {

    changedInput = true;

}\);

