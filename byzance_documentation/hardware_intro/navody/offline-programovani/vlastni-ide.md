# Programování ve vlastním IDE

Pro programování ve vlastním IDE je třeba zajistit následující

* Instalace MBED a Python
* Instalace vlastního IDE, např. [SW4STM32](http://www.st.com/en/development-tools/sw4stm32.html), nebo [Eclipse](https://www.eclipse.org/downloads/?)
* Stažení GITu Byzance FIXME zatím nepodporujeme
* Vytvoření projektu
* Nastavení kompilace

# Vytvoření nového projektu

Pro prostředí Eclipse či jeho deriváty typu SW4STM32 je postup následující. Ve složce se staženými knihovnami z GITu se vytvoří nová podsložka s vlastním názvem dle projektu a v ní se udělá soubor main.cpp. V IDE je nutno kliknout na 

```
File -> New -> Makefile Project with Existing Code

```

viz screenshot níže.

![](/assets/ide_new_project.png)

Dále je třeba vyplnit název projektu, který by se měl shodovat s názvem složky s projektem a vybrat umístění složky

![](/assets/import_project.png)

V nastavení projektu je třeba nastavit vlastní build command, který může vypadat následovně

```
node ../../_makescript_.js custom/custom_project BYZANCE_IODAG3E
```

který se skládá z následujících částí

* node - příkaz pro [interpreter Javascriptu](https://nodejs.org/en/Node.JS])
* ../\_makescript\_.js -&gt; cesta k build scriptu
* custom/custom_project -&gt; cesta k projektu a název projektu
* BYZANCE\_YODAG3E -&gt; build makro pro identifikaci targetu

![](/assets/ide_custom_project.png)

Důležité je prolinkovat projekt s knihovnami.

![](/assets/ide_libs.png)

# Programování

Až je vlastní kód hotový, je třeba provést build, čímž se vytvoří odpovídající .bin soubor. Nahrátí samotné binárky může probíhat buď z [prostředí GUI](/byzance_documentation/hardware_intro/navody/offline-programovani/upload-kodu-z-gui.md), nebo [z konzole](/byzance_documentation/hardware_intro/navody/offline-programovani/upload-kodu-z-konzole.md). Pro pohodlnější programování je možné použít desku [DevKit](/byzance_documentation/hardware_intro/hardware/dk3g.md), která obsahuje programátor a disponuje vlastností Drag&Drop, kdy je možné zařízení programovat pouhým přetažením na virtuální disk v průzkumníku souborů v počítači.

