# Repositorio de misiones

Este repositorio contiene misiones para Arma  3. Cada una de ellas tiene su propia carpeta y la nomenclatura que se usa para indentificar a cada una de ellas es la siguiente:

`aa@bb-cc_NombreMision.Isla` o también `aa@x_NombreMision.Isla` cuando el número de jugadores es variable.

donde:

* `aa` es el tipo de misión: `co` (Cooperativa), `tvt` (Team vs team), ... 
* `bb` es el número mínimo de jugadores.
* `cc` es el número máximo de jugadores.
* `MissionName` és una abreviación del nombre de la misión *sin espacios*.
* `Isla` es el idenfificador del mapa: Altis, Stratis, Tanoa, Chernarus, ...

### Lista de misiones

| **Misión**                   | **Carpeta**                             | **Autor**     | **Colaboradores**           | **Plantilla** |
| -----------------------------| --------------------------------------- | ------------- | --------------------------- | ------------- |

## Cómo añadir una misión que usa la *Arma 3 - Basic Mission Template*

La plantilla *Arma 3 - Basic Mission Template* (A3-BMT) es una plantilla diseñada con el objetivo de que sea fácil de actualizar. Esto se consigue separando los archivos con scripts básicos de aquellos que acostumbran a ser modificados misión a misión. No obstante, todos los scripts pueden ser actualizados un día u otro para solventar incompatibilidades o simplemente para mejorar los scripts en si.

Por tal de evitar comprovar cada vez qué ha cambiado, se sugiere el siguiente método, basado en *git-subtree* a la hora de generar des de cero una misión con la A3-BMT.

### Paso 1: Configurar el repositorio git

Este paso sólo se debe realizar una sola vez, especialmente tras clonar o descargar el repositorio al disco duro. Para ello deberemos abrir el fichero .git/config y añadir las siguientes líneas si se usa el método ssh:

```
[alias]
# Este acrónimo es lo mismo que "subtree add"
sba = "!f() { git subtree add --prefix $1 git@github.com:ust101/Basic-Mission-Template.git master --squash; }; f"

# Este acrónimo es lo mismo que "subtree update"
sbu = "!f() { git subtree pull --prefix $1 git@github.com:ust101/Basic-Mission-Template.git master --squash; }; f"
```
o si se usa https:

```
[alias]
# Este acrónimo es lo mismo que "subtree add"
sba = "!f() { git subtree add --prefix $1 https://github.com/ust101/Basic-Mission-Template.git master --squash; }; f"

# Este acrónimo es lo mismo que "subtree update"
sbu = "!f() { git subtree pull --prefix $1 https://github.com/ust101/Basic-Mission-Template.git master --squash; }; f"
```

### Paso 2: Añadir una misión

Una vez se tenga el repositorio git correctamente configurado, podemos proceder a crear la carpeta con la mision. Para ello haremos lo siguiente:

`git sba aa@bb-cc_NombreMision.Isla`

Esto creará una carpeta con el estado actual de la plantilla A3-BMT. Procederemos a crear nuestra mision de la forma habitual (Editor de Arma 3). Una vez se hayan realizado los cambios y la misión esté lista "guardaremos" el estado con `git commit -am "Versión 1.0"` seguido de un `git push`.

### Paso 3: Actualizar una misión

Si queremos actualizar los scripts de la misión con una nueva versión de la A3-BMT, procederemos de la siguiente forma:

1. Nos aseguraremos que el directorio esté limpio. Si no es así, se deberán descartar los cambios mediante `git reset --hard`, guardarlos con `git stash` o hacerlos permanentes usando `git commit -am "Cambios ..."`.
2. Actualizar la mision con `git sbu aa@bb-cc_NombreMision.Isla`. Esto, a diferencia del método manual, hará actualizará recursivamente los cambios y nos avisará en el caso de que haya conflictos.
3. Resolver los conflictos en el caso de que los haya y guardar los cambios con `git commit`.
4. Actualizar el repositorio con `git push`.
