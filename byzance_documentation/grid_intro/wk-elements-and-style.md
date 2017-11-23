Všechny možné styly

```js
label.style.background = "transparent"|"#FFFFFF"|"rgb(255,255,255,1)";        //  Barva pozadí  
label.style.color = "#000000"|"rgb(255,255,255,1)";                        //  barva fontu (či FA ikonek)  
label.style.fontSize = "32";                         //  velikost fontu v pixelech  
label.style.x = '50%';                                       //  position on x axis - can be in % (of element width), or in pixels  
label.style.y = '50%';                                       //  position on y axis - can be in % (of element height), or in pixels  
label.style.width = '100%';                             //  width - can be in % (of element width), or in pixels  
label.style.height = '100%';                           //  height - can be in % (of element height), or in pixels  
label.style.originX = '0.5';                             //  origin on x axis, 0 - positioning from left border, 1 - positioning from right border  
label.style.originY = '0.5';                             //  origin on y axis, 0 - positioning from top border, 1 - positioning from bottom border  
label.style.lineHeight = '100vh';                   //  Line height for text rendering - it can be in pixels or vh (widget height)  
label.style.textShadow = '#000 50 0 0';      //  Define shadow for text rendering  
label.style.fontFamily = 'Arial';  
label.style.horizontalAlign = 'center';  
label.style.multiline = 'true';  
label.style.textShadow = 'null'|'none';
```

```
"transparent" = průhledná
"#FFFFFF" = Hex. barva 
"rgb(255,255,255,1)" = rgb, poslední hodnota je alpha (1 - solid, 0.5 poloprůhledné, 0 = průhledné)
```

button.style.x = '50%';  
![](/assets/widget50x.png)

button.style.x = '-50%';  
![](/assets/posun-50x.png)

button.style.y = '-50%';  
![](/assets/posuny50.png)

button.style.originX = '0.5';  
![](/assets/orginposunx.png)

button.style.originY = '0.5';

![](/assets/posunoriginy.png)

Z přiloženého sloupce musí být jasné, jaký je rozdíl mezi X/Y pozicí, která pracuje buďto s pixely nebo s procenty a s origin, která pracuje na celočíselná čísla.



kombinaci 

```js
label.style.width = '100%';                              
label.style.height = '100%';                             
label.style.originX = '0.5';                               
label.style.originY = '0.5';
```

používáme pro to, abychom daný prvek s jistotou vycentrovali. \(na střed\).

