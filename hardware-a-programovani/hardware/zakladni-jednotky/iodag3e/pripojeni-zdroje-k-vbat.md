# Připojení zdroje k VBAT

Zařízení IODAG3E disponuje pinem **VBAT**. Pokud se na tento pin přivede externím zdrojem napětí 1.65 - 3.6 Zajistí se tím udržení hodnot dvaceti **backup registrů** , ve kterých se může uchovávat 80 bytů uživatelských dat. Dále tento externí zdroj **zachová hodnotu RTC**, která by se v případě odpojení hlavního napájecího zdroje vynulovala.

Napájení je nutné připojit podle schámatu napájecí části procesoru.

![Power supply schema](../../../../.gitbook/assets/power_schema.PNG)

U pinu VBAT je kapacitor, který udrží při napájení VBAT 3.6V hodnotu RTC i při úplném odpojení zhruba na 10 sekund.

