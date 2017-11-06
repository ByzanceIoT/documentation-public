

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









