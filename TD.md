# TD Bluetooth

Ce TD va vous permettre de prendre en main la gestion du Bluetooth sur vos objets connectés.
Le premier exercice est guidé afin de vous aider à mettre en place votre premier programme utilisant le Bluetooth, tandis que sur le deuxième exercice vous êtes en autonomie.

## Exercice 1 : Controller une LED via Bluetooth

L'idée de ce programme est d'allumer la LED lorsque la donnée reçu est '1', et de l'éteindre lorsque l'on reçoit '0'.

Pour commencer, il nous faut importer la librairie Bluetooth :

``` C
#include "BluetoothSerial.h"
```

Vous pouvez ensuite créer un objet pour le bluetooth :

``` C
BluetoothSerial ESP_BT;
```

Dans la fonction setup(), nous avons besoin d'initialiser notre nouvel objet, ainsi que notre LED :

``` C
void setup() {
	Serial.begin(9600);
	ESP_BT.begin("Bluetooth LED"); //Changez ce nom afin de reconnaître facilement votre ESP au moment de l'appareillage
	Serial.println("Bluetooth Device is Ready to Pair");

	pinMode (LED_BUILTIN, OUTPUT);
}
```

Afin de récupérer les données reçues via le Bluetooth, on check à chaque loop si l'on a reçu des données. Si des données sont reçues, on vérifie leur valeur et si elles sont égales à '0' ou '1' alors on éteind / allume la LED.

``` C
if (ESP_BT.available()) 
{
	incoming = ESP_BT.read();
	Serial.print("Received:"); 
	Serial.println(incoming);
	if (incoming == 49) // 49 : code ASCII pour '1'
	{
		digitalWrite(LED_BUILTIN, HIGH);
		ESP_BT.println("LED turned ON");
	}
       
	if (incoming == 48) // 48 : code ASCII pour '0'
	{
		digitalWrite(LED_BUILTIN, LOW);
		ESP_BT.println("LED turned OFF");
	}
}
```

Vous avez maintenant un code fonctionnel. Afin de le tester, vous devez maintenant appareiller votre ESP32 à votre téléphone, vous le trouverez sous le nom que vous lui avez donné dans le code. Il vous faut ensuite un terminal Bluetooth afin de lui envoyer des données, il en existe plusieurs, nous avons effectué la démo avec l'application "Bluetooth Terminal". Vous pouvez maintenant envoyer des données à votre ESP32 et observer les résultats.


## Exercice 2 : Afficher du texte sur un écran via Bluetooth

2.1 Connecter et configurer votre écran.
2.2 Afficher "Hello world" sur votre écran.
2.3 Afficher le texte reçu par Bluetooth à l'écran.