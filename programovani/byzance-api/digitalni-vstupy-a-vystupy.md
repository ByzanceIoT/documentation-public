# Digitální vstupy a výstupy 

![](/assets/hw IN OUTs _ porty na lince.png)

##Vstupy

###Digitální

Digitální vstup je definován makrem DIGITAL_INPUT(). Jeho argumentem je název digitálního vstupu, následovaný anonymní metodou s obsluhou argumentu "value".

```cpp
DIGITAL_INPUT(NAME, {
	// METHOD BODY
	// do something with variable 'value'
});
```

Tedy například pro vytvoření digitální vstupu s názvem 'custom_digital_input' a vypsání přijaté hodnoty vstupem je třeba napsat

```cpp
DIGITAL_INPUT(custom_digital_input, {
	printf("custom_digital_value = %d\n", value);
});
```

###Analogový

Podobně jako digital input se vytváří analog input
```cpp
ANALOG_INPUT(NAME, {
	// METHOD BODY
	// do something with variable 'value'
});
```

Analogový vstup s názvem 'custom_analog_input' a výpisem svojí hodnoty se tedy vytvoří následovně

```cpp
ANALOG_INPUT(custom_analog_input, {
	printf("custom_analog_value = %f\n", value);
});
```

###Message

Vstup typu 'message' je trochu odlišný od předchozích dvou variant. Umožňuje příjem několika hodnot různých typů v jedné zprávě. Seznam typů je nutno nadefinovat v hlavičce metody. Jednotlivé argumenty je možno vyčítat z proměnných 'argn', kdy 'n' je počet argumentů (1-8). Tedy nikoliv z proměnné 'value', jako v předchozích dvou případech.

Typy argumentů mohou být

- bool
- int
- float
- string

Message vstup s jedním argumentem typu 'string'
```cpp
// message input with 1 argument - string
MESSAGE_INPUT(custom_message_input_str, STRING, {
	printf("received message input string %s\n", arg1);
});
```

Příklad message vstupu s jedním argumentem typu 'integer'
```cpp
// message input with 1 argument - integer
MESSAGE_INPUT(custom_message_input_int, INTEGER, {
	printf("received message input integer %d\n", arg1);
});
```

Kombinovaný message vstup se čtyřmi argumenty typu 'bool', 'int', 'float' a 'string'
```cpp
// message input with 4 arguments - bool, int, float a string
MESSAGE_INPUT(custom_message_input_combi, BOOLEAN, INTEGER, FLOAT, STRING {
	printf("received message input bool %d, int %d, float %f, string %s\n", arg1, arg2, arg3, arg4);
});
```

##Výstupy

Prototypy výstupu je nutno definovat v hlavičce kódu.

###Digitální

Definice vlastního digitálního výstupu s názvem 'custom_digital_output'

```cpp
DIGITAL_OUTPUT(custom_digital_output);
```

Příklad použití v kódu

```cpp
bool value = 1;
custom_digital_output(value);
```

###Analogový

Analogový výstup s názvem 'custom_analog_output'
```cpp
ANALOG_OUTPUT(custom_analog_output);
```

Příklad použití v kódu

```cpp
float value = 1;
custom_analog_output(value);
```

###Message

Message výstup, analogicky s vstupem, podporuje více argumentů, které je třeba specifikovat. Podporované jsou stejné typy, jako v případě vstupu:

- bool
- int
- float
- string

Takto může vypadat prototyp funkce s argumentem typu 'string'.
```cpp
MESSAGE_OUTPUT(custom_message_output_str, STRING);
```

Kombinovaný prototyp funkce s argumenty typu 'bool', 'int', 'float' a 'string'.
```cpp
MESSAGE_OUTPUT(custom_message_output_str, BOOLEAN, INTEGER, FLOAT, STRING);
```

Příklad použí kombinovaného výstupu v aplikaci
```cpp
bool value_bool = true;
int value_int = 42;
float value_float = 1.234;
char value_string[64];
sprintf(value_string, "test containing another values - %d, %d, %f\n", value_bool, value_int, value_float);
custom_message_output_str(value_bool, value_int, value_float, value_string);
```











