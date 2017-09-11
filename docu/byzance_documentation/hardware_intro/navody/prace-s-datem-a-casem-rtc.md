===== Práce s datem a časem \(RTC\) ======



Každé Byzance zařízení je vybaveno obvodem pro udržování reálného času \(RTC\). Jeho obsluha je poměrně triviální a dodržuje \[\[http://www.cplusplus.com/reference/ctime/time/\|standardy C++\]\].



Čas je synchronizován Yodovi automaticky při připojení k Homerovi FIXME HOMER-111 ticket.



Základní jednotkou je Unixové časové razítko, které reprezentuje počet sekund, které uplynuly od 1.1. 1970. K převodu jednotek je možné využít například jeden z mnoha \[\[http://www.onlineconversion.com/unix\_time.htm\|online nástrojů\]\].



Jednoduchý kód, jak získat časové razítko může vypadat například takto



==== Ukázka pro práci s Unix timestamp ====



&lt;code&gt;

\#include "byzance.h"



Serial pc\(SERIAL\_TX, SERIAL\_RX\);



time\_t timestamp;



void init\(\){



    pc.baud\(115200\);    

    pc.printf\("RTC test\n"\);

    

    // nastaveni Unix timestamp

    timestamp = 1234567890;

    set\_time\(timestamp\);

    

    pc.printf\("Cas nastaven\n"\);

}



void loop\(\){



    // vycteni Unix timestamp

    time\(&timestamp\);

    pc.printf\("Cas je: %u\n",\(unsigned int\) timestamp\);



    Thread::wait\(1000\);

}

&lt;/code&gt;



==== Vlastní časové pásmo a parsování timestamp do struktury ====



Časové razítko je v zařízení automaticky nastaveno nastaveno na UTC pásmo. Pro vlastní offset od UTC je třeba příslušnou položku změnit v \[\[bootloader:commands\|command režimu bootloaderu\]\]. Nastavený offset se za běhu normálního programu získat pomocí veřejné funkce ''Byzance::get\_timeoffset\(\)''.



S tím souvisí i parsování podle regionálního nastavení. K unixovému časovému razítku se přičte lokální offset a výslednou položku je možné konvertovat do časové struktury funkcí \[\[http://www.cplusplus.com/reference/ctime/gmtime/\|gmtime\(\)\]\].



&lt;code&gt;

\#include "byzance.h"



Serial	pc\(SERIAL\_TX, SERIAL\_RX\); // tx, rx



void init\(\){



	pc.baud\(115200\);



	pc.printf\("Time demo\n"\);



	time\_t time\_utc;

	time\_t time\_local;



	struct tm \*p\_utc;

	struct tm \*p\_local;



	p\_utc	= \(tm\*\)malloc\(sizeof\(tm\)\);

	p\_local = \(tm\*\)malloc\(sizeof\(tm\)\);



	// load UTC time to variable

	time\(&time\_utc\);



	// calculate local time using timeoffset getter

	time\_local = time\_utc + Byzance::get\_timeoffset\(\);



	// convert UTC from timestamp to time struct

	memcpy\(p\_utc, gmtime\(&time\_utc\), sizeof\(tm\)\);

	pc.printf\("UTC time   = %2d:%02d\n", \(p\_utc  -&gt;tm\_hour\)%24, p\_utc  -&gt;tm\_min\);



	// convert localtime from timestamp to time struct

	memcpy\(p\_local, gmtime\(&time\_local\), sizeof\(tm\)\);

	pc.printf\("Local time = %2d:%02d\n", \(p\_local-&gt;tm\_hour\)%24, p\_local-&gt;tm\_min\);



}



&lt;/code&gt;

