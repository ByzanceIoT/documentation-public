## Logování chyb

Chyby se logují pomocí třídy utilities.loggy.Loggy

  * Loggy je třída pro zaznamenávání, načítání a uploadování chyb na [[http://byzance.youtrack.cz| Youtrack]].

  * Loggy všechny chyby ukládá do databáze a zároveň je zapisuje do souboru

  * Pro zaznamenání vyjímek v catch se nejčastěji používá univerzální metoda ``` 
    ..
    ..
    catch(Exception e){
        return Loggy.internalServerError(e, request());
    }
``` která chybu uloží a vrátí prázdný 500 result. 

  * Pokud nemůžete metodě poskytnout vyjímku, použijte ``` Loggy.internalServerError([popis problému], request()) ```
  * Pokud chcete pouze zapsat string a result, stack trace a další data chcete řešit sami, použijte ``` Loggy.error([název chyby], [obsah]) ```

  * Pro zobrazení chyb v prohlížeči otevřete kartu **Bug Reporting** na dashboardu serveru, zobrazí se tak všechny chyby uložené v databázi.

  * Na stránce zobrazující chyby lze také smazat všechny uložené chyby, mazat jednotlivé chyby, nebo některou z uložených chyb nahrát na youtrack. Po úspěšném nahrání na youtrack se tlačítko Report to Youtrack změní na View on Youtrack.