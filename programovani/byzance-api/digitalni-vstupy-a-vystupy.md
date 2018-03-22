# Digitální vstupy a výstupy 

![](/assets/input_output.jpg)

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

Message vstup s jedním argumentem typu 'string'
```cpp
// message input with 1 argument - string
MESSAGE_INPUT(message_input_str, STRING, {
	printf("received message input string %s\n", arg1);
});
```

Message vstup s jedním argumentem typu 'integer'
```cpp
// message input with 1 argument - integer
MESSAGE_INPUT(message_input_int, INTEGER, {
	printf("received message input integer %d\n", arg1);
});
```


##Výstupy


```cpp
DIGITAL_OUTPUT(digital_output);
ANALOG_OUTPUT(analog_output);
MESSAGE_OUTPUT(message_output_str, STRING);
```



