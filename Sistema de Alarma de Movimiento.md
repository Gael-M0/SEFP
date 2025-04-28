# Sensor de Movimiento
Proyecto Sistemas Embebidos
## 1. Introducción
Este proyecto consiste en el desarrollo de un sistema capaz de identificar movimientos en su entorno mediante un sensor PIR, utilizando como plataforma principal el microcontrolador PIC16F877A.
Además de la detección local mediante un LED y una pantalla LCD, el sistema cuenta con la capacidad de enviar alertas inalámbricas a un dispositivo móvil Android mediante un módulo Bluetooth HC-05.

De esta manera, se logra un sistema eficiente, portátil y de fácil expansión para su integración en proyectos de monitoreo de espacios.
Esto permite alertar visual y remotamente sobre eventos de movimiento.
## 2. Objetivo
El objetivo de este proyecto es desarrollar un sistema de detección de movimiento basado en el microcontrolador PIC16F877A, capaz de:

    - Detectar movimientos mediante un sensor PIR.
    - Alertar localmente encendiendo un LED y mostrando mensajes en una pantalla LCD 16x2.
    - Notificar remotamente los eventos de movimiento a un dispositivo móvil a través de un módulo Bluetooth HC-05 y una aplicación desarrollada en MIT App Inventor 2.
## 3. Materiales Utilizados
Para realizar este proyecto se utilizaron los siguientes componentes:
|Componente                               | Descripción / Uso PIC16F877A                      | 
|-----------------------------------------|---------------------------------------------------|
|Microcontrolador principal del sistema.  | PIC16F877A                                        |
|Sensor PIR                               | Detecta movimientos en el área monitoreada.       |
|Pantalla LCD 16x2                        | Muestra mensajes de estado (modo 4 bits).         |
|Módulo Bluetooth HC-05                   | Envía avisos de movimiento al celular Android.    |
|LED rojo 5mm                             | Se enciende al detectar movimiento.               |      
|Resistencia 220Ω                         | Limitadora de corriente para el LED.              |
|Potenciómetro 10kΩ                       | Ajusta el contraste de la pantalla LCD.           |
|Protoboard o PCB                         | Para montar y conectar el circuito.               |
|Fuente de alimentación 5V                | Para alimentar todo el circuito de forma estable. |
|Cables de conexión                       | Para unir todos los componentes.                  |
|Celular Android                          | Para recibir las notificaciones mediante la app.  |

## 4. Diagrama de conexiones
Aquí se explica cómo se conectaron todos los componentes al PIC16F877A:

![e5f74743-3e89-47fe-9133-62ad192253c3](https://github.com/user-attachments/assets/c847c7e0-98db-4047-b28d-681c69d26d06)
## 5. Flujo de funcionamiento
![f3e289e7-126c-46bc-b1d2-a21e1cb26307](https://github.com/user-attachments/assets/9f7f921d-efe0-4ebd-8859-24b889e36e8c)

## 6. Codigo Principal

Aquí se muestra el resumen del programa que se grabó en el PIC16F877A para controlar todo el sistema.

El código está dividido en varias partes importantes:
 ### Configuración inicial:
    Se configura el oscilador a 20 MHz.
    Se establecen los puertos de entrada/salida:

        - RA0 como entrada (sensor PIR).
        - RB0 como salida (LED).
        - Puerto D como salida (para la LCD).

    Se desactiva el conversor analógico para usar pines digitales.

### Inicialización:

    LCD_Init(): Prepara la pantalla LCD para trabajar en modo 4 bits.
    UART_Init(): Prepara el PIC para enviar datos por Bluetooth.

Después de inicializar:

    Se limpia la pantalla.
    Se muestra el mensaje: "Sistema listo".
    Se espera 2 segundos y luego se limpia la pantalla.

### Bucle principal (while(1)):

    El PIC lee el sensor PIR.
    Si detecta movimiento:

        - Enciende el LED.
        - Muestra en la LCD el mensaje "Movimiento!".
        - Envía por Bluetooth el texto "Movimiento detectado".

    Si no detecta movimiento:

        - Apaga el LED.
        - Muestra en la LCD el mensaje "Sin movimiento".

Todo esto ocurre continuamente mientras el sistema está encendido.

## 7. Descripción de la App Móvil
Se desarrolló una aplicación móvil sencilla usando MIT App Inventor 2.

Esta app tiene como función recibir avisos de movimiento enviados por el módulo Bluetooth HC-05 conectado al PIC16F877A.
Funcionamiento de la App

    - Al abrir la app, aparece un botón para conectarse vía Bluetooth.
    - Al pulsar el botón:

        -- Se despliega una lista de dispositivos Bluetooth cercanos.
        -- Se selecciona el módulo HC-05 (ya debe estar emparejado previamente).

    - Una vez conectado:

        -- El estado de la conexión cambia a "Conectado" en la pantalla.

    - Si el sistema detecta movimiento:

        -- El PIC envía el mensaje "Movimiento detectado" vía Bluetooth.
        -- La app recibe el mensaje y:

           --- Muestra una alerta (Notificación emergente).
           --- Cambia el texto en pantalla a "Movimiento detectado".

### Componentes principales usados en la app:

|Componente | Uso|
|-----------|----|
|ListPicker | Permite seleccionar el dispositivo Bluetooth (HC-05).|
|Label | Muestra el estado de conexión y detección.|
|BluetoothClient | Permite manejar la conexión Bluetooth.|
|Notifier | Muestra las alertas cuando hay movimiento detectado.|

### Resumen de bloques de programación en App Inventor:

  Cuando se selecciona un dispositivo:
    → Se intenta conectar al módulo HC-05.
    → Si se conecta, cambia el estado a "Conectado".

  Cuando se recibe un mensaje:
    → Si el mensaje recibido es "Movimiento detectado", muestra una alerta y actualiza el estado en la pantalla.

  ![imagen](https://github.com/user-attachments/assets/41b81b7a-3df5-43c0-a69b-b2f64681dafe)

## 8. Resultados Esperados

Cuando el sistema funciona correctamente, se espera que ocurran las siguientes acciones:
Evento	Resultado en el sistema

Se detecta movimiento (el sensor PIR se activa)	

- El LED se enciende.

- La pantalla LCD muestra el mensaje: "Movimiento!".

- Se envía el mensaje "Movimiento detectado" por Bluetooth.

- La app móvil recibe el mensaje y muestra una alerta.

No se detecta movimiento (el sensor PIR no se activa)	

- El LED se mantiene apagado.

- La pantalla LCD muestra el mensaje: "Sin movimiento".

- No se envía ningún mensaje por Bluetooth.

## 9.  Errores Encontrados
Durante el desarrollo del proyecto surgieron algunos problemas que fue necesario identificar y corregir:

 1. Problema con la app de MIT App Inventor (Play Store)

  - Descripción:
    - Al utilizar la app oficial de MIT AI2 Companion desde la Play Store, al intentar conectar vía Bluetooth, muchas veces se quedaba congelada o simplemente no permitía la conexión con el módulo HC-05.

  - Causa:
    - La versión actual de la app tiene problemas de compatibilidad en algunos celulares o versiones recientes de Android.

 2. Problema con la configuración de la LCD

  - Descripción:
    - Aunque el circuito estaba bien conectado, la pantalla LCD no mostraba los mensajes correctamente. Solamente se veían cuadros oscuros, y no se lograban visualizar los textos esperados.

   - Causa:
    - La inicialización del LCD no era la adecuada. También algunos retrasos (__delay_ms()) faltaban entre los comandos enviados en modo 4 bits. Esto hacía que el LCD no interpretara bien las órdenes.
