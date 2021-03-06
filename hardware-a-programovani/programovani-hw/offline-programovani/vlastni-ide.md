# Vlastní IDE

## Programování ve vlastním IDE

Pro programování ve vlastním IDE je třeba zajistit následující

* Instalace vlastního IDE, např. [SW4STM32](http://www.st.com/en/development-tools/sw4stm32.html), nebo [Eclipse](https://www.eclipse.org/downloads/?)
* Stažení GITu Byzance FIXME zatím nepodporujeme
* Vytvoření projektu
* Nastavení kompilace

## Vytvoření nového projektu

Pro prostředí Eclipse či jeho deriváty typu SW4STM32 je postup následující. Ve složce se staženými knihovnami z GITu se vytvoří nová podsložka s vlastním názvem dle projektu a v ní se udělá soubor main.cpp. V IDE je nutno kliknout na

```text
File -> New -> Makefile Project with Existing Code
```

viz screenshot níže.

![](../../../.gitbook/assets/ide_new_project.png)

Dále je třeba vyplnit název projektu, který by se měl shodovat s názvem složky s projektem a vybrat umístění složky

![](../../../.gitbook/assets/import_project.png)

Po vytvoření projektu je třeba dostat se do jeho nastavení kliknutím pravého tlačítka na název, případně v horním menu pod položkou 

> Project -&gt; Properties

![](../../../.gitbook/assets/nastaveni_projektu.png)

V nastavení projektu v sekci **C/C++ Build** je třeba nastavit vlastní build command, který může vypadat následovně

```text
node ../../_makescript_.js custom/custom_project BYZANCE_IODAG3E
```

který se skládá z následujících částí

* node - příkaz pro [interpreter Javascriptu](https://nodejs.org/en/)
* ../\_makescript\_.js -&gt; cesta k build scriptu
* custom/custom\_project -&gt; cesta k projektu a název projektu
* BYZANCE\_YODAG3E -&gt; build makro pro identifikaci targetu

![](../../../.gitbook/assets/ide_custom_project.png)

Důležité je referencovat projekt s knihovnami.

![](../../../.gitbook/assets/ide_libs.png)

Tímto je nastavení nového projektu dokončeno. Po kliknutí na položku v menu

> Project -&gt; Build Project

by mělo dojít k buildu projektu. Pokud neobsahuje chyby \(exit code 0\), výsledkem by měla být informace o úspěšném dokončení a přehled využití jednotlivých částí paměti, oboje vypsané do konzole.

![](../../../.gitbook/assets/compile.PNG)

## Programování

Až je vlastní kód hotový, je třeba provést build, čímž se vytvoří odpovídající .bin soubor. Nahrátí samotné binárky může probíhat buď z [prostředí GUI](upload-kodu-z-gui.md), nebo [z konzole](upload-kodu-z-konzole.md). Pro pohodlnější programování je možné použít desku [DevKit](../../hardware/ostatni/devkitg3/), která obsahuje programátor a disponuje vlastností Drag&Drop, kdy je možné zařízení programovat pouhým přetažením na virtuální disk v průzkumníku souborů v počítači.

