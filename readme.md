# Práctica del curso de git, gitHub y Sourcetree

## Respuestas a las preguntas

* **¿Qué comando utilizaste en el paso 11? ¿Por qué?**

Usé `git reset --hard HEAD~1` para ir al commit anterior, con la opción `--hard` para perder los cambios en el working copy. Si no hubiese puesto esa opción, el fichero de markdown seguiría teniendo las últimas modificaciones y no el contenido inicial.

Teniendo en cuenta el estado del repositorio en ese momento, también se podría haber usado el comando `git reset --hard master` con idéntico resultado.

* **¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?**

Primero ejecuté `git reflog` para ver el histórico de modificaciones. Ahí busqué el commit que tenía las modificaciones en la rama styled y por último usé `git reset --hard 0603be9` para volver al último commit y recuperar los cambios en el fichero en el working copy.

* **El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?**

Este merge no causa ningún cambio ni conflicto, ya que en la rama styled ya tenemos el commit al que apunta master.

* **El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?**

Las dos ramas apuntan a commits distintos con un padre común (el commit al que apunta master), así que se produce un conflicto al hacer el merge.

* **El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?**

Este merge no causó ningún conflicto y se pudo hacer con fast-forward, ya que el commit al que apuntaba master estaba incluido en el grafo de la rama styled.

* **¿Qué comando o comandos utilizaste en el paso 25?**

Con `git log --graph --decorate --pretty=oneline` obtenemos un diagrama simplificado de la situación en la que estamos actualmente:

```
*   9111ad70fe7b1e37de9b55c812c6cfc5c7529800 (HEAD -> master, styled) Mezclamos la rama htmlify en styled
|\
| * 72942654d8b53d075cd3efcd4835eefc9ad2f823 (htmlify) Modificamos el Git Nuestro en la rama htmlify
* | 0603be9e286ba6cae6d68e644178bef040b43287 Modificamos el Git Nuestro en la rama styled
|/
* badc75fe8ebf2ae3157dd27cfb3dab1c81b9dec6 Añadimos el Git Nuestro
```

Como estamos en master, no se ve la rama title, ya que tiene otro commit superior.

* **El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?**

Efectivamente, podría haber sido fast-forward, ya que el commit al que apuntaba title era el que estaba justo "por encima" del commit al que apuntaba master.

* **¿Qué comando o comandos utilizaste en el paso 27?**

Podríamos haber hecho este paso de tres maneras:

1. `git reset HEAD~1` (o bien `git reset HEAD~`, que es equivalente)
2. `git reset styled` (ya que master y styled apuntaban al mismo commit antes de hacer el merge con title)
3. `git reset HEAD^1` 

Yo he optado por la primera opción.

* **¿Qué comando o comandos utilizaste en el paso 28?** 

Como el merge se hizo sin conflictos no se puede volver al último commit y hacer un `git merge --abort`. La solución que me ha parecido más sencilla para descartar los cambios es ejecutar `git reset --hard styled`.

* **¿Qué comando o comandos utilizaste en el paso 29?** 

Como ahora la rama no está fusionada, hay que borrarla con `git branch -D title`.

* **¿Qué comando o comandos utilizaste en el paso 30?**

Con `git reflog` miramos el histórico de cambios y buscamos el merge. En mi caso he vuelto con `git reset --hard 5112b04`.

* **¿Qué comando o comandos usaste en el paso 32?**

Tras ejecutar `git log` vamos al último commit que sale en la lista (que es el primero que se hizo). En mi caso con `git reset badc75fe8ebf2ae3157dd27cfb3dab1c81b9dec6`. No se ha especificado nada sobre el working copy, así que no he puesto la opción `--hard`.

* **¿Qué comando o comandos usaste en el punto 33?**

Ejecuté un `git reflog`, revisé los pasos y volví al último con `git reset 5112b04`. Aunque teniendo en cuenta que en el paso 30 habíamos hecho algo parecido, podría haber ejecutado directamente el mismo comando (aunque en este caso el `--hard` no hacía falta ya que había vuelto al primer commit sin cambiar el working copy).

## Pasos de la práctica

1. **Crear un repositorio**

