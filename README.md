# Proyectos
Rama desarrollo de una webapp en html/css/js/node-express/mysql

# GUÍA PARA EL DESARROLLO
## 1- Para iniciar un proyecto en NodeJS añadimos en la terminal el siguiente comando
``` npm init ```

### Este comando crea una archivo "package.json" que contiene la info de nuestro proyecto y las dependencias necesarias para su funcionamiento.

### 2- Para instalar paquetes (dependencias) en nuestro proyecto, utilizamos el gestos de paquetes "npm". Instalamos "express" (web server): 
``` npm install express ```

### 3- Si iniciamos un proyecto clonado por primera vez desde Github, para que se instalen todos los paquetes necesarios (Irá a mirar el package.json):

``` npm install ```

### 4- Documentación de Node Express (webserver):
- https://expressjs.com/es/

### 5- Para que el servidor se reinicie cada vez que detecta un cambio en el código, instalamos el paquete (modo desarrollo):
``` npm i nodemon -g -D ```

### 6- Para que funcione en Windows añadir en el terminal:
``` Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser ```

# DEPLOY

### 7- Ejemplo de despliegue (deploy) de la app en "railway" (proveedor gratuito):

1- https://railway.app/ 
2- Desinstalar el paquete "mysql" e instalar "mysql2"
```
npm uninstal mysql
npm install mysql2
```
3- Realizar los siguientes cambios en el código del proyecto:

  - Cambiar la constante "port" añadiendo la variable de entorno "PORT" (el puerto que utilizará "railway)
  ```
  const port = process.env.PORT || 3000;
  ``` 

4- Crear un proyecto nuevo en "railway" -> "Provision MYSQL":
5- En la base de datos creada, ir a la pestaña "query" y añadir nuestro código sql que crea la tabla:
```
create table dato (
	id int primary key auto_increment,
    dato varchar(255)
);

```
6- Ir a la pestaña de "Connect" -> "Available Variables" y copiar los datos de acceso en nuestro código del proyecto:
```
const pool = mysql.createPool({
  host: process.env.HOST || 'localhost',
  user: process.env.USER || 'root',
  password: process.env.PASSWORD || '',
  database: process.env.NAME || 'proyecto',
  port: process.env.PORT || 3306,
  connectionLimit: 10
});
```

7- Añadir esta linea en la prop de "scripts" en el "package.json":
```
"start": "node server.js"
```
8- Crear un nuevo proyecto "GitHub Repo", conectar con tu cuenta de GitHub y seleccionar el repositorio que quieres deplegar.

9- Entrar en la pestaña "variables" y añadir las 5 variables de entorno de conexion a la DB:

``` 
HOST *******
NAME *******
PASSWORD *******
PORT *******
USER *******
```

10- En los "settings" del proyecto, crear un dominio. Esta URL es donde apunta a nuestra webapp. 

11- Si ha habido algun error en el depliegue o app, clickar en el propio despliegue -> "Deploy Logs"



