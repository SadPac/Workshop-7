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
$(function(){
  $(document).verbatim();
});
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
