## Dokumentace Swagger

Každá API i každý objekt, se kterým frontend pracuje je nutné dokumentovat. Pro zobrazení dokumentace slouží web  [[http://swagger.byzance.cz|Swagger]], který se defaultně připojuje na lokálně spuštěný Tyrion. Stačí změnit url adresu na produkční server tyrion.byzance.cz. 

Swagger je framework plně integrovaný do Tyriona. Anotace včetně obsahu jsou algoritmy vyseparovány na dokumentaci.

Máme anotaci dokumetnace nad
  *  Modely (Objekty databáze ".. extends Model {.. ") 
  *  Pomocné objekty - které přijímáme jako Rest-Api požadavky z frontendu 
  *  Pomocné objekty - které vracíme, ale nejsou ukládány v databázi
  *  Jednotlivé API (metody v controlleru)          

----

### Dokumentování 

-----

### Pomocné objekty 

V **app/utilities/swagger** se nachází naimplementovaný framework Swagger. Jsou zde taktéž dvě velmi důležité a používané složky. 

  * **documentationClass** - Seznam (jednoúrovňový - je zakázáno vytvářet další složky!!) tříd, které dokumentují vstupní Json hodnoty - zasílané frontendem na naše Api. V příkladu [[http://swagger.byzance.cz/#!/B_Program/new_b_Program|Swagger dokumentace]] je v záločce body (tělo http reqestu) model - respektive parametry, které daná Api vyžaduje. A to jsou naše objekty v documentationClass. Tyto třídy jsou v drtivém případě překládány na modely do databáze.      
  * **outboundClass** - Jde o objekty (alternativy k modelům v DB) reprezentující odchozí data. Lze buď odeslat přímo objekt Json.toJson( muj_dB_Modem) nebo v případě potřeby sloučení několika objektů, zamaskování nebo doplnění dalšími informacemi máme objekty v outboundClass. 

### Anotace nad příchozím objektem 

Přijímané objekty mají navíc anotaci **@Constraints.Required** 
Ta určuje minimální a maximální délku řetězce, vstupní hodnoty int (třeba nezápornost), validitu email a další 

```

@ApiModel(description = "Json Model for new B_Program",
        value = "B_Program_New") //---- Zamaskováváme reálný jednoznačně určující název třídy a její účel v kódu---- 
public class Swagger_B_Program_New {

    @ApiModelProperty(required = false, value = "program_description can be null")
    public String program_description;

    @Constraints.Required
    @Constraints.MinLength(value = 8)
    @ApiModelProperty(required = true, value = "MinLength >= 8")
    public String name;
}

```


### Anotace nad odchozím non DB objektem 
Neobsahuje kontrolní anotace @Constraints jinak je shodný s ostatními třídami (objekty) 


```
@ApiModel(description = "Json Model for file content",
        value = "File_Content")
public class Swagger_File_Content {

    // required = true -< tím říkáme frontendu, že toto pole vždy v Jsonu bude!! 
    @ApiModelProperty(required = true, readOnly = true, value = "Content in String")
    public String content;

    @ApiModelProperty(required = true, readOnly = true)
    public String file_name;
}
```


-----
### API (metody v Controlleru) 

Každý Controller je opatřen stejnou anotací - která nezdokumentované API v controlleru (jednotlivé metody na které jsou odkazy z routes souboru) vloží do kategorie **Not Documented API - InProgress or Stuck** ve [[http://swagger.byzance.cz/|Swagger nástroji]]

```
    @Api(value = "Not Documented API - InProgress or Stuck")
    @Security.Authenticated(Secured.class) //<--- Anotace vynucující přihlášeného uživatele 
                                           // může být nad celým controllerem nebo nad jednotlivými metodami  
    public class GridController extends Controller { 
      ...
      ...
```


### Dokumentace metody v controlleru má 5 části 
  * @ApiOperation
  * @ApiImplicitParams
  * @ApiResponses
  * @BodyParser
  * @Security.Authenticated(Secured.class)

### @ApiOperation 
Každá metoda obsahuje @ApiOperation - základní popis co metoda v případě úspěchu vrací, jak se jmenuje, popis a kategorii (složku). **Hvězdičky** značí že tyto parametry editujeme - ostatní jsou neměnné a všude stejné. 

```
@ApiOperation(
** value = "Create new M_Project",
** tags = {"M_Program"},  // Definuje Kategorii ve Swagger nástroji (podobně jako složky) 
                          // 10 různých api může míst stejný tags a tím je vložíme do jedné "složky" 
** notes = "Super dlouhý popisující text co api dělá" +
           "a co nedělá - jen ukázka jak to děláme s \"plusem\" aby text nevylezl mimo monitor :)",
   produces = "application/json", 
   protocols = "https",
** code = 201, // Podle tohoto čísla vracím stejně přiřazený objekt z @ApiResponses řádku
***extensions = {
        @Extension( name = "permission_description", properties = {
              @ExtensionProperty(name = "M_Project_create_permission", value = M_Project.create_permission_docs ),
            }),
               @Extension( name = "permission_required", properties = {
                   @ExtensionProperty(name = "Project_create_permission", value = "true"),
                   @ExtensionProperty(name = "Static Permission key",     value =  "M_Project_create" )
            })
        }
   )
```

*** Extension: Jedná se o definování oprávnění - Viz oprávnění [[tyrion_permission|Oprávnění a validace uživatele]]


==@ApiImplicitParams==
Uvádíme ho v anotaci jen v případě že metoda přijímá z těla http requestu Json - který následně zpracujeme viz: [[dynamicke_objekty|Transformace Json do Model (objektu)]]
```
  @ApiImplicitParams(
            {
                    @ApiImplicitParam(
                            name = "body",
Jediný řádek který měníme ->dataType = "utilities.swagger.documentationClass.Swagger_M_Project_New",
                            required = true,
                            paramType = "body",
                            value = "Contains Json with values"
                    )
            }
    )
```

### @ApiResponses 
Popisují co za objekty vrátíme. Zde je ukázka všech možných případů co vracíme. 

```
@ApiResponses(value = {
  @ApiResponse(code = 201, message = "Successful created",      response = M_Project.class),
  @ApiResponse(code = 200, message = "Update successful",       response = M_Project.class),
  @ApiResponse(code = 200, message = "Ok Result",               response = Result_ok.class),  
    
  // následující objekty jsou v app/utilities/response/response_object 
  @ApiResponse(code = 200, message = "Ok Result",               response = Result_ok.class),    
  @ApiResponse(code = 400, message = "Some Json value Missing", response = Result_JsonValueMissing.class),
  @ApiResponse(code = 401, message = "Unauthorized request",    response = Result_Unauthorized.class),
  @ApiResponse(code = 403, message = "Need required permission",response = Result_PermissionRequired.class),
  @ApiResponse(code = 500, message = "Server side Error")
})
```


### Výsledné správně zadokumentované API 

```
 @ApiOperation(value = "Create new M_Program",
            tags = {"M_Program"},
            notes = "creating new M_Program",
            produces = "application/json",
            response =  M_Program.class,
            protocols = "https",
            code = 201,
            extensions = {
                    @Extension( name = "permission_description", properties = {
                            @ExtensionProperty(name = "M_Program.create_permission", value = M_Program.create_permission_docs),
                    }),
                    @Extension( name = "permission_required", properties = {
                            @ExtensionProperty(name = "M_Project.create_permission", value = "true"),
                            @ExtensionProperty(name = "Static Permission key", value =  "M_Program_create" )
                    })
            }
    )
    @ApiImplicitParams(
            {
                    @ApiImplicitParam(
                            name = "body",
                            dataType = "utilities.swagger.documentationClass.Swagger_M_Program_New",
                            required = true,
                            paramType = "body",
                            value = "Contains Json with values"
                    )
            }
    )
    @ApiResponses(value = {
            @ApiResponse(code = 201, message = "Successful created",      response = M_Program.class),
            @ApiResponse(code = 400, message = "Some Json value Missing", response = Result_JsonValueMissing.class),
            @ApiResponse(code = 401, message = "Unauthorized request",    response = Result_Unauthorized.class),
            @ApiResponse(code = 403, message = "Need required permission",response = Result_PermissionRequired.class),
            @ApiResponse(code = 500, message = "Server side Error")
    })
    @BodyParser.Of(BodyParser.Json.class)
    @Security.Authenticated(Secured.class)
    public Result new_M_Program( @ApiParam(value = "m_project_id", required = true) @PathParam("m_project_id") String m_project_id ) {
        try {
            final Form<Swagger_M_Program_New> form = Form.form(Swagger_M_Program_New.class).bindFromRequest();
            if (form.hasErrors()) {return GlobalResult.formExcepting(form.errorsAsJson());}
            Swagger_M_Program_New help = form.get();

            M_Project m_project = M_Project.find.byId( m_project_id );
            if(m_project == null) return GlobalResult.notFoundObject("M_Project m_project_id not found");

            Screen_Size_Type screen_size_type = Screen_Size_Type.find.byId( help.screen_type_id);
            if(screen_size_type == null) return GlobalResult.notFoundObject("Screen_Size_Type screen_type_id not found");

            M_Program m_program = new M_Program();

            m_program.date_of_create      = new Date();
            ..
            ..
            ..
            
            if (!m_program.create_permission())  return GlobalResult.forbidden_Permission();
            m_program.save();

            return GlobalResult.created(Json.toJson(m_program));
            
        } catch (Exception e) {
            return Loggy.result_internalServerError(e, request());
        }

    }
```
