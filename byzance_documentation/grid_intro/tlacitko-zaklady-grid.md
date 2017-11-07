Jakožto první příklad si vytvoříme jednoduché tlačítko, které při stisknutí pošle digitální hodnotu `true `a při puštění `false `



začneme novým, čistým widgetem:

![](/assets/start.png)

  
  
  
  
vybereme nebo vytvoříme novou skupinu, dle toho kam chceme widget![](/assets/start2.png)  
  
  
  
  
a stiskneme "create new grid widget"  
![](/assets/last.png)



vytvoříme widget a otevřeme ho: ![](/assets/import.png)







## Programová část:

Nejdříve se zamyslíme nad tím, co chceme aby náš widget dělal a co vše k tomu bude potřebovat.  
Naše tlačítko bude reagovat na stisk tím, že pošle signál že je stisknuto.  
Naše tlačítko nic nepříjímá, pouze posílá jednu boolean hodnotu.  
  
Tudíž nám stačí jeden output, vzhledem k tomu že se jedná o boolean, jenž pouze nabývá hodnot true/false, tak nám stačí digitální výstup.  
  
**Pozn.:** Z praktického hlediska vždy začínáme s psaním input/output na začátku.

protože píšeme v jazyku Typescript, začneme takto  
`let valueDigOutput = context.outputs.add("valDigOut","digital","value digital out");`

let `valueDigOutput `definuje promněnou abychom mohli k daménu outputu přistupovat v kódu  ![](/assets/code1.png)





























