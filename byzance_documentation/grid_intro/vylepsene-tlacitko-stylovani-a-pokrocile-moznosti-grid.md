Po chvíli testování jistě zjistíte, že naše základní tlačítko je vlastně veskrze hloupé, neintuitivní a vzhledově špatné.

Proto si vytvoříme hezký, barvičky měnící, ikonkový přepínač pro komunikaci s uživatelem.

---

Založíme si nový Widget a přidáme output, sizeProfile a button element  
![](/assets/code13.png)

Stejně jakožto v minulé kapitole, avšak s několika vylepšeními:

* poslední argument u `addSizeProfiles donutí widget` držet tvar čterce \(pouze čtverce\).

* `let iconTrue = context.configProperties.add("iconTrue","fa-icon","icon when true","fa-check");`  
  může být překvapující. Jedná se o přidání další položky jenž se dá nastavit při rozkliknutí _confurigations. \_Argumenty jsou podobné jako u \_Inputu_/_outputu_. **První** argument je jednoslovné pojmenování, **druhý** je typ dané property , **třetí** je pojmenování v nastavení a **poslední** je defalutní hodnota.

  * Fa-icon je ikona z [Font Awesome. ](http://fontawesome.io/) Je důležité aby názvy seděli dle FA, pro správně zobrazení. Postupně probereme všechny typy nastavení

* `let button = new WK.Button(context, "[fa]"+ iconTrue.value +"[/]");` je stejné jako minule, až nadruhý argument, protože místo textu chceme zobrazit ikonu z config properities. Nejdříve musíme Wigetu ohraničit kde se ikona nachází pomocí `[fa]IKONA[/]` pokud chceme vícero ikon najedou, musíme každou ikonu ohraničit zvlášť.

* iconTrue.value bere hodnotu z config properities, v tomto případě se jedná o ikonu

Klikneme na test  
![](/assets/code14.png)

pokud se vše povedlo, uvidíme toto.  
Pro nastavení ikonky klikneme na _configuration_  
![](/assets/code16.png)  
Zde vidíme co vše lze nastavit ve Widgetu. Toto se hodí do Grid Projektů, kdy můžete nastavit vícero instancím stejného widgetu různé ikonky a barvy.

Protože budeme chtít jiné barvy a ikony při posílání true/false, přidáme ještě napíšeme ještě několik řádků, ![](/assets/code17.png)U `colorTrue`používáme typ "_color_" a jako defalutní hodnotu můžeme použít jak barvy v hexadecimálu, tak i můžeme napsat _rgb_ hodnoty.

## stylizace

Nyní tlačítko kompletně nastylizujeme:  
![](/assets/code19.png)  
všechny možnosti které mohou být v daném stylu napovídá našeptávač \(ctrl + mezerník\) při psaní daného stylu.

Můžeme i upravit pozici elementu pomocí_    
_`button.style.originX    
 button.style.originY`

`button.style.x     
 button.style.y`

Ale v našem případě to není třeba, více informací najdeme v [Styly a jejich použití](/byzance_documentation/grid_intro/wk-elements-and-style.md).  




## Reaktivní stylyzování

Můžeme si všimnout problému s tím, že pokud styly napíšeme takto, tak se pouze nastaví jednou a nelze s nimi nikterak vícero pracovat.   
Pokud např. cheme aby se velikost textu měnila v závislosti na velikosti widgetu apod.  
  
 