```
mkdir PracticaGit
cd PracticaGit
git init
```

2. **Crear un archivo git-nuestro.md con el contenido...**

```
vim git-nuestro.md
```

3. **Añadir git-nuestro.md al staging area**

```
git add git-nuestro.md
```

4. **Mover lo que hay en el staging area al repositorio**

```
git commit -m "Añadimos el Git Nuestro"
```

5. **Crear una rama llamada “styled”**

```
git branch styled
```

6. **Listar las ramas que hay en el repositorio**

```
git branch
```

7. **Moverse a la rama “styled”**

```
git checkout styled
```

8. **Comprobar que se está en la rama correcta**

```
git branch
```

9. **Modificar en el archivo git-nuestro.md...**

```
vim git-nuestro.md
```

10. **Añadir los cambios al staging área y luego pasarlos al repositorio**

```
git add git-nuestro.md
git commit -m "Modificamos el Git Nuestro en la rama styled"
```

11. **Deshacer el último commit (perdiendo los cambios realizados en el working copy)**

```
git reset --hard HEAD~1
```

12. **Rehacer el último commit (el que acabamos de deshacer)**

```
git reflog
git reset --hard 0603be9
```

13. **Hacer un merge con ‘master’ (styled absorbe a master)**

```
git merge master
```

14. **Volver a la rama master**

```
git checkout master
```

15. **Crear una nueva rama llamada “htmlify”**

```
git branch htmlify
```

16. **Cambiar a la rama htmlify**

```
git checkout htmlify
```

17. **Modificar en el archivo git-nuestro.md...**

```
vim git-nuestro.md
```

18. **Hacer un commit**

```
git add git-nuestro.md
git commit -m "Modificamos el Git Nuestro en la rama htmlify"
```

19. **Hacer un merge de “htmlify” en “styled” (styled absorbe a htmlify)**

```
git checkout styled
git merge htmlify
```

20. **Si hay conflictos, deberemos resolverlos quedándonos con el contenido de la rama “styled”.**

```
vim git-nuestro.md
git add git-nuestro.md
git commit -m "Mezclamos la rama htmlify en styled"
```

21. **Desde “master”, hacer un merge con “styled”**

```
git checkout master
git merge styled
```

22. **Crear una rama “title” y cambiarse a esa rama**

```
git branch title
git checkout title
```

23. **Añadir un título (a tu gusto) al archivo git-nuestro.md y hacer un commit.**

```
vim git-nuestro.md
git add git-nuestro.md
git commit -m "Añadimos un título al fichero git-nuestro.md en la rama titled"
```

24. **Volver a la rama master**
 
```
git checkout master
```

25. **Dibujar el diagrama**

```
git log --graph --decorate --pretty=oneline
```

26. **Hacer un merge “no fast-forward” de “title” en “master” (master absorbe a title)**

```
git merge --no-ff title
```

27. **Deshacer el merge (sin perder los cambios del working copy)**

```
git reset HEAD~1
```

28. **Descartar los cambios**

```
git reset --hard styled
```

29. **Eliminar la rama “title”**

```
git branch -D title
```

30. **Rehacer el merge que hemos deshecho**

```
git reflog
git reset --hard 5112b04
```

31. **Volver a master y eliminar el resto de ramas**

```
git branch
git branch -d styled
git branch -d htmlify
```

32. **Volver al commit inicial cuando se creó el poema**

```
git log
git reset badc75fe8ebf2ae3157dd27cfb3dab1c81b9dec6
```

33. **Volver al estado final, cuando pusimos título al poema**

```
git reflog
git reset 5112b04
```

34. **Crear los siguientes tags:**
* inicial: en el primer commit 
* styled: modificación del paso 10  
* htmlify: modificación del paso 17-18  
* title: modificación del paso 30

```
git log
git tag inicial badc75fe8ebf2ae3157dd27cfb3dab1c81b9dec6
git tag styled 0603be9e286ba6cae6d68e644178bef040b43287
git tag htmlify 72942654d8b53d075cd3efcd4835eefc9ad2f823
git tag title 
```

35. **Ir al tag htmlify**

```
git checkout htmlify
```
