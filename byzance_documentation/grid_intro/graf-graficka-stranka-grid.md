Zatím jsme do widgetů dávali pouze jeden \(grafický\) element, aniž bychom s ním nějak více pracovali.

Zde si ukážeme práci s vícero elementama a jejich kreslení do nich.

---

Založíme si nový projekt a pojmenujeme si ho \_LineGraph.

\_vytvoříme Analogový vstup.  
Analog je reprezontován \(desetiným\) číslem. které může jít i do záporných hodnot.  
\(Poslední datový typ messeage, si ukážeme později.\)

`let anaIn = context.inputs.add("analin","analog","Analog Input");`

a přidáme sizeProfile  
`context.addSizeProfiles(3,2,20,20);`

a nakonec přidáme "generický element", ve kterém budeme pracovat.

\`let element = new WK.Element\(context\);

\`![](/assets/code24.png)

Tímto jsme si vytvořili bílý obdélník jenž vyplňuje celou plochu widgetu.  
Určitě budeme chtít zaznamenat hodnoty, které pak vykreslíme do widgetu jako graf. Proto si vytvoříme pole., do kterého si budeme ukládat hodnoty.  
\(připomínám, že pole v Javascriptu\(typescriptu\) fungují jinak než v Javě,C\(++/\#\) apod.\)

`let dataStorage = [];`

Nejlepší způsob, jak získat hodnotu z inputu je event listenerem. Proto napíšem

`anaIn.listenEvent("valueChanged", e => {      
    dataStorage.push(anaIn.value);    
});`

**Pozn.: **kvůli bugu v GRID se nová hodnota nedá získat z callbacku \(e\).

tímto při každé změně uložíme novou hodnotu do pole.  
![](/assets/code25.png)  
Nyní je třeba začít s vykreslováním  do elementu.

## Event render a kreslení

Widgety vykreslovány v Canvasu, díky tomu můžeme použít oficiální dokumentaci Canvasu. [\(LINK\).  ](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

Veškeré vykreslování se děje v 

`context.listenEvent("render", e => {      
    let draw = e.context;  
}) `

  
čímž kreslíme na vrh celé "plochy" widgetu.   
Protože budeme hodně používat e.context, uložil jsem si ho do promněné pro jednodušší práci.  
  
Ve zkratce nyní shrnu nejduležitější body z dokumentace Canvasu, 

* Prakticky veškeré úkony s ním začínáme tím, že zavoláme metodu `.beginPath();`
* bod 0,0 se nachází v levém horním rohu
* veškeré změny projeví až poté co zavoláme `.stroke();`



Nakreslíme si základní testovací čáru.  
pod námi definovaný _draw _napíšeme   


        `draw.beginPath();  
     draw.moveTo(0,0);  
     draw.lineTo(context.root.visibleRect.size.width,context.root.visibleRect.size.height);  
     draw.strokeStyle = "#000000";  
     draw.stroke();`

![](/assets/code28.png)

a klikneme na test

![](/assets/code26.png)  
  
Čára by vždy měla být z levého horního rohu do dolního pravého.  
Pozornější si jistě všimli     `context.root.invalidate();   
`Tato metoda se volá kdykoliv se změní widget a je třeba znovu ho celý vykreslit \(znova zavolá render\).  
Např. při změně velikosti widgetu, nebo když ho zavoláme my s tím že chceme vykreslit nově příchozí hodnoty.

když už jsme dali dohromady základy práce s canvasem, jsem si udělat graf z hodnot co ukládáme do pole.

---

Pro snažší práci si zabarvíme pozadí na bílo a vytvoříme si několik promněných pro snažší práci.



