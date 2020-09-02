---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Compilación e instalación de Quantum ESPRESSO con el compilador de GNU"
subtitle: "GNU/Linux Ubuntu y sus derivadas"
summary: "Instalación de Quantum ESPRESSO en un entorno linux utilizando el compilador de GNU"
authors: []
tags: [Linux, Installation, QuantumESPRESSO, "Density Functional Theory"]
categories: [Software]
date: 2020-09-01T22:03:57-05:00
lastmod: 2020-09-01T22:03:57-05:00
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

En un artículo anterior mostré como realizar la compilación con el compilador de Fortran de Intel.

<https://shiguerunagata.com/post/quantumespresso_installation/>

Este artículo pretende servir de guía para aquellas personas que no tengan acceso a los compiladores de Intel. O quizás tengan un procesador de AMD, en cuyo caso utilizar el compilador de Intel no conlleva un beneficio.

La instalación se realizará en un sistema GNU/Linux Ubuntu 20.04 Focal Fosa. Los comandos utilizados también son compatibles con distribuciones de Linux derivadas de Ubuntu.

Primero necesitas instalar las dependencias necesarias para la compilación.

* libopenblas-dev
* liblapack-dev
* libfftw3-dev
* build-essential
* gfortran
* libxc-dev

Puedes usar el siguiente comando para instalar las dependencias

[![dependencias-install.png](https://i.postimg.cc/85Rqk5LM/dependencias-install.png)](https://postimg.cc/bDv63qCw)

Puedes descargar el código fuente de Quantum ESPRESSO desde su repositorio oficial de GitHub. En el siguiente enlace.

<https://github.com/QEF/q-e/releases>

Al momento de escribir este artículo la última versión disponibles es 6.6.

[![QE-download.png](https://i.postimg.cc/9Fc9kbc8/QE-download.png)](https://postimg.cc/dDSDk8kr)

En el repositorio de GitHub podrás observar que existen tres archivos en la sección **Assets**. Debes descargar **Source code (tar.gz)**.

Luego debes descomprimir el archivo. Puedes hacerlo de manera gráfica como se muestra en la siguiente imagen.

[![descomprimir-editado.png](https://i.postimg.cc/jjHptcVZ/descomprimir-editado.png)](https://postimg.cc/4K3L1zx9)

Luego de descomprimir te sugiero que coloques la carpeta en una ubicación más adecuada. Porque los ejecutables de Quantum ESPRESSO obtenidos en la compilación se ubicaran dentro de esta carpeta. Y existe la posibilidad de que borres por error la carpeta si la dejas en **Descargas**.

Yo usualmente creo una carpeta en mi directorio **Home** llamada **shigueru** (le coloco mi nombre para evitar confusiones) dentro creo otra carpeta llamada **quantum_espresso** y coloco la carpeta descomprimida dentro. También cambio el nombre de la carpeta descomprimida de **q-e-qe-6.6** a **qe-6.6**

Voy a considerar los cambios anteriores en siguientes pasos. No olvides realizar los cambios pertinentes según tu caso.

Ahora debes abrir una terminal de Ubuntu y dirigirte a la carpeta descomprimida. Utiliza el siguiente comando.

[![dirigirse-a-carpeta.png](https://i.postimg.cc/85xSK5L6/dirigirse-a-carpeta.png)](https://postimg.cc/Hc0RjTZY)

Ahora debes configurar las opciones de compilación de Quantum ESPRESSO. Utiliza el siguiente comando.

[![configure-QE.png](https://i.postimg.cc/J0JW9LQd/configure-QE.png)](https://postimg.cc/CnFtq9Xj)

En este punto me gustaría hacer una aclaración. El comando **configure** anterior solo configura la compilación para obtener un ejecutable que se ejecuta en forma serial. Con esto quiero decir que el programa solo se ejecuta en un solo núcleo del procesador. Si se desea utilizar varios núcleos del procesador se debe agregar la siguiente opción al comando configure anterior: **--enable-openmp** . Pero al agregar esta opción se utilizará la versión interna de la librería FFTW y se ignora la versión instalada en el sistema. Es importante que sepas que la versión interna de FFTW es antigua en comparación a la instalada en el sistema.

Debes obtener al final de la configuración el siguiente mensaje: **configure: success** como se muestra en la siguiente imagen.

[![configure-exitoso-editado.png](https://i.postimg.cc/T2WGyVXq/configure-exitoso-editado.png)](https://postimg.cc/NLYZSrF5)

Además debes observar que reporta haber hallado las librerías **BLAS**, **LAPACK**, **FFT** y **LIBXC**.

Abre una terminal de Linux y ubícate dentro de la carpeta descomprimida de Quantum ESPRESSO. Luego procede a compilar utilizando el siguiente comando.

[![compilacion.png](https://i.postimg.cc/K844HKM9/compilacion.png)](https://postimg.cc/hXWSJtMx)

Si tu computador posee varios núcleos puedes acelerar la compilación utilizando el siguiente comando.

[![compilacion-acelerada.png](https://i.postimg.cc/4ynrgTQT/compilacion-acelerada.png)](https://postimg.cc/n9bd4gWd)

Recuerda adecuar el número junto a la **j** de acuerdo al número de núcleos de tu computador.

En este momento ya has completado el procedimiento de compilación, y los diferentes ejecutables se encuentran dentro de la carpeta **bin**.

Una forma de utilizar algún ejecutable para realizar una simulación, es copiar el ejecutable a tu carpeta de trabajo donde se encuentran tus archivos de **input**. Esta forma la encuentro muy poco eficiente y si no eres cuidadoso podrías terminar con muchas copias de los ejecutables.

A continuación te mostraré una manera más eficiente de utilizar los ejecutables y al final te mencionaré algunos otros beneficios de utilizar esta forma.

Los ejecutables van a permanecer en su ubicación actual. Lo que debes hacer es crear una variable de entorno.

Primero ubica el archivo **.bashrc** en tu directorio **Home**. Como lleva un punto delante de su nombre es un archivo oculto y para poder verlo debes presionar la siguiente combinación de teclas dentro del navegador de archivos **Ctrl + h**. Aparecerán varios archivos como se muestra en la siguiente imagen.

[![bashrc-editado.png](https://i.postimg.cc/HxCYdzSL/bashrc-editado.png)](https://postimg.cc/wt08kXYK)

Abre el archivo con el editor de texto. Al final del archivo agrega el siguiente texto.

[![export-path.png](https://i.postimg.cc/PfR7DJjW/export-path.png)](https://postimg.cc/XX9xSVXq)

Recuerda cambiar **snt** por tu nombre de usuario y **shigueru** por el nombre que hayas escogido para esta carpeta. Luego guarda los cambios y cierra el archivo.

Con esto podrás utilizar todos los ejecutables que se encuentran en la carpeta **bin** desde cualquier ubicación sin necesidad de copiarlos.

Otra ventaja de utilizar esta forma es la posibilidad de tener varias versiones de Quantum ESPRESSO instaladas. Y solo debes editar la variable de entorno de acuerdo a la versión que desees utilizar.
