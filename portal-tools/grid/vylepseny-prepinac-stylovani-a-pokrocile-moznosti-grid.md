# vylepšený Přepínač \(stylování a pokročilé možnosti GRID\)

Po chvíli testování jistě zjistíte, že naše základní tlačítko je vlastně veskrze hloupé, neintuitivní a vzhledově špatné.

Proto si vytvoříme hezký, barvičky měnící, ikonkový přepínač pro komunikaci s uživatelem.

## programová část:

Založíme si nový Widget a přidáme output, sizeProfile a button element

![](../../.gitbook/assets/code13.png)

```javascript
let digOut = context.outputs.add("digOut","digital","digital output");
context.addSizeProfiles(2,2,5,5,true);

let iconTrue = context.configProperities.add("iconTrue","fa-icon","icon when true","fa-check");

let button = new WK.Button(context,"[fa]"+ iconTrue.value+"[/]");

context.root.add(button);
```

Stejně jakožto v minulé kapitole, avšak s několika vylepšeními:

* poslední argument u `addSizeProfiles`donutí widget držet tvar čterce \(pouze čtverce\).
* `let iconTrue = context.configProperties.add("iconTrue","fa-icon","icon when true","fa-check");` může být překvapující. Jedná se o přidání další položky jenž se dá nastavit při rozkliknutí _confurigations. \_Argumenty jsou podobné jako u \_Inputu_/_outputu_. **První** argument je jednoslovné pojmenování, **druhý** je typ dané property , **třetí** je pojmenování v nastavení a **poslední** je defalutní hodnota.
  * Fa-icon je ikona z [Font Awesome. ](http://fontawesome.io/) Je důležité aby názvy seděli dle FA, pro správně zobrazení. Postupně probereme všechny typy nastavení
* `let button = new WK.Button(context, "[fa]"+ iconTrue.value +"[/]");` je stejné jako minule, až nadruhý argument, protože místo textu chceme zobrazit ikonu z config properities. Nejdříve musíme Wigetu ohraničit kde se ikona nachází pomocí `[fa]IKONA[/]` pokud chceme vícero ikon najedou, musíme každou ikonu ohraničit zvlášť.
* iconTrue.value bere hodnotu z config properities, v tomto případě se jedná o ikonu

### testování:

Klikneme na test

![](../../.gitbook/assets/code14.png)

pokud se vše povedlo, uvidíme toto.

Pro nastavení ikonky klikneme na 

_configuration_

![](../../.gitbook/assets/code16.png)

Zde vidíme co vše lze nastavit ve Widgetu. Toto se hodí do Grid Projektů, kdy můžete nastavit vícero instancím stejného widgetu různé ikonky a barvy.

### přidání vícero možností stylizace

Protože budeme chtít jiné barvy a ikony při posílání true/false, přidáme ještě napíšeme ještě několik řádků, 

![](../../.gitbook/assets/code17.png)

```javascript
let iconTrue = context.configProperties.add("iconTrue","fa-icon","icon when true","fa-check");
let iconFalse = context.configProperties.add("iconFalse","fa-icon","icon when false","fa-check");
let colorTrue = context.configProperties.add("colorTrue","color","color when true","#00FF00");
let colorFalse = context.configProperties.add("colorFalse","color","color when false","rgb(255,0,0)");
```

U `colorTrue`používáme typ "_color_" a jako defalutní hodnotu můžeme použít jak barvy v hexadecimálu, tak i můžeme napsat _rgb_ hodnoty.

## stylizace

Nyní tlačítko kompletně nastylizujeme:

![](../../.gitbook/assets/code19.png)

všechny možnosti které mohou být v daném stylu napovídá našeptávač 

\(

ctrl + mezerník

\)

 při psaní daného stylu.

Můžeme i upravit pozici elementu pomocí __

```text
 button.style.originX          
 button.style.originY
 button.style.x           
 button.style.y
```

Ale v našem případě to není třeba, více informací najdeme v [Styly a jejich použití](styly-a-jejich-pouziti.md).

## Reaktivní stylyzování a Interakce s widgetem

Můžeme si všimnout problému s tím, že pokud styly napíšeme takto, tak se pouze nastaví jednou a tím veškeré změny končí.

Řekněme, že chceme zvětšit velikost fontu v závislosti na velikosti widgetu.  
Napíšeme do kódu toto:

```javascript
button.listenEvent("resize", e =>{      
    button.style.fontSize = button.visibleRect.size.height * 0.8 + "";      
 });
```

Jako minule, posloucháme změny na _button_ a při jakékoliv změny velikosti buttonu se zavolá funkce za tím.

`button.style.fontSize = button.visibleRect.size.height * 0.8 + "";`protože styly se dají měnit "za běhu" můžeme upravit velikost bloku, barvu pozadí apod.

`button.visibleRect.size.height * 0.8 + "";`  
vezme velikost viditelného obdélníku z _buttonu_ a z něho vezme jeho výšku v pixelech. proto dané číslo násobíme "koeficientem" 0.8. část `+" "` je pouze ošetření toho, že daná vlastnost požaduje datový typ string, né number.

Pozn. z widgetu se dá dostat i "celková" výška celého widgetu pomocí **root** a to  
`context.root.visibleRect.size.height`

samozřejmě, daná výška je v pixelech

V podobném stylu napíšeme i funkci, která změní barvu pozadí a ikonu dle \_digOut

```javascript
function changeIconAndText(){_if(digOut.value){      
        button.style.background = ColorTrue.value;      
        button.text = "[fa]"+iconTrue.value+"[/]";      
    }else{      
        button.style.background = ColorFalse.value;      
        button.text = "[fa]"+iconFalse.value+"[/]";      
    }      
};
```

protože digOut je boolean, můžeme zkrátit zápis. Při změně textu nesmíme zapomenout že pracujeme s ikonami a je třeba připsat dané ohraničení.

nakonec napíšeme event listener na button, že ve chvíli kdy je na button kliknuto, obrátíme hodnotu \_digOut \_a zavoláme naší funkci.

```javascript
button.listenEvent("mousedown", e => {      
        digOut.value = !digOut.value;'      
        changeIconAndText();      
});
```

![](../../.gitbook/assets/17.png)

**Pozn.:** `if(button.isHover)` funguje jakožto pojistka při vícero prvcích která potvrdí, že je kurzor opravdu nad naším elementem \(prvkem\). Je dobré o ní vědět a psát jí do vetšiny event listenerů, jenž mají spojitost s myší.

nyní klikneme na test a otestujeme naše tlačítko:

![](../../.gitbook/assets/code20.png)

Pokud se vše povedlo, mělo by se tlačítko při zvetšení zvětšit i text a při kliknutí změnit barvu a poslat negaci předešlé hodnoty.

![](../../.gitbook/assets/code21.png)

**Pozn.:**

 Widget se při změně v 

_Configuration_ 

 sám nezmění, je třeba přidat event listener.

můžeme buďto poslouchat konkrétní config-property , nebo rovnou celému contextu

![](../../.gitbook/assets/code22.png)

v tomto případě můžeme zavolat `changeIconAndText();`protože tam již nastavujeme ikonku a barvu.  
hodí se poznamenat, že pokud posloucháme konkrétní property, vrátí se nám její hodnota po změně. pokud nasloucháme celému context.configProperities, vrátí se nám objekt která ve value obsahuje \`tag\_property:hodnota\_property.

\`

![](../../.gitbook/assets/code23.png)

### slovo závěrem:

Tímto máme funkční přepínač, jenž se ná změnit dle potřeby a mění svůj vzhed

Pokud jste opravdu perfekcionalisti, můžete ještě přidat event listener při vytvoření projektu na nastavení správé velikosti a změny ikonky a barvy pozadí pomocí `context.listenEvent("ready", e => {});`

