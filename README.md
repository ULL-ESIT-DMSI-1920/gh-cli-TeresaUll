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


# 3. Alias gh org-list

Queremos un alias que liste todas los nombres y las urls de las organizaciones a las que el usuario pertenece:

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