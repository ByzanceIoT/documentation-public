Grid dokáže být až překvapivě tvárný a dají se v něm dělat i složitější věci, doslova od píky.  
  
Co třeba si udělat horizontální slider?

![](/assets/sliderFirst.png)

---

Začneme tím, že si vytvoříme Widget a pojmenujeme si ho Hslider.

Vyjměčně nezačneme s `context.addSizeProfiles` ale s třídou Slider. 

```js
class Slider{


}
```

a přidáme do naší třídy několik promněných pro práci s ní:

```js
class Slider {
    protected _emitter: WK.Emitter<WK.Event>;
    // slouží k tomu, abychom mohli přidat event.listener na tento objekt

    protected _rootView: WK.View; // main element, aby to všechno bylo na co dát (něco jako context.root) pro tuto třídu
    protected _backgroundElement: WK.View; // na celkové podbarvení panelu
    protected _valueElement: WK.Element; // na podbarvení vybrání pod tlačítkem
    protected _buttonElement: WK.Button; // na vytvoření kulatého tlačítka
    
    constructor(){
    
    }
    
    }
```

a v kontsruktoru je vytvoříme a nastylujeme.  
Samozřejmě pro vytvoření prvků potřebujeme context, proto si ho prřidáme do konstruktoru.

```js
constructor(context: WidgetContext){
        this._emitter = new WK.Emitter<WK.Event>(); //inicializaace emitoru
        this._rootView = new WK.View(context); //inicializace našeho root.view
        
        //přidáme stylizaci
        this._rootView.style.padding = "22px"; // chceme, aby posuvník byl uprostřed 1 čtverečku
        this._rootView.style.background = "transparent"; // necheme pozadí, proto průhledná 


        this._backgroundElement = new WK.View(context); // inicializace
        this._backgroundElement.style.background = "#838383"; // nastaavíme šedou po celé délce
        this._backgroundElement.style.height = "10px"; // tímto z toho uděláme tenký proužek
        this._backgroundElement.style.y = "-3px"; // kvůli paddingu děláme drobnou korekturu
        this._backgroundElement.style.width = "100%"; // roztáhneme ho po celé šíři widgetu
        this._backgroundElement.style.radius = "5px"; //zakulatíme rohy
        this._rootView.add(this._backgroundElement);  //přidáme element na náš základní element

        this._valueElement = new WK.Element(context); // inicializace
        this._valueElement.style.background = "#2274ff";
        this._valueElement.style.height = "10px";
        this._valueElement.style.y = "0";
        this._valueElement.style.width = "0";
        this._valueElement.style.radius = "0";
        this._backgroundElement.add(this._valueElement);

        this._buttonElement = new WK.Button(context,"");// inicializace
        this._buttonElement.style.width = "30px"; //
        this._buttonElement.style.height = "30px"; // nastavíme velikosst tlačítka napevno
        this._buttonElement.style.x = "0"; 
        this._buttonElement.style.y = "2px";
        this._buttonElement.style.radius = "15px" //tímto tlačítko bude kulaté
        this._buttonElement.style.border = "#FFFFFF 5px"; //nastavíme hezký, velký zdobný okraj
        this._buttonElement.style.background = "#2274ff";
        this._buttonElement.style.shadow = "#000000 30px 0 0"; //vytvoříme stín, přímo pod tlačítkem
        this._buttonElement.style.originX = "0.5";
        this._buttonElement.style.originY = "0.5"; 
        this._rootView.add(this._buttonElement);
}
```

A nakonec přidáme několik listenerů do konstruktoru, abychom mohli manipulovat s posuvníkem

```js
 this._buttonElement.listenEvent("mousedown",this.onButtonMouseDown); //reagování při kliknutí na button
 this._backgroundElement.listenEvent("mousedown",this.onBackgroundMouseDown); // reakce při kliknutí kamkoliv na posuvník
 context.root.listenEvent("appmouseup",this.onAppMouseUp); //ve chvíli kdy uživatel pustí tlačítko
 context.root.listenEvent("appmousemove",this.onAppMouseMove); //kvůli celemů posuvníku je třeba vyřešit co jak moc uživatel posunul
```

