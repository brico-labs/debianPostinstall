Introducción
============

Mi portátil es un ordenador Acer 5755G con las siguientes características:

-   Core i5 2430M 2.4GHz

-   NVIDIA Geforce GT 540M

-   8Gb RAM

-   750Gb HD

La gráfica es una Nvidia Optimus, es decir una tarjeta híbrida que funciona perfectamente en Ubuntu 14.04 usando Bumblebee.

Para hacer la actualización del sistema opté por desinstalar el dvd y montar en su lugar un disco SSD en un Caddie para Acer. La instalación fué muy fácil, y aunque el portátil arranca perfectamente de cualquiera de los dos discos opté por instalar el SSD en la bahía del HD original y pasar el HD al caddie.

Comentar los problemas con calentamiento en Ubuntu

Comentar la creación de usb bootable

Lo primero fue la instalación del Bumblebee

firmware-linux-nonfree Bumblebee-nvidia primus

Gestión de paquetes
===================

Instalamos *aptitude*, *synaptic* y *gdebi*

``` {bash}
sudo apt-get install aptitude
sudo apt-get install synaptic
sudo apt-get install gdebi
```

Cambiamos las opciones de *aptitude* para que **no instale** los paquetes recomendados.

Quitamos el cdrom de los sources.list
-------------------------------------

Editamos el fichero */etc/apt/sources.list* y comentamos las lineas del cdrom.

Habilitamos los backports y multimedia
--------------------------------------

### Backports:

``` {bash}
sudo cat > /etc/apt/sources.list.d/backports.list << EOF
# backports
deb http://ftp.debian.org/debian/ jessie-backports main contrib non-free
EOF
```

### Multimedia:

``` {bash}
sudo cat >> /etc/apt/sources.list.d/multimedia.list << EOF
# multimedia
deb http://www.deb-multimedia.org/ jessie main non-free
EOF

sudo apt-get -y --allow-unauthenticated install --reinstall deb-multimedia-keyring
```

Y actualizamos

``` {bash}
sudo aptitude update
```

Instalación de varios paquetes sueltos
======================================

Programas de utilidad y uso frecuente
-------------------------------------

### Menulibre

Un editor de menús para Gnome, nos permite generar los archivos desktop para cualquier aplicación. Mucho más completo que *alacarte* la otra alternativa.

    sudo apt-get install menulibre

### Terminator

Terminator es un emulador de terminal muy completo y muy flexible. Los instalamos desde *aptitude*

``` {bash}
sudo aptitude install terminator python-keybinder
```

### Keepass2

Instalado *keepass2* desde Debian

    sudo aptitude install keepass2

### gksu

Un *sudo* en modo gráfico:

    sudo aptitude install gksu

### Diskmanager

Para gestionar discos portátiles

    sudo apt-get install ntfs-3g disk-manager

### Gnucash

Finanzas en linux

    sudo apt-get -t jessie-backports install gnucash

### Herramientas *sync*

No sin mis *backups*

    sudo apt-get install rsync grsync

### Dropbox

