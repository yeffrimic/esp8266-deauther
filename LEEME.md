## Introducción ##
###¿Qué es?

Basicamente es un dispositivo que puede realizar un ataque de desautenticación. Seleccionas los clientes que quieres desconectar de su red y comenzar con el ataque.  Mientras el ataque se esté llevando acabo, los dispositivos seleccionados no serán capaces de acceder a la red.

###¿Cómo funciona?###

El protocolo 802.11 contiene algo llamado trama de desautenticación, es utilizado para desconectarse de manera segura de una red inalámbrica.

Por qué no estan encriptadas, lo unico que necesitas es la direccion mac de el router wifi y la de el dispositivo que quieres desautenticar. No necesitas ni siquiera estar conectado en la misma red o conocer la clave, es suficiente con estar en el rango mínimo.

###¿Cómo protegerse?

Con el 802.11w-2009 tuvo una actualizacion para encriptar el manejo de las tramas, Entonces verifica que tu router esta actualizado asi como tus dispositivos tengan la proteccion del manejo de tramas activada, Tanto el dispositivo como el router tienen que tenerlo activado para que pueda funcionar de la mejor manera. He probado dispositivos nuevos y muchos de los dispositivos no lo tienen activado por defecto, asi que tu tendrás que hacerlo por tu cuenta,.

###Descargo de responsabilidad

Usalo solamente para propositos de investigacioni con tus propios dispositivos.

Por favor ver las leyes regulatorias de tu propio pais antes de usarlo, un transmisor de interferencia es ilegal en muchos paises y este dispositivo puede caer en esta misma categoria, aunque tecnicamente no sean lo mismo.

Mi intencion con este proyecto es dar a conocer este problema. este ataque muestra qué tan vulnerable es el protocolo 802.11 WiFi y como puede ser arreglado. La solucion ya esta, ¿Porqué no usarla?

###Instalación

Lo único que necesitas es una computadora y un ESP8266 con por lo menos 1 Mb de memoria flash.

yo recomiendo comprar la placa de desarrollo USB(NodeMCU, wemos, etc), porque por lo menos tienen 4Mb de memoria flash, no importa cual utilices siempre y cuando tenga un ESP8266 en él .

**1.** Instalar Arduino y abrirlo.

**2.**  Ir a Archivo > preferencias

**3.** Agregar  http://arduino.esp8266.com/stable/package_esp8266com_index.json a la URL del   administrador de placas.

**4.** Ir a herramientas, placas, administrador de placas.

**5.** Escribir esp8266

**6.** Seleccionar la version 2.0.0 y click en instalar


![screenshot of arduino, selecting the right version](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/arduino_screenshot_1.JPG)


**7.** Archivo, preferencias.

**8.** abrir la carpeta que esta bajo, para mas preferencias editar el siguiente archivo.

![screenshot of arduino, opening folder path](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/arduino_screenshot_2.JPG)

**9.** Ir a packages > esp8266 > hardware > esp8266 > 2.0.0 > tools > sdk > include

**10.** Con un editor de texto abrimos el archivo User_interface.h

**11.** Baja y antes de #endif agregar las siguientes lineas


`typedef void (*freedom_outside_cb_t)(uint8 status);`  
`int wifi_register_send_pkt_freedom_cb(freedom_outside_cb_t cb);`  
`void wifi_unregister_send_pkt_freedom_cb(void);`  
`int wifi_send_pkt_freedom(uint8 *buf, int len, bool sys_seq);`  

![screenshot of notepad, copy paste the right code](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/notepad_screenshot_1.JPG)


**No te olvides de guardar antes de salir.

**12.** Descarga y abre esp8266_deauther > esp8266_deauther.ino en Arduino.

**13.** Selecciona tu placa ESP8266, en herramientas, placas y el puerto adecuado en herramientas, puerto, sino te aparece ningun puerto no olvides instalar los drivers.

**14.** Subelo.


Tu desautenticador ESP8266 esta listo.

###Cómo usarlo

Primero conecta tu ESP8266 dandole poder, si tienes un cable USB OTG puedes conectarlo a tu celular. 
![esp8266 deauther with a smartphone](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/smartphone_esp_2.jpg)


Escanea las redes wifi y conectate a pwned, La clave es deauther . Una vez conectado puedes abrir tu navegador e ir a la direccion 192.168.4.1

Escanea ahora para encontrar redes.
![webinterface AP scanner](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/web_screenshot_1.JPG)


Escanea para los dispositivos clientes.
![webinterface client scanner](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/web_screenshot_2.JPG)


Nota: Mientras el ESP8266 esta escaneando apagará su access point, entonces tendras que conectarte manualmente desde la configuracion.

... y Ahora empieza con los diferentes ataques.

![webinterface attack menu](https://raw.githubusercontent.com/spacehuhn/esp8266_deauther/master/screenshots/web_screenshot_3.JPG)

Feliz Hacking :)

##Licencia.

Este proyecto esta bajo la licencia MIT - ver la [license file](LICENSE) file for detail


## Fuentes y enlaces adicionales.

deauth attack: https://en.wikipedia.org/wiki/Wi-Fi_deauthentication_attack

deauth frame: https://mrncciew.com/2014/10/11/802-11-mgmt-deauth-disassociation-frames/

ESP8266: 
* https://de.wikipedia.org/wiki/ESP8266
* https://espressif.com/en/products/hardware/esp8266ex/overview

packet injection with ESP8266: 
* http://hackaday.com/2016/01/14/inject-packets-with-an-esp8266/
* http://bbs.espressif.com/viewtopic.php?f=7&t=1357&p=10205&hilit=wifi_pkt_freedom#p10205
* https://github.com/pulkin/esp8266-injection-example

802.11w-2009: https://en.wikipedia.org/wiki/IEEE_802.11w-2009

wifi_send_pkt_freedom function limitations: http://esp32.com/viewtopic.php?f=13&t=586&p=2648&hilit=wifi_send_pkt_freedom#p2648

esp32 esp_wifi_internal function limitations: http://esp32.com/viewtopic.php?f=13&t=586&p=2648&hilit=wifi_send_pkt_freedom#p2648