Jistě jste si všimli, že místo kasického `e => { foo.bar() });` voláme funkci, proto si rovno vytvoříme prázdé funkce, později se k ním vrátíme.

```js
/*MIMO KONSTRUKTOR, ALE POŘÁD DO NAŠÍ TŘÍDY Slider*/

   protected onButtonMouseDown = (e) => { 
    }

   protected onBackgroundMouseDown = (e) => {      
    }
    
   protected onAppMouseUp = (e) => {
    }

   protected onAppMouseMove = (e: WK.MouseEvent) => { 
    }

```

pokud si chceme otestovat, že náš widget je nastylovaný správně, přidáme getter do naší třídy

```js
  public get rootElement(): WK.View {
        return this._rootView;
    }

```

a poté úplně mimo třídu napíšeme

```js
context.addSizeProfiles(3,1,50,1);

let slider = new Slider(context);
slider.rootElement.style.width = "100%";
slider.rootElement.style.height = "100%";
context.root.add(slider.rootElement); //přidáme slider.rootElement, na který jsme napojili všechny ty prvky dohromady

```

při testování dostaneme něco takového:  
![](/assets/slider2.png)

Můžeme trochu upravit pozice všech objektů.   


### přidání getterů a pokrytí základní funkčnosti

Upravíme naší třídu.  Přidáme do ní ještě několik getterů 

```js
    public getButtonElement(): WK.Button {
        return this._buttonElement;
    }

    public getBackgroundElement(): WK.View {
        return this._backgroundElement;
    }

    public getValueBarElement(): WK.Element {
        return this._valueElement;
    }
      public get isMoving(): boolean {
        return this._moving;
    }

```

Abychom později mohli měnit detaily jako barvy, zaoblení rohu apod.

Přidáme možnost poslouchat události ve třídě

```js
public listenEvent(key: "valueChanged" , callback: (event: WK.Event) => void): WK.Listener<WK.Event> {
        return this._emitter.listenEvent(key, callback);
 }
```

Jedné, co děláme je, že vrátíme přesněji typovaný emmiter, ke kterému jsme přidali specifikovaný key a callback.

Napíšeme si kód, jenž bude posouvat posuvník, pro širší využití budeme pracovat v procentech \(1 = 100%, 0.5 = 50%, 0.25 = 25%\)

```js
  protected internalSetValue(value: number) { 
         this._value = Math.min(Math.max(value, 0), 1); //podobně jako u grafu, jak jsme vybírali větší číslo

        this._valueElement.style.width = value * 100 + "%"; //šířka podbavení

        if (this._reversed) { //později přidáme i možnost mít posuvník z druhé strany, připravíme si tedy danou možnost předem
            this._buttonElement.style.x = (1 - value) * 100 + "%";// v případě že chceme invertovanou hodnotu
        } else {
            this._buttonElement.style.x = value * 100 + "%"; //posun tlačítka(posuvníku) na správnou pozici
        }
     }
```

Rovnou přidáme možnost umožnit mít posuvník "obráceně" 

```js
  public setReversed(reversed: boolean) {
        if (this._reversed != reversed) { //pokud se hodnoty, co aktuálně máme liší od té, co chceme
            this._reversed = reversed;

            if (this._reversed) {
                this._valueElement.style.originX = "1"; 
                this._valueElement.style.x = "100%"; //tímto "překlopíme" value.element, jenž podbarvuje posuvník 
            } else {
                this._valueElement.style.originX = "0";
                this._valueElement.style.x = "0";
            }
            this.internalSetValue(this._value); //aby se změny dostaly i k posuvníku
        }
    }
```

Do budoucna ještě pro posun tlačítka

```js
   protected setButtonPosition(e: WK.MouseEvent) {
        const max = this._rootView.visibleRect.size.width; //zapamatujeme si max. šířku panelu
        let newX = Math.min( Math.max(e.mousePosition.x - this._movingOffset, 0), max); //tooto rozepíšu o kousek níže
        this._value = newX / max;

        if (this._reversed) { //kontrolujeme zda nescrollujeme z druhé strany
            this._value = 1 - this._value;
        }

        this.internalSetValue(this._value); //nastavíme novou "vnitřní" hodnotu
        this._emitter.emit(this, new WK.Event("valueChanged")); //vyšleme změny komukoliv,kdo je poslouchá
    }
```

