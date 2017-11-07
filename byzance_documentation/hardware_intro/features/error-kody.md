## Error kódy


Error cody slouží k identifikaci problémů bez potřeby parsovat a chápat komentáře - které zasíláme.
Ty jsou momentálně stále vyžadovány - zvláště kvůli testování a rychlé čitelnosti nás vývojářů. 
Ale pro automatické uchopení a reakci na typy chyb je nutné zavét seznam (viz jak fungují [[https://cs.wikipedia.org/wiki/Stavové_kódy_HTTP|Htttp stavové kódy]]

#### TYRION - HOMER - YODA / DEVICE 

Seznam společných Error Kódů. Ty se můžou a používají uvnitř programu pro vyhodnocování chyb a zároveň ke komunikaci s ostatními systémy - Error kód je zasílán v JSON a to vždy jeh číslo a dobrovolně jeho popis. (Ten je vhodný během vývoje)  

```
{
 "status" : "error" <- Status může být "success" nebo "error" a označuje - zda v JSON očekávat chybový kod, nebo je vše v pořádku.  
 "error_code" : 203321, <- Number
 "error_message" : "this is optional value" 
}
```



#### Seznam Error Codů

^ Error Code ^ Error Message                    ^ Určeno pro                   ^ Komentář               ^
| 99999999    | "GENERAL ERROR"                    | Hardware / Hardware-Homer    | Some unidentified general error |
| 1    | "UNKNOWN_TOPIC"                           | Hardware / Hardware-Homer    | Nerozeznaný MQTT Topic |
| 2    | "MISSING_LABEL"                           | Hardware / Hardware-Homer    | Missing some Label     |
| 3    | "UNKNOWN_LABEL"                           | Hardware / Hardware-Homer    | JSON label is unsupported     |
| 4    | "MALLOC ERROR"                            | Hardware / Hardware-Homer    | MALLOC ERROR -> not enough memory     |
| 50   | "ERROR"                                   | ALL                          | Nedefinovatelný Error  |

=== Tyrion-Homer-Instance ====
| 100  | "INSTANCE_NOT_FOUND"                      | Homer / Homer-Tyrion         | Instance neexistuje |
| 101  | "INSTANCE_ALREADY_EXIST"                  | Homer / Homer-Tyrion         | Instance already Exist |
| 102  | "BLOCKO_JSON_ERROR"                       | Homer / Homer-Tyrion         | |
| 103  | "HARDWARE_ALREADY_IN_ANOTHER_INSTANCE"    | Homer / Homer-Tyrion         | |
| 104  | "HARDWARE_ALREADY_ADDED"                  | Homer / Homer-Tyrion         | |
| 105  | "HARDWARE_NOT_IN_INSTANCE"                | Homer / Homer-Tyrion         | |

=== Tyrion-Homer-Hardware ====
| 201  | "HARDWARE_IS_OFFLINE"                     | Homer / Homer-Tyrion         | |
| 202  | "BINARY_FILE_NOT_VALID"                   | Homer / Homer-Tyrion         | |
| 203  | "BINARY_TYPE_NOT_RECOGNIZE"               | Homer / Homer-Tyrion         | Device ještě nebyl spárován s Yodou |
| 204  | "BINARY_FILE_NOT_FOUND"                   | Homer / Homer-Tyrion         | Při párování došlo k chybě          |
| 204  | "UPDATE_PROCEDURE_TIMEOUT"                | Homer / Homer-Tyrion         | Při párování došlo k chybě          |

| 300  | "TYRION_IS_OFFLINE"                       | Homer / Homer-Tyrion         | |
| 301  | "TOKEN_IS_INVALID"                        | Homer / Homer-Tyrion         | |

| 670  | "BLOCKO_JSON_ERROR"                       | Homer / Homer-Tyrion         | Json for Blocko with not valid |

|10000 | JSON INVALID                              | Hardware / Hardware-Homer    | JSON is invalid, parsing failed|
|10001 | MSGID MISSING                             | Hardware / Hardware-Homer    | There is no label "messageId" in JSON|
|10002 | JSON NOT OBJECT                           | Hardware / Hardware-Homer    | Given JSON is not object|
|30000 | UNKNOWN COMPONENT                         | Hardware / Hardware-Homer    | Unknown component (in binary update)|
|30001 | UNKNOWN FULLID                            | Hardware / Hardware-Homer    | Unknown full-id|
|30002 | UNKNOWN SHORTID                           | Hardware / Hardware-Homer    | Unknown shot-id|
|30003 | UNEXPECTED PART                           | Hardware / Hardware-Homer    | Unexpected part (in binary update) |
|30004 | CRC ERROR                                 | Hardware / Hardware-Homer    | CRC Error |
|30005 | ADD FAILED                                | Hardware / Hardware-Homer    | Add device failed|
|30006 | REMOVE FAILED                             | Hardware / Hardware-Homer    | Remove device failed|
|30007 | BACKUP FAILED                             | Hardware / Hardware-Homer    | Backup failed|
|30008 | INVALID DEVICE STATE                      | Hardware / Hardware-Homer    | Invalid device state|
|30009 | BIN DUPLICITY                             | Hardware / Hardware-Homer    | Attempt to upload binary which is already uploaded|
|30010 | ERASE IN PROGRESS                         | Hardware / Hardware-Homer    | Attempt to upload/start while upload/start is in progress|
|30011 | AUTOBACKUP ENABLED                        | Hardware / Hardware-Homer    | Attempt to upload static backup while autobackup feature is enabled|
|40000 | HOSTNAME ERROR                            | Hardware / Hardware-Homer    | Hostname is invalid|
|50000 | MSG NOT SAVED                             | Hardware / Hardware-Homer    | Device is not saved|
|50001 | MSG UNKOWN ITF                            | Hardware / Hardware-Homer    | Device with unknown interface|
|50002 | MSG INVALID                               | Hardware / Hardware-Homer    | Invalid message for device|
|50003 | MSG NOT ENUMERATED                        | Hardware / Hardware-Homer    | Device is not enumerated yet|
|50004 | DEV NOT IN LIST                           | Hardware / Hardware-Homer    | Device id is missing in yoda list|
|50005 | BASE LVL                                  | Hardware / Hardware-Homer    | Bus critical error - collision on bus cable|
|60000 | EXTMEM READ ERROR                         | Hardware / Hardware-Homer    | Read from external memory failed|
|60001 | EXTMEM WRITE ERROR                        | Hardware / Hardware-Homer    | Write to external memory failed|
|60002 | EXTMEM ERASE ERROR                        | Hardware / Hardware-Homer    | Erase of external memory failed|
|70000 | INTMEM READ ERROR                         | Hardware / Hardware-Homer    | Read from internal memory failed|
|70001 | INTMEM WRITE ERROR                        | Hardware / Hardware-Homer    | Write to internal memory failed|
|70002 | INTMEM ERASE ERROR                        | Hardware / Hardware-Homer    | Erase of internal memory failed|
----------

Příklady:: 
| 0 |  | Hardware / Hardware-Homer | |
| 0 |  | Tyrion / Tyrion-Becki | |
| 0 |  | Homer / Homer-Tyrion | |
 


