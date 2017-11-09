Zatím jsme do widgetů dávali pouze jeden \(grafický\) element, aniž bychom s ním nějak více pracovali.  
  
Zde si ukážeme práci s vícero elementama a jejich kreslení do nich. 

---

Založíme si nový projekt a pojmenujeme si ho _LineGraph.  
  
_vytvoříme Analogový vstup.   
Analog je reprezontován \(desetiným\) číslem. které může jít i do záporných hodnot.  
\(Poslední datový typ messeage, si ukážeme později.\)  
  
`  
let anaIn = context.inputs.add("analin","analog","Analog Input");`

a přidáme sizeProfile  
`context.addSizeProfiles(3,2,20,20);`

a nakonec přidáme "generický element", ve kterém budeme pracovat.  
  
`let element = new WK.Element(context);  
  
`![](/assets/code24.png)  
  
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



## Event render a .draw\(\)

Widgety vykreslovány v Canvasu, díky tomu můžeme použít oficiální dokumentaci Canvasu. [\(LINK\).  ](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

---

---

  
  
  




