# Práctica gh-cli 
Teresa Bonet Costa
DMSI


En esta práctica vamos a ver diversos comandos utilizados para controlar GitHub desde la terminal, todos ellos empezarán con el comando gh. 
Es necesario autentificarse en el terminal para que se nos den los permisos para alterar lo que deseemos de Github, para ello empezamos utilizando el comando: 

 `gh auth login`

 Aquí se nos pedirá autentificarnos con un token que debemos crear desde la página de GitHub, en "Developer Settings" -> "Personal Access Tokens". 

Crearemos diversos alias para aquellos comandos más utilizados, de este modo Ese simplifica su utilización.

Es importante explicitar todos los arguments y también los flags del comando de lo que se quiere hacer el alias. El comando base que se utiliza para hacer un alias es el siguiente:

`gh alias <comando> [flags]`

# 1. Alias gh create-repo

Para crear un nuevo repositorio utilizamos el siguiente comando: 

`gh repo create ULL-ESIT-DMSI-1920/teresaprueba`

Vamos a crear un alias para que el comando sea el siguiente: 

`gh create-repo teresaprueba ULL-ESIT-DMSI-1920`

# 2. Alias delete-repo
Para eliminar un repositorio utilizamos el siguiente comando: 

`gh api -X DELETE /repos/ULL-ESIT-DMSI-1920/pruebateresa`

Vamos a crear un alias para que el comando sea el siguiente: 

`gh delete-repo teresaprueba ULL-ESIT-DMSI-1920`

# 3. Alias gh org-list

Queremos un alias que liste todas los nombres y las urls de las organizaciones a las que el usuario pertenece:

`gh api /user/memberships/orgs | jq '.[].organization | .login, .url'`


Vamos a crear un alias para que el comando sea el siguiente: 

`gh org-list ULL-ESIT-DMSI-1920`


# 4. Extensión en JS