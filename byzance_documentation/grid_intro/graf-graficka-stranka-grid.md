Samozřejmě, někdy se nám stane že chceme měnit grafickou stránku našeho widgetu za běhu.

Jak již bylo řečeno, Parrent objekt všech WK objektů které přidáváme do widgetu, je **root.    
**Pro práci s ním použijeme `context.root`.

K tomu by vám měli dopomoci následující kusy kódu:

```js
context.listenEvent("render", e =>{
xy.style.fontsize = context.root.visibleRect.size.height * 0.8 + "px"; //vezme výšku viditelného panelu a dle toho zvětší text
})

//dále také
context.listenEvent("render"...
context.listenEvent("ready"... //při inicializaci
context.listenEvent("destroy"... //při smazání
```

Render se volá ve chvíli, kdy je třeba znovu vykreslit widget \(např. při změně velikosti\) nebo zavoláme metodu `context.root.invalidate();`



Pro kreslení čar a podobným `draw` funkcím můžeme přistoupit v renderu



```
context.listenEvent("render", e =>{
    let renderer = e.context;
renderer.beginPath();
    renderer.moveTo(Math.floor(Math.random() * 1000), Math.floor(Math.random() * 1000));
    renderer.lineTo(Math.floor(Math.random() * 1000), Math.floor(Math.random() * 1000));
    renderer.lineTo(Math.floor(Math.random() * 1000), Math.floor(Math.random() * 1000));
    renderer.strokeStyle = "#000000";
    renderer.stroke();
})


```



tento ukázkový kód nakreslí náhodnou čáru, vybarví ji a nakreslí ji.  
  
místo hexa lze použít i `rgb(255, 153, 0)`

