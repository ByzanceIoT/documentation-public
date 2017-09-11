# Revision



To může být typicky například jiný paměťový čip o stejné velikosti a stejných parametrech, ale s jiným Jedec ID, které je nutno zadávat při inicializaci. V této chvíli si Yoda zjistí svůj ''revision'' a podle toho zinicializuje paměť s příslušným ID ke své revizi. Další příklad využití ''revision'' může být například Yoda GEN2.0 a Yoda GEN2.1, které se buildily s targetem YODAG2 pro obě generace, ale generace 2.0 potřebovala zapnout clock pro ethernet a generace 2.1 už nikoliv. V takové chvíli obě generace dostávají stejný Target, ale různý ''revision'', podle kterého samy sebe identifikují.

Revision je interně interpretováno jako 32 bitové číslo, které se zobrazuje v HEX ASCII. Může tedy nabývat hodnoty ''0x00000000'' až ''0xFFFFFFFF''.

Číslo Byzance automaticky nastavuje při výrobě a toto už nelze změnit.

## Jak lze revision zjistit

    \* V \[\[bootloader:overview\|bootloaderu\]\] v \[\[bootloader:commands\|command režimu\]\]

    \* Zjištění pomocí příslušného \[\[yoda:topic\_info\#informace\_o\_revision\|info topicu MQTT\]\]. Nastavení není možné, protože položka je read-only.

    \* \[\[tutorial:public\_functions\|Veřejnou funkcí třídy Byzance\]\]

    \* Ve \[\[tutorial:webview\|webovém rozhraní\]\]
