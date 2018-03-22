# Digitální vstupy a výstupy 

![](/assets/input_output.jpg)

##Vstupy

```

// message input with 1 argument - string
MESSAGE_INPUT(message_input_1, STRING, {
	to_computer("received message string %s\n", arg1);
});

// message input with 1 argument - integer
MESSAGE_INPUT(message_input_2, INTEGER, {
	to_computer("received message int %d\n", arg1);
});

ANALOG_INPUT(analog_input, {
	to_computer("test_anal val = %f\n", value);
});

DIGITAL_INPUT(digital_input, {
	to_computer("test_dig val = %d\n", value);
});
```

##Výstupy



```

```



