## Transformace Json do Model (objektu) 

  * Pro přijetí příchozích dat z API requestu uvedeme nejdříve nad konkrétní metodou anotaci kontrolující obsah body HTTP requestu že je to validní JSON ( Tím ho už nemusíme kontrolovat a zároveň označíme metodu za data přijímající)  ``

// Metoda v controlleru
@BodyParser.Of(BodyParser.Json.class) <--- Api vyžaduje v těle http requestu Json 
public Result zpracujData(){
   .
   .
}

  * Druhým bodem je transformace JSON na objekt (Ten je vázán na Swagger Dokumentaci! Viz Swagger Anotace)
  * Protože to co přijímáme, musíme dokumentovat pro front-end! A jako pojistka, že nikdy nebudeme mít odchylku od dokumentace a zpracovávaného objektu se používá objekt, který to sám na sobě dokumentuje. Důležité je zdokumentování přijímaného Json **@ApiImplicitParams!!**
  *  Je zde uveden **dataType = "utilities.swagger.documentationClass.Swagger_B_Program_Version_Update"**
  *  Bohužel Swagger v tomto případě musí mít přímou cestu ke třídě. A tak jsou všechny Swagger třídy určené k dokumentaci ve složce utilities/swager/documentationClass (To jsou třídy, které dokumentují příchozí Json) 
  * Pro odchozí máme složku utilities/swager/outboundClass


 @ApiOperation(value = "create new Version of B Program",
            tags = {"B_Program"},
            ....
            // Více Swagger Anotace (dokumentace) 
            ....
    )
    @ApiImplicitParams(
            {
                    @ApiImplicitParam(
                            name = "body",
                            dataType = "utilities.swagger.documentationClass.Swagger_B_Program_Version_Update",
                            required = true,
                            paramType = "body",
                            value = "Contains Json with values"
                    )
            }
    )
    @ApiResponses(value = {
            @ApiResponse(code = 200, message = "Ok Result", response =  Version_Object.class),
            // Více Swagger Anotace (dokumentace) 
    })
@BodyParser.Of(BodyParser.Json.class)
public  Result update_b_program(){

    Form<Swagger_Object> form = Form.form(Swagger_Object.class).bindFromRequest();
    if(form.hasErrors()) {return GlobalResult.formExcepting(form.errorsAsJson());}
    Swagger_Object help = form.get();
    
    Model_x moled_x = new Model_x();
    model_x.name = help.name();  // <----- z help do finálního objektu! 
    .
    .
    .
    
    // Kontrola oprávnění, zda uživatel objekt může uložit do DB 
    f (!  model_x.create_permission())  return GlobalResult.forbidden_Permission();
    
    model_x.save();
    
    return GlobalResult.result_ok(Json.toJson(model_x));
    
}
```

Pokud se podíváme na řádek form.hasError, tak ten podle anotace uvnitř objektu Swagger_Object ```
  if(form.hasErrors()) {return GlobalResult.formExcepting(form.errorsAsJson());}```
   zkontroluje obsah Json respektive zhmotěného objektu a vrátí co chybí, nebo nesplňuje požadavky - například na délku řetězce, validitu proměnné emailu atd. 
   
Anotace (Pro kontrolu obsahu JSONu) můžou být: ```
    @Constraints.Required // tato hodnota v Json je vyžadována 
    public String name; 
    
    @Constraints.MinLength(value = 8, message = "Error zpráva, kterou vrátíme když to není ok")
    public String description;
    
    @Constraints.Email
    public String email;
    
```

 
  * Pokud potřebujeme příjímat Objekty v Objektech (často celé pole) (Respektive skládané JSON) 
 
  * ```
  {
   "version_name"        : "První Verze Programu",
   "version_description" : "Novy program",
   "code"                : "....code....",
   "user_files" : [
        {
                 "file_name":"soubor dva",
                 "code" : "....code...."
        },
        {
                "file_name":"Uzivatelská třída 2 - tvoří složky",
                 "code" : "....code...."
        }
    ],
   "external_libraries":[
      {
         "library_name":"Uživatelův název SER",
         "files" : [
                  {
                      "file_name" :   "Ser/Ser.cpp",
                      "content" : "....code...."
                  },
                  {
                      "file_name" :   "Ser/Ser.h",
                      "content" : "....code...."
                  }
            ]
      },
       {
         "library_name":"Uživatelův název Blink",
         "files" : [
                  {
                      "file_name" :   "inc_blink.cpp",
                      "content" : "....code...."
                  },
                  {
                      "file_name" :   "inc_blink.h",
                      "content" : "....code...."
                  }
            ]
      }
   ],
    ```

  * ```
@ApiModel(description = "Json Model for new Version of C_Program",
          value = "C_Program_Version_New")
public class Swagger_C_Program_Version_Update {
    
    // Nutný fiktivní contructor pro zhmotnění vnitřních tříd
    public Swagger_C_Program_Version_Update(){}


    @ApiModelProperty(required = true)
    public String code;

    @Valid public List<User_Files> user_files;

    @Valid public List<External_Libraries>  external_libraries;



            public static class User_Files {
                public User_Files(){}

                public String file_name;
                public String code;

            }

            public static class External_Libraries {
                public External_Libraries(){}

                       public String library_name;
                @Valid public List<File_Lib> files;

                    public static class File_Lib {
                        public File_Lib(){}

                        public String file_name;
                        public String content;
                    }
            }
}
```