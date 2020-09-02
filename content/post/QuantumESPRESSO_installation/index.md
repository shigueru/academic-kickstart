---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Compilación e instalación de Quantum ESPRESSO con el compilador de Intel"
subtitle: "GNU/Linux Ubuntu y sus derivadas"
summary: "Instalación de Quantum ESPRESSO en un entorno linux utilizando el compilador de Intel."
authors: []
tags: [Linux, Installation, QuantumESPRESSO, "Density Functional Theory"]
categories: [Software]
date: 2020-08-04T22:12:54-05:00
lastmod: 2020-08-04T22:12:54-05:00
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
La instalación se realizará en un sistema GNU/Linux Ubuntu 20.04 Focal Fosa. Los comandos utilizados también son compatibles con distribuciones derivadas de Ubuntu.

Para compilar el código fuente de Quantum ESPRESSO necesitas el compilador de Fortran de Intel y las librerías openmp y mpi también de Intel. Todo lo obtienes al instalar los compiladores de Intel. Puedes seguir mi tutorial sobre la instalación.

<https://shiguerunagata.com/post/intel-compiler-install/>

Puedes descargar el código fuente de Quantum ESPRESSO desde su repositorio oficial de GitHub. En el siguiente enlace. <https://github.com/QEF/q-e/releases> . Al momento de escribir este artículo la última versión disponibles es 6.6.

