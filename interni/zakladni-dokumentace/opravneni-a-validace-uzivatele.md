## Oprávnění a validace uživatele 

Každý ORM objekt má z historických důvodů několik samostatných segmentů. 
  * Database value ( proměnné a navázané proměnné )
  * JSON IGNORE (privátní a obslužné metody  
  * Permission (oprávnění nad objektem) 
  * Finder 
  * Geter a Seter metody (výjimečná situace kdy jí vyžaduje Ebean u xxx.update() ) 

-----
 
### Permission 

  * Každý objekt má 4 základní oprávnění, které lze libovolně potřeby rozšířit ( canInvite_permission atd..).
  * Každá z těchto metod vrací boolean a "TRUE" pokud lze operaci provést. @JsonIgnore a @ JsonProperty používáme pro informování frontendu co může konkrétní uživatel s objektem dělat.
  * create_permission a read_permission jsou defaultně @JsonIgnore protože nedává smysl to frontendu ukazovat. Používáme ho my na Tyrionovi vnitřně v metodách pro ověřování. Některé vyžadují create_permission(){return true;}
  
```
   @JsonIgnore public Boolean create_permission(){....}
   @JsonIgnore public Boolean read_permission(){....}
   
   @JsonProperty public Boolean edit_permission(){....}
   @JsonProperty public Boolean update_permission(){....}
       Rozdíl v edit a update: Několik objektů má verzování - což je update. Ale například změna názvu daného 
       programu je edit.  
   
   @JsonProperty public Boolean delete_permission(){....}
```

V případě provedení requestu se objekt zhmotňuje a na něm je teprve provedeno ověření oprávnění. 
```

  // Metoda v controlleru
  // Swagger anotace
  //...
  public Result get_SuperCar(String car_id){
  
     Car car = Car.find.byId( car_id);
     if( ! car.read_permission() ) return GlobalResult.forbidden_Permission();
     
     return Json.toJson( car );
  
  }
  
  // Metoda v controlleru
  // Swagger anotace
  //...
  public Result create_SuperCar(){
    
     final Form<Swagger_Car_New> form = Form.form(Swagger_Car_New.class).bindFromRequest();
     if(form.hasErrors()) {return GlobalResult.formExcepting(form.errorsAsJson());}
     Swagger_Car_New help = form.get();
    
     Car car = Car();
     car.car_name = help.car_name;
     ...
     ...
     ...
    
     // POZOR!! -> záměrně je oprávnění zkoumáno až po uložení proměnných. A to z důvodu možného jiného hodnocení       
                  // oprávnění. Například globální objekt vytvoří admin, ale privátní objekt vytvoří uživatel.    
     if( ! car.create_permission() ) return GlobalResult.forbidden_Permission( "You have no permission to create");
     
    
     car.save();
     
     return Json.toJson( car );
  
  }
  
```