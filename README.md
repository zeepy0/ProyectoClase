# Práctica guiada de Git y GitHub
## Todos los comandos usados en la consola de git.

## 1.-Creamos la carpeta y entramos:

```bash
mkdir prueba_git
cd prueba_git
```

## 2.- Entramos en la carpeta y creamos los archivos:

**Archivo `texto.txt`:**

```text
uno
dos
tres
```

**Archivo `script.sh`:**

```bash
echo Listado completo
ls -l
```
## 3.- Ejecutamos los comandos:

```bash
chmod a+x script.sh
./script.sh
```

# Y nos devuelve por pantalla: 

```text
Listado completo
total 2
-rw-r--r-- 1 raulc 197609 27 Oct 29 22:29 script.sh
-rw-r--r-- 1 raulc 197609 15 Oct 29 22:28 texto.txt
```

## 4.- Ejecutamos git innit dentro de prueba_git

```bash
git init
```

Salida:

```text
Initialized empty Git repository in C:/Users/raulc/prueba_git/.git/
```

Consultamos el estado

```bash
git status
```

Salida:

```text
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Cambiamos el nombre de la rama principal a `main`:

```bash
git branch -m main
git status
```

La salida de `git status`:

```text
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Volvemos el nombre a master: 

```bash
git branch -m master
```

## 5.- Añadimos los archivos


```bash
git add script.sh
git status
```
Salida: 

```text
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   script.sh

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt
```

Configuramos el correo de la cuenta para hacer el commit

```bash
git config --global user.email "cordeiromoreiraraul@gmail.com"
```

Hacemos el primer commit:

```bash
git commit -m "Confirmacion inicial"
```

Salida:

```text
[master (root-commit) 93582cf] Confirmacion inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh
```

Comrpobamos el estado:

```bash
git status
```

Salida:

```text
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Lo mismo con texto.txt:

```bash
git add texto.txt
git commit -m "Añadido archivo texto.txt"
```

Salida:

```text
[master 40d4038] Añadido archivo texto.txt
 1 file changed, 3 insertions(+)
 create mode 100644 texto.txt
```

De nuevo status:

```bash
git status
```

```text
On branch master
nothing to commit, working tree clean
```

## 6.- Comprobamos que pasa al modificar el archivo texto.txt

```bash
git status
```

Se detecta que ha sido modificado

```text
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Guaramos los cambios

```bash
git add texto.txt
git status
```

Añadimos el texto pero sin commit

```text
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt
```

modificamos de vuelta

```bash
git status
```

muestra los cambios preparados y los que quedan por preaparar

```text
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt
```

añadimos los últimos cambios y hacemos commit:

```bash
git add texto.txt
git commit -m "Ampliada la explicacion del texto"
git status
```

Salida:

```text
[master 6d2ebf1] Ampliada la explicacion del texto
 1 file changed, 3 insertions(+), 1 deletion(-)

On branch master
nothing to commit, working tree clean
```

## 7.- Probamos el comando:

```bash
git commit -a -m "Nueva version"
```

como no hay cambios pendientes

```text
On branch master
nothing to commit, working tree clean
```

Consultamos los detalles del último commit:

```bash
git show
```

La salida mostró el commit `6d2ebf1`, su autor, fecha y las diferencias introducidas en `texto.txt`.

Consultamos el historial completo

```bash
git log
```

El historial obtenido fue:

```text
commit 6d2ebf1dff71c080f8aca134aa7d68a299639938 (HEAD -> master)
Author: Raul Y David <cordeiromoreiraraul@gmail.com>
Date:   Thu Oct 29 22:40:40 2026 +0100

    Ampliada la explicacion del texto

commit 40d4038d327b64d853d05d2a0c5e3e252e4740e6
Author: Raul Y David <cordeiromoreiraraul@gmail.com>
Date:   Thu Oct 29 22:38:38 2026 +0100

    Añadido archivo texto.txt

commit 93582cf9f8b82f52f69b9998cb3dd71ad46992bf
Author: Raul Y David <cordeiromoreiraraul@gmail.com>
Date:   Thu Oct 29 22:36:37 2026 +0100

    Confirmacion inicial
```

## 7. Diferencias entre versiones: `git diff`

Modificamos `texto.txt` para añadir `seis`

```bash
git diff
```

Se mostraron las líneas añadidas y eliminadas. Después confirmamos los cambios:

```bash
git commit -a -m "Probando diff"
```

