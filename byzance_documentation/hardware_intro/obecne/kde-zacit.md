# Kde začít?

Tato dokumentace popisuje, jak spustit, programovat a ovládat zařízení BYZANCE

![](/images/ioda_board.png)





Dostane se ti do ruky nějaké zařízení Byzance.

\* Jaké zařízení mám v ruce? Identifikace konkrétního targetu.

\* Připojení zařízení k napájení

## První spuštění

Zařízení se automaticky spustí po připojení napájení. Zařízení lze napájet několika různými způsoby, které jsou zdokumentovány v kapitole [Metody napájení](/byzance_documentation/hardware_intro/features/zdroj-internetu.md). Při prvním spuštění ovšem doporučujeme napájet zařízení pomocí USB.

/- Klipart se zvýrazněným konektorem microUSB nebo Gif připojujícího kabelu

Po připojení USB kabelu lze pozorovat rozsvícení několika indikačních LED diod a speciálně pomalé blikání zelené diody LED modulu, které indikuje stav zařízení nepřipojeného k internetu.

/- Obrázek indikující blikající ledku po startu

##Připojení zařízení k PC

Před připojením zařízení k internetu, je vhodné provést kontrolu jeho nastavení v bootloaderu. Bootloader je speciální část firmwaru, která uchovává nastavení zařízení. O bootloaderu se můžete více dočíst v sekci [Bootloader](/byzance_documentation/hardware_intro/features/bootloader.md)

Aby bylo možné spravovat nastavení bootloaderu, je potřea připojit zařízení k počítači. Postup jak se k zařízení připojit naleznete v sekci [Připojení zařízení k počítači](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md)

## Pripojení zařízení k internetu

Pokud zařízení správně komunikuje s počítačem přes USB nebo sériovou linku je možné přejít k nastavení připojení k internetu. V této fázi se nastavení liší podle typu zařízení a komunikačního rozhraní, které je schopné využívat (Ethernet, Wi-fi). Zařízení se bude připojovat k serveru Becky a proto je také potřeba se nejprve zaregistrovat na portál.

### Přihlášení na portál a nastavení Becky



### Připojení pomocí Ethernetu



### Připojení pomocí WIFI



# Testovací program 




\* \[\[[https://portal.stage.byzance.cz/\|Zaregistrovat](https://portal.stage.byzance.cz/|Zaregistrovat) se na servery Byzance\]\] FIXME odkaz směřuje na stage, což nebude finální URL.

\* Nastavení, [jakým způsobem se bude zařízení připojovat k internetu](/byzance_documentation/hardware_intro/features/zdroj-internetu.md)

\* [Připojení zařízení k počítači (/byzance_documentation/hardware_intro/navody/pripojeni-k-pc.md) [pomocí sériové](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc/pomoci-seriove-linky.md) linky nebo [USB](/byzance_documentation/hardware_intro/navody/pripojeni-k-pc/pomoci-usb.md).

\* Zařízení by mělo být nakonfigurováno. Pokud není, je třeba se seznámit s tím, co je [bootloader](/byzance_documentation/hardware_intro/features/bootloader.md), respektive dostat se do jeho [command režimu](/byzance_documentation/hardware_intro/features/bootloader/command-rezim.md) a nastavit připojení k lokálnímu počítači, nebo do serverů Byzance.

\* \[\[tutorial:basics\|Test nahrátí některého pokusného programu do zařízení přes Byzance servery\]\].

