# Practica 3b

### Código
````
#include <WiFi.h>
#include <WebServer.h>
// SSID & Password
const char* ssid = "MOVISTAR_252A"; // Enter your SSID here
const char* password = "88879C62F447277C17F6"; //Enter your Password here
WebServer server(80); // Object of WebServer(HTTP port, 80 is defult)

// Handle root url (/)
void handle_root(void);


void setup() {

Serial.begin(9600);
Serial.println("Try Connecting to ");
Serial.println(ssid);

// Connect to your wi-fi modem
WiFi.begin(ssid, password);

// Check wi-fi is connected to wi-fi network
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}

Serial.println("");
Serial.println("WiFi connected successfully");
Serial.print("Got IP: ");
Serial.println(WiFi.localIP()); //Show ESP32 IP on serial
server.on("/", handle_root);
server.begin();
Serial.println("HTTP server started");
delay(100);
}

void loop() {

server.handleClient();
}

// HTML & CSS contents which display on web server
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1>Practica3 wifi Arnau Bosque</h1>\
<h2> Este es el texto que enviamos con la ESP32 </h2>\
</body>\
</html>";

void handle_root(){
server.send(200, "text/html", HTML);
}
````
### Funcionamiento

Por lo que es el void setup podemos observar que creamos un objeto de la clase BluetoothSerial llamado SerialBT, mediante este objeto accederemos a las funciones que tiene su clase. Con la funcion SerialBT.begin("###") se nos permite asignar el nombre del dispositivo, es decir que para conectarnos a el nos saldra ese nombre.

Seguidamente en el loop miramos si tenemos algo para enviar por parte del usuario. Para ello utilizaremos la aplicación Bluetooth Terminal. Mediante la función SerialBT.avaliable parará el código hasta que finalmente se le envíe algo. Tambien declararemos un char el cual se encargará de guardad toda la información que se le ha enviado por el puerto serie a partir de Bluetooth Terminal. Despues solo tendremos que comparar con los condicionales y cuando se haya elegido la función volver a pedir que se le envíe una nueva.