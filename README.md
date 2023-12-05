# 1-Data-Modeling

1. [Instalar PostgreSQL](#schema1)
2. [Instalar psycopg2](#schema2)
3. [Paso a paso para crear una base de datos y un usuario en PostgreSQL](#schema3)
4. [Creating table with Cassandra](#schema4)
5. [Normalización y dernomalización](#schema5)
6. [Formas Normales](#schema6)


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



<hr>

<a name="schema4"></a>

## 4- Demo2: Creating table with Cassandra

- Instalar la librearía para que se ejecute Apache Cassandra.
```
pip install cassadra-driver
```
- Instalar Apache Cassandra para ejecutarlo localmente en locacl. 
Pasos a seguir: https://cassandra.apache.org/doc/stable/cassandra/getting_started/installing.html

Lesson 1 - Demo 2 -creating-a-table-with-apache-cassandra.ipynb



<hr>

<a name="schema5"></a>

## 5. Normalización y dernomalización


La normalización y la denormalización son dos conceptos importantes en el diseño de bases de datos relacionales. 
Ambos están relacionados con la eficiencia y la integridad de los datos en una base de datos, pero se aplican 
en contextos diferentes.

### **Normalización:**

- Definición: La normalización es el proceso de organizar los datos en una base de datos para reducir la redundancia 
y mejorar la integridad de los datos.
- Objetivo: Eliminar la redundancia y dependencias funcionales, asegurando que los datos estén almacenados de manera 
eficiente y sin anomalías.
- Métodos: Se logra dividiendo las tablas grandes en tablas más pequeñas y relacionadas, aplicando reglas específicas 
(formas normales) que eliminan ciertos tipos de redundancia y aseguran que cada dato esté almacenado en un lugar 
específico.
Las formas normales más comunes son la primera forma normal (1NF), la segunda forma normal (2NF), la tercera 
forma normal (3NF), y así sucesivamente. Cada forma normal aborda diferentes tipos de redundancia y dependencias.

### **Denormalización:**

- Definición: La denormalización es el proceso opuesto a la normalización. Implica combinar tablas relacionadas para 
formar tablas más grandes y menos normalizadas.
- Objetivo: Mejorar el rendimiento de las consultas y reducir la complejidad de la base de datos al costo de 
introducir cierta redundancia.
- Métodos: Se logra permitiendo duplicidad de datos y almacenando información de manera más redundante para f
acilitar consultas más rápidas y simples.
La denormalización es útil en situaciones donde el rendimiento de las consultas es crítico y la redundancia 
controlada no compromete la integridad de los datos. Se aplica típicamente en bases de datos orientadas a la 
lectura intensiva, como sistemas de informes o almacenes de datos.

En resumen, mientras que la normalización busca eliminar la redundancia y asegurar la integridad de los datos, 
la denormalización busca mejorar el rendimiento de las consultas al permitir cierta redundancia controlada. 
La elección entre normalización y denormalización depende de los requisitos específicos y las características 
de uso de la base de datos.



<hr>

<a name="schema6"></a>

## 6. Formas Normales


### **Primera Forma Normal (1NF):**

- Definición: Una tabla se encuentra en la 1NF si todos sus atributos contienen valores atómicos, es decir, 
valores que no se pueden dividir más. Además, no debe haber conjuntos de valores repetidos en ninguna fila.
- Ejemplo: Si tienes una tabla de estudiantes y sus cursos, en 1NF cada celda de la tabla debe contener un único valor. 
Por ejemplo, en lugar de tener una columna "Cursos" con varios cursos separados por comas, cada curso debería estar en una fila separada junto con la información del estudiante.

### **Segunda Forma Normal (2NF):**

- Definición: Una tabla está en 2NF si cumple con la 1NF y, además, ningún atributo no clave depende de una parte de 
una clave primaria compuesta, sino de la totalidad de esa clave.
- Ejemplo: Supongamos que tienes una tabla de pedidos con información del cliente y de los productos en cada pedido. 
Si la clave primaria es (Número de Pedido, ID del Producto), y tienes un atributo como "Nombre del Cliente" que 
depende solo del "Número de Pedido" (una parte de la clave), entonces para cumplir con la 2NF, debes separar 
la información del cliente en otra tabla.

### **Tercera Forma Normal (3NF):**

- Definición: Una tabla está en 3NF si cumple con la 2NF y, además, ningún atributo no clave depende transitivamente 
de una clave primaria. Esto significa que no debe haber dependencias no directas entre atributos no clave.
- Ejemplo: Consideremos una tabla de empleados con atributos como "Dirección del Departamento" y "Nombre del 
Jefe del Departamento". Si la clave primaria es el "ID del Empleado", y la "Dirección del Departamento" y 
el "Nombre del Jefe del Departamento" dependen solo del "ID del Departamento" (y no directamente del "ID del Empleado"),
entonces para cumplir con la 3NF, debes trasladar la información del departamento a otra tabla.

Estas formas normales son pasos graduales en el proceso de normalización y se aplican para reducir la redundancia 
y mejorar la integridad de los datos en una base de datos relacional. Es importante señalar que existen formas normales 
más allá de la 3NF, como la Forma Normal de Boyce-Codd (BCNF) y la Cuarta Forma Normal (4NF), que abordan situaciones 
más específicas.


<hr>

<a name="schema7"></a>

## 7. Clustering Column

En Apache Cassandra, un "clustering column" se refiere a una columna en la clave primaria de una tabla que 
determina el orden de los datos dentro de una partición. La clave primaria en Cassandra se compone de dos partes: 
la "partición key" y las "clustering columns".

- Partición Key: Es responsable de la distribución de los datos a través de los nodos del clúster. 
Cada fila de la tabla pertenece a una partición determinada según los valores de la partición key.

- Clustering Columns: Son responsables de la ordenación de los datos dentro de una partición. 
Los datos dentro de una partición se ordenan según los valores de las clustering columns.




En una clave primaria compuesta en Cassandra, la primera columna especificada es la "partición key", y 
las columnas subsiguientes son las "clustering columns".

Aquí hay un ejemplo con una explicación más detallada:

```
CREATE TABLE ejemplo (
    partition_key_column text,
    clustering_column1 int,
    clustering_column2 text,
    other_columns text,
    PRIMARY KEY (partition_key_column, clustering_column1, clustering_column2)
);
```

En este caso:

partition_key_column es la "partición key". Es la primera columna en la clave primaria y se utiliza para distribuir 
los datos a través de las particiones en el clúster.

clustering_column1 y clustering_column2 son las "clustering columns". Son las columnas que determinan el orden de 
los datos dentro de una partición.

Cuando realizas consultas en esta tabla, la "partición key" especifica la partición a la que pertenecen los datos, 
y las "clustering columns" determinan el orden de los datos dentro de esa partición.


Lesson  3 - Demo 3 -clustering-column.ipynb