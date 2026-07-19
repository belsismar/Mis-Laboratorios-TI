# Despliegue de Zentyal Server en entorno virtualizado con VirtualBox 💎🔗📌🏬


## 📝 Descripción del Proyecto
Este laboratorio práctico inicia con la implementación de Zentyal 8.1 en una ambiente de laboratorio usando maquinas virtuales de VirtualBox. El objetivo principal es configurar Zentyal como el Directorio Activo, Servidor de Archivos, DHCP, DNS y Firewall en una red pequeña que demuestre la funcionalidad de los servicios.. En esta primera entrega, además de detallar el paso a paso de la instalación, es compartir las lecciones aprendidas del proceso.

## 🔬Entorno del laboratorio

- VirtualBox
- Ubuntu Server 24.04
- 2 vCPU
- 4 GB RAM


##  Versión Zentyal a instalar
Zentyal puede instalarse de varias formas y hay varias versiones. Para efectos del laboratorio se descargar la versión Servidor de Desarrollo pues la misma ya viene embebida sobre Ubuntu Server 24.4 LTS y agiliza el proceso de instalación. Solo se necesita entrar a la comunidad de Zentyal y descargar. 

https://www.zentyal.com/comunidad/

![Página de download Zentyal](img/version-zentyal.png)

## 🛠️ Configuración inicial de VirtualBox

En VirtualBox vamos a crear una ""Nueva"" Máquina Virtual. En la pestaña inicial configuramos:
- El nombre de la máquina (VN Name) que en el laboratorio será Zentyal_AD
- La carpeta donde se guardará la máquina (VM Folder). Dejaré por defecto el indicado.
- Se debe ubicar la ruta donde esta la imagen ISO que se descargo antes (ISO Image). En este caso estaba en descargas. 
- Automáticamente se pone la ISO VirtualBox detecta sistema operativo (OS) que es Linux, la distribución (OS Distribution) que  es Ubuntu, y la versión del sistema operativo (OS Versión) que en este caso es Ubuntu (64-bit).
- Es importante que la instalación desatendida este ""desmarcada"".

![Primera pantalla de configuración de la máquina Virtual](img/new-virtual-machine.png)

Ahora vamos a pasar la pantalla donde empezamos a especificar el hardware (Specify virtual hardware). En este caso, selecciones 4Mb de memoria y 4 CPU.

![Pantalla de configuración del Hardware1](img/hardware.png)

Y por último configuramos el disco duro, que en este caso usaré 50Gb.

![Pantalla de configuración del Hardware2](img/hardware2.png)

### 👁️ Configuración de la Red para Zentyal

Antes de encender la máquina, nos falta configurar las tarjetas de Red. Entonces aquí en la máquina apagada seleccionamos ""Configuración"" y luego buscamos Red.

![Pantalla de configuración del Hardware1](img/apagada.png)

Por defecto la red esta en modo ""NAT"" y la vamos a cambiar a ""Adaptador Punete"". También en Modo Promiscuo vamos a seleccionar "Permitir todo" para que el DHCP y DNS fluyan sin bloqueos del hipervisor. Le decimos Terminar para que guarde los cambios.

![Pantalla de configuración de la NIC](img/red.png)


## 📋 Paso a paso de la pre-instalación en Ubuntu

Procedemos a encender la máquina virtual y lo primero que vemos es el nombre de Ubuntu arrancando.

![Encendiendo la VM](img/arranque.png)

Ubuntu nos pregunta el idioma de preferencia y seleccionamos ""Español""

![Idioma](img/idioma.png)

Podemos dejar por defecto Spanish o usar la opción "Identificar Teclado" para que detecte el Español Latinoamericano.

![Latino](img/latino.png)

Dejamos por defecto la NIC (olvide colocar el modo Puente así que lo hice al finalizar la instalación) 

![NIC](img/red2.png)

Nos pregunta si hacemos cambio en el disco y almacenamiento, lo dejamos como está. 

![Particiones](img/disk.png)

![Storage](img/disk2.png)

Ahora nos da la advertencia de eliminación de datos anteriores con esta instalación y le damos ""Continuar"".

![Advertencia](img/advertencia.png)

Finalmente nos pregunta los datos de usuario, contraseña, nombre del servidor y de quien instala. 

![Perfil](img/perfil.png)

### Instalación de Zentyal sobre Ubuntu Server

Así empieza la instalación y puede tardar entre 10 a 15 minutos aproximadamente (no tome el tiempo).

![Instalación](img/install.png)

Cuando termina la instalación ya vemos la solicitud de usuario y contraseña de Zentyal en mod GUI.

![Zentyal Gui](img/zentyal1.png)

## 📚 Lecciones aprendidas

1) Es necesario configurar la máquina virtual como "Adaptador Puente" de lo contrario solo tomará la IP de VirtualBox por defecto modo "NAT" y se requiere para usar la ""External WAN" y la ""Red Interna"" que requieren los servicios que se van a implementar con Zentyal. 

¿Qué aprendí? En VirtualBox en la configuración inicial no aparece por eso se nos suele olvidar. Antes de encender la máquina puedes ir a configuración y modificar la sección de Red. Pero si se te olvidó como a mí, apagas la máquina una vez termine la instalación y lo configuras.

2) Si estas acostumbrado a crear la máquina virtual con el modo "Proceed with Unattended Installation" el modo GUI no aparece al completar la instalación. Si es así tienes dos opciones:
	2.1) Reinstalar y quitar el modo "Proceed with Unattended Installation"
	2.2) Logearte en modo consola y descargar e instalar un GUI. Como esto es laboratorio para aprender, lo pimero que intente fue instalar una nueva GUI así:
		sudo apt update
		sudo apt install xfce4 xfce4-goodies lightdm -y
		sudo reboot
	     Sí apareció el modo GUI, pero no pude iniciar sesión, básicamente hice muchas pruebas cambiando la clave, reinstalando teclado latino, borrando temporales, asegurándome de tener los permisos, pase muchas veces a modo TTY con Ctrl + Alt + F2 y luego a modo GUI con Ctrl + Alt + F7 pero no logre entrar. Finalmente, fue necesario hacer la opción 1 (reinstalar).

![No debe ser desatendida](img/unattendend.gif)


3) Debido a todo lo que sufri porque no podía entrar en modo GUI por hacer la instalación desatendida, en la preinstalación del idioma de Ubuntu, preferí hacer el proceso de Identificar Teclado para que reconociera el Español Latinoamericano porque no aparecía explicito en la lista inicial y no lo quise dejar solo Spanish por defecto.

![Teclado latino](img/teclado.png)