Bajado el paquete Debian desde la página [web de Dropbox](https://www.dropbox.com/install-linux), instalado el paquete con *packageinstall*, es decir, simplemente pinchando desde el gestor de ficheros.

### Compresores et al

``` {bash}
sudo apt-get install rar unrar zip unzip unace bzip2 lzop p7zip p7zip-full p7zip-rar
```

Internet
--------

### Chrome

Instalado chrome añadiendo fuentes a aptitude. No recuerdo como las añadí, en el fichero */etc/apt/sources.list.d/google-chrome.list*, tengo los siguientes contenidos:

    ###
    ###
    ###
    ###
    ### THIS FILE IS AUTOMATICALLY CONFIGURED ###
    # You may comment out this entry, but any other modifications may be lost.
    deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main

Ejecutamos:

``` {bash}
sudo aptitude install google-chrome-stable
sudo aptitude install chromium
```

### Tor

Bajado el comprimido desde la web y descomprimido en *~/apps* copiado el fichero desktop a *~/.local/share/applications*

### Deluge

Instalamos desde aptitude

    sudo aptitude install deluge
    xdg-mime default deluge.desktop x-scheme-handler/magnet

Gráficos
--------

### Inkscape

``` {bash}
apt-cache policy inkscape
apt-get -t jessie-backports install inkscape
aptitude install ink-generator
```

### LibreCAD y FreeCAD

Instalado desde repos con aptitude

    apt-get install librecad

    apt-get -t jessie-backports install freecad

### Gimp

Gimp ya estaba instalado, adicionalmente instalado el gimp data-extra

    sudo aptitude install gimp-plugin-registry gimp-texturize gimp-data-extras gimp-gap

Fotografía
----------

### Rawtherapee y Darktable: Tratamiento de imágenes fotogŕaficas

    sudo aptitude install icc-profiles icc-profiles-free
    sudo aptitude install rawtherapee darktable

### Stopmotion

    sudo aptitude install stopmotion vgrabbj dvgrab

TODO: Probar qStopmotion

Audio y video
-------------

### Codecs

Instalamos los codecs

``` {bash}
sudo apt-get install libav-tools

sudo apt-get install faad gstreamer0.10-ffmpeg gstreamer0.10-x \
gstreamer0.10-fluendo-mp3 gstreamer0.10-plugins-base \
gstreamer0.10-plugins-good gstreamer0.10-plugins-bad \
gstreamer0.10-plugins-ugly ffmpeg lame twolame vorbis-tools \
libquicktime2 libfaac0 libmp3lame0 libxine2-all-plugins libdvdread4 \
libdvdnav4 libmad0 sox libxvidcore4 libstdc++5

sudo apt-get install w64codecs
```

### Reproductores de música

Instalamos *Clementine*, *decibel*, *audacity*, *soundconverter*:

``` {bash}
sudo aptitude install clementine gstreamer0.10-plugins-bad
sudo aptitude install decibel-audio-player audacity soundconverter
```

### Gpodder

Instalamos *gpodder* para gestionar nuestros podcast, aunque *Clementine* también nos vale.

    sudo aptitude install gpodder

### Spotify

Cliente de *Spotify*

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys BBEBDCB318AD50EC6865090613B00F1FD2C19886
    echo deb http://repository.spotify.com stable non-free | sudo tee /etc/apt/sources.list.d/spotify.list
    sudo aptitude update
    sudo aptitude install spotify-client

### Video

Instalamos también utilidades de video:

``` {bash}
sudo aptitude install vlc browser-plugin-vlc
sudo aptitude install recordmydesktop gtk-recordmydesktop
sudo aptitude install handbrake handbrake-cli handbrake-gtk
```

Documentos
==========

Calibre
-------

Ejecutamos lo que manda la página web:

    sudo -v && wget -nv -O- https://raw.githubusercontent.com/kovidgoyal/calibre/master/setup/linux-installer.py \
    | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()"

Para usar el calibre con el Kobo Glo:

-   Desactivamos todos los plugin de Kobo menos el *Kobo Touch Extended*
-   Creamos una columna *MyShelves* con identificativo *\#myshelves*
-   En las opciones del plugin:

    -   En la opción *Collection columns* añadimos las columnas *series,\#myshelves*
    -   Marcamos las opciones *Create collections* y *Delete empy collections*
    -   *Update metadata on device* y *Set series information*

Algunos enlaces útiles:

-   <https://github.com/jgoguen/calibre-kobo-driver>
-   <http://www.lectoreselectronicos.com/foro/showthread.php?15116-Manual-de-instalaci%C3%B3n-y-uso-del-plugin-Kobo-Touch-Extended-para-Calibre>
-   <http://www.redelijkheid.com/blog/2013/7/25/kobo-glo-ebook-library-management-with-calibre>
-   <https://www.netogram.com/kobo.htm>

Pandoc
------

Instalado el Pandoc descargando paquete *deb* desde la página web del Pandoc.

Descargamos las plantillas desde [el repo](https://github.com/jgm/pandoc-templates) ejecutando los siguientes comandos:

``` {bash}
cd ~/.pandoc
git clone https://github.com/jgm/pandoc-templates templates
```

Vanilla LaTeX
-------------

El LaTeX de Debian está un poquillo anticuado, si se quiere usar una versión reciente hay que aplicar [este truco](http://tex.stackexchange.com/questions/1092/how-to-install-vanilla-texlive-on-debian-or-ubuntu).

``` {bash}
cd ~
mkdir tmp
cd tmp
wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz
tar xzf install-tl-unx.tar.gz
cd install-tl-xxxxxx
```

La parte xxxxxx varía en función del estado de la última versión de LaTeX disponible.

``` {bash}
sudo ./install-tl
```

Una vez lanzada la instalación podemos desmarcar las opciones que instalan la documentación y las fuentes. Eso nos obligará a consultar la documentación *on line* pero ahorrará practicamente el 50% del espacio necesario. En mi caso sin *doc* ni *src* ocupa 2,3Gb

``` {bash}
mkdir -p /opt
sudo ln -s /usr/local/texlive/2016/bin/* /opt/texbin
```

Por último para acabar la instalación añadimos **/opt/texbin** al *path*.

### Falsificando paquetes

Ya tenemos el **texlive** instalado, ahora necesitamos que el gestor de paquetes sepa que ya lo tenemos instalado.

``` {bash}
sudo apt-get install equivs --no-install-recommends
mkdir -p /tmp/tl-equivs && cd /tmp/tl-equivs
equivs-control texlive-local
```

Para hacerlo más fácil podemos descargarnos un fichero ya preparado, ejecutando:

``` {bash}
wget http://www.tug.org/texlive/files/debian-equivs-2015-ex.txt
/bin/cp -f debian-equivs-2015-ex.txt texlive-local
```

Editamos la versión y

``` {bash}
equivs-build texlive-local
sudo dpkg -i texlive-local_2015-1_all.deb
```

Todo listo, ahora podemos instalar cualquier paquete que dependa de texlive

### Fuentes

Para dejar disponibles las fuentes opentype y truetype que vienen con texlive para el resto de aplicaciones:

``` {bash}
sudo cp $(kpsewhich -var-value TEXMFSYSVAR)/fonts/conf/texlive-fontconfig.conf /etc/fonts/conf.d/09-texlive.conf
gksudo gedit /etc/fonts/conf.d/09-texlive.conf
```

Borramos la linea:

``` {xml}
<dir>/usr/local/texlive/2016/texmf-dist/fonts/type1</dir>
```

Y ejecutamos:

``` {bash}
sudo fc-cache -fsv
```

### Actualizaciones

Para actualizar nuestro latex a la última versión de todos los paquetes:

``` {bash}
sudo /opt/texbin/tlmgr update --self
sudo /opt/texbin/tlmgr update --all
```

También podemos lanzar el instalador gráfico con:

``` {bash}
sudo /opt/texbin/tlmgr --gui
```

Para usar el instalador gráfico hay que instalar previamente:

``` {bash}
sudo apt-get install perl-tk --no-install-recommends
```

### Lanzador para el actualizador de texlive

``` {bash}
mkdir -p ~/.local/share/applications
/bin/rm ~/.local/share/applications/tlmgr.desktop
cat > ~/.local/share/applications/tlmgr.desktop << EOF
[Desktop Entry]
Version=1.0
Name=TeX Live Manager
Comment=Manage TeX Live packages
GenericName=Package Manager
Exec=gksu -d -S -D "TeX Live Manager" '/opt/texbin/tlmgr -gui'
Terminal=false
Type=Application
Icon=system-software-update
EOF
```

Ojo que hay que dejar instalado el gksu (aunque debería estar de antes si sigues este doc)

``` {bash}
sudo aptitude install gksu
```

Emacs
-----

Instalado emacs desde los repos:

``` {bash}
sudo aptitude install emacs
```

Instalamos los paquetes *markdown-mode*, *mardown-plus* y *pandoc-mode* desde el menú de gestión de paquetes de **emacs**.

También instalamos *d-mde* y *flymake-d*. Hay una sección de configuración en el fichero *.emacs*.

Configuramos el fichero *.emacs* definimos algunas preferencias, algunas funciones útiles y añadimos orígenes extra de paquetes.

``` {lisp}
(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(column-number-mode t)
 '(show-paren-mode t))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(default ((t (:family "Mensch" :foundry "bitstream" :slant normal :weight normal :height 128 :width normal)))))
;;------------------------------------------------------------
;; Some settings
(setq inhibit-startup-message t) ; Eliminate FSF startup msg
(setq frame-title-format "%b")   ; Put filename in titlebar
;(setq visible-bell t)            ; Flash instead of beep
(set-scroll-bar-mode 'right)     ; Scrollbar placement
(show-paren-mode t)              ; Blinking cursor shows matching parentheses
(setq column-number-mode t)  ; Show column number of current cursor location
(mouse-wheel-mode t)         ; wheel-mouse support

(setq fill-column 78)
(setq auto-fill-mode t)          ; Set line width to 78 columns...

(setq-default indent-tabs-mode nil)       ; Insert spaces instead of tabs
(global-set-key "\r" 'newline-and-indent) ; turn autoindenting on
;(set-default 'truncate-lines t)           ; Truncate lines for all buffers
(require 'iso-transl)

;;------------------------------------------------------------
;; Some useful key definitions
(define-key global-map [M-S-down-mouse-3] 'imenu)
(global-set-key [C-tab] 'hippie-expand)                    ; expand
(global-set-key [C-kp-subtract] 'undo)                     ; [Undo]
(global-set-key [C-kp-multiply] 'goto-line)                ; goto line
(global-set-key [C-kp-add] 'toggle-truncate-lines)         ; goto line
(global-set-key [C-kp-divide] 'delete-trailing-whitespace) ; delete trailing whitespace
(global-set-key [C-kp-decimal] 'completion-at-point)       ; complete at point
(global-set-key [C-M-prior] 'next-buffer)                  ; next-buffer
(global-set-key [C-M-next] 'previous-buffer)               ; previous-buffer

;;------------------------------------------------------------
;; Set encoding
(prefer-coding-system 'utf-8)
(setq coding-system-for-read 'utf-8)
(setq coding-system-for-write 'utf-8)

;;------------------------------------------------------------
;; Maximum colors
(cond ((fboundp 'global-font-lock-mode)  ; Turn on font-lock (syntax highlighting)
       (global-font-lock-mode t)               ; in all modes that support it
       (setq font-lock-maximum-decoration t))) ; Maximum colors

;;------------------------------------------------------------
;; Use % to match various kinds of brackets...
;; See: http://www.lifl.fr/~hodique/uploads/Perso/patches.el

(global-set-key "%" 'match-paren)               ; % key match parents
(defun match-paren (arg)
  "Go to the matching paren if on a paren; otherwise insert %."
  (interactive "p")
  (let ((prev-char (char-to-string (preceding-char)))
        (next-char (char-to-string (following-char))))
    (cond ((string-match "[[{(<]" next-char) (forward-sexp 1))
          ((string-match "[\]})>]" prev-char) (backward-sexp 1))
          (t (self-insert-command (or arg 1))))))

;;------------------------------------------------------------
;; The wonderful bubble-buffer
(defvar LIMIT 1)
(defvar time 0)
(defvar mylist nil)

(defun time-now ()
   (car (cdr (current-time))))

(defun bubble-buffer ()
   (interactive)
   (if (or (> (- (time-now) time) LIMIT) (null mylist))
       (progn (setq mylist (copy-alist (buffer-list)))
          (delq (get-buffer " *Minibuf-0*") mylist)
          (delq (get-buffer " *Minibuf-1*") mylist)))
   (bury-buffer (car mylist))
   (setq mylist (cdr mylist))
   (setq newtop (car mylist))
   (switch-to-buffer (car mylist))
   (setq rest (cdr (copy-alist mylist)))
   (while rest
     (bury-buffer (car rest))
     (setq rest (cdr rest)))
   (setq time (time-now)))

(global-set-key [f8] 'bubble-buffer)    ; win-tab switch the buffer

(defun geosoft-kill-buffer ()
   ;; Kill default buffer without the extra emacs questions
   (interactive)
   (kill-buffer (buffer-name))
   (set-name))
(global-set-key [C-delete] 'geosoft-kill-buffer)

;;----------------------------------------------------------------------
;; MELPA and others
(when (>= emacs-major-version 24)
  (require 'package)
  (package-initialize)
  (add-to-list 'package-archives '("melpa" . "http://melpa.org/packages/") t)
  (add-to-list 'package-archives '("gnu" . "http://elpa.gnu.org/packages/") t)
  (add-to-list 'package-archives '("marmalade" . "https://marmalade-repo.org/packages/") t)
  )

;;----------------------------------------------------------------------
;; flymake installed from package

(require 'flymake)
(global-set-key (kbd "C-c d") 'flymake-display-err-menu-for-current-line)
(global-set-key (kbd "C-c n") 'flymake-goto-next-error)
(global-set-key (kbd "C-c p") 'flymake-goto-prev-error)

;; Activate flymake for D
(add-hook 'd-mode-hook 'flymake-d-load)
```

Scribus
-------

Instalado con aptitude

    sudo aptitude install scribus

Comix
-----

Instalado con aptitude

    sudo aptitude install comix

Desarrollo sw
=============

Git
---

Instalado git desde aptitude

``` {bash}
sudo aptitude install git
```

Configuración básica de **git**

``` {bash}
git config --global user.name "Sergio Alvariño"
git config --global user.email "salvari@gmail.com"
git config --global core.editor emacs
git config --global color.ui true
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=7200'
git config --global push.default simple
git config --global alias.sla 'log --oneline --decorate --graph --all'
git config --global alias.car 'commit --amend --no-edit'
git config --global alias.unstage reset
git config --global alias.st status
git config --global alias.last  'log -1 HEAD'
git config --global alias.ca 'commit -a'
```

Paquetes esenciales
-------------------

    sudo apt-get install build-essential checkinstall make automake cmake autoconf git git-core dpkg wget

Open Java
---------

    apt-get install openjdk-7-jre icedtea-7-plugin

D-apt e instalación de programas
--------------------------------

configurado d-apt, instalados todos los programas incluidos

``` {bash}
sudo wget http://master.dl.sourceforge.net/project/d-apt/files/d-apt.list -O /etc/apt/sources.list.d/d-apt.list
sudo apt-get update && sudo apt-get -y --allow-unauthenticated install --reinstall d-apt-keyring && sudo apt-get update
```

Instalamos todos los programas asociados.

DCD
---

Configuración de DCD

Emacs para editar D
-------------------

Instalados los siguientes paquetes desde *marmalade*

-   *d-mode*
-   *flymake-d*

Se configura en el fichero **~/.emacs**:

``` {lisp}
(require 'flymake)
(global-set-key (kbd "C-c d") 'flymake-display-err-menu-for-current-line)
(global-set-key (kbd "C-c n") 'flymake-goto-next-error)
(global-set-key (kbd "C-c p") 'flymake-goto-prev-error)

;; Activate flymake for D
(add-hook 'd-mode-hook 'flymake-d-load)
```

Processing
----------

Bajamos los paquetes de las respectivas páginas web, descomprimimimos en *~/apps/* y creamos los desktop file con **Menulibre**

Openframeworks
--------------

Bajamos el paquete comprimido de la página web del proyecto.

Descomprimimos en *~/apps*

Bajamos al directorio de la aplicación y ejecutamos:

    sudo  scripts/linux/debian/install_dependencies.sh
    sudo  scripts/linux/debian/install_codecs.sh

    cd scripts/linux
    ./compileOF.sh -j2

    cd OF/examples/graphics/polygonExample
    make
    make Run

    cd OF/scripts/linux
    ./compilePG.sh

Va a instalar un montón de dependencias, hay que tomarlo con calma.

Al final también va a añadir una linea al fichero *~/.profile*

    export PG_OF_PATH=/home/salvari/apps/of/of_v0.9.3_linux64_release

Python
------

De partida tenemos instalado dos versiones: *python* y *python3*

``` {bash}
python -V
Python 2.7.9

python3 -V
Python 3.4.2
```

Instalado python-pip y python-virtualenv desde aptitude.

``` {bash}
sudo aptitude install python-pip python-virtualenv
```

Instalamos a mayores *Ananconda*, es la forma fácil de poder usar *ipython notebook*. De hecho me he instalado dos versiones la que incluye el python2 y la que incluye el python3.

Las instalaciones de *Anaconda* son redundantes, basta con instalar uno de ellos. En cualquier caso para realizar la instalación basta con descargar los scripts de instalación desde la página web de Anaconda.

``` {bash}
bash Anaconda3-4.2.0-Linux-x86_64.sh
bash Anaconda2-4.2.0-Linux-x86_64.sh
```

Los he dejado instalados en *~/apps/anaconda2* y *~/apps/anaconda3*

Cada una de estas instalaciones incorpora su propia versión de Python. Para usarlas tenemos que cambiar nuestro PATH para que el Python deseado sea el primero que se selecciona.

Por ejemplo para activar anaconda3 en bash:

``` {bash}
export PATH="~/apps/anaconda3/bin:$PATH"
```

Para hacer lo mismo en fish:

``` {fish}
set -x PATH ~/apps/anaconda3/bin $PATH
```

### iPython y GraphLab

Creamos un entorno conda con Python 2.7.x

    conda create -n gl-env python=2.7 anaconda 

Activamos el nuevo entorno (todo esto lo hice en bash, en fish hay un problemilla con el entorno conda [mas info](https://penandpants.com/2014/02/28/using-conda-environments-and-the-fish-shell/))

    bash
    source activate gl-env

En el futuro esto es todo lo que tendremos que hacer activar el entorno conda donde estamos instalando el iPython.

Nos aseguramos de tener *pip* al dia:

    conda update pip

Instalamos la biblioteca [GraphLab Create](https://turi.com/products/create/). Esta biblioteca se supone que es fácil de usar pero está sujeta a licencia. [1]

Una vez registrado en la página web te pasan un número de registro que tienes que usar para instalar la biblioteca.

    pip install --upgrade --no-cache-dir https://get.graphlab.com/GraphLab-Create/2.1/your registered email address here/your product key here/GraphLab-Create-License.tar.gz

Y para terminar instalamos iPython [2]:

    conda install ipython-notebook

Desde ahora basta con activar el entorno que hemos creado para tener acceso al iPython.

    source activate gl-env

    ipython notebook

    source deactivate gl-env

#### Instalación alternativa con virtualenv

    # Create a virtual environment named e.g. gl-env
    virtualenv gl-env

    # Activate the virtual environment
    source gl-env/bin/activate

    # Make sure pip is up to date
    pip install --upgrade pip

    # Install IPython Notebook (optional)
    pip install "ipython[notebook]"

    # Install Jupyter Notebook (optional)
    pip install "jupyter"


    # Install your licensed copy of GraphLab Create
    pip install --upgrade --no-cache-dir https://get.graphlab.com/GraphLab-Create/2.1/your registered email address here/your product key here/GraphLab-Create-License.tar.gz

### Usar Emacs para editar Python

Instalamos *elpy* desde el gestor de paquetes de Emacs, concretamente desde el repo *marmalade*

Hay que habilitar *elpy* en el fichero **~/.emacs** para ello añadimos la linea

``` {lisp}
(elpy enable)
```

#### TODO

Estudiar esto con calma <https://elpy.readthedocs.io/en/latest>

Desarrollo hardware
===================

Arduino IDE
-----------

Bajamos los paquetes de la página [web](https://www.arduino.cc) , descomprimimimos en *~/apps/arduino*.

Creamos un link al directorio del software que hemos descargado:

    cd ~/apps/arduino
    ln -s arduino-x.y.z current

La primera ves que instalamos será necesario crear el desktop file con **Menulibre** con las actulizaciones no será necesario, siempre y cuando apunte a *~/apps/arduino/current*

Pinguino IDE
------------

Tenemos el paquete de instalación disponible en su página [web](http://pinguino.cc/download.php)

Ejecutamos el programa de instalación. El programa descargará los paquetes Debian necesarios para dejar el IDE y los compiladores instalados.

Al acabar la instalación he tenido que crear el directorio *~/Pinguino/v11*, parece que hay algún problema con el programa de instalación y no lo crea automáticamente.

El programa queda correctamente instalado en */opt* y arranca correctamente, habrá que probarlo con los micros.

KiCAD
-----

Instalamos desde *backports*:

``` {bash}
sudo aptitude install -t jessie-backports kicad
```

Vamos a instalar a mayores algunas librerias de KiCAD, para poder crear Shields de Arduino.

-   [Freetronics](https://github.com/freetronics/freetronics_kicad_library) una libreria que no solo incluye Shield para Arduino sino una completa colección de componentes que nos permitirá hacer proyectos completos. [Freetronics](http://www.freetronics.com) es una especie de BricoGeek australiano, publica tutoriales, vende componentes, y al parecer mantiene una biblioteca para KiCAD. La biblioteca de Freetronics se mantiene en un repo de github. Lo suyo es incorporarla a cada proyecto, por que si la actualizas se pueden romper los proyectos que estes haciendo.
-   [eklablog](http://meta-blog.eklablog.com/kicad-librairie-arduino-pretty-p930786) Esta biblioteca de componentes está incluida en el github de KiCAD, así que teoricamente no habría que instalarla en nuestro disco duro.

Docker
======

``` {bash}
apt-get install apt-transport-https ca-certificates
apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
edit docker.list with
deb https://apt.dockerproject.org/repo debian-jessie main

apt-cache policy docker-engine   -- comprobamos que todo está bien.


sudo apt-get install docker-engine   -- da un error en makedev por udev activo


sudo service docker start

sudo docker run hello-world   - todo bien

sudo gpasswd -a salvari docker
```

Shells alternativos: zsh y fish
===============================

Los dos son muy interesantes. He usado zsh casi un año, ahora voy a probar **fish**.

fish
----

Instalamos **fish** desde aptitude con:

``` {bash}
sudo aptitude install fish
```

Instalamos oh-my-fish

``` {bash}
curl -L https://github.com/oh-my-fish/oh-my-fish/raw/master/bin/install > install
fish install
rm install

chsh -s `which fish`
```

zsh
---

Igualmente instalamos **zsh**:

``` {bash}
sudo aptitude install zsh
```

Vamos a usar antigen así que nos lo clonamos en \_~/apps/

``` {bash}
cd ~/apps
git clone https://github.com/zsh-users/antigen
```

Y editamos el fichero *~/.zshrc* para que contenga:

    source ~/apps/antigen/antigen.zsh

    # Load the oh-my-zsh's library.
    antigen use oh-my-zsh

    # Bundles from the default repo (robbyrussell's oh-my-zsh).
    antigen bundle git
    antigen bundle command-not-found
    antigen bundle autojump
    antigen bundle extract
    # antigen bundle heroku
    # antigen bundle pip
    # antigen bundle lein


    # Syntax highlighting bundle.
    antigen bundle zsh-users/zsh-syntax-highlighting

    # git
    antigen bundle arialdomartini/oh-my-git
    antigen theme arialdomartini/oh-my-git-themes oppa-lana-style

    # autosuggestions
    antigen bundle tarruda/zsh-autosuggestions

    #antigen theme agnoster

    # Tell antigen that you're done.
    antigen apply

    # append to path
    path+=('/home/salvari/apps/julia/current/bin/')
    # prepend
    # path=('/home/salvari/bin/' $path)
    # export PATH

Antigen ya se encarga de descargar todo lo que queramos utilizar en zsh.

Nos queda arreglar las fuentes para que funcione correctamente la linea de estado en los repos de git. Necesitamos una fuente *Awesome*

Instalación de fuentes adicionales
----------------------------------

Nos bajamos unas cuantas fuentes que soporten los iconos *Awesome*.

``` {bash}
cd ~/tmp
git clone https://github.com/abertsch/Menlo-for-Powerline
git clone https://github.com/powerline/fonts

mkdir ~/.fonts
cp someFontFile ~/.fonts/
fc-cache -vf ~/.fonts/
```

Cambiar las opciones de idioma
==============================

Ejecutamos:

``` {bash}
sudo dpkg-reconfigure locales
```

Y después solo tenemos que cambiar la selección del idioma en la configuración de Gnome.

Nos pedirá rearrancar Gnome y renombrará todos los directorios de sistema.

Reprap
======

Sl1c3r
------

Descargamos el paquete binario desde la página web.

-   Cambiar permisos en directorio */lib/vrt/*
-   Instalado *lib-canberra-module* desde aptitude
-   Es necesario instalar *freeglut*

OpenScad
--------

Instalado desde aptitude.

Printrun
--------

Descargamos desde github

Cura
----

Descargamos desde la pagina web

    sudo aptitude install python3-pyqt5
    sudo dpkg -i Cura-2.1.3-Linux.deb

``` {bash}
sudo apt-get install python-serial python-wxgtk2.8 python-pyglet python-numpy \
cython python-libxml2 python-gobject python-dbus python-psutil python-cairosvg git

python setup.py build_ext --inplace
```

Bases de datos
==============

MySQL
-----

Instalamos desde aptitude *mysql-server.5.6*

Opcionalmente (y muy recomendable)

    mysql_secure_instalallation

### Actualización

Cambiamos el fichero *mysql.conf.d/mysqld.cnf*

    # max_allowed_packet      = 16M
    max_allowed_packet  = 500M

Reiniciamos el servicio:

    /etc/init.d/mysql restart

Cliente SQL SQuirreL SQL
------------------------

Descargamos el paquete desde la página [web](http://squirrel-sql.sourceforge.net/) y lo descomprimimos en *~/apps*, también tendremos que descargar el conector de mysql para java, por ejemplo desde [aquí](http://dev.mysql.com/downloads/connector/j/3.0.html)

Una vez instalado, creamos el desktop-file con *MenuLibre* y configuramos el driver *MySQL* añadiendo el path a donde hayamos dejado el conector java.

Cuentas online abiertas
=======================

-   google
-   pocket (plugin de chrome)

TODO
====

-   cinelerra
-   zotero
-   playonlinux
-   darktable
-   rawtherapee
-   krita
-   mypaint
-   qStopmotion

Inkscape https://elizsarobhasa.makes.org/thimble/MTMwNDIzMjE5Mg==/3d-printing-from-a-2d-drawing Instalar tb jessyink

chibios \* http://wiki.chibios.org/dokuwiki/doku.php?id=chibios:community:setup:openocd\_chibios \* http://www.josho.org/blog/blog/2014/11/30/nucleo-gcc/ \* http://www.stevebate.net/chibios-rpi/GettingStarted.html

rclone \[https://syncthing.net/\]

vmware

sudo aptitude install chromium

Links
=====

-   [Systemd](https://wiki.debian.org/systemd)
-   [Gnome shortcuts](https://wiki.gnome.org/Design/OS/KeyboardShortcuts)
-   [Gnome optimizaciones](https://www.linux.com/learn/easy-steps-make-gnome-3-more-efficient)
-   [Instalación Debian](https://diversidadyunpocodetodo.blogspot.com.es/2015/03/sensores-temperatura-hardware-discos-cpu-debian-ubuntu.html)
-   [zsh](http://joshldavis.com/2014/07/26/oh-my-zsh-is-a-disease-antigen-is-the-vaccine/)
-   [zsh](http://blog.namangoel.com/zsh-with-antigen)
-   <https://www.roaringpenguin.com/products/remind>
-   <http://taskwarrior.org/>

[1] TODO: Pasarme a *scikit-learn*

[2] TODO: conda install jupyter