zaměříme se na let `newX = Math.min( Math.max(e.mousePosition.x - this._movingOffset, 0), max);`   
nejedná se o nic složitého, jenom menší číslo, abychom nevyjeli z pole, ze dvou možných, kde ještě upravujeme, abychom se nedostali pod nulu. Nejdříve vyhodnotíme zda je pozice posuvíku \(mínus offset pro správnou pozici\) větší než nula a později, jestli nepřekračujeme nejvyšší možnou.



### přidání funkcí

Když už jsme si konečně dopsali veškeré potřebné drobnosti pro barvení a posuv tlačítek, přidáme interaktivitu.

Přepíšeme původní prázdné funkce na:

```js
protected onButtonMouseDown = (e) => {
        if (this._buttonElement.isHover) { //kontrolujeme, zda opravdu je kurzor nad tlačítkem
            this._moving = true; //potvrdíme že se hýbe s posuvníkem
            this._movingOffset = e.mousePosition.x - this._buttonElement.visibleRect.position.x; // uložíme si bokem offset, odkud se tlačítko posouvalo
        }
   }
```

Zde nám pouze stačí "přepnout" boolean na přesun, změnu hodnoty provedeme v "onAppMouseMove". 



samozřejmě, kromada uživatelů spíše než tahem tlačítka preferuje klikání přímo na lištu posuvníku, proto přepíšeme interaktivitu k němu

```js
protected onBackgroundMouseDown = (e) => {
        if (this._backgroundElement.isHover && !this._buttonElement.isHover) { //kontrolujeme, zda je myš na liště, ale né na tlačítku (pustili bychom tímto dvě funkce najednou)
            this._movingOffset = this._buttonElement.visibleRect.size.width / 2;
            this.setButtonPosition(e);
        }
    }
```

Všimněte si, že zde \_moving neupravujeme. přednostně kvůli tomu, že ve chvíli co se klikne na danou pozici 

Při puštění vypneme "moving" abychom neposouvali tačítko když nechceme

```js
  protected onAppMouseUp = (e) => {
        this._moving = false;
    }
```



A samozřejmě, při posunu myší, pokud držíme posuvník

```js
  protected onAppMouseMove = (e: WK.MouseEvent) => {
        if (this._moving) {
            this.setButtonPosition(e);
        }
    }
```

### 

### doladění detailů

Pro jednodušší práci si ještě přidáme několik "nastavovátek" na barvy, stíny a podobné

```js
 public setReversed(reversed: boolean) {
        if (this._reversed != reversed) {
            this._reversed = reversed;

            if (this._reversed) {
                this._valueElement.style.originX = "1";
                this._valueElement.style.x = "100%";
            } else {
                this._valueElement.style.originX = "0";
                this._valueElement.style.x = "0";
            }
            this.internalSetValue(this._value);
        }
    }

   
```

Zapínání/vypínání stínu

```js
    public enableShadow(enabled: boolean) {
        if (!enabled) {
            this.getButtonElement().style.shadow = "none";
        } else {
            this.getButtonElement().style.shadow = "#000000 30px 0 0";
        }
    }
```

kulatost hran

```js
    
    public enableRadius(enabled: boolean) {
        if (!enabled) {
            this.getBackgroundElement().style.radius = "0";
            this.getButtonElement().style.radius = "0";
        } else {
            this.getBackgroundElement().style.radius = "5px";
            this.getButtonElement().style.radius = "15px";
        }
    }
```



```js
   
    public setBackgroundColor(color: string) {
        this.getBackgroundElement().style.background = color;
    }
```



```js

    public setFrontColor(color: string) {
        this.getValueBarElement().style.background = color;
        this.getButtonElement().style.background = color;
    }

```



```js
  
    public setBorder(color: string, width: number) {
        if (width == 0) {
            this.getButtonElement().style.border = "none";
        } else {
            this.getButtonElement().style.border = color + " " + width + "px";
        }
    }
```

Rovnou přidáme i Setter na value \(abychom mohli nastavit námi požadovanou hodnotu při vytvoření např.\)

```js
    public set value(value: number) {
        this.internalSetValue(value);
        this._emitter.emit(this, new WK.Event("valueChanged"));
    }
```



