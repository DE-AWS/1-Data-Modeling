# 1-Data-Modeling

1. [Instalar PostgreSQL](#schema1)
2. [Instalar psycopg2](#schema2)
3. [3- Paso a paso para crear una base de datos y un usuario en PostgreSQL](#schema3)


<hr>

<a name="schema1"></a>

## 1- Instalar PostgreSQL

```
sudo apt install postgresql

```
<hr>

<a name="schema2"></a>

## 2- Instalar psycopg2
```
conda install -c anaconda psycopg2
```

<hr>

<a name="schema3"></a>

## 3- Paso a paso para crear una base de datos y un usuario en PostgreSQL:

- Iniciar la consola de PostgreSQL:

```
sudo -u postgres psql
```

- Crear un usuario:

Dentro de la consola de PostgreSQL, ejecuta el siguiente comando para crear un nuevo usuario. 
Reemplaza nuevo_usuario y tu_contraseña con el nombre de usuario y la contraseña que deseas usar:
```
CREATE USER nuevo_usuario WITH PASSWORD 'tu_contraseña';
```

- Crear una base de datos:

A continuación, crea una nueva base de datos. Reemplaza nueva_base_de_datos con el nombre de la base de datos 
que deseas crear:
```
CREATE DATABASE nueva_base_de_datos;
```

- Conceder privilegios al usuario sobre la base de datos:

Otorga todos los privilegios al usuario sobre la nueva base de datos. 
Reemplaza nuevo_usuario y nueva_base_de_datos con los valores que has utilizado anteriormente:

```
GRANT ALL PRIVILEGES ON DATABASE nueva_base_de_datos TO nuevo_usuario;
```

- Salir de la consola de PostgreSQL:

Puedes salir de la consola de PostgreSQL escribiendo:
```
\q
```




```
CREATE DATABASE studentdb;

# para saber la base de datos en la que estas
SELECT current_database();
```