Salida:

```text
[master bc7f289] Probando diff
 1 file changed, 2 insertions(+), 2 deletions(-)
```

Añadimos la linea siete al archivo

```bash
git diff
```
La salida: 

```diff
@@ -3,3 +3,4 @@ dos
 cuatro
 cinco
 seis
+siete
```
Mostrando con el + que se añadió el 7

## 7. Ignorar archivos: `.gitignore`

Creamos el archivo `.gitignore` y `Hola.java`.

```gitignore
# ignora los archivos terminados en .class
*.class

# ignora los archivos terminados en ~
*~

# no ignora este archivo aunque termine en ~
!importante~
```
Hola.java:

```java
class Hola {
    public static void main(String[] args) {
        System.out.println("Welcome to the Java World");
    }
}
```

Creamos los archivos `temporal~` e `importante~`

Comprobamos el contenido del directorio

```bash
ls -a
```

Salida:

```text
./  ../  .git/  .gitignore  Hola.java  importante~  script.sh  temporal~  texto.txt
```
Consulté el estado del repositorio:

```bash
git status
```

Salida:

```text
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   script.sh
        modified:   texto.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        Hola.java
        importante~

no changes added to commit (use "git add" and/or "git commit -a")
```

Hacemos add para todos los cambios y commit.

```bash
git add .
git commit -m "Añadidos fuentes en java y archivos importantes"
```

Salida:

```text
[master 0d5a953] Añadidos fuentes en java y archivos importantes
 5 files changed, 15 insertions(+), 1 deletion(-)
 create mode 100644 .gitignore
 create mode 100644 Hola.java
 create mode 100644 importante~
```

Para ver los archivos incluidos en la última versión ejecutamos:

```bash
git ls-tree --name-only -r HEAD
```

Salida:

```text
.gitignore
Hola.java
importante~
script.sh
texto.txt
```

## 8. Tags

Consultamose el historial abreviado

```bash
git log --oneline
```

Salida:

```text
0d5a953 (HEAD -> master) Añadidos fuentes en java y archivos importantes
bc7f289 Probando diff
6d2ebf1 Ampliada la explicacion del texto
40d4038 Añadido archivo texto.txt
93582cf Confirmacion inicial
```

Creamos una etiqueta `v0.7`

```bash
git tag v0.7
```

Después asignamos otra etiqueta a un commit anterior

```bash
git tag v0.3 bc7f2898a7f0c1f48de2bb01cd496b2c9655ea15
```

Consultamos con show mediante las etiquetas 

```bash
git show v0.3
```
Donde git mostro el commit de la etiqueta con la version v0.3

Para volver a esa versión ejecutamos:

```bash
git checkout v0.3
```

resultado: 

```text
Note: switching to 'v0.3'.

You are in 'detached HEAD' state...
HEAD is now at bc7f289 Probando diff
```

Volvimos a master.

```bash
git checkout master
```

Salida:

```text
Previous HEAD position was bc7f289 Probando diff
Switched to branch 'master'
```

## 9. Ramas:

Creamos una rama llamada `Prueba`:

```bash
git branch Prueba
```

Consultamos el historial resumido:

```bash
git log --oneline
```


Comprobamos las ramas con branch:

```bash
git branch
```

Salida:

```text
  Prueba
* master
```

Donde el asteriosco marca la rama en la que estoy

cambiamos a la rama `Prueba`:

```bash
git switch Prueba
```

Salida:

```text
Switched to branch 'Prueba'
```

volvimos a consultar las ramas:

```bash
git branch
```

```text
* Prueba
  master
```

Creamos otra etiqueta
```bash
git tag v0.7-Ent-Release
```
## 10. Repositorio remoto: GitHub

Enlazamos los repositorios local con remoto

```bash
git remote add origin https://github.com/zeepy0/ProyectoClase
```

Descargue los archivos del repositorio;

```bash
git pull origin main --no-rebase --allow-unrelated-histories
```

```text
Already up to date.
```

Hacemos un push del repositorio local: `Prueba` y `main`: 

```bash
git push -u origin Prueba
```

Salida:

```text
* [new branch]      Prueba -> Prueba
branch 'Prueba' set up to track 'origin/Prueba'.
```

```bash
git push -u origin main
```

Salida:

```text
To https://github.com/zeepy0/ProyectoClase
   d367ea5..5171a24  main -> main
branch 'main' set up to track 'origin/main'
```
