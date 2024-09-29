---
layout: post
title:  "Instalar ruby en GNU/Linux!"
---


## Como instalar ruby en gnu/linux sin volverse loco
Podemos usar alguno de estos dos gestores de versiones de ruby : RVM o rbenv

En este caso vamos a hacerlo con rbenv ,¿por qué? porque se me da la gana

#### Observación importante: 
No debemos tener instalados RVM y rbenv al mismo tiempo porque trae conflictos. Debemos elegir uno o el otro.


* 1 ° paso : instalar rbenv

Para instalar rbenv lo mejor es NO hacerlo mediante los repositorios oficiales de las distros , ya que suele estar desactualizado.

En cambio vamos directamente al repositorio del proyecto y lo clonamos


```git
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```

* 2 ° paso : Agregamos el directorio rbenv a la variable de entorno $PATH.
Esto es para que luego se pueda ejecutar como un comando más de bash rbenv , y no tengamos que especificar toda la ruta hasta la carpeta cada vez que lo usemos.

```git
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc 
echo 'eval "$(rbenv init -)"' >> ~/.bashrc 
source ~/.bashrc
```

*Nota* : estos pasos son para el shell bash , si tenés otro fijate en la documentación del mismo como hacerlo.

* 3 ° paso : Configuramos rbenv 

```git
~/.rbenv/bin/rbenv init
```

* 4 ° paso : Reiniciamos la terminal . Cerramos y la abrimos nuevamente para que tomen efecto los cambios.
- 5 ° paso : Verificamos que la instalación haya sido exitosa con el siguiente comando

```git
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash
```
Y deberíamos obtener lo siguiente como salida.

```git
Checking for `rbenv' in PATH: /usr/local/bin/rbenv
Checking for rbenv shims in PATH: OK
Checking `rbenv install' support: /usr/local/bin/rbenv-install (ruby-build 20170523)
Counting installed Ruby versions: none
  There arent any Ruby versions installed under `~/.rbenv/versions'.
  You can install Ruby versions like so: rbenv install 2.2.4
Checking RubyGems settings: OK
Auditing installed plugins: OK
```

- 6 ° Paso : Ahora sí , instalamos Ruby . 
- 
 Listamos las versiones disponibles 
 ```git
 rbenv install -l
```
y por ejemplo en este momento obtenemos las siguientes : 

```git
2.6.10
2.7.6
3.0.4
3.1.2
jruby-9.3.7.0
mruby-3.1.0
picoruby-3.0.0
rbx-5.0
truffleruby-22.2.0
truffleruby+graalvm-22.2.0

Only latest stable releases for each Ruby implementation are shown.
Use 'rbenv install --list-all / -L' to show all local versions.
```
En mi caso voy a instalar la más actual : 3.1.2

```git
rbenv install ruby 3.1.2
```

Podría suceder que aparezcan errores si no tenemos en el sistema las dependencias necesarias. Como por ejemplo *openssl* y *libssl-dev*, en ese caso instalarlas y volver a intentarlo.

Y con eso ya lo tenemos listo. Podemos ver que se instaló con : 

```bash
ruby -v
```
```bash
ruby 3.1.2p20 (2022-04-12 revision 4491bb740a) [x86_64-linux]
```

El chiste de rbenv es poder tener múltiples versiones de ruby e ir usando cada una donde se necesite. Para instalar otra versión distinta seguimos los mismos pasos. Y para listar todas las que tengamos instaladas

```bash
rbenv versions
```

rbenv tiene más comandos para configurar la versión *global* y *local* . Leer la documentación en https://github.com/rbenv/rbenv

### Quiero instalar una versión de ruby que rbenv no muestra.

Si al hacer `rbenv install -l` en las versiones disponibles a instalar no se encuentra la que deseamos (recordar que solo muestra versiones estables) entonces debemos actualizar ruby-build , la herramienta que se encarga de instalar las versiones de ruby.

Vamos a ir a la carpeta donde se instaló rbenv y una vez dentro de ella traemos los cambios que se hayan hecho a ruby-build desde el repo oficial de rbenv.

```sh
git -C plugins/ruby-build pull

# La opción -C es porque ruby-build tiene su propio repo.
```