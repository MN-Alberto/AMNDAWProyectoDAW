## 📑 Índice

- [1. GitHub](#1-github)
  - [1.1 Ramas principales](#11-ramas-principales)
  - [1.2 Crear un repositorio](#12-crear-un-repositorio)
  - [1.3 Crear y gestionar ramas](#13-crear-y-gestionar-ramas)
  - [1.4 Commit y merge con la rama Master](#14-commit-y-merge-con-la-rama-master)
  - [1.5 Creación de Tags y Releases](#15-creación-de-tags-y-releases)
- [2. Git](#2-git)
  - [2.1 Merge](#21-merge)
  - [2.2 Rebase](#22-rebase)
  - [2.3 CherryPick](#23-cherrypick)
- [3. Subir un proyecto y Utilizar Git](#3-subir-un-proyecto-y-utilizar-git)

  # 3. **Subir un proyecto y Utilizar Git**

# 1. **GitHub**

Utilizaremos GitHub para subir nuestros proyectos y versionarlos poco a poco.
En cada proyecto tendremos una rama developer y una rama master.

## 1.1. Ramas principales
- **master**: Rama estable, lista para producción.
- **developerAMN**: Rama de desarrollo, donde se integran nuevas funcionalidades y cambios antes de pasarlos a `master`.

## 1.2. Crear un repositorio
1. Entraremos a [GitHub](https://github.com/) y en nuestros repositorios, haremos click en **New repository**.
![alt text](usoGitHub/1.png)
2. Le daremos un nombre a nuestro repositorio y, opcionalmente, una descripción.
![alt text](usoGitHub/2.png)
3. Al crearlo podemos indicar si el repositorio será **público** o **privado**.
![alt text](usoGitHub/3.png)
4. Podremos crear el repositorio con un archivo `Readme.md` de primeras.
![alt text](usoGitHub/4.png)
5. Haz click en **Create repository** y ya se crearía nuestro repositorio.
![alt text](usoGitHub/5.png)

## 1.3. Crear y gestionar ramas

Vamos a crear la rama ``developerAMN`.
Para ello, deberemos de clicar en el desplegable de las ramas, y clicaremos en "View all branches"

![alt text](usoGitHub/6.png)

Aquí podremos ver todas las ramas que tenemos en nuestro repositorio y las podremos editar, nosotros vamos a crear una nueva asi que deberemos de clicar en "New branch"
![alt text](usoGitHub/7.png)

Al crear la rama, deveremos de indicarle un nombre, en este caso "developerAMN" y la rama de origen que queremos que tenga, en este caso la rama master.

![alt text](usoGitHub/8.png)

Al crearla podremos ver la rama por defecto de nuestro repositorio, asi como todas las ramas que tiene y las ramas activas.

![alt text](usoGitHub/9.png)

Para cambiarnos de rama deberemos de clicar de nuevo en el desplegable y seleccionar la rama que queramos utilizar.

![alt text](usoGitHub/10.png)


## 1.4. Commit y merge con la rama Master

Vamos a realizar nuestro primer commit a nuestra rama developerAMN para después hacer un merge con la rama master.

Para ello en primer lugar clicaremos en el desplegable de "Add file" y clicaremos en "Upload files".

![alt text](usoGitHub/11.png)

Aquí podremos seleccionar los archivos que queramos subir, nosotros subiremos un archivo de ejemplo. También debemos indicar un mensaje y una descripción para nuestro commit. Podremos hacer el commit directamente a la rama developerAMN o crear una nueva rama para este commit.

![alt text](usoGitHub/12.png)

Cuando hayamos clicado en "Commit changes" veremos que aparece un mensaje para comparar y hacer una "Pull request"

![alt text](usoGitHub/13.png)

Le indicaremos un titulo y un mensaje y crearemos la request.

![alt text](usoGitHub/14.png)

Al hacerlo nos aparecerá un mensaje para hacer una solicitud de merge con la rama master.

![alt text](usoGitHub/15.png)

Nos pedirá un titulo y una descripción.

![alt text](usoGitHub/16.png)

Al confirmar el merge, ambas ramas se fusionarán y tendran el archivo que hemos subido en nuestro primer commit.

![alt text](usoGitHub/17.png)

## 1.5 Creación de Tags y Releases

Vamos a crear una release de nuestro proyecto de ejemplo.

Para ello deveremos de clicar en "Create a new release" en nuestro repositorio.

![alt text](usoGitHub/18.png)

Después, como no tenemos nigun Tag creado, deberemos de crear uno. Para ello deberemos de clicar en "Select tag".

![alt text](usoGitHub/19.png)

Clicaremos en "Create new tag" para crear un Tag nuevo.

![alt text](usoGitHub/20.png)

Aquí podremos ponerle un nombre a nuestro primer tag, nosotros vamos a llamarlo "v1.0.0" ya que va a ser nuestra primera versión funcional del repositorio.

![alt text](usoGitHub/21.png)

Al haberla creado, la seleccionaremos, le pondremos un titulo a nuestra release, en este caso el mismo que el tag, y también podremos indicar una descripción de lo que contiene. También podemos elejir a que rama queremos que se publique nuestra release.

![alt text](usoGitHub/22.png)

Después de crearla, ya podriamos descargar el código/archivos de nuestro repositorio en el momento de hacer la release.

![alt text](usoGitHub/23.png)

# 2. **Git**

Vamos a explicar la utilización de Git con "git merge", "rebase" y "cherrypick".

## 2.1 Merge

Imaginemos que estamos trabajando en un repositorio que tiene 2 ramas: developerAMN y master.

En primer lugar es recomendable comporbar las ramas que tenemos con:

```bash
  git branch
```

Y cambiarnos de rama a la rama master con:

```bash
  git checkout master
```

Después es recomendable actualizar la rama master:

```bash
  git pull origin master
```

Y tras hacer esto hacemos el merge:

```bash
  git merge developerAMN
```

Tras ejecutar ese comando, Git intenta unir automáticamente los cambios, si no hay conflictos crea un nuevo commit al hacer el merge. Si hay conflictos, se para el merge y da un error para que solucionemos los conflictos.

Un ejemplo de conflicto puede ser:

```bash
  Auto-merging src/login.js
  CONFLICT (content): Merge conflict in src/login.js
  Automatic merge failed; fix conflicts and then commit the result.
```

Para resolver un conflicto, deberemos de editar el archivo en el que nos indica que hay un conflicto, y podremos ver algo parecido a esto:

```bash
  <<<<<<< HEAD
  loginUser();
  =======
  loginUserWithToken();
  >>>>>>> developerAMN
```

En este caso solo quiero dejar "loginUserWithToken();", entonces deberemos de borrar el resto, básicamente, para resolver un conflicto debemos de editar el archivo y borrar lo que no queramos conservar.

El archivo quedaría asi:

```bash
    loginUserWithToken();
```

Para seguir con el merge, deberemos de volver a añadir el nuevo archivo modificado y hacer un nuevo commit:

```bash
  git add src/login.js
  git commit
```

Git nos abrirá un bloc de notas con un mensaje que podemos modificar, un ejemplo sería:

```bash
  Merge branch 'developerAMN'
```

Tras hacer el merge, podremos ver el gráfico de Git para comprobar los cambios:

```bash
  git log --oneline --graph

      *   a1b2c3d Merge branch 'developerAMN'
      |\
      | * d4e5f6g Añadido login con token
      |/
      * 789abcd Versión estable
```

También existe la opción de hacer un merge sin commit automático.

Desde master:
```bash
  git merge --no-commit master
```

## 2.2 Rebase

Imaginemos que estamos trabajando en un repositorio que tiene 2 ramas: developerAMN y master. En este caso queremos poner la rama developerAMN "encima" de master antes de integrarla.

En primer lugan nos dirigiremos a la rama que queramos rebasar:

```bash
  git checkout developerAMN
```

Es recomendable actualizar la rama master en este punto:

```bash
  git fetch origin
```

Hacemos el rebase:

```bash
  git rebase main
```

Este comando coge los commits de la rama developerAMN los "despega" y los aplica delante del último commit de la rama master.

Puede haber conflictos como al hacer merge, se solucionan de la misma forma, borrando lo que no queramos conservar.

Si no ha habido conflictos:

```bash
  Successfully rebased and updated refs/heads/developerAMN.
```

Si ha habído algún conflicto, deberemos continuar con el rebase:

```bash
  git add src/login.js
  git rebase --continue
```

Si por algún casual no queremos continuar con el rebase, podremos ejecutar:

```bash
  git rebase --abort
```

Al ejecutar ese comando, todo vuelve a como estaba al principio.

Después de hacer el rebase, deberemos cambiar a master para poder hacer un merge:

```bash
  git checkout master
  git merge developerAMN
```

Podremos comprobar el gráfico de Git con:

```bash
  git log --oneline --graph

    * d4e5f6g Añadido login con token
    * 789abcd Versión estable
```

## 2.3 CherryPick

Imaginemos que estamos trabajando en un repositorio que tiene 2 ramas: developerAMN y master. En este caso, cherrypick nos sirve para copiar 1 o varios commits concretos de una rama a otra sin necesidad de fusionar toda la rama.

En primer lugar, para poder copiar un comit concreto necesitamos su identificador o hash, lo podemos obtener con:

```bash
  git log --oneline

    c3a91f2 Arreglado error de autenticación

    Esto es lo que nos interesa --> c3a91f2
```

Después de haber copiado el hash, nos cambiamos a la rama en la que vamos a copiarlo:

```bash
  git checkout master
```

Y hacemos el cherrypick con el hash del commit que queramos:

```bash
  git cherry-pick c3a91f2
```

Al ejecutar este comando, Git copia los cambios del commit y crea un commit nuevo en la rama de destino, en este caso master. Importante que el hash del nuevo commit es distinto al original aunque esencialmente el contenido sea el mismo.

Si todo ha ido bien nos saldrá algo parecido a esto:

```bash
  [master 9f82bd1] Arreglado error de autenticación
  Date: Tue Feb 6 10:32:00 2026 +0100
  1 file changed, 3 insertions(+), 1 deletion(-)
```

Si nos da conflicto, lo podremos solucionar de la misma forma que con el merge o el rebase vistos anteriormente. Borramos lo que no queramos conservar.

Para continuar con el cherry-pick en caso de conflicto:

```bash
  git add src/login.js
  git cherry-pick --continue
```

Al igual que con el rebase, si por algún casual queremos parar el cherry-pick, podremos ejecutar:

```bash
  git cherry-pick --abort
```

En el caso de cherry-pick, tenemos varias opciones:

Copiar varios commits específicos:

```bash
  git cherry-pick a1b2c3d d4e5f6g
```

Copiar commits específicos dentro de un rango:

```bash
  git cherry-pick a1b2c3d..d4e5f6g
```

IMPORTANTE: Al copiar por rango, el primer commit no se incluye.
SI queremos incluirlo:

```bash
  git cherry-pick a1b2c3d^..d4e5f6g
```

Al igual que con rebase, si no queremos que se haga un commit automático, podremos ejecutar:

```bash
  git cherry-pick --no-commit c3a91f2
```

# 3. **Subir un proyecto y Utilizar Git**

  ## 3.1 Crear un nuevo repositorio

Para crear un nuevo repositorio necesitaremos, en la carpeta del proyecto ejecutar:

  ```bash
    git init
  ```
  ## 3.2 Clonar un repositorio

  ```bash
    git clone https://github.com/usuario/proyecto.git
  ```

## 3.3 Tipo de estados de los archivos

```bash
  Untracked: Git no los conoce

  Modified: cambiaron pero no están preparados

  Staged: listos para commit

  Committed: guardados en el historial
```

## 3.4 Flujo básico

  ```bash
  git status                  # Muestra el estado de los archivos
  git add archivo              # Añade un archivo al staging
  git add .                    # Añade todos los cambios al staging
  git commit -m "mensaje"      # Guarda los cambios en el historial
  ```

## 3.5 Ver historial

```bash
  git log                     # Muestra el historial completo
  git log --oneline           # Historial resumido (1 línea por commit)
  git log --graph --all       # Historial visual con ramas
```

## 3.6 Deshacer cambios

Antes del commit:

```bash
  git restore archivo          # Revierte cambios locales de un archivo
  git restore --staged archivo # Saca el archivo del staging
```

Después del commit:

```bash
  git revert <hash> # Crea un commit que revierte otro commit
```

"git reset" reescribe historia

## 3.7 Ramas

```bash
  git branch nueva-rama        # Crea una nueva rama
  git checkout nueva-rama     # Cambia a esa rama
  git checkout -b nueva-rama  # Crea y cambia a la rama en un solo paso
```

Ver ramas:

```bash
  git branch                  # Muestra ramas locales
  git branch -a               # Muestra ramas locales y remotas
```

Borrar rama:

```bash
  git branch -d rama           # Borra una rama local
```

Fusionar ramas:

```bash
  git checkout main            # Cambia a la rama principal
  git merge feature            # Fusiona la rama feature en main
```

Si hay conflictos:

Git los marca en los archivos

    Resolver manualmente

    git add

    git commit

## 3.8 Stash

```bash
  git stash                   # Guarda cambios sin hacer commit
  git stash list              # Lista stashes guardados
  git stash pop               # Aplica y borra el último stash
  git stash drop              # Borra un stash sin aplicarlo
```

## 3.9 Repositorios remotos

Agregar remote:

```bash
  git remote add origin https://github.com/usuario/repo.git # Vincula repo remoto
```

Subir cambios:

```bash
  git push origin main         # Sube commits al repositorio remoto
```

Bajas cambios:

```bash
  git pull                    # Trae y fusiona cambios remotos
  git fetch                   # Trae cambios sin fusionarlos
```

## 3.10 Tags

```bash
  git tag v1.0.0               # Crea un tag simple
  git tag -a v1.1.0 -m "release" # Crea un tag anotado
  git push --tags              # Sube los tags al remoto
```

## 3.11 Subir a remoto

Guardar cambios en la rama actual

Asegúrate de estar en la rama correcta (por ejemplo feature):

```bash
  git checkout feature        # Cambia a la rama feature
```
Guardar cambios:


```bash
  git add .                   # Añade todos los cambios al staging
  git commit -m "Add new feature"  # Crea un commit con los cambios
```

Comprobar commits pendientes:


```bash
  git log --oneline --all --graph   # Muestra el historial con ramas
```

Vincular el repositorio local con GitHub (solo una vez)

Si aún no tienes el remoto configurado:

```bash
  git remote add origin https://github.com/usuario/repositorio.git
```

Verificar:

```bash
  git remote -v               # Muestra los remotos configurados
```

Subir la rama principal (main) a GitHub

Cambiar a main:

```bash
  git checkout main           # Cambia a la rama main
```

Asegurarse de que está actualizada:

```bash
  git pull origin main        # Trae cambios remotos si existen
```

Subir a la rama:

```bash
  git push -u origin main     # Sube main y la vincula con GitHub
```
-u crea el seguimiento (tracking) entre local y remoto

Subir la segunda rama (feature) a GitHub

Cambiar a la rama secundaria:

```bash
  git checkout feature        # Cambia a la rama feature
```

Subirla por primera vez:

```bash
  git push -u origin feature  # Sube la rama feature a GitHub
```
Ahora ambas ramas existen en GitHub.

Subir cambios futuros (flujo normal)

Después del primer push, solo necesitas:

```bash
  git add .
  git commit -m "Update feature"
  git push                    # Sube cambios de la rama actual
```
Git sabe automáticamente a qué rama remota subir.

Fusionar la rama feature en main (opcional)

Cuando la feature esté lista:

```bash
  git checkout main           # Cambia a main
  git pull origin main        # Asegura que esté actualizada
  git merge feature           # Fusiona feature en main
```

Subir la fusión:

```bash
  git push                    # Sube main actualizada a GitHub
```

Borrar la rama feature (opcional)
Borrar localmente:

```bash
  git branch -d feature       # Borra la rama feature local
```

Borrar en GitHub

```bash
  git push origin --delete feature  # Borra la rama remota
```