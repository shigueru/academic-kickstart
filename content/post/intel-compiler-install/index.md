---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Instalación de los compiladores de Intel"
subtitle: "Linux/Ubuntu y derivadas"
summary: "Instalación de los compiladores de Intel para C++, C y Fortran en su version de cluster en un entorno linux."
authors: []
tags: [Intel, Compiler, Linux]
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
## Introducción

La instalación se realizara en un sistema GNU/Linux. Para ser más específicos se utilizará la distribución Ubuntu 20.04 Focal Fosa. Por lo tanto los comandos utilizados tambien son validos para distribuciones derivadas.

## Obtención

El conjunto de compiladores que vamos a utilizar se encuentra bajo el nombre de **Parallel studio XE 2020 cluster edition**. El instalador puede ser descargado de la pagina de Intel de manera gratuita, pero para ello se deben registrar en la pagina utilizando una cuenta de correo educativa, es decir el alguna universidad o institución de investigación. El presente artículo no es sobre como descargar el instalador, por lo tanto asumira que ya tienen acceso al instalador.

## Dependencias

Para realizar la instalación necesitamos de un compilador de c++, dado que el compilador tambien trae capas de compatibilidad para los compiladores de GNU.

Para instalar el compilador de GNU usaremos el siguiente comando

> sudo apt install g++

## Instalación

Supondre que el instalador se encuentra dentro de la carpeta **Descargas** y que se llamma **Parallel studio XE 2020 cluster edition.tgz**. Luego de descomprimir el instalador debemos posicionarnos dentro de la carpeta descomprimida, para lo cual usaremos el siguiente comando en la terminal.

> cd ~/Descargas/parallel_studio_xe_2020_cluster_edition

Luego debemos iniciar el instalador, para lo cual utilizamos el siguiente comando

> ./install_GUI.sh

y se abrira la siguiente ventana

