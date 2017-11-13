pro vytvoření grafického prvku v Gridu použijeme

let \[nazevPrvku\] = new WK.\[button,label,element...\]\(context,"text"\)



```js
label.style.background = "transparent";        //  color of background  
label.style.color = "#000000";                        //  color of font  
label.style.fontSize = "32px";                         //  size of font  
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
label.style.textShadow = null;
```



