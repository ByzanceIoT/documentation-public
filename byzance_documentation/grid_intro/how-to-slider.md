tož do kédu pastneme toto  
  
/\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

 \* 

 \* Widget components

 \* 

 \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/



/\*\*

 \* 

 \* 

 \* Slider component

 \* 

 \*/

class Slider {

    protected \_emitter: WK.Emitter&lt;WK.Event&gt;;

    protected \_rootView: WK.View;

    protected \_backgroundElement: WK.View;

    protected \_valueElement: WK.Element;

    protected \_buttonElement: WK.Button;

    protected \_reversed: boolean = false;



    protected \_moving = false;

    protected \_movingOffset = 0;

    protected \_value = 0;



    constructor\(context: WidgetContext\) {

        this.\_emitter = new WK.Emitter&lt;WK.Event&gt;\(\);

        this.\_rootView = new WK.View\(context\);

        this.\_rootView.style.padding = "22px";

        this.\_rootView.style.background = "transparent";



        this.\_backgroundElement = new WK.View\(context\);

        this.\_backgroundElement.style.background = "\#838383";

        this.\_backgroundElement.style.height = "10px";

        this.\_backgroundElement.style.y = "-3px";

        this.\_backgroundElement.style.width = "100%";

        this.\_backgroundElement.style.radius = "5px";

        this.\_rootView.add\(this.\_backgroundElement\);



        this.\_valueElement = new WK.Element\(context\);

        this.\_valueElement.style.background = "\#2274ff";

        this.\_valueElement.style.height = "10px";

        this.\_valueElement.style.y = "0";

        this.\_valueElement.style.width = "0";

        this.\_valueElement.style.radius = "0";

        this.\_backgroundElement.add\(this.\_valueElement\);



        this.\_buttonElement = new WK.Button\(context,""\);

        this.\_buttonElement.style.width = "30px";

        this.\_buttonElement.style.height = "30px";

        this.\_buttonElement.style.x = "0";

        this.\_buttonElement.style.y = "2px";

        this.\_buttonElement.style.radius = "15px"

        this.\_buttonElement.style.border = "\#FFFFFF 5px";

        this.\_buttonElement.style.background = "\#2274ff";

        this.\_buttonElement.style.shadow = "\#000000 30px 0 0";

        this.\_buttonElement.style.originX = "0.5";

        this.\_buttonElement.style.originY = "0.5";

        this.\_rootView.add\(this.\_buttonElement\);



        this.\_buttonElement.listenEvent\("mousedown",this.onButtonMouseDown\);

        this.\_backgroundElement.listenEvent\("mousedown",this.onBackgroundMouseDown\);

        context.root.listenEvent\("appmouseup",this.onAppMouseUp\);

        context.root.listenEvent\("appmousemove",this.onAppMouseMove\);

    }



    /\*\*

     \* 

     \* Get value of this slider

     \* 

     \*/

    public get value\(\): number {

        return this.\_value;

    }



    /\*\*

     \* 

     \* Set value of slider

     \* 

     \*/

    public set value\(value: number\) {

        this.internalSetValue\(value\);

        this.\_emitter.emit\(this, new WK.Event\("valueChanged"\)\);

    }



    /\*\*

     \* 

     \* Get root view from this slider

     \* 

     \*/

    public get rootElement\(\): WK.View {

        return this.\_rootView;

    }



    /\*\*

     \* 

     \* Get button element

     \* 

     \*/

    public getButtonElement\(\): WK.Button {

        return this.\_buttonElement;

    }



    /\*\*

     \* 

     \* Get background element

     \* 

     \*/

    public getBackgroundElement\(\): WK.View {

        return this.\_backgroundElement;

    }



    /\*\*

     \* 

     \* Get value bar element

     \* 

     \*/

    public getValueBarElement\(\): WK.Element {

        return this.\_valueElement;

    }



    /\*\*

     \* 

     \* Listen value change event

     \* 

     \*/

    public listenEvent\(key: "valueChanged" , callback: \(event: WK.Event\) =&gt; void\): WK.Listener&lt;WK.Event&gt; {

        return this.\_emitter.listenEvent\(key, callback\);

    }



    /\*\*

     \* 

     \* Set slider reversed \(right down to left\) or not \(left to right\)

     \* 

     \*/

    public setReversed\(reversed: boolean\) {

        if \(this.\_reversed != reversed\) {

            this.\_reversed = reversed;



            if \(this.\_reversed\) {

                this.\_valueElement.style.originX = "1";

                this.\_valueElement.style.x = "100%";

            } else {

                this.\_valueElement.style.originX = "0";

                this.\_valueElement.style.x = "0";

            }

            this.internalSetValue\(this.\_value\);

        }

    }



    /\*\*

     \* 

     \* Enable or disable shadow property

     \* 

     \*/

    public enableShadow\(enabled: boolean\) {

        if \(!enabled\) {

            this.getButtonElement\(\).style.shadow = "none";

        } else {

            this.getButtonElement\(\).style.shadow = "\#000000 30px 0 0";

        }

    }



    /\*\*

     \* 

     \* Enable or disable radius on button and background element

     \* 

     \*/

    public enableRadius\(enabled: boolean\) {

        if \(!enabled\) {

            this.getBackgroundElement\(\).style.radius = "0";

            this.getButtonElement\(\).style.radius = "0";

        } else {

            this.getBackgroundElement\(\).style.radius = "5px";

            this.getButtonElement\(\).style.radius = "15px";

        }

    }



    /\*\*

     \* 

     \* Set color of background

     \* 

     \*/

    public setBackgroundColor\(color: string\) {

        this.getBackgroundElement\(\).style.background = color;

    }



