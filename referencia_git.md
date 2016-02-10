# Pequeña referencia acerca de Git y GitHub


## Configurar Git


### Configuración básica

``` bash
	git config --global user.name "Usuario"				# Nombre de usuario
	git config --global user.email ejemplo@ejemplo.com 	# e-mail
```


#### Escoger editor de texto por defecto que utilizará Git

```bash
	git config --global core.editor "atom --wait" 	# Atom
	git config --global core.editor "nano"			# Nano
```


#### Escoger herramientas para resolver problemas de conflictos
```bash
	git config --global merge.tool meld 	# Meld
	git config --global merge.tool p4merge 	# P4merge
```
Git acepta `kdiff3`, `tkdiff`, `meld`, `xxdiff`, `emerge`, `vimdiff`, `gvimdiff`, `ecmerge`, y `opendiff` como herramientas válidas.
Herramienta recomendada [`p4merge`](http://www.perforce.com/product/components/perforce-visual-merge-and-diff-tools). Página sobre como instalarlo en Linux [aquí](http://blogs.pdmlab.com/alexander.zeitler/articles/installing-and-configuring-p4merge-for-git-on-ubuntu/).

Luego el programa externo que se encarga de mostrar las diferencias y resolver conflictos al unir se llaman con:
```bash
	git difftool
	git mergetool
```

* Info ProGit:

  * **Archivo `/etc/gitconfig`**: Contiene valores para todos los usuarios del sistema y todos sus repositorios.
Si pasas la opción `--system` a `git config`, lee y escribe específicamente en este archivo.

  * **Archivo `~/.gitconfig file`**: Configuración **Git** específica a tu usuario.
Puedes hacer que Git lea y escriba específicamente en este archivo pasando la opción `--global`.

  * **Archivo config en el directorio de Git (es decir, `.git/config`) del repositorio que estés utilizando actualmente**: Específico a ese repositorio. 

  * Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de `.git/config` tienen preferencia sobre los de `/etc/gitconfig`.
  
  * Si quieres sobrescribir esta información con otro nombre o dirección de correo para proyectos específicos, puedes ejecutar el comando sin la opción `--global` cuando estés en ese proyecto.

- - -


## Iniciar un repositorio desde un PC hacia GitHub

* Inicio el repositorio en la carpeta donde quiero iniciar el proyecto
``` bash
	git init  # Creo carpeta .git
```

* Para añadir archivos al repositorio
``` bash
	git add <archivo_ejemplo> [<archivos_ejemplo>]
	git add -A  # Añade todos los archivos
```

* Con `commit` hago seguimiento de los archivos en git (localmente)
```bash
	git commit -m "Descripción del commit"
	git commit -am "Descripción" # Realiza un add y luego el commit
```

* Luego en la página de GitHub se inicia un nuevo repositorio

* Para conectar mi repositorio local con el repositorio de **GitHub** digitar:
```bash
	git remote add origin <URL dada por GitHub>
```
**Nota**: para referirme al repositorio alojado en **GitHub** se usará `origin`, sin embargo se puede usar cualquier otro nombre.

* Finalmente:
```bash
	git push origin master
```
Enviamos los cambios al repositorio central en **GitHub**.
Con el parametro `-u` hace que recuerde los parametros insertados en el comando, haciendo que la próxima vez que digitemos el comando no los tengamos que poner de nuevo.
Ejemplo: `git push -u origin master`

* Con
```bash
	git pull origin master
```
Trae y/o actualiza el contenido desde el repositorio en **GitHub**.

**Notas**:
* `git stash`: Funciona para guardar los cambios que llevamos antes de hacer `push`, luego con `git stash apply` se hace un tipo de `merge`, con la nueva *imagen* traída desde **GitHub**.

* Es recomendable hacer `pull` antes de hacer `push`, para de esta manera tener la copia más reciente del repositorio remoto, y evitar confilctos.


##Iniciar o editar un repositorio desde el GitHub hacia un PC
* Se crea un repositorio en **GitHub**. Luego se copia la **URL** del repositorio creado.

* En la carpeta donde quiero almacenar mi proyecto digito:
```bash
	git clone <URL>
```

* El pasado comando *clona* el repositorio que se encuentra en **GitHub**, luego ingreso a la carpeta que se acaba de crear y inserto y/o modifico los archivos.

* Para añadir archivos al repositorio
``` bash
	git add <archivo_ejemplo> [<archivos_ejemplo>]
	git add . # Añade todos los archivos
```

* Con `commit` hago seguimiento de los archivos en git (localmente)
```bash
	git commit -m "Descripción del commit"
	git commit -am "Descripción" # Realiza un add y luego el commit
```

* Finalmente:
```bash
	git push origin master
```
Enviamos los cambios al repositorio central en **GitHub**.
Con el parametro `-u` hace que recuerde los parametros insertados en el comando, haciendo que la próxima vez que digitemos el comando no los tengamos que poner de nuevo.
Ejemplo: `git push -u origin master`

* Con
```bash
	git pull origin master
```
Trae y/o actualiza el contenido desde el repositorio en **GitHub**.

- - -


## Comandos:

### Generales

```bash
	git status
```
Podemos observar el estado de los archivos que han sido modificados, agrgados o eliminados tanto en el directorio de trabajo como en el área de preparación.
___


```bash
	git reset HEAD <archivo>
```
Quita el archivo del área de preparación.
___


```bash
	git checkout -- <archivo>
```
Descarta los cambios en ese archivo. Lo vuelve al estado del último *commit*.
___


```bash
	git rm <archivo_ejemplo>
```
Borra el archivo de los archivos seguidos por git.
___


```bash
	git rm -r <archivo_ejemplo>
```
Borra todos los archivos del folder.
___


```bash
	git rm --cached <archivo_ejemplo>
```
Git deja de seguir el archivo, sin embargo deja el archivo en el proyecto.
___

```bash
	git log
```
Mostrará información acerca de los ***commits*** que se han hecho. Hay muchas opciones de formato.
___


```bash
	git fetch origin
```
Trae la última versión del repositorio remoto. La diferencia de este comando con `pull` es que `pull` hace un `fetch` y un `merge`. Con fetch debemos ser nosotros quién hagamos el *merge*.
___


```bash
	git diff
```
Mostrará la diferencia que tiene los archivos en el directorio de trabajo con el último *commit*.
___


```bash
	git diff –-staged	
```
Se muestran los cambios que has preparado y que irán en tu próxima confirmación.
___


```bash
	git reset --soft <SHA1>
```
Deshace los *commits* a partir del commit con hash `<SHA1>`. Los archivos con modificaciones de los *commits* que se deshicieron quedan en el área de preparación.
**Nota**: `HEAD~1` es un atajo a el último commit realizado.
___


```bash
	# Volver a un commit anterior, descartando los cambios
	git reset --hard <SHA1>
```
Devuelve el repositorio local a ese *commit* y descarta los *commit* (con sus archivos modificados) de `<SHA1>` < en adelante.
___


```bash
	git commit --amend
```
Este comando utiliza lo que haya en tu área de preparación para la confirmación. Si no has hecho ningún cambio desde la última confirmación (por ejemplo, si ejecutas este comando justo después de tu confirmación anterior), esta instantánea será exactamente igual, y lo único que cambiarás será el mensaje de confirmación.

Ejemplo:
```bash
	git commit -m 'commit'
	git add forgotten_file
	git commit --amend
```
___


```bash
	git revert HEAD
```
Deshacer el último commit. Creo que borra los cambios del `commit` a revertir.


---

<br>
### Repositorios remotos

```bash
	git remote -v
```
Nombre de el repositorio.

```bash
	git remote show <remote-name>
```
Muestra información acerca de el repositorio remoto.
___


```bash
	git remote rename <viejo_nombre> <nuevo_nombre>
```
Renombrar el repositorio remoto.
___


```bash
	git remote rm <repositorio_remoto>
```
Borrar un repositorio remoto (de mi PC).


- - -

<br>
### Ramas

```bash
	git branch
```
Muestra todas las ramas.
___


```bash
	git checkout -b <new_branch>
```
Es para crear una nueva "rama" y pasarse a esta imediatamente, es un sinónimo de `git branch new_branch` & `git checkout new_branch`.
___


```bash
	git branch -m <nombre_rama_anterior> <nombre_rama_nuevo>
```
Cambia de nombre a una rama.
___


```bash
	git merge <rama>
```
Para realizar la unión de dos ramas debemos estar ubicados en la rama a la que se le quieren agregar los cambios y luego aplicar la unión.
___


```bash
	git branch -d <rama>
```
Borra una rama. Utilizando la bandera `-d` eliminamos la rama unicamente si esta se ha unido. De lo contrario nos arrojará un error. Si queremos desechar la rama completa sin importar la unión utilizamos `-D` como bandera.
___


**Nota**: Las rams locales no se sincrinizan con las ramas del repositorio remoto.

```bash
	git checkout --track origin/arreglos-varios
```
Generalmente cuando uno clona un repositorio remoto únicamente se comienza a seguir los cambios de *master* que viene siendo la rama o raíz principal del proyecto. para realizarle el seguimiento a una rama remota adicional se utiliza el este comando.
___


```bash
	git fetch <branch>
    	o
    git checkout -t origin/<branch>
```
Traer una rama en específica.
___

```bash
	git push origin :<branch>
```
Borrar una rama del repositorio remoto.

- - -

<br>
### Stash
Información sobre que es rebase & stash [aquí](http://codehero.co/rebase-y-stash/)

```bash
	git stash
```
Se guardan los cambios temporalmente.
___


```bash
	git stash pop
```
Reaplica los cambios guardados.
___


```bash
	git stash drop
```
Descarta los cambios guardados.
___

```bash
	git stash pop stash@{0} # Para reaplicar
	git stash drop stash@{0} # Para borrarlos
```
`pop` & `drop` a un `stash` específico.

- - -

<br>
### Tag:

```bash
	git tag
```
Muestra las etiquetas hechas en el repositorio.
___


```bash
	git tag -a <nombre_tag> <SHA1>
```
Añadir un tag.
___


```bash
	git push --tags
```
Subir tags al repositorio.

* * *

<br>
### Páginas con información

* **Ignorar el salto de línea en Git**: http://help.github.com/line-endings/
* **Reset de archivos**: http://codehero.co/git-desde-cero-reset-y-cherry-pick/
