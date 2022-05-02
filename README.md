# Práctica 3: Compilación del kernel de Linux

##  ¿Cómo hacer un respaldo de una máquina virtual? y ¿cómo levantar ese respaldo?
Cuando se realizan procedimientos que involucran al kernel, es importante realizar una copia de seguridad para prevenir que se pierdan los datos en caso de que exista algún fallo, está práctica fue realizada en un clon de la máquina virtual. Para hacer el respaldo se selecciona la máquina y se selecciona la opción de clonar, como se puede observar en la siguiente figura:

![Imagen1](PIC1.PNG)

Nos aparece la siguiente ventana, en donde se debe seleccionar un nombre para la máquina virtual, la ruta para guardarla y marcar las opciones adicionales. 

![Imagen1](PIC2.png)

Seleccionamos la opción de clonación completa e inciamos la clonación de la máquina virtual. 

![Imagen1](image2.png)

Una vez finalizado el proceso se puede observar en la parte izquierda, la copia de la máquina virtual.
![Imagen1](PIC3.PNG)

En la parte superior izquierda se puede observar como la máquina que esta corriendo en la clonada.

![Imagen1](PIC4.PNG)

##  Explicar la nomenclatura del kernel

##  Investigar y enlistar los paquetes requeridos para la compilación y ¿cómo instalarlos desde terminal?

Antes de poder realizar la compilación del kernel es necesario instalar los siguientes paquetes:

* git
* fakeroot
* build-essential
* ncurses-dev
* xz-utils
* libssl-dev
* bc
* flex
* libelf-dev
* bison

Para poder realizar la instalación desde terminal se utiliza el siguiente comando:
```bash
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
```
![Imagen1](PIC5.PNG)
![Imagen1](PIC6.PNG)

Además se requiere de la instalación de los siguientes modúlos adicionales:
* dwarves
* zstd

Para poder realizar la instalación desde terminal se utilizan los siguientes comandos:
```bash
sudo apt install dwarves
```
```bash
sudo apt-get install zstd
```
![Imagen1](PIC7.PNG)
![Imagen1](PIC8.PNG)

Es importante mencionar que para la instalación y pasos posteriores se debe contar con todos los permisos. 

##  ¿Cómo descargar una versión de kernel desde terminal?

Para descargar una versión de kernel se utiliza el comando wget junto con el link de la versión que se requiere, en este caso se seleccionó la versión  5.17.5. Para esto, se visita el sitio oficial de Linux con las diversas versiones de kernel : https://www.kernel.org/

```bash
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.17.5.tar.xz
```
![Imagen1](PIC9.PNG)

##  ¿Cómo extraer el código comprimido del kernel desde terminal?
Una vez que se descarga la versión del kernel, es necesario extraer el código ya que se encuentra compromido, para esto se debe hacer uso del siguiente comando, en donde se coloca el archivo que fue previamente descargado. 
```bash
tar xvf linux-5.17.5.tar.xz
```
![Imagen1](PIC10.PNG)
![Imagen1](PIC11.PNG)

##  ¿Cómo configurar el kernel?
Primero, es necesario movernos a la carpeta del kernel, después se realiza una copia del archivo de configuración del kernel actual a el archivo de configuración del kernel que queremos instalar.
```bash
cd linux-5.17.5
cp -v /boot/config-$(uname -r) .config
make menuconfig
```
![Imagen1](PIC12.PNG)

Para poder cambiar la configuración, se necesario utilizar el siguiente comando, el cual depsliega una interfaz gráfica para hacer las modificaciones correspondientes. Una vez que se termine, se guarda y se sale del menú, regresando así, a la línea de comandos. 

![Imagen1](PIC13.PNG)

En la siguiemte figura se muestra el menu correspondiente, en donde se tienen diversas opciones, al final es importante guardar los cambios correspondientes y salir. 

![Imagen1](PIC14.PNG)

##  ¿Cómo compilar el código del kernel?
Antes de poder realizar la compilación del kernel, es necesario realizar unos pasos previos. En el archivo de configuración del kernel, es necesario modificar las siguientes líneas, a través de los siguientes comandos:

```bash
scripts/config --set-str SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
```
![Imagen1](PIC15.PNG)

Una vez realizado lo anterior se comienza con la compilación con el siguiente comando:
```bash
make
```
![Imagen1](PIC16.PNG)
![Imagen1](PIC17.PNG)


##  ¿Cómo instalar módulos?
El comando para instalar los módulos es el siguiente:
```bash
sudo make modules_install
```
![Imagen1](PIC18.PNG)
![Imagen1](PIC19.PNG)

##  ¿Cómo instalar el kernel?

Finalemente se realiza la instalación del kernel a través del siguiente comando:

```bash
sudo make install
```
![Imagen1](PIC20.PNG)

##  ¿Cómo indicarle a la computadora con cuál kernel debe iniciar?
Al momento de iniciar la computadora es necesario presionar la tecla shift para poder ver el menú grub, el cual contiene las opciones de kernel que están disponibles, para poder visualizar ese menú se realizaron los siguientes pasos, se utilizó el siguiente comando para poder entrar al archivo de configuración de grub para poder insertar las siguientes tres líneas al inicio:
```bash
sudo nano /etc/default/grub
```
![Imagen1](PIC21.PNG)


```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
![Imagen1](PIC22.PNG)

##  ¿Cómo verificar el cambio de kernel a partir de consola?