[![install-intel-compiler-1.png](https://i.postimg.cc/05W9gtBG/install-intel-compiler-1.png)](https://postimg.cc/G9yWGjr9)

aceptamos los terminos de licencia y damos click en **Next**, para pasar a la siguiente ventana

[![install-intel-compiler-2.png](https://i.postimg.cc/8P7NTh22/install-intel-compiler-2.png)](https://postimg.cc/8jgqHrP4)

Yo marco la opción de **no recolectar mi información** pero eso queda a criterio de cada uno, cualquiera de las opciones es valida y presionamos **Next** para continuar

[![install-intel-compiler-3.png](https://i.postimg.cc/52vJCfNp/install-intel-compiler-3.png)](https://postimg.cc/pm23Nbjn)

Esta ventana nos advierte que se necesitan permisos de administrador para el driver de sampling de intel, pero este driver no sera necesario para nosotros, por lo que podemos ignorar esta advertencia. Tambien nos indica que el sistema operativo utilizado no esta soportado y nos da una lista de los que sí estan soportados. Una vez mas podemos ignorar esta advertencia. Damos click en **Next** y continuamos a la siguiente ventana.

[![install-intel-compiler-4.png](https://i.postimg.cc/TwTTxBx0/install-intel-compiler-4.png)](https://postimg.cc/NyC37J52)

Aqui nos piden una forma de activación, se debe escoger la opción mas adecuada segun sea el caso. En mi caso yo usare un número de serie, el cual obtuve en el momento de la descarga del compilador desde la pagina de intel. Damos click en **Next** para continuar.

[![install-intel-compiler-5.png](https://i.postimg.cc/d3xF81yN/install-intel-compiler-5.png)](https://postimg.cc/fSm1sM5Y)

Aqui seleccionamos la opción de solo instalar en este sistema, la otra opcion es para un cluster. Damos click en **Next** para continuar.

[![install-intel-compiler-6.png](https://i.postimg.cc/ncNZrXZC/install-intel-compiler-6.png)](https://postimg.cc/CzC96LRg)

Aquí debemos escoger la opción **Customize** para poder personalizar nuestra instalación. Es posible saltar los siguientes pasos y dar directamente en **Install**, pero de esta forma se instalaran varios modulos que no son utiles para nosotros, que solo buscamos compilar programas. Los modulos que descartaremos son referentes a clusteres y detección de errores durante el proceso de desarrollo de software.

[![install-intel-compiler-7.png](https://i.postimg.cc/vBXbZXHs/install-intel-compiler-7.png)](https://postimg.cc/k6VkjQb1)

nos muestra que va a crear una carpeta llamada **intel** donde instalara todo lo necesario, es posible cambiarlo pero recomiendo dejarlo por defecto. Damos click en **Next** y continuamos.

[![install-intel-compiler-8.png](https://i.postimg.cc/9fhhPsD2/install-intel-compiler-8.png)](https://postimg.cc/rDQ3MnGZ)

A partir de este punto debemos ser cuidadosos, ya que debemos escoger los elementos que debemos excluir de la instalación. Comencemos

[![install-intel-compiler-9-1.png](https://i.postimg.cc/QtNZw5gn/install-intel-compiler-9-1.png)](https://postimg.cc/94kkqDnG)

Desmarcamos las siguientes opciónes, como se muestra en la imagen:

- Intel Trace Analyzer and Collector 2020
- Intel Cluster Checker 2019 Update 6
- Intel VTune Profiler 2020
- Intel Inspector 2020

seguimos descendiendo por las opciones, con la barra de desplazamiento

[![install-intel-compiler-9-2.png](https://i.postimg.cc/0Qt1sQc5/install-intel-compiler-9-2.png)](https://postimg.cc/jwJF6RpB)

Desmarcamos la siguiente opción, como se muestra en la imagen:

- Intel Advisor 2020

seguimos descendiendo por las opciones, con la barra de desplazamiento

[![install-intel-compiler-9-3.png](https://i.postimg.cc/D08kyTMr/install-intel-compiler-9-3.png)](https://postimg.cc/JHVdP9m0)

Las opciones que se muestran en la imagen deben quedar marcadas (no las modificamos). Seguimos descendiendo por las opciones con la barra de desplazamiento.

[![install-intel-compiler-9-4.png](https://i.postimg.cc/WzCRdHBQ/install-intel-compiler-9-4.png)](https://postimg.cc/D4rpDByg)

Desmarcamos las siguientes opciones, como se muestra en la imagen:

- Intel Data Analytics Acceleration Library 2020
- GNU* GDB 8.3

Aquí llegamos a la ultima opción, podemos observar que el espacio requerido para la instalación se redujo a 9.2 Gb.

[![install-intel-compiler-9-5.png](https://i.postimg.cc/dQxcNhh4/install-intel-compiler-9-5.png)](https://postimg.cc/Wtgyhb6k)

Vemos que en la parte superior se muestran dos opciones marcadas, que hacen referencia a las arquitecturas **IA-32** y **Intel\* 64**. Debemos desmarcar la opción que corresponde a la arquitectura **IA-32**. Observamos que ahora solo se requierre 6.8 Gb. de espacio para la instalación. Damos click en **Next**

[![install-intel-compiler-10.png](https://i.postimg.cc/VL0QxzM1/install-intel-compiler-10.png)](https://postimg.cc/xcQ4HDtF)

Aqui nos muestra un resumen de las preferencias de instalación: 

- el espacio requerido 6.8 Gb.
- La carpeta de instalación, Recuerden que **snt** es mi usuario en su caso sera diferente, lo importante es que indique la carpeta **intel** o la que ustedes escogieron en el paso referente a esto.
- Los paquetes a instalar

Damos click en **Install**

[![install-intel-compiler-11.png](https://i.postimg.cc/7Zv8DjMz/install-intel-compiler-11.png)](https://postimg.cc/GHjSx7f3)

No mostrara una advertencia al no encontrar las librerias de 32 bits. Es posible que no muestre esta advertencia si dichas librerias estan instaladas. En caso no se tengan instaladas, es seguro ignorar la advertencia. Damos click en **Next**

[![install-intel-compiler-12.png](https://i.postimg.cc/tg5L3J0d/install-intel-compiler-12.png)](https://postimg.cc/PLC3ht5N)

El proceso de instalación inicia y solo debemos esperar a que termine.

[![install-intel-compiler-13.png](https://i.postimg.cc/0ypgNZcB/install-intel-compiler-13.png)](https://postimg.cc/dhtNHRM2)

Muestra que la instalación se ha completado. Damos click en **Finish**.

Al momento de finalizar la instalación, generalmente se abre una pestaña de nuestro navegador de forma automatica. La página web nos muestra las intrucciones para configurar las variables de entorno y poder usar los compiladores. 

[![install-intel-compiler-14.png](https://i.postimg.cc/CKY3nD2L/install-intel-compiler-14.png)](https://postimg.cc/xXxxWkYW)

Las intrucciones son las siguientes.

Utilizaremos el comando **source** y ejecutaremos el archivo **psxevars.sh**, con el siguiente comando

> source /home/snt/intel/parallel_studio_xe_2020.0.088/bin/psxevars.sh

recuerde cambiar el usuario **snt** por el suyo. finalmente, recuerde ejecutar el comando anterior cada vez que vaya a compilar algun programa, si desea utilizar el compilar de intel.
