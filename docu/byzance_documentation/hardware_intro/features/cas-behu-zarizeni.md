# Uptime

Uptime je čítač, který je implementovaný v každém Byzance zařízení. Vyjadřuje počet sekund uplynulých od zapnutí zařízení. Slouží především k monitoringu stability kódu a zjištění všeobecného přehledu o zařízení. Čítač se inkrementuje automaticky. Jeho maximální hodnota může být 2^32 - 1, tedy zhruba 136 let. Poté čítač přeteče znova na nulu.

Pokud je zařízení přepnuto do \[\[bootloader:overview\|bootloaderu\]\], ''uptime'' se neinkrementuje.

## Jak zjistit hodnotu uptime

  \* Dotazem do příslušného \[\[yoda:topic\_info\#informace\_o\_uptime\|MQTT topicu\]\]

  \* Ve \[\[tutorial:webview\|webovém rozhraní\]\]



