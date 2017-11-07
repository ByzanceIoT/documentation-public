## Konfigurace MBED na Windows

  * Je třeba mít nainstalovaý GIT. Nejlépe přímo z [[https://git-scm.com/ | git webu]]
  * Stáhne se MBED OS z [[https://github.com/ARMmbed/mbed-os | githubu]].
  * Stáhne se Python 2.x.x z [[https://www.python.org/downloads/ | oficiálního webu]].
  * Nainstaluje se Python 2.x.x. Při instalaci se v nějakém instalačním kroku musí zakliknout "přidat python do paths". Pokud se to neudělá, musí se pak python přidat ručně ve windows přes "enviroment variables". Python se musí nainstalovat do adresáře C:\Python27 (nikoliv do Program Files), protože jinak nebude správně fungovat. Mezery a závorky v adrese totiž dělají problémy.
  * Po instalaci Pythonu se otevře složka C:\Python27 a soubor "python.exe" se zkopíruje a vyrobí se tak nový soubor "python2.exe", takže tyto dva jsou totožné. Ve složce je ještě po instalaci soubor "pythow.exe", který zůstane, jak je.
  * Při spuštění git bash se musí po napsání příkazu ''python -V'' ukázat verze pythonu. Pokud se tak nestane, něco z předchozích kroků je špatně (nejspíš paths). (Lze použít i příkaz ''python --version'', který je se dvěma pomlčkama před version, není to tu pořádně vidět.)
  * Je třeba stáhnout a nainstalovat "pip". To se dá udělat ze [[https://pip.pypa.io/en/stable/installing/ | stránek pip]]. Zajímá nás soubor get-pip.py. Instalace by měla stačit tak, že se soubor stáhne např. na plochu a pokliká se na něho.
  * Ve složce, kam se stáhl MBED do počítače se klikne pravým a dá se "git bash here". Pokud není po pravém kliku tlačítko "git bash here" v nabídce, nezakliklo se to při instalaci gitu.
  * Napíše se příkaz ''python setup.py install''. Pyhton by si měl nainstalovat balíčky, které potřebuje MBED. Pokud není nainstalován pip z kroků výše, toto neproběhne správně.
  * Je třeba stáhnout GCC kompilátor. Stažení je možné na webu [[https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads | oficiálním webu]].
  * Nainstaluje se GCC kompilátor dle standardního postupu. Je třeba jej zase přidat do paths, to se nastaví někdy v průběhu instalace (defaultně to totiž není zaškrtnuto).
  * Nyní by mělo fungovat standardní buildění, viz níže. Pokud není nainstalován kompilátor viz výše, toto neproběhne správně.
====== Jak rozběhat MBED na LINUX? ======

FIXME napíše David nebo Martin

====== Jak buildit MBED? ======

MBED se kompiluje pomocí MBED python skriptu. Pro kompilaci na OS Windows je nutné mít funkční GIT Bash.
  * V místě, kde je MBED stažený, se otevře soubor ''BYZANCE_README''
  * Ve složce o úroveň výš se klikne pravým a dá se ''git bash here''
  * v souboru ''BYZANCE_README'' jsou jednotlivé buildící příkazy pro jednotlivé targety.

===== Aktuální targety =====
```
mbed/tools/build.py -m BYZANCE_YODAG2 -t GCC_ARM --source mbed --build mbed-os_BYZANCE_YODAG2 --no-archive --profile small
mbed/tools/build.py -m BYZANCE_YODAG2_BOOTLOADER -t GCC_ARM --source mbed --build mbed-os_BYZANCE_YODAG2_BOOTLOADER --no-archive --profile small
mbed/tools/build.py -m BYZANCE_YODAG3E -t GCC_ARM --source mbed --build mbed-os_BYZANCE_YODAG3E --no-archive --profile small
mbed/tools/build.py -m BYZANCE_YODAG3E_BOOTLOADER -t GCC_ARM --source mbed --build mbed-os_BYZANCE_YODAG3E_BOOTLOADER --no-archive --profile small
mbed/tools/build.py -m BYZANCE_WRLSKITG2 -t GCC_ARM --source mbed --build mbed-os_BYZANCE_WRLSKITG2 --no-archive --profile small
mbed/tools/build.py -m BYZANCE_BUSKITG2 -t GCC_ARM --source mbed --build mbed-os_BYZANCE_BUSKITG2 --no-archive --profile small
```

===== Další info =====

Při změně např. v YODAG2 targetu je dobré vybuildit oba targety BYZANCE_YODAG2 i BYZANCE_YODAG2_BOOTLOADER. Ideální možností je přebuildit všechny targety, pokud se dělala změna v nějaké části, která zasahuje do všech targetů.

Po vybuildění obou variant a **vyčištění .temp** se obsah složky ''build'' překopíruje do ''hw_libs/_libs_''a commitne do gitu ''hw_libs''.