[![QE-download.png](https://i.postimg.cc/9Fc9kbc8/QE-download.png)](https://postimg.cc/dDSDk8kr)

En el repositorio de GitHub podrás observar que existen tres archivos en la sección **Assets**. Debes descargar **Source code (tar.gz)**.

Luego debes descomprimir el archivo. Puedes hacerlo de manera gráfica como se muestra en la siguiente imagen.

[![descomprimir.png](https://i.postimg.cc/FsGJvQhG/descomprimir.png)](https://postimg.cc/HVcL0Rc7)

Luego de descomprimir te sugiero que coloques la carpeta en una ubicación más adecuada. Porque los ejecutables de Quantum ESPRESSO obtenidos en la compilación se ubicaran dentro de esta carpeta. Y existe la posibilidad de que borres por error la carpeta si la dejas en **Descargas**.

Yo usualmente creo una carpeta en mi directorio **Home** llamada **shigueru** (le coloco mi nombre para evitar confusiones) dentro creo otra carpeta llamada **quantum_espresso** y coloco la carpeta descomprimida dentro. También cambio el nombre de la carpeta descomprimida de **q-e-qe-6.6** a **qe-6.6**

Voy a considerar los cambios anteriores en siguientes pasos. No olvides realizar los cambios pertinentes según tu caso.

Ahora debes abrir una terminal de Ubuntu y dirigirte a la carpeta descomprimida. Utiliza el siguiente comando.

[![cd-descargas.png](https://i.postimg.cc/fLqFMMNQ/cd-descargas.png)](https://postimg.cc/gXR4DFjg)

Ahora debes configurar las variables de entorno de los compiladores de Intel. Usa el siguiente comando.

[![variables-entorno.png](https://i.postimg.cc/j52ggBJg/variables-entorno.png)](https://postimg.cc/0Mg0rWnD)

Este comando está basado en la forma de instalación que te mostré en el artículo sobre la instalación de los compiladores de Intel. Recuerda cambiar **snt** por tu usuario de Ubuntu.

Ahora debes configurar las opciones de compilación de Quantum ESPRESSO. Utiliza el siguiente comando.

[![configure.png](https://i.postimg.cc/9fWNTDXj/configure.png)](https://postimg.cc/K1HNhvg9)

Debes obtener al final de la configuración el siguiente mensaje: **configure: success** como se muestra en la siguiente imagen.

[![configure-exitoso.png](https://i.postimg.cc/DZL3QFCT/configure-exitoso.png)](https://postimg.cc/5Y4rbcd7)

Ahora debes abrir una pestaña del navegador y dirigirte a la siguiente página web.

<https://software.intel.com/en-us/articles/intel-mkl-link-line-advisor>

La página web anterior es el advisor de Intel. Te ayudará a definir el comando que debes usar para incluir las librerías necesarias para la compilación. La imagen a continuación te muestra como debes marcar las distintas opciones del advisor de Intel.

[![advisor-intel.png](https://i.postimg.cc/K81dj2yk/advisor-intel.png)](https://postimg.cc/gxPMt1jm)

Luego copia el texto que aparece en la sección **Use this link line**. La que se muestra en la siguiente imagen.

[![advisor-variables-entorno.png](https://i.postimg.cc/zvMFP426/advisor-variables-entorno.png)](https://postimg.cc/kRQS2Ymv)

Ahora debes editar el archivo **make.inc** utilizando el texto copiado. El archivo lo encuentras en la carpeta descomprimida de Quantum ESPRESSO como se muestra en la siguiente imagen.

[![make-inc-archive.png](https://i.postimg.cc/Y9jFSsLb/make-inc-archive.png)](https://postimg.cc/yg4xQnPZ)

Abre el archivo **make.inc** con el editor de textos. Y procede con los siguientes pasos.

### Paso 1: librerías externas

Busca la línea con la siguiente opción **DFLAGS** y verifica que diga lo siguiente. (*En mi archivo esta línea corresponde a la número 48*)

[![1-paso.png](https://i.postimg.cc/0jrTSbfN/1-paso.png)](https://postimg.cc/BP979ZRW)

Con esto compruebas que está configurada la compilación para usar las librerías externas de Intel.

### Paso 2: optimización para el compilador de C

Busca la línea con la opción **CFLAGS** en la cual debes hacer un cambio. (*En mi archivo esta línea corresponde a la número 108*). La línea dice lo siguiente.

[![2-paso-dice.png](https://i.postimg.cc/BZV90BSP/2-paso-dice.png)](https://postimg.cc/bdkF0b2q)

Y debe decir lo siguiente

[![2-paso-debe.png](https://i.postimg.cc/WzKQwTWw/2-paso-debe.png)](https://postimg.cc/hQLySWqX)


### Paso 3: optimización para el compilador de Fortran90

La linea siguiente a la anterior tiene la opción **F90FLAGS** y debes cambiarla también. La línea dice.

[![3-paso-dice.png](https://i.postimg.cc/SNY0NYRT/3-paso-dice.png)](https://postimg.cc/hfnZ2j9T)

Y debe decir lo siguiente.

[![3-paso-debe.png](https://i.postimg.cc/wTCCtxs6/3-paso-debe.png)](https://postimg.cc/fJv2pNKF)

### Paso 4: optimización para el compilador de Fortran

La linea siguiente a la anterior tiene la opción **FFLAGS** y debes cambiarla también. La línea dice.

[![4-paso-dice.png](https://i.postimg.cc/pLKgKNDK/4-paso-dice.png)](https://postimg.cc/Js46W2Yh)

Y debe decir lo siguiente.

[![4-paso-debe.png](https://i.postimg.cc/nLZNkdkg/4-paso-debe.png)](https://postimg.cc/0zWt50h0)

### Paso 5: librería BLAS

Busca la línea con la opción **BLAS_LIBS** (*En mi archivo esta línea corresponde a la número 137*). Esta línea posee un texto por defecto el cual debes borrar y reemplazar por el texto copiado desde la página web del Intel advisor. Debe quedar del siguiente modo.

[![5-paso.png](https://i.postimg.cc/JhqvdbYn/5-paso.png)](https://postimg.cc/XZrsrybS)

### Paso 6: librería LAPACK

Busca la línea con la opción **LAPACK_LIBS** (*En mi archivo esta línea corresponde a la número 146*). Esta línea no debería tener ningún texto luego de **LAPACK_LIBS**. En  caso tuviera texto debes borrarlo y colocar lo que copiaste del Intel advisor. Y debe quedar del siguiente modo.

[![6-paso.png](https://i.postimg.cc/ZR52kCXL/6-paso.png)](https://postimg.cc/jWBZPdxW)

### Paso 7: librería SCALAPACK

Busca la línea con la siguiente opción **SCALAPACK_LIBS** (*En mi archivo esta línea corresponde a la número 149*). Esta línea no debería tener ningún texto luego de **SCALAPACK_LIBS**. En caso tuviera texto debes borrarlo y colocar lo que copiaste del Intel advisor. Y debe quedar del siguiente modo.

[![7-paso.png](https://i.postimg.cc/4xvSm6g5/7-paso.png)](https://postimg.cc/hXjrY7hz)

### Paso 8: librería FFTW3

Busca la línea con la siguiente opción **FFT_LIBS** (*En mi archivo esta línea corresponde a la número 154*). Esta línea no debería tener ningún texto luego de **FFT_LIBS**. En caso tuviera texto debes borrarlo y colocar lo que copiaste del Intel advisor. Y debe quedar del siguiente modo.

[![8-paso.png](https://i.postimg.cc/YqWVwcDT/8-paso.png)](https://postimg.cc/SJmVWPhG)

### Paso 9: librería MPI

Busca la línea con la siguiente opción **MPI_LIBS**. Esta línea no debería tener ningún texto luego de **MPI_LIBS**. En caso tuviera texto debes borrarlo y colocar lo siguiente.

[![9-paso.png](https://i.postimg.cc/3NyqRz84/9-paso.png)](https://postimg.cc/p5HCcGnR)

Recuerda que debes cambiar **snt** por tu usuario. Si seguiste mi tutorial para instalar el compilador de Intel este es el único cambio. Si no lo seguiste adecua el texto a la ubicación de tu compilador de Intel. El patrón que debe tener esta línea de texto es el siguiente.

[![9-paso-patron.png](https://i.postimg.cc/NFWzrbFN/9-paso-patron.png)](https://postimg.cc/sG4ckYpS)

Estos son todos los cambios que debes realizar al archivo **make.inc**. Asegurate de guardar los cambios y cierra el archivo.

Abre una terminal de Linux y ubícate dentro de la carpeta descomprimida de Quantum ESPRESSO. Luego procede a compilar utilizando el siguiente comando.

[![compilacion.png](https://i.postimg.cc/131dmWLX/compilacion.png)](https://postimg.cc/3d919ZrQ)

Si tu computador posee varios núcleos puedes acelerar la compilación utilizando el siguiente comando.

[![compilacion-j.png](https://i.postimg.cc/43B21XnH/compilacion-j.png)](https://postimg.cc/p95BWbfP)

Recuerda adecuar el número junto a la **j** de acuerdo al número de núcleos de tu computador.

En este momento ya has completado el procedimiento de compilación, y los diferentes ejecutables se encuentran dentro de la carpeta **bin**.

Una forma de utilizar algún ejecutable para realizar una simulación, es copiar el ejecutable a tu carpeta de trabajo donde se encuentran tus archivos de **input**. Esta forma la encuentro muy poco eficiente y si no eres cuidadoso podrías terminar con muchas copias de los ejecutables.

A continuación te mostraré una manera más eficiente de utilizar los ejecutables y al final te mencionaré algunos otros beneficios de utilizar esta forma.

Los ejecutables van a permanecer en su ubicación actual. Lo que debes hacer es crear una variable de entorno.

Primero ubica el archivo **.bashrc** en tu directorio **Home**. Como lleva un punto delante de su nombre es un archivo oculto y para poder verlo debes presionar la siguiente combinación de teclas dentro del navegador de archivos **Ctrl + h**. Aparecerán varios archivos como se muestra en la siguiente imagen.

[![bashrc.png](https://i.postimg.cc/2jJJJjG4/bashrc.png)](https://postimg.cc/4n6BHgrd)

Abre el archivo con el editor de texto. Al final del archivo agrega el siguiente texto.

[![export-path.png](https://i.postimg.cc/ZRQf1j8T/export-path.png)](https://postimg.cc/KknrTPpV)

Recuerda cambiar **snt** por tu nombre de usuario y **shigueru** por el nombre que hayas escogido para esta carpeta. Luego guarda los cambios y cierra el archivo.

Con esto podrás utilizar todos los ejecutables que se encuentran en la carpeta **bin** desde cualquier ubicación sin necesidad de copiarlos.

Otra ventaja de utilizar esta forma es la posibilidad de tener varias versiones de Quantum ESPRESSO instaladas. Y solo debes editar la variable de entorno de acuerdo a la versión que desees utilizar.
