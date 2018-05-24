# Callbacky připojení

## Ukázka kódu

V následujícím kódu jsou vytvořeny 2 metody "change\_link" a "change\_client". Pro změnu linkové vrstvy je použita metoda "change\_link" a jejím úkolem je oznámit \(například\) připojení či odpojení kabelu ethernetu.  Druhá metoda "change\_client" detekuje změnu stavu [MQTT clienta](../../konektivita/komunikace-s-portalem.md). Připojení callbacků probíhá v sekci inicializace, protože je potřeba volat ji pouze jednou. 

```cpp
#include "byzance.h"

void change_link(nsapi_connection_status status){

	switch(status){
	case NSAPI_STATUS_LOCAL_UP:
		printf("LINK:  \t > state changed to LOCAL_UP\n");
		break;
	case NSAPI_STATUS_GLOBAL_UP:
		printf("LINK:  \t > state changed to GLOBAL_UP\n");
		break;
	case NSAPI_STATUS_DISCONNECTED:
		printf("LINK:  \t > state changed to DISCONNECTED\n");
		break;
	case NSAPI_STATUS_CONNECTING:
		printf("LINK:  \t > state changed to CONNECTING\n");
		break;
	}

}

void change_client(client_status_t status){

	switch(status){
	case CLIENT_CONNECTION_STATUS_DISCONNECTED:
		printf("CLIENT:\t > state changed to DISCONNECTED\n");
		break;
	case CLIENT_CONNECTION_STATUS_CONNECTING:
		printf("CLIENT:\t > state changed to CONNECTING\n");
		break;
	case CLIENT_CONNECTION_STATUS_CONNECTED:
		printf("CLIENT:\t > state changed to CONNECTED\n");
		break;
	case CLIENT_CONNECTION_STATUS_SUBSCRIBED:
		printf("CLIENT:\t > state changed to SUBSCRIBED\n");
		break;
	case CLIENT_CONNECTION_STATUS_REFUSED:
		printf("CLIENT:\t > state changed to REFUSED\n");
		break;
	case CLIENT_CONNECTION_STATUS_FAILED:
		printf("CLIENT:\t > state changed to FAILED\n");
		break;
	}

}


void init(){

	Byzance::attach_link_connection_changed(&change_link);
	Byzance::attach_client_connection_changed(&change_client);

}

void loop() {

	Thread::wait(500);

}


```

