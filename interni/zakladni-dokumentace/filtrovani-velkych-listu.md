## Filtrování velkých List<Model> 

  * Jelikož není výhodné z databáze vytáhnout a zhmotnit stovky prvků a ty poslat na frontend, byla vytvořena jednoduchá procedura jak omezit odesílaný seznam na 25 prvků s možností stránkování ze strany frontendu. Aby to bylo normované a dokumentovatelné pro Swagger Api Doc.  

  * Počet prvků omezujeme na Modulo 25 a to vždy, kde je riziko velkého množství prvků a kde volání bude probíhat velmi často - třeba u počtu vlastních **Board** (desek IoT).  

  * Nebo u možnosti Filtrování objektů třeba u **"Post"** příspěvků v našem BlockoOverflow kde filtr vstupy čerpáme z Json, a stránku z @PathParam později snad z @QueryParam - kde filtr parametry budou tvořit url adresu.    


----

### Základní hlavička metody vracející seznam 

```
// Doporučuje se u Routes vyžadovat kontrolu na @Integer 
PUT   /compilation/board/filter/:page_number    @......get_Board_Filter(page_number: Integer)
```

```
// Metoda v contructoru
public Result get_BigList( @ApiParam(value = "page_number is Integer. 1,2,3...n" +
                                             "For first call, use 1",required = true)
                           @PathParam("page_number") Integer page_number)
{...// obsah metody}
  
```

----
### Základní obsah metody vracející seznam 
  * **Rozdíl oproti běžnému získání dat z DB je vytboření jen částečného Query - který je následně doplněn omezením na počet prvků a podle stránky. Viz kód.**  
  * Page number může být 0 i záporné číslo (je to ohlídáno dále) 
  * Povšimněte si, že Query zde netvoří list a ani počet prvků - query pouze definuje který objekt (Notification) a vlastnosti omezení seznamu (majitel objektu a setříděné podle stáří)
  * Zbytek je přenechán na Swagger objektu
  * Je vytvořen vzor (Swaggeg_JmenoObjektu_List) níže 
```
{
  ...
  Query< Notification > query = Notification.find.where().
                             .eq("person.id", SecurityController.getPerson().id) // vlastník notifikace
                             .order().desc("created");                           // setřídění
                             
   Swagger_Notification_List result = new Swagger_Notification_List(query, page_number); 
  
   return  GlobalResult.result_ok(Json.toJson(result));
   ...
}
```

----

==== Složitá metoda vracející seznam (Podle filtr parametrů) ====
  * Momentálně parametry filtru nemáme v url jak je běžné, ale v těle (v Json) 
  * Standartě metoda obsahuje Form.form(Swagger_Board_Filter.class).bindFromRequest(); 
  * Query< Board > je stavěna postupně podle filtru 
  * Na konci dochází naprosto k totožnému kdy je Query předána Swagger třídě Swagger_Board_List(query, page_number
 
```
{
     ...
     final Form<Swagger_Board_Filter> form = Form.form(Swagger_Board_Filter.class).bindFromRequest();
     if(form.hasErrors()) {return GlobalResult.formExcepting(form.errorsAsJson());}
     Swagger_Board_Filter help = form.get();
     
     Query<Board> query = Ebean.find(Board.class);
     
         // If Json contains TypeOfBoards list of id's
            if(help.typeOfBoards != null ){
                query.where().in("type_of_board.id", help.typeOfBoards);
            }

            // If contains confirms
            if(help.active != null){
                Boolean isActive = help.active.equals("true");
                query.where().eq("isActive", isActive);
            }

            // From date
            if(help.projects != null){
                query.where().in("projects.id", help.projects);
            }


            if(help.producers != null){
                query.where().in("type_of_board.producer.id", help.producers);
            }

            Swagger_Board_List result = new Swagger_Board_List(query, page_number);
            
            return GlobalResult.result_ok(Json.toJson(result));
           
       ...
}


```
### Swagger Dokumentační objekt **(Swagger_Notification_List)** ====

```
@ApiModel(description = "Individual Notification List",
          value = "Notifications")
public class Swagger_Notification_List {

/* Content--------------------------------------------------------------------------*/

    @ApiModelProperty(required = true, readOnly = true)
    public List<Notification> content;

/* Basic Filter Value --------------------------------------------------------------*/

    @ApiModelProperty(required = true, readOnly = true, 
                      value = "First value position from all subjects. Minimum is 0.")
    public int from;

    @ApiModelProperty(required = true, readOnly = true, value = "Minimum is \"from\" Maximum is \"total\"")
    public int to;

    @ApiModelProperty(required = true, readOnly = true, value = "Total subjects")
    public int total;

    @ApiModelProperty(required = true, readOnly = true, value = "Numbers of pages, which you can call")
    public List<Integer> pages = new ArrayList<>();

/* Set --------------------------------------------------------------------------*/

    public Swagger_Notification_List(Query<Notification> query , int page_number){

        if(page_number < 1) page_number = 1;
        this.content =  query.setFirstRow((page_number - 1) * 25).setMaxRows(25).findList();
        this.total   = query.findRowCount();
        this.from   = (page_number - 1) * 25;
        this.to     = (page_number - 1) * 25 + content.size();
        for (int i = 1; i < (total / 25) + 2; i++) pages.add(i);

    }
}


```
 