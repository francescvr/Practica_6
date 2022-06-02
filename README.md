# Codi
```
#include <SPI.h>
#include <MFRC522.h>

#define RST_PIN 21
#define SS_PIN 5

MFRC522 mfrc522(SS_PIN, RST_PIN); //Creamos el objeto para el RC522
void setup() {
Serial.begin(115200); //Iniciamos la comunicación

SPI.begin();
//Iniciamos el Bus SPI

mfrc522.PCD_Init(); // Iniciamos el MFRC522

Serial.println("Lectura del UID");
}

void loop() {

// Revisamos si hay nuevas tarjetas presentes
if ( mfrc522.PICC_IsNewCardPresent())
{
//Seleccionamos una tarjeta

if ( mfrc522.PICC_ReadCardSerial())
{

// Enviamos serialemente su UID
Serial.print("Card UID:");
for (byte i = 0; i < mfrc522.uid.size; i++) {
Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
Serial.print(mfrc522.uid.uidByte[i], HEX);
}
Serial.println();

// Terminamos la lectura de la tarjeta actual
mfrc522.PICC_HaltA();
}
}
}
```

### Funcionament:

En primer lloc tenim les llibreries i les funcions dels pins necessàries per a poder utilitzar el sensor

```
#include <SPI.h>
#include <MFRC522.h>

#define RST_PIN 21
#define SS_PIN 5

MFRC522 mfrc522(SS_PIN, RST_PIN); //Creamos el objeto para el RC522
```

Al setup iniciem la comunicació, el SPI i el MFRC522. Que posteriorment treura per pantalla un missatge que ens doni pas a utilitzar tant la 
targeta o el pin amb el sensor.

```
void setup() {
Serial.begin(115200); //Iniciamos la comunicación

SPI.begin();
//Iniciamos el Bus SPI

mfrc522.PCD_Init(); // Iniciamos el MFRC522

Serial.println("Lectura del UID");
}
```

Per últim tenim el loop en el cual s'ordenarà que el sensor avisi de qualsevol interacció amb pin o targeta i mostri per pantalla la identificació pròpia d'aquest/s.

```
void loop() {

// Revisamos si hay nuevas tarjetas presentes
if ( mfrc522.PICC_IsNewCardPresent())
{
//Seleccionamos una tarjeta

if ( mfrc522.PICC_ReadCardSerial())
{

// Enviamos serialemente su UID
Serial.print("Card UID:");
for (byte i = 0; i < mfrc522.uid.size; i++) {
Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
Serial.print(mfrc522.uid.uidByte[i], HEX);
}
Serial.println();

// Terminamos la lectura de la tarjeta actual
mfrc522.PICC_HaltA();
}
}
}
```
