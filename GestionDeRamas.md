##Gestión de Ramas

<---	Este documento constituye una revisión en profundidad del comando git branch y una exposición general del modelo de creación de ramas de Git. 
  La creación de ramas es una función disponible en la mayoría de los sistemas de control de versiones modernos. La creación de ramas en otros sistemas de control 
  de versiones puede tanto llevar mucho tiempo como ocupar mucho espacio de almacenamiento. En Git, las ramas son parte del proceso de desarrollo diario. 
  Las ramas de Git son un puntero eficaz para las instantáneas de tus cambios. Cuando quieres añadir una nueva función o solucionar un error, independientemente de su tamaño, 
  generas una nueva rama para alojar estos cambios. Esto hace que resulte más complicado que el código inestable se fusione con el código base principal, y te da la oportunidad 
  de limpiar tu historial futuro antes de fusionarlo con la rama principal.
  El diagrama anterior representa un repositorio con dos líneas de desarrollo aisladas, una para una función pequeña y otra para una función más extensa. 
  Al desarrollarlas en ramas, no solo es posible trabajar con las dos de forma paralela, sino que también se evita que el código dudoso se fusione con la rama main.

<---	La implementación que subyace a las ramas de Git es mucho más sencilla que la de otros modelos de sistemas de control de versiones. 
  En lugar de copiar archivos entre directorios, Git almacena una rama como referencia a una confirmación. En este sentido, una rama representa el extremo de una serie de confirmaciones, 
  es decir, no es un contenedor de confirmaciones. El historial de una rama se extrapola de las relaciones de confirmación.

<---	Durante la lectura, recuerda que las ramas de Git no son como las ramas de SVN. Las ramas de SVN solo se usan para capturar el esfuerzo de desarrollo a gran escala ocasional, mientras que las 
  ramas de Git son una parte integral del flujo de trabajo diario. El siguiente contenido amplía la información sobre la arquitectura interna de creación de ramas de Git.

**Funcionamiento**

<---	Una rama representa una línea independiente de desarrollo. Las ramas sirven como una abstracción de los procesos de cambio, preparación y confirmación. 
  Puedes concebirlas como una forma de solicitar un nuevo directorio de trabajo, un nuevo entorno de ensayo o un nuevo historial de proyecto. Las nuevas confirmaciones se registran 
  en el historial de la rama actual, lo que crea una bifurcación en el historial del proyecto.

<---	El comando git branch te permite crear, enumerar y eliminar ramas, así como cambiar su nombre. No te permite cambiar entre ramas o volver a unir un historial bifurcado. 
  Por este motivo, git branch está estrechamente integrado con los comandos git checkout y git merge.

**Opciones comunes**

**git branch**
<---Enumera todas las ramas de tu repositorio. Es similar a git branch --list.

**git branch <branch>**
<---Crea una nueva rama llamada ＜branch＞. Este comando no extrae la nueva rama.

**git branch -d <branch>**
<---Elimina la rama especificada. Esta es una operación segura, ya que Git evita que elimines la rama si tiene cambios que aún no se han fusionado.

**git branch -D <branch>**
<---Fuerza la eliminación de la rama especificada, incluso si tiene cambios sin fusionar. 
<---Este comando lo puedes usar si quieres eliminar de forma permanente todas las confirmaciones asociadas con una línea concreta de desarrollo.

**git branch -m <branch>**
<---Cambia el nombre de la rama actual a ＜branch＞.

**git branch -a**
<---Enumera todas las ramas remotas.

**Creación de ramas**

<---	Es importante comprender que las ramas son solo punteros a las confirmaciones. Cuando creas una rama, todo lo que Git tiene que hacer es crear un nuevo puntero, 
  no modifica el repositorio de ninguna otra forma. Si empiezas con un repositorio que tiene este aspecto:

<---	Y, a continuación, creas una rama con el siguiente comando:

**git branch crazy-experiment**
<---  El historial del repositorio no se modificará. Todo lo que necesitas es un nuevo puntero de la confirmación actual:

<---  Ten en cuenta que este comando solo crea la nueva rama. Para empezar a añadir confirmaciones, necesitas seleccionarla con el comando git checkout y, a continuación, 
  utilizar los comandos estándar git add y git commit.

**Creación de ramas remotas**
<---	Por ahora, todos los ejemplos han ilustrado operaciones de ramas locales. El comando git branch también funciona con ramas remotas. Para trabajar en ramas remotas, 
  primero hay que configurar un repositorio remoto y añadirlo a la configuración del repositorio local.

**$ git remote add new-remote-repo https://bitbucket.com/user/repo.git**
# Add remote repo to local repo config
**$ git push <new-remote-repo> crazy-experiment~**
# pushes the crazy-experiment branch to new-remote-repo
<---Este comando enviará una copia de la rama local crazy-experiment al repositorio remoto ＜remote＞.

**Eliminación de ramas**
<---	Una vez que hayas terminado de trabajar en una rama y la hayas fusionado con el código base principal, puedes eliminar la rama sin perder ninguna historia:

**git branch -d crazy-experiment**
<---No obstante, si la rama no se ha fusionado, el comando anterior mostrará un mensaje de error:

<---error: The branch 'crazy-experiment' is not fully merged. If you are sure you want to delete it, run 'git branch -D crazy-experiment'.
Esto te protege ante la pérdida de acceso a una línea de desarrollo completa. Si realmente quieres eliminar la rama (por ejemplo, si se trata de un experimento fallido), 
puedes usar el indicador -D (en mayúscula):

**git branch -D crazy-experiment**
<---Este comando elimina la rama independientemente de su estado y sin avisos previos, así que úsalo con cuidado.

<---	Los comandos anteriores eliminarán una copia local de la rama. La rama seguirá existiendo en el repositorio remoto. Para eliminar una rama remota, ejecuta estos comandos.

**git push origin --delete crazy-experiment**
O

**git push origin :crazy-experiment**
<---Enviarán una señal de eliminación al repositorio de origen remoto que desencadena la eliminación de la rama remota crazy-experiment.

**Resumen**

<---	En este documento, hemos hablado de la creación de ramas de Git y del comando git branch. Las funciones principales de los comandos git branch consisten en crear, 
  enumerar y eliminar ramas, así como en cambiarles el nombre. Para trabajar con las ramas resultantes, el comando se suele usar con otros distintos, como git checkout. 
  Obtén más información sobre las operaciones de rama de git checkout, como cambiar o fusionar ramas, en la página de git checkout.

<---	En comparación con otros sistemas de control de versiones, las operaciones de ramas de Git son rentables y se utilizan con frecuencia. 
  Esta flexibilidad permite una profunda personalización del flujo de trabajo de Git. Para obtener más información sobre los flujos de trabajo de Git, visita nuestras páginas 
  sobre el flujo de trabajo de creación de ramas de función, el flujo de trabajo de Gitflow y el flujo de trabajo de bifurcación.

