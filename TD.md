# TD Bluetooth Classique

Ce TD va vous permettre de prendre en main la gestion du Bluetooth dit classique sur vos objets connectés.
Le premier exercice est guidé afin de vous aider à mettre en place votre premier programme utilisant le Bluetooth, tandis que sur le deuxième et le troisème exercice vous êtes en autonomie.

## Exercice 1 : Controller une LED via Bluetooth

L'idée de ce programme est d'allumer la LED lorsque la donnée reçue est '1', et de l'éteindre lorsque l'on reçoit '0'.

Pour commencer, il nous faut importer la librairie BluetoothSerial :

``` C
#include "BluetoothSerial.h"
```

Vous pouvez ensuite créer un objet pour le bluetooth :

``` C
BluetoothSerial ESP_BT;
```

Dans la fonction setup(), on initialise notre objet, ainsi que la LED :

``` C
void setup() {
	ESP_BT.begin("Bluetooth LED"); //Changez ce nom afin de reconnaître facilement votre ESP au moment de l'appareillage
	pinMode (LED_BUILTIN, OUTPUT);
}
```

Afin de récupérer les données reçues via le Bluetooth, à chaque tour de boucle on vérifie si l'on a reçu ou non des données. Si c'est le cas, on vérifie leurs valeurs et on agit en conséquence.

``` C
if (ESP_BT.available()) 
{
	incoming = ESP_BT.read();
	if (incoming == 49) // 49 : code ASCII pour '1'
	{
		digitalWrite(LED_BUILTIN, HIGH);
		ESP_BT.println("La LED est allumée"); // Permet d'envoyer des données au client.
	}
       
	if (incoming == 48) // 48 : code ASCII pour '0'
	{
		digitalWrite(LED_BUILTIN, LOW);
		ESP_BT.println("La LED est éteinte");
	}
}
```

Vous avez maintenant un code fonctionnel. Afin de le tester, vous devez maintenant appareiller votre ESP32 à votre téléphone, vous le trouverez sous le nom que vous lui avez donné dans le code. Il vous faut ensuite un terminal Bluetooth afin de lui envoyer des données, il en existe plusieurs, nous avons effectué la démo avec l'application "Bluetooth Terminal". Vous pouvez maintenant envoyer des données à votre ESP32 et observer les résultats.


## Exercice 2 : Afficher du texte sur un écran via Bluetooth

1. Connecter et configurer un écran à votre ESP32.
2. Afficher la phrase "Hello world" sur cet écran.
3. Afficher les textes reçus par Bluetooth à l'écran.

## Exercice 3 (BONUS) :

1. Permettre à votre ESP32 de gérer plusieurs clients.