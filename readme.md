# ESP32-S3 BME280 Relay

Esquema de conexionado correspondiente al Capítulo 168 en YouTube de Computadoras y Sensore

![EsquemaConex](EsquemaConex.png)

# Código a ingresar

Adafruit_BME280 bme;

unsigned long tiempoAnterior = 0;


Dentro del setup():

pinMode(4, OUTPUT);
bme.begin(0x76);


Dentro del loop():

unsigned long tiempoActual = millis();

if (tiempoActual - tiempoAnterior >= 2000){
  s3_temperatura = bme.readTemperature();
  s3_humedad = bme.readHumidity() ;
  s3_presion = bme.readPressure() / 100.0F ;
  tiempoAnterior = tiempoActual;
}

Dentro de la función onS3ReleChange():

if (s3_rele){
  digitalWrite(4, HIGH);
} else {
  digitalWrite(4, LOW);
}