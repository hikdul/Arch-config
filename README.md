# Configuracion Para Arch Linux

este archivo es para tener almacenado todo el proceso de instalacion y configuracion de mi Arch Linux. realmente luego de leer varios documentos y muchos videos de youtube pude hacerme con algo. 

## Pasos para generar la instalacion

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
 * TODO: Buscar como crear mi propia plantilla para Oh-mi-zsh. Aca se deben de instalar diferentes plugins.
 6.1 [Zsh History Substring Search](https://github.com/zsh-users/zsh-history-substring-search)
        Un complemento que facilita la búsqueda en el historial de comandos de Zsh.

 6.2 [Zsh Syntax Highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
        Proporciona resaltado de sintaxis para comandos en la terminal Zsh. 

 6.3 [Zsh Autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)
        Sugerencias automáticas mientras escribes en la terminal Zsh. https://github.com/zsh-users/zsh-auto...

7.- Ahora mi paso a seguir es configurar neovim, para esto se puede usar mi propio [repositorio](https://github.com/hikdul/nvim)

---


### carpeta config

* Up[26JUN2024] => contiene todos los datos que se estan manejando hasta ahora

#### Referencias

* en este [video](https://www.youtube.com/watch?v=Ka76a9UzRDM&list=PL6hUe7QiuXd6IjklArH0KlqcW-S4KHsCG&index=10) se muestra una configuracion bastante interesante, francamente esta es la que use como base final de configuracion.
* con este [video](https://www.youtube.com/watch?v=ltbhkjipafs&t=124s) se esplica un poco de la instalacion gracias a instalador de archinstall
https://www.youtube.com/watch?v=ltbhkjipafs&t=124s
* En este otro [video](https://www.youtube.com/watch?v=2rh4Ik4WQZA&t=2883s) explica todos los pasos a seguir previos a la instalacion para una instalacion manual. De este realmente lo importante fue tomar la palabras ttecnicas para luego ampliar mi vocabulario

