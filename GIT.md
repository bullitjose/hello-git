# GIT 
[web MoureDev en youtube](https://https://www.youtube.com/watch?v=3GymExBkKjE&ab_channel=MoureDevbyBraisMoure)




**$git checkout hellogit.py**  

Descartar cambios del working directory e ir a la ultima foto de commit del fichero:
```
$git status                             
En la branca master
Canvis no «staged» per a cometre:
  (useu «git add <fitxer>...» per a actualitzar què es cometrà)
  (useu «git restore <file>...» per a descartar canvis en el directori de treball)
	modificat:        hellogit.py

no hi ha canvis afegits a cometre (useu «git add» o «git commit -a»)
 ```
 ```
$git checkout hellogit.py          
S'ha actualitzat un camí des de l'índex
```


Moverse o situarse por los diferentes commits:
```
$git checkout n0commit(verlo en el git log)
```
Para mover el HEAD a ese commit antiguo:
```
$git checkout HEAD
```

Moverse de un fichero que no queremos grabar o hacer commit, volver a su ultimo commit:
```
$git checkout nombreFichero
```

Crear un alias, en este caso muestra log, entre comillas, todos los commits realizados, y en que formato:
```
$git config --global alias.tree "log --graph --decorate --all --oneline"
```

Eliminar commits previos y situarse en uno determinado:
```$git reset --hard idCommit```
Ojo, no eliminamos commits!! con reflog se puede ver todos los movimientos:
```
$git reflog
8a05197 (HEAD -> master) HEAD@{0}: checkout: moving from 18eab43b197e0117440099cc38fd80dfdf61645c to master
18eab43 HEAD@{1}: checkout: moving from 8a051976f98c2358c3dc67846dfe3ad62ed008a1 to 18eab43
8a05197 (HEAD -> master) HEAD@{2}: checkout: moving from 627f2be77547bc81291e357c0b18c4b108239777 to 8a05197
627f2be HEAD@{3}: checkout: moving from master to 627f2be77547bc81291e357c0b18c4b108239777
8a05197 (HEAD -> master) HEAD@{4}: commit: Se añade el .gitingnore
18eab43 HEAD@{5}: commit: Se actualiza el texto del print
5f06fcb HEAD@{6}: reset: moving to HEAD
5f06fcb HEAD@{7}: reset: moving to HEAD
5f06fcb HEAD@{8}: commit: Este es mi segundo commit
627f2be HEAD@{9}: commit (initial): Este es mi primer commit
```

$git reset --hard idCommit , tambien sirve para resetear e ir a una posicion de commit final (idCommit).

**tag**.Los tags se utilizan como puntos importantes
```
$git tag clase_1
$git log
commit 8a051976f98c2358c3dc67846dfe3ad62ed008a1 (HEAD -> master, tag: clase_1)
Author: JOSE <bullit.jose@gmail.com>
Date:   Tue Feb 28 12:53:29 2023 +0100

    Se añade el .gitingnore

commit 18eab43b197e0117440099cc38fd80dfdf61645c
Author: JOSE <bullit.jose@gmail.com>
Date:   Tue Feb 28 12:37:36 2023 +0100

    Se actualiza el texto del print

commit 5f06fcbd4b17f07fa0462c578d530797f3257190
Author: JOSE <bullit.jose@gmail.com>
Date:   Mon Feb 27 18:10:08 2023 +0100

    Este es mi segundo commit

commit 627f2be77547bc81291e357c0b18c4b108239777
Author: JOSE <bullit.jose@gmail.com>
Date:   Mon Feb 27 13:39:48 2023 +0100

    Este es mi primer commit
```
Con tag, indicamos que ese 4 commit tambien se puede llamar clase_1
Si añadimos commits tras clase_1, se mueve el HEAD y se veria:
```
* 901be81 (HEAD -> master) este es mi 5 commit
* 8a05197 (tag: clase_1) Se añade el .gitingnore
* 18eab43 Se actualiza el texto del print
* 5f06fcb Este es mi segundo commit
* 627f2be Este es mi primer commit
```
Para volver a tag creado, mover el 	HEAD al commit al que apunta clase_1:
```
git checkout tags/clase_1 
```
la salida de git tree, seria:
```
* 901be81 (master) este es mi 5 commit
* 8a05197 (HEAD, tag: clase_1) Se añade el .gitingnore
* 18eab43 Se actualiza el texto del print
* 5f06fcb Este es mi segundo commit
* 627f2be Este es mi primer commit

```

Añadir a area de stage todo los ficheros pendientes:
```
$git add .
```

+ Git branch i switch
Crear ramas o branchs:
```
$git branch login
$git tree
* 901be81 (HEAD -> master, login) este es mi 5 commit
* 8a05197 (tag: clase_1) Se añade el .gitingnore
* 18eab43 Se actualiza el texto del print
* 5f06fcb Este es mi segundo commit
* 627f2be Este es mi primer commit
```
Se ha creado rama login, pero nuestro HEAD, APUNTA!!! AUN A MASTER (HEAD -> master), como cambiar a login:
```
$git switch login
```
Si ahora hacemos cambios, se añaden (add .) y luego commit, se añaden a la nueva rama.

Si volvemos a master, los cambios de la nueva rama no se ven!!

**¡¡utilizar siempre switch para cambiar de ramas , no checkout ¡¡**

+ GIT MERGE
Merge, combinar cambios, de la master a nuestra rama, login:
```
$git merge main
$git tree
*   7cef54b (HEAD -> login) Merge branch 'master' into login
|\  
| * 47da440 (master) Git 3 v2
* | 2575035 Login
|/  
* 901be81 este es mi 5 commit
* 8a05197 (tag: clase_1) Se añade el .gitingnore
* 18eab43 Se actualiza el texto del print
* 5f06fcb Este es mi segundo commit
* 627f2be Este es mi primer commit

```


+ Conflictos en git

Si hacemos un merge de master a una rama de trabajo (login), y hay conflictos, nos lo indica:
```
$git merge master
S'està autofusionant hellogit3.py
CONFLICTE (contingut): Conflicte de fusió en hellogit3.py
La fusió automàtica ha fallat; arregleu els conflictes i després cometeu el resultat.
```
Hay que sincronizar los conflictos,git nos dice que el coflicto esta en hellogit3.py, si vamos al fichero (vscode):

head (current change)
print("hello git 3 v login")

=======
print("hello git 3! v3")
>>>>>
>> master (Incoming Change)

Aquí se puede ver las diferencias entre lo que queremos incorporar (master), y lo que tenemos en la rama de trabajo (HEAD)

+ Stash
Commits se hacen de codigo que funciona. En otro caso utilizar stash, guarda el codigo temporalmente en la maquina local:
```
$git stash
S'han desat el directori de treball i l'estat d'índex WIP on login: 05378b6 Correccion hellogit3.py
```
```
$git stash list
stash@{0}: WIP on login: 05378b6 Correccion hellogit3.py
(END)
```
con el stash list vemos los cambios guardados en local!!!

Recuperar lo que habia en stash:
```
$git stash pop
En la branca login
Canvis no «staged» per a cometre:
  (useu «git add <fitxer>...» per a actualitzar què es cometrà)
  (useu «git restore <file>...» per a descartar canvis en el directori de treball)
	modificat:        hellogit3.py
	modificat:        login.py

no hi ha canvis afegits a cometre (useu «git add» o «git commit -a»)
Descartada refs/stash@{0} (f7b1a0d9c524d15daf00efdb6cc079a325ed0de4)
```
Eliminar lo que hay en stash:
```
$git stash drop
```


+ Reintegración de ramas en Git

Para integrar la rama login a master, previo hacer git status en login para ver que no hay nada a cometer (commit); luego ir a la rama master:
´´´
$git switch master
´´´
Mirar si puede haber complictos, comparamos ramas:

```
$git diff login
diff --git a/hellogit3.py b/hellogit3.py
index 2b7a0ac..00218d0 100644
--- a/hellogit3.py
+++ b/hellogit3.py
@@ -1 +1 @@
-print("hello git 3! v3")
+print("hello git 3! v3")
\ No newline at end of file
diff --git a/login.py b/login.py
deleted file mode 100644
index bf59e16..0000000
--- a/login.py
+++ /dev/null
@@ -1 +0,0 @@
-print ("login v32")
\ No newline at end of file
```


Podemos hacer merge,
```
$git merge login
S'estan actualitzant 9527612..feea8e0
Fast-forward
 hellogit3.py | 2 +-
 login.py     | 1 +
 2 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 login.py
```

Eliminar rama login (estando en master):
```
$git branch -d login
S'ha suprimit la branca login (era feea8e0).

```
**En realidad, todo lo que hacemos commit NO SE ELIMINA**
```
$reflog
saldran todos los commits realizados, incluso los "eliminados"
$git checkout idCommitEliminado
Nos indica que estamos en 'detached HEAD' state, o un estat de «HEAD separat»
$git tree
* feea8e0 (master) Login v4
* 980bbcf (HEAD) Login v3
* fcbfaa3 Login v2
*   05378b6 Correccion hellogit3.py
|\  
| * 9527612 Git commit v3
* | 0f05722 Git 3 login v2
* | 7fdd70b Git 3 login
* | 7cef54b Merge branch 'master' into login
|\| 
| * 47da440 Git 3 v2
* | 2575035 Login
|/  
* 901be81 este es mi 5 commit
* 8a05197 (tag: clase_1) Se añade el .gitingnore
* 18eab43 Se actualiza el texto del print
* 5f06fcb Este es mi segundo commit
* 627f2be Este es mi primer commit
```
**Aquí si indica con HEAD, DONDE NOS HEMOS POSICIONADO CON EL checkout idCommitEliminado!!!**

**Volver a master con checkout**

**Si lo hacemos con switch, y anteriormente login se ha eliminado tendremos:**
```
$git switch login
fatal: referència no vàlida: login
```

