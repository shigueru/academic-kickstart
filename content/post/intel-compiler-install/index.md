---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Instalación de los compiladores de Intel"
subtitle: "Linux/Ubuntu y derivadas"
summary: "Instalación de los compiladores de Intel para C++, C y Fortran en su version de cluster en un entorno linux."
authors: []
tags: [Intel, Compiler, Linux, Installation]
categories: [compilers]
date: 2020-06-26T22:16:38-05:00
lastmod: 2020-06-26T22:16:38-05:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
La instalación se realizará en un sistema GNU/Linux Ubuntu 20.04 Focal Fosa. Los comandos de terminal también serán compatibles en distribuciones de GNU/Linux derivadas de Ubuntu.

Los compiladores se encuentran reunidos en el paquete **Parallel studio XE 2020 cluster edition**. El instalador se puede descargar de la página de Intel (enlace). Se pueden obtener versiones para Windows, Linux o Mac.

En caso de ser estudiante puedes descargar el instalador de manera gratuita. Para esto necesitarás una cuenta de correo electrónico de una institución académica. La descarga libre también esta habilitada para contribuidores de software libre o educadores.

El instalador requiere de algunas dependencias. Podemos obtenerlas ejecutando el siguiente comando en la terminal.

> sudo apt install g++

Asumiré que el instalador se encuentra en la carpeta **Descargas** en el **Home** de tu usuario. El instalador que estoy utilizando se llama **Parallel_studio_XE_2020_cluster_edition.tgz** este nombre puede cambiar según pase el tiempo y se vaya actualizando a nuevas versiones.

Primero debes descomprimir el instalador. Luego tienes que abrir la terminal de Ubuntu y moverte dentro de la carpeta descomprimida. Utilizando el siguiente comando.

> cd ~/Descargas/parallel_studio_xe_2020_cluster_edition

Ejecuta el instalador utilizando el siguiente comando en la terminal de Ubuntu.

> ./install_GUI.sh

Deberías ver la siguiente ventana.

