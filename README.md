- [Diagrama de Actividades](#diagrama-de-actividades)
- [Documentación de Código](#documentacion-de-codigo)
    - [Arduino Maestro](#arduino-maestro)
    - [Arduino Esclavo](#arduino-esclavo)
- [Testing](#testing)
    - [Arduino Maestro](#arduino-maestro)
    - [Arduino Esclavo](#arduino-esclavo)
 

# Diagrama de Actividades

<p align="center">
  <img src="https://raw.githubusercontent.com/SadPac/Workshop-6/main/img/getmessage.png">
</p>

# Documentación de Código

Se realizaron dos archivos de código, uno para el arduino maestro, el cual envia todos los datos del sensor, y uno para el arduino esclavo el cual recibe estos datos, el código se escribió de la siguiente forma:

## Arduino Maestro

```
$(function(){
  $(document).verbatim();
});
```

## Arduino Esclavo

```
#include <Wire.h>//librería que permite la conexión y paso de datos entre maestro  y esclavo
int PinLM35=0;
float tempC=0.0;

void setup()
{
 //En la configuración I2C A5 es por default el pin análogo del Serial Clock (SCL) ---tiempo que dura la transmisión de datos 
//y A4es el Pin análogo encargado del serial data(SDA)--- la transmisión de datos
  Serial.begin(9600);
  Wire.begin(2);                // join i2c bus with id #2
  Wire.onRequest(requestEvent); // registro del evento para la comunicación slave-master 
}

void loop()
{
  int reading=analogRead(PinLM35);
  float voltagemV=reading*(5000/1024.0);
  tempC=(voltagemV-500)/10;
  delay(1000);
}

// this function is registered as an event, see setup()
void requestEvent()
{
  String txtTempC= String(tempC,2);
  if(tempC<10){
  txtTempC="00"+txtTempC;
  }else if(tempC<100){
    txtTempC="0"+txtTempC;
  }
  Serial.println(txtTempC);
 
   Wire.write(txtTempC.c_str());
  // mensaje de respuesta de 6 bytes del master master
}

```

# Testing

Se realizó la revisión de los logs para verificar la transmisión de datos entre los dispositivos utilizando el programa 'screen' en Linux, el puerto del arduino maestro fue asignado como ttyACM0, mientras que el arduino esclavo fue asignado como ttyACM1, a continuación se muestran los logs respectivamente para cada uno de los arduinos, en estos se puede evidenciar que la transmisión de datos entre ambos dispositivos  es la correcta.

## Arduino Maestro

```
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.61
445.61
445.61
445.61
445.12
445.12
445.12
445.12
445.61
445.61
445.61
445.61
445.12
445.12
445.12
445.12
445.61
445.61
445.61
445.61

```

## Arduino Esclavo

```
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.12
445.61
445.61
445.61
445.61
445.12
445.12
445.12
445.12
445.61
445.61
445.61
445.61
445.12
445.12
445.12
445.12
445.61
445.61
445.61
445.61

```

Como podemos observar cada uno de los datos enviados por el arduino maestro es recibido por el esclavo, por lo que de esta manera podemos corroborar el correcto funcionamiento del montaje.
