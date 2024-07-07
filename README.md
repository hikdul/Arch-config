# Configuracion Para Arch Linux

este archivo es para tener almacenado todo el proceso de instalacion y configuracion de mi Arch Linux. en particular uso linux en dual boot junto a windows, asi que este documento se prepara para hacer esa configuracion.

## Pasos para generar la instalacion

### pre-instalacion
normalmente hay que hacer una configuracion previa en windows para que linux no nos moleste; todos esos datos los podemos conseguir en este [link](https://wiki.archlinux.org/title/Dual_boot_with_Windows).

de igual modo y a nivel general los pasos son desactivar el inicio rapido y modo de hibernacion de windows; y por otro lado desactivar el arranque seguro dentro del sistema UEFI.

### instalacion

para instalar arch no es mas si no configurar nuestros disco duro y generar la instalacion con **archinstall** y alli saber que vamos a tener el modo desktop con el tipo de escritorio **hyprland** ya que toda mi configuracion se basa en esto. Tambien recordar agregar los siguientes paquetes:
* gcc => GNU Compiler Collection.
* nvim => como editor de texto inicial, aunque el instalador de arch instala vim.
* git => para tener acceso a los repositorios
* firefox => para ingresar a internet
* fastfetch => para ver los datos del consumo y trabajo de nuestro equipo con el nuevo sistema operativo.
y por ultimo agregar el repositorio extra **mustilib**

### postinstalacion
aca se cubren varias etapas, pero la primera es configurar el dual boot ya que arch no instala ni configura todos los elementos necesarios para que esto funcione a la perfeccion; ya luego iremos instalando y configurando cada paquete piana a piano.

#### configuracion de dual boot

una ves completada la instalacion nos indica que si deseamos hacer root, aca aceptamos y seguimos los siguientes pasos:
* `sudo pacman -Syu` 
* `sudo pacman -S grub efibootmgr mtools` 
* `grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`
* `grub-mkconfig -o /boot/grub/grub.cfg`
luego reiniciamos el sistema y entramos a linux, aun nos falta un par de pasos mas para que esto funcione. 
una ves en linux ingresamos en nuestro terminal, en mi caso debo de pasar el teclado a la distro *dvorak* en el archivo de configuracion de *hypr* y continuamos trabajando (para pasar solo agregamos la linea `kb_variant = dvorak` en los datos de configuracion del teclado o input)
* ahora instalamos el *os-prober* que es quien nos detectara nuestro windows sudo `pacman -S os-prober`
* una ves instalado entramos en el archivo **/etc/default/grub** y descamentamos la siguiente linea `GRUB_DISABLE_OS_PROBER=true`.
* luego ejecutamos el siguiente comando para que recosca nuestros so's `sudo grub-mkconfig -o /boot/grub/grub.cfg`
* si al reiniciar esto no funciona, se debe de hacer nuevamente los ultimos 2 pasos y asi nuestro so queda funcionando.

#### intstalando yay
en este segmento obtendremos acceso a los paquetes de la comunidad, para poder instalar paquetes opcionales que no estan en el repositorio original. este paso es importante ya que con el accederemos a la instalacion de otras aplicaciones. debido a que puede cambiar el modo de instalacion lo recomendable es seguir las instrucciones [oficiales](https://github.com/Jguer/yay?tab=readme-ov-file)


---
desde aca son elementos... aun no se termina este documonto
---

#### etapa 1, instalacion, fuente, terminal y editor base.

1.- Instalacion: En cuanto a la configuracion, del disco y los demas elemento se puede hacer de manera manual o utilizando el instalador `archinstall`. 
 * para el type se recomienda hacer una instalacion minima, asi solo tenemos los paquetes base de arch.
 * en el caso de los paquetes extras se recomienda agregar: git, neovim y gcc.
 * tambien agregar los repositorios extra (multilib)
 De este modo la instalacion durara unos pocos minutos. Una ves se complete esta instalacion reiniciamos nuestro sistema. 

2.- En este caso vamos a ir instalando y configurando cada una de las aplicaciones necesarias, en lo personal luego de la instalacion actualiza el sistema con `sudo pacman -Syu` y los primero que prefiero instar  es [yay](https://github.com/Jguer/yay?tab=readme-ov-file) y configurar nuestro neovim para trabajar con comodidad. [es posible que necesites conectarte a internet]

3.- Empezamos a instalar los paquetes: `fastfetch` => [configuracion](./config/fastfetch/config.jsonc); con este elemento probando antes y el despues de configurar ya podemos ver que camino va tomando nuestro SO.

4.- ahora instalamos [hyprland](https://wiki.archlinux.org/title/Hyprland), [firefox o buscar otro explorador] , [kitty](https://wiki.archlinux.org/title/Kitty), _ranger_ (sustituir por: [thunar](https://wiki.archlinux.org/title/thunar)). En el caso de las fuentes escojemos las gnu-free-fonts(opt 1), y ya aqui esperamos que todo instale y luego continuamos con la configuraciones.
 * __hyprland__, es el windows Mannagement. [config](./config/hypr/hyprland.conf)
 * __kitty__, es el simulador de terminal. [config](./config/kitty); 
 * __ranger__ o __thunar__, son en si el explorador de archivos.[Aun no selecciono con cual quedarme]

5.- en este punto arrancamos el sistema con `Hyprland`. Una ves iniciado nos muestra un disclaimer horrible en la parte superior que nos indica como quitarlo y empezar a trabajar con la edicion de nuestro Windows Mannagement.[basicamente es undir WIN+Q y con neovim editar una linea del archivo de configuracion y ya esta]. la [configuracion final](./config/hypr/hyprland.conf) esta activa y se podra aplicar una ves se instalen todas las aplicasiones necesarias.

6.- Para configurar Kitty, use el siguinte [video](configuracion) como base. mi [configuracion](./config/kitty) se rige bajo el repositorio, pero los pasos bases a seguir son los siguientes:
 * instalar [zsh](https://wiki.archlinux.org/title/Zsh). Con el simple comando `sudo pacman -S zsh` se instala
 * una ves instalado el zsh, lo ponemos como linea de comandos principal `chsh -s $(which zsh)`; _Nota:_ si lo creas con el `sudo` el cambio se realiza para el superUsuario no para el usuarios actual. 
 * ahora instalamos [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh), la instalacion esta en el github.
 * para configurar mi zsh, configuramos el archivo `.zshrc` con `sudo nvim .zshrc`. puede ojerar mi [configuracion](./config/zshrc.copy) 
  Para la configuracion por favor retirar `.copy`
  * [Zsh History Substring Search](https://github.com/zsh-users/zsh-history-substring-search)
        Un complemento que facilita la búsqueda en el historial de comandos de Zsh.

  * [Zsh Syntax Highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
        Proporciona resaltado de sintaxis para comandos en la terminal Zsh. 

  * [Zsh Autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)
        Sugerencias automáticas mientras escribes en la terminal Zsh. https://github.com/zsh-users/zsh-auto...
  * instalar las fuentes de [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts?tab=readme-ov-file#option-4-arch-extra-repository) (aca la que me gusta)[https://aur.archlinux.org/packages/nerd-fonts-complete-mono-glyphs) y de manera manual descargar la fuente [agave](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/Agave.zip)

7.- Ahora mi paso a seguir es configurar neovim, para esto se puede usar mi propio [repositorio](https://github.com/hikdul/nvim)


#### etapa 2, windows mannagement, aplicasienes necesarias y cambios visuales validos.

una ves configurado de el terminal y todo lo que lleva se viene la parte de instalar aplicasiones he ir dejando las configuraciones necesarias

* waypaper: para manejar los fondos de escritorio
* Weybar: La verdad que no me gusto.. mi idea es quitarme este weybar para generar mayor productividad..
* fastfetch: para ver los datos del equipo con un simple comando.
* rofi: o un lanzador de aplicasiones[todo]

---

### carpeta config

* Up[26JUN2024] => contiene todos los datos que se estan manejando hasta ahora
---

###### Referencias

* en este [video](https://www.youtube.com/watch?v=Ka76a9UzRDM&list=PL6hUe7QiuXd6IjklArH0KlqcW-S4KHsCG&index=10) se muestra una configuracion bastante interesante, francamente esta es la que use como base final de configuracion.
* con este [video](https://www.youtube.com/watch?v=ltbhkjipafs&t=124s) se esplica un poco de la instalacion gracias a instalador de archinstall
https://www.youtube.com/watch?v=ltbhkjipafs&t=124s
* En este otro [video](https://www.youtube.com/watch?v=2rh4Ik4WQZA&t=2883s) explica todos los pasos a seguir previos a la instalacion para una instalacion manual. De este realmente lo importante fue tomar la palabras ttecnicas para luego ampliar mi vocabulario