[![install-intel-compiler-1.png](https://i.postimg.cc/05W9gtBG/install-intel-compiler-1.png)](https://postimg.cc/G9yWGjr9)

Acepta los términos de licencia y presiona **Next** para continuar.

[![install-intel-compiler-2.png](https://i.postimg.cc/8P7NTh22/install-intel-compiler-2.png)](https://postimg.cc/8jgqHrP4)

Yo marco la opción de **no recolectar mi información**, pero eso queda a tu criterio. Cualquiera de las dos opciones es válida. Presiona Next para continuar.

[![install-intel-compiler-3.png](https://i.postimg.cc/52vJCfNp/install-intel-compiler-3.png)](https://postimg.cc/pm23Nbjn)

Ahora se te muestran algunos requisitos que el sistema no cumple. El primero te informa que se requieren permisos de administrador para un driver. Este driver no lo utilizarás si tu intención es solo compilar.

Si por alguna razón necesitas el driver. La solución es ejecutar el instalador con permisos de administrador.

> sudo ./install_gui

También te indica que el sistema operativo no está soportado. Esta advertencia puedes ignorarla sin preocupación. Presiona **Next** para continuar.

[![install-intel-compiler-4.png](https://i.postimg.cc/TwTTxBx0/install-intel-compiler-4.png)](https://postimg.cc/NyC37J52)

Aquí se te solicita una forma de activación. Debes escoger la opción adecuada según sea tu caso. Yo utilizo un número de serie. Lo obtuve durante la descarga del instalador. Presiona **Next** para continuar.

[![install-intel-compiler-5.png](https://i.postimg.cc/d3xF81yN/install-intel-compiler-5.png)](https://postimg.cc/fSm1sM5Y)

Aquí debes seleccionar **Install on the current system only**. La otra opción es para un cluster. Presiona **Next** para continuar.

[![install-intel-compiler-6.png](https://i.postimg.cc/ncNZrXZC/install-intel-compiler-6.png)](https://postimg.cc/CzC96LRg)

Aquí debes seleccionar **customize**. De esta forma podrás seleccionar que paquetes se instalaran. El instalador está preparado para trabajar también en clústeres. Debido a esto instala varios paquetes que solo son útiles en dichos entornos. Presiona **Next** para continuar.

[![install-intel-compiler-7.png](https://i.postimg.cc/vBXbZXHs/install-intel-compiler-7.png)](https://postimg.cc/k6VkjQb1)

Creara una carpeta llamada **intel** donde instalara todo. Es posible cambiar la ubicación y nombre de la carpeta. Pero recomiendo dejarlo por defecto. Presiona **Next** para continuar.

[![install-intel-compiler-8.png](https://i.postimg.cc/9fhhPsD2/install-intel-compiler-8.png)](https://postimg.cc/rDQ3MnGZ)

A partir de este momento debes ser cuidadoso. Porque vas a seleccionar que paquetes no instalar. Presiona **Next** para continuar.

[![install-intel-compiler-9-1.png](https://i.postimg.cc/QtNZw5gn/install-intel-compiler-9-1.png)](https://postimg.cc/94kkqDnG)

Desmarca las siguientes opciones, como se muestra en la imagen.

- Intel Trace Analyzer and Collector 2020
- Intel Cluster Checker 2019 Update 6
- Intel VTune Profiler 2020
- Intel Inspector 2020

Continúa descendiendo por las opciones con la barra de desplazamiento.

[![install-intel-compiler-9-2.png](https://i.postimg.cc/0Qt1sQc5/install-intel-compiler-9-2.png)](https://postimg.cc/jwJF6RpB)

Desmarca la siguiente opción como se muestra en la imagen.

- Intel Advisor 2020

Continúa descendiendo por las opciones con la barra de desplazamiento.

[![install-intel-compiler-9-3.png](https://i.postimg.cc/D08kyTMr/install-intel-compiler-9-3.png)](https://postimg.cc/JHVdP9m0)

Las opciones que se muestran en la imagen debes dejarlas marcadas. Continúa descendiendo por las opciones con la barra de desplazamiento.

[![install-intel-compiler-9-4.png](https://i.postimg.cc/WzCRdHBQ/install-intel-compiler-9-4.png)](https://postimg.cc/D4rpDByg)

Desmarca las siguientes opciones como se muestra en la imagen.

- Intel Data Analytics Acceleration Library 2020
- GNU* GDB 8.3

Esta son las últimas opciones. Ahora puedes ver que el espacio requerido para la instalación se ha reducido a 9.2 GB.

[![install-intel-compiler-9-5.png](https://i.postimg.cc/dQxcNhh4/install-intel-compiler-9-5.png)](https://postimg.cc/Wtgyhb6k)

Observa que en la parte superior se encuentran dos opciones marcadas.

- IA-32
- Intel\* 64

Desmarca la opción **IA-32**. Observa que ahora solo se requiere 6.8 GB de espacio para la instalación. Presiona **Next** para continuar.

[![install-intel-compiler-10.png](https://i.postimg.cc/VL0QxzM1/install-intel-compiler-10.png)](https://postimg.cc/xcQ4HDtF)

Aquí te muestra un resumen de las preferencias de instalación.

- Espacio requerido 6.8 GB.
- La carpeta de instalación. Recuerda que **snt** es mi usuario.
- Los paquetes a instalar.

Presiona **Install**.

[![install-intel-compiler-11.png](https://i.postimg.cc/7Zv8DjMz/install-intel-compiler-11.png)](https://postimg.cc/GHjSx7f3)

Te indica que no encontro algunas librerías de 32 bits. Es seguro ignorar la advertencia. Presiona **Next** para continuar.

[![install-intel-compiler-12.png](https://i.postimg.cc/tg5L3J0d/install-intel-compiler-12.png)](https://postimg.cc/PLC3ht5N)

El proceso de instalación inicia y solo debes esperar a que termine.

[![install-intel-compiler-13.png](https://i.postimg.cc/0ypgNZcB/install-intel-compiler-13.png)](https://postimg.cc/dhtNHRM2)

Al terminar la instalación presiona **Finish**.

Al momento de finalizar la instalación, generalmente se abre una pestaña de tú navegador de forma automática. La página web te mostrará las instrucciones para configurar las variables de entorno y poder usar los compiladores.

[![install-intel-compiler-14.png](https://i.postimg.cc/CKY3nD2L/install-intel-compiler-14.png)](https://postimg.cc/xXxxWkYW)

Las instrucciones son las siguientes.

Utiliza el comando **source** y ejecuta el archivo **psxevars.sh** con el siguiente comando

> source /home/snt/intel/parallel_studio_xe_2020.0.088/bin/psxevars.sh

Recuerda cambiar el usuario **snt** por el tuyo. Debes ejecutar el comando anterior cada vez que utilices algún compilador de intel.
