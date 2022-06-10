## Práctica 9.
### Operaciones en una base de datos.
Objetivo: Demostrar las operaciones que se realizan en una base de datos, aplicar el modelo relacional y el lenguaje SQL

Evaluación: Para poder tener correcto cada ejercicio deberán de mostrar el resultado que se da en cada respuesta.


Lista el nombre de todos los productos que hay en la tabla producto.
![image](https://user-images.githubusercontent.com/101668305/172985100-1fc47edb-0664-4dd4-8fec-58ce7f70da24.png)
![image](https://user-images.githubusercontent.com/101668305/172985139-4f8c9dd5-7d33-4947-9805-81e8c575591c.png)

1. Lista los nombres y los precios de todos los productos de la tabla producto.
![image](https://user-images.githubusercontent.com/101668305/172984917-2dd9a4a5-ec08-4561-8eec-3e75e3885b16.png)
![image](https://user-images.githubusercontent.com/101668305/172984966-9576441f-a45d-4a3f-8ad7-6aefb694be15.png)

2. Lista todas las columnas de la tabla producto.
![image](https://user-images.githubusercontent.com/101668305/172985212-20fbd241-d6c6-45cc-8baa-a9601b987096.png)
![image](https://user-images.githubusercontent.com/101668305/172985260-e274cfd6-6523-44b2-9c4b-f73d355103de.png)

3. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de
todos los productos de la base de datos.

![image](https://user-images.githubusercontent.com/101668305/173125224-abc9cc3d-0cac-4a31-87c0-87eb0462de9b.png)
![image](https://user-images.githubusercontent.com/101668305/173125278-569ee598-e338-43f5-aa42-dee4677aee55.png)


Subconsultas (En la cláusula WHERE)
1. Devuelve todos los productos del fabricante Lenovo. (Sin utilizar INNER
JOIN).
![image](https://user-images.githubusercontent.com/101668305/173130788-02ff3480-20dc-4bd1-88b6-c39667b7a328.png)
![image](https://user-images.githubusercontent.com/101668305/173130820-c030699e-5405-4c16-b285-0af4f7322960.png)



2. Devuelve todos los datos de los productos que tienen el mismo precio que el
producto más caro del fabricante Lenovo. (Sin utilizar INNER JOIN).

![image](https://user-images.githubusercontent.com/101668305/173133911-9450b940-630b-4170-b508-dac11974e81e.png)
![image](https://user-images.githubusercontent.com/101668305/173133960-016d5600-bcb0-4e0b-a0dc-4a7a2acb7b9f.png)


Hice una modificación a uno de los costos para ver si funcionaba y si lo arrojó
![image](https://user-images.githubusercontent.com/101668305/173134042-1eae22af-0b36-488c-93b2-130fa30f6169.png)

3. Lista el nombre del producto más caro del fabricante Lenovo.
**Schema (MySQL v5.7)**

    CREATE DATABASE tienda_informatica;
    USE tienda_informatica;
    
    CREATE TABLE fabricante (
      id_fabricante INT UNSIGNED PRIMARY KEY,
      nombre_fabricante VARCHAR(100) NOT NULL  
      );
      INSERT INTO fabricante VALUES (01,'SEAGATE');
      INSERT INTO fabricante VALUES (02,'CRUCIAL');
      INSERT INTO fabricante VALUES (03,'SAMNSUNG');
      INSERT INTO fabricante VALUES (04,'GIGAYTE');
      INSERT INTO fabricante VALUES (05,'ASUS');
      INSERT INTO fabricante VALUES (06,'LENOVO');
      INSERT INTO fabricante VALUES (07,'HP');
      
      CREATE TABLE producto (
       codigo VARCHAR (100) PRIMARY KEY,
       descrip_producto VARCHAR (100) NOT NULL,
       precio FLOAT UNSIGNED NOT NULL,
       existencia INT UNSIGNED   NOT NULL    
       );
      INSERT INTO producto VALUES('DD-23','Disco duro SATA 3 1TB',86.99,0);
      INSERT INTO producto VALUES( 'MM-34','Memoria RAM DDR4 8GB', 120,6);
      INSERT INTO producto VALUES('DD-98','Disco SSD 1 TB', 150.99,0 );
      INSERT INTO producto VALUES('MM-98','GeForce GTX 1050Ti',185,7 );
      INSERT INTO producto VALUES('MM-23','GeForce GTX 1080 Xtreme', 755,6 );
      INSERT INTO producto VALUES('MT-12','Monitor 24 LED Full HD', 202,1 );
      INSERT INTO producto VALUES('MT-08','Monitor 27 LED Full HD', 245.99,0 );
      INSERT INTO producto VALUES('LP-19','Portatil Yoga 520',559,2);
     INSERT INTO producto VALUES('LP-11','Portatil Ideapd 320',444,2 );
      INSERT INTO producto VALUES('IM-56','Impresora HP Deskjet 3720',59.99,3);
     INSERT INTO producto VALUES('IP-54','Impresora HP Laserjet Pro M26nw', 180,3);
       
      CREATE TABLE elabora(
       
       id_fabricante1 INT UNSIGNED,
       codigo1 VARCHAR (100),
    	FOREIGN KEY (id_fabricante1) REFERENCES fabricante (id_fabricante),
        FOREIGN KEY (codigo1) REFERENCES producto (codigo)     
     );
       
    INSERT INTO elabora VALUES (01,'DD-23');
    INSERT INTO elabora VALUES (02,'MM-34');
    INSERT INTO elabora VALUES (03,'DD-98');
    INSERT INTO elabora VALUES (04,'MM-98');
    INSERT INTO elabora VALUES (02,'MM-23');
    INSERT INTO elabora VALUES (05,'MT-12');
    INSERT INTO elabora VALUES (05,'MT-08');
    INSERT INTO elabora VALUES (06,'LP-11');
    INSERT INTO elabora VALUES (07,'IM-56');
    INSERT INTO elabora VALUES (07,'IP-54');
    INSERT INTO elabora VALUES (06,'LP-19');
    

---

**Query #1**

    USE tienda_informatica;

There are no results to be displayed.

---
**Query #2**

    SELECT descrip_producto AS 'PRODUCTO'
    FROM producto
    
    WHERE  codigo like 'LP-%'
    
    and (select MAX (precio) FROM producto WHERE codigo like 'LP-%');

| PRODUCTO            |
| ------------------- |
| Portatil Ideapd 320 |
| Portatil Yoga 520   |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/kAzBPA9TnpEXGJQPGyJru1/1)