    /\*\*

     \* 

     \* Set color of front

     \* 

     \*/

    public setFrontColor\(color: string\) {

        this.getValueBarElement\(\).style.background = color;

        this.getButtonElement\(\).style.background = color;

    }



    /\*\*

     \* 

     \* Set border of button

     \* 

     \*/

    public setBorder\(color: string, width: number\) {

        if \(width == 0\) {

            this.getButtonElement\(\).style.border = "none";

        } else {

            this.getButtonElement\(\).style.border = color + " " + width + "px";

        }

    }



    /\*\*

     \* 

     \* Return true, if user moving slider

     \* 

     \*/

    public get isMoving\(\): boolean {

        return this.\_moving;

    }



    /\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

     \* 

     \* Protected implementation

     \* 

     \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/



     /\*\*

      \* 

      \* Set internal value without emiting event

      \*

      \*/

     protected internalSetValue\(value: number\) {

         this.\_value = Math.min\(Math.max\(value, 0\), 1\);



        this.\_valueElement.style.width = value \* 100 + "%";



        if \(this.\_reversed\) {

            this.\_buttonElement.style.x = \(1 - value\) \* 100 + "%";

        } else {

            this.\_buttonElement.style.x = value \* 100 + "%";

        }

     }



    /\*\*

     \* 

     \* When user clicks on button

     \* 

     \*/

    protected onButtonMouseDown = \(e\) =&gt; {

        if \(this.\_buttonElement.isHover\) {

            this.\_moving = true;

            this.\_movingOffset = e.mousePosition.x - this.\_buttonElement.visibleRect.position.x;

        }

    }



    /\*\*

     \* 

     \* When user click background element

     \* 

     \*/

    protected onBackgroundMouseDown = \(e\) =&gt; {

        if \(this.\_backgroundElement.isHover && !this.\_buttonElement.isHover\) {

            this.\_movingOffset = this.\_buttonElement.visibleRect.size.width / 2;

            this.setButtonPosition\(e\);

        }

    }



    /\*\*

     \* 

     \* When user release mouse button

     \* 

     \*/

    protected onAppMouseUp = \(e\) =&gt; {

        this.\_moving = false;

    }



    /\*\*

     \* 

     \* When user moving mouse in applicatin

     \* 

     \*/

    protected onAppMouseMove = \(e: WK.MouseEvent\) =&gt; {

        if \(this.\_moving\) {

            this.setButtonPosition\(e\);

        }

    }



    /\*\*

     \* 

     \* Set button position from mouse event

     \* 

     \*/

    protected setButtonPosition\(e: WK.MouseEvent\) {

        const max = this.\_rootView.visibleRect.size.width;

        let newX = Math.min\( Math.max\(e.mousePosition.x - this.\_movingOffset, 0\), max\);

        this.\_value = newX / max;



        if \(this.\_reversed\) {

            this.\_value = 1 - this.\_value;

        }



        this.internalSetValue\(this.\_value\);

        this.\_emitter.emit\(this, new WK.Event\("valueChanged"\)\);

    }

}









/\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

 \* 

 \* Widget code

 \* 

 \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/



/\*

 \* 

 \* 

 \* Widget size profiles

 \* 

 \*/

context.addSizeProfiles\(1,1,50,1\);



/\*

 \*

 \* Widget input configuration

 \*

 \*/

const input = context.inputs.add\("ain","analog","Analog input"\);



/\*

 \*

 \* Widget output configuration

 \*

 \*/

const output = context.outputs.add\("aout","analog","Analog output"\);



/\*

 \* 

 \* Config properties

 \* 

 \*/



const backgroundColorProperty = context.configProperties.add\('backgroundColor','color', 'Color of background', '\#838383'\);

const frontColorProperty = context.configProperties.add\('frontColor','color', 'Color of front', '\#2274ff'\);

const outlineColorProperty = context.configProperties.add\('outlineColor','color', 'Color of border', '\#FFFFFF'\);

const outlineWidthProperty = context.configProperties.add\('outlineWidth','integer', 'Size of border', 5\);

const radiusProperty = context.configProperties.add\('radius','boolean', 'Enable border radius', true\);

const shadowProperty = context.configProperties.add\('shadow','boolean', 'Enable shadow', true\);

const reversedProperty = context.configProperties.add\('reversed','boolean', 'Reversed', false\);



/\*

 \* 

 \* Define widget user interface

 \* 

 \*/



context.enableGlobalMouseEvents\(\);

context.root.style.background = "transparent";



const slider = new Slider\(context\);

slider.rootElement.style.width = "100%";

slider.rootElement.style.height = "100%";

context.root.add\(slider.rootElement\);





function setupSliderFromProperties\(\) {

    slider.enableRadius\(radiusProperty.value\);

    slider.setBackgroundColor\(backgroundColorProperty.value\);

    slider.setFrontColor\(frontColorProperty.value\);

    slider.setBorder\(outlineColorProperty.value, outlineWidthProperty.value\);

    slider.enableShadow\(shadowProperty.value\);

    slider.setReversed\(reversedProperty.value\);

}



setupSliderFromProperties\(\);



/\*

 \* 

 \* 

 \* Values

 \* 

 \*/

slider.listenEvent\("valueChanged", function\(e\) {

    output.value = \(&lt;Slider&gt;e.target\).value;

}\);



input.listenEvent\("valueChanged", function\(e\) {

    if \(!slider.isMoving\) {

        slider.value = input.value;

    }

}\);



/\*

 \* 

 \* Config properties events

 \* 

 \*/

context.configProperties.listenEvent\("valueChanged", setupSliderFromProperties\);

