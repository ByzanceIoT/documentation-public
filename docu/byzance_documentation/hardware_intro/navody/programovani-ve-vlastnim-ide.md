# Programování ve vlastním IDE

Pro programování ve vlastním IDE je třeba zajistit následující

* \[\[mbed:build\|Instalace MBED, Python a vše s tím související\]\]
* Instalace vlastního IDE, např. \[\[[http://www.st.com/en/development-tools/sw4stm32.html\|SW4STM32\]\](http://www.st.com/en/development-tools/sw4stm32.html|SW4STM32]\)\] nebo \[\[[https://www.eclipse.org/downloads/?\|Eclipse\]\](https://www.eclipse.org/downloads/?|Eclipse]\)\]
* Stažení GITu Byzance FIXME zatím nepodporujeme
* Vytvoření projektu
* Nastavení kompilace

# Vytvoření nového projektu

Pro prostředí Eclipse či jeho deriváty typu SW4STM32 je postup následující. Ve složce se staženými knihovnami z GITu FIXME zatím nic takového neumožňume pro cizí lidi se vytvoří nová podsložka s vlastním názvem dle projektu a v ní se udělá soubor main.cpp. V IDE je nutno kliknout na ''File-&gt;New-&gt;Makefile Project with Existing Code'', viz screenshot níže.

// obrázek

Dále je třeba vyplnit název projektu, který by se měl shodovat s názvem složky s projektem a vybrat umístění složky

// obrázek

V nastavení projektu je třeba nastavit vlastní build command, který se skládá z následujících částí

* node - příkaz pro interpreter Javascriptu \[\[[https://nodejs.org/en/\|Node.JS\]\](https://nodejs.org/en/|Node.JS]\)\]
* ../\_makescript\_.js -&gt; cesta k build scriptu
* byzance -&gt; název projektu
* BYZANCE\_YODAG3E -&gt; build makro pro identifikaci targetu

// obrázek

Také nezapomeňte na propojení vašeho projektu s knihovnami.

// obrázek

# Programování

Samotné programování binárky může probíhat buď z \[\[tutorial:programming\|prostředí GUI\]\], nebo z \[\[Hardware:commands\_stm32\_st\_link\|příkazové řádky\]\].

