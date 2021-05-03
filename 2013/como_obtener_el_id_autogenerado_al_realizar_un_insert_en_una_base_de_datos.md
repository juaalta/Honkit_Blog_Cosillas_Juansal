# Como obtener el ID autogenerado al realizar un insert en una base de datos

Para obtener el ID autogenerado se han de concatenar las sentencias marcadas en negrita:

## SQLServer

INSERT INTO Foo () VALUES (); **SELECT CAST(scope_identity() AS int);**

## MySql

INSERT INTO Foo () VALUES (); **SELECT LAST_INSERT_ID();**

## SQlite

INSERT INTO Foo () VALUES (); **SELECT last_insert_rowid();**
