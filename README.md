# Práctica gh-cli 
Teresa Bonet Costa
DMSI

## Introducción 

En esta práctica vamos a ver diversos comandos utilizados para controlar GitHub desde la terminal, todos ellos empezarán con el comando ` gh `. 
Es necesario autentificarse en el terminal para que se nos den los permisos para alterar lo que deseemos de Github, para ello empezamos utilizando el comando: 
```
 gh auth login

```
 Aquí se nos pedirá autentificarnos con un token que debemos crear desde la página de GitHub, en "Developer Settings" -> "Personal Access Tokens". 

En la siguiente documentación crearemos diversos alias para aquellos comandos más utilizados, de este modo se simplifica su utilización.

Es importante explicitar todos los arguments y también los flags del comando de lo que se quiere hacer el alias. El comando base que se utiliza para hacer un alias es el siguiente:
```
gh alias <comando> [flags`

```
Los comandos disponibles son:

set: para crear un nuevo alias
delete: para eliminar un alias ya existente
list: para enumerar los alias

# 1. Alias gh create-repo

Para crear un nuevo repositorio utilizamos el siguiente comando: 

`gh repo create organización-propietario/nombreRepositorio`

Vamos a crear un alias para que el comando sea el siguiente: 

`gh create-repo nombreRepositorio org`

Ejecutamos el siguiente código para que se cree el alias:

```
gh alias set create-repo 'repo create "$2"/"$1"' 

```
La forma de utilizar el alias es la siguiente:

gh create-repo [repositorio] [organización o propietario]


# 2. Alias delete-repo
Para eliminar un repositorio utilizamos el siguiente comando: 

`gh api -X DELETE /repos/organización-propietario/nombreRepositorio`

Vamos a crear un alias para que el comando sea el siguiente: 

`gh delete-repo nombreRepositorio organización-propietario`

Ejecutamos el siguiente código para que se cree el alias:

```
gh alias set delete-repo 'api -X DELETE /repos/"$2"/"$1"' 

```
La forma de utilizar el alias es la siguiente:

gh delete-repo [repositorio] [organización o propietario]

El flag -X indica que podrá utilizar el método delete para cambiar el repositorio.
# 3. Alias gh org-list

Queremos un alias que liste todas los nombres y las urls de las organizaciones a las que el usuario pertenece:
Para ver todas las organizaciones a las que pertenece una persona podemos utilizar gh api /user/memberships/orgs, esto nos devuelve las organizaciones pero no es la información que realmente deseamos. Debemos utilizar una serie de comandos para obtener la organización y su url:


`gh api /user/memberships/orgs | jq '.[].organization | .login, .url'`


Vamos a crear un alias para que el comando sea el siguiente: 

`gh org-list organización-propietario`

Ejecutamos el siguiente código para que se cree el alias:

```
gh alias set org-list "api --paginate /user/memberships/orgs --jq '.[].organization | .login, .url'"

```

La forma de utilizar el alias es la siguiente:

gh org-list [organización o propietario]

 Explicación de los argumentos utilizados para obtener la lista:

* --paginate: Junta request que llegan desde el serivicio web.
* --jq: Filtra la entrada en JSON.
* .[]: Devuelve todos los elementos del array del fichero Json.
* .organization: Escoge los elementos que se llamen organization.
* | .login, .url: Indica que queremos los elementos login y url de organization.


# 4. Extensión en JS
Una extensión de gh es  un comando de GitHub CLI que añade una nueva funcionalidad al gh que no existe por defecto. Por convención, las extensiones han de llamarse gh-nombre-de-la-funcionalidad.

 Gh extension tiene 5 comandos:

* create: para crear una nueva gh extension
* install: para instalar una gh extension desde un repositorio que ya existe
* list: muestra la lista de todos los gh extension que se han instalado
* remove: quita una gh extension ya instalada
* upgrade: hace un upgrade de una gh extension ya instalada

Como ejemplo, desarrollaremos una extensión utilizando código JavaScript que nos permitirá cambiar el nombre de un repositorio usando el comando creado, le llamaremos gh-repo-rename.

Empezamos creando la extensión con los siguiente comandos:

```
gh extension create gh-teresa-repo-rename
cd gh-teresa-repo-rename
gh repo create --public ULL-ESIT-DMSI-1920 gh-teresa-repo-rename

```


Ahora tenemos un repositorio creado en la organización ULL-ESIT-DMSI-1920  desde el cual podremos implementar el código que cambiará el nombre a un repositorio.

Necesitaremos crear un package json en este repositorio donde quedarán fijadas las dependencias.

En el package.json tenemos información importante 
