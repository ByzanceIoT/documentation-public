# OTP \(one time programmable\) paměť

OTP paměť \(one time programmable\) je speciální flash paměť, která je součást mikrokontroléru a je možno ji naprogramovat pouze jednou. Slouží k ukládání jedinečných identifikátorů zařízení, unikátních neměnných klíčů, sériových čísel a podobně. 

OTP paměť v zařízení IODAG3E má velikost

```
OTP_BLOCKS * OTP_BYTES_IN_BLOCK
```

což odpovídá

```
16*32 = 512 bytů
```

a začíná na adrese 0x1FFF7800. Další podrobnosti, včetně možností dodatečného zamknutí jednotlivých bloků je možné nalézt v [referenčním manuálu](http://www.st.com/content/ccc/resource/technical/document/reference_manual/5d/b1/ef/b2/a1/66/40/80/DM00096844.pdf/files/DM00096844.pdf/jcr:content/translations/en.DM00096844.pdf).

## Využité bloky

Byzance paměť OTP využívá k vypálení MAC adresy a kódu revize zařízení. K tomu jsou rezervovány první 2 bloky OTP

```
Blok 0 -> adresa od 0x1FFF7800 - [6 bytů MAC adresa][10 bytů rezervováno]
Blok 1 -> adresa od 0x1FFF7810 - [4 byty Revision][12 bytů rezervováno  ]
```



