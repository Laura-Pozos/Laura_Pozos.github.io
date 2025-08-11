# 2. Tipos de Variables en SAS

[← Volver al inicio](./index.html)

## ¿Qué son las variables en SAS?

Las variables son las columnas de una tabla y los registros u observaciones son las filas. En SAS tenemos **dos tipos principales** de variables:

- **Variables Numéricas** - para números y cálculos.
- **Variables de Texto (Character)** - para letras y palabras.

> 💡 **Nota**: SAS también tiene tipos más avanzados como fechas, formatos especiales y variables categóricas que veremos en el [8. Variables avanzadas y formatos](./08-variables-avanzadas.html).

## 🔢 Variables Numéricas

Son variables que contienen **números** (enteros o decimales).

```sas
data ejemplo_numericas;
    input edad salario altura peso;
    datalines;
    25 35000 1.75 70.5
    30 42000 1.80 85.2
    28 38500 1.65 62.8
    ;
run;
```

### Características de las variables numéricas:
- **No hay que incluir** el símbolo `$` en el INPUT.
- Pueden tener **decimales** (usa punto, no coma).
- Permiten **cálculos matemáticos**
- **Valores perdidos o nulos** se representan con punto (.).

## 📝 Variables de Texto (Character)

Son variables que contienen **texto, letras o caracteres**.

```sas
data ejemplo_texto;
    input nombre $ ciudad $ genero $;
    datalines;
    Pablo Granada M
    Laura Barcelona F
    Carlos Valencia M
    ;
run;
```

### Características de las variables de texto:
- **Requieren** el símbolo `$` en el INPUT.
- **No permiten** cálculos matemáticos.
- **Sensibles** a mayúsculas/minúsculas.
- **Longitud máxima** por defecto: 8 caracteres.

## Longitud de las variables de texto

Como veíamos en el apartado anterior, si la variable de texto tiene más de 8 caracteres, debes especificar la longitud: 

```sas
/* Mi primer programa SAS */
data mi_primer_dataset;
    input nombre $ edad ciudad $11.;
    datalines;
    Pablo 25 Granada
    Laura 30 Barcelona
    Carlos 28 Valencia
    ;
run;

proc print data=mi_primer_dataset;
    title "Mi primera tabla en SAS";
run;
```

Hemos puesto 11 caracteres para la variable ciudad por lo que ahora podremos leer todas las ciudades del ejemplo completas:

<img width="241" height="118" alt="image" src="https://github.com/user-attachments/assets/9cb5939d-8ba0-4eca-95eb-f5a68e063a85" />

## Espacios en las variables de texto

Al crear variables de texto que contengan espacios, SAS necesita instrucciones para acotarlas correctamente. Para ello, necesitaremos:
tenemos que decirle a SAS hasta dónde debe coger y para ello añadiremos en el código `infile datalines dlm=' ' dsd;`,  utilizaremos `""` como delimitadores y añadiremos `:` en el tipo de variable: `:$12.`
Aquí dsd hace que SAS interprete que las comillas dobles agrupan texto con espacios y no lo divide, y dlm=' ' indica que el delimitador es el espacio.


1. **`infile datalines dlm=' ' dsd;`** - Le dice a SAS que el delimitador entre variables es el espacio y que interprete las comillas dobles como agrupadores de texto.
2. **Comillas dobles `""`** - Para agrupar el texto que necesitemos que contenga espacios.  
3. **Dos puntos `:$longitud.`** - Los dos puntos permiten que la variable use menos caracteres si no los necesita.

En el siguiente ejemplo creamos una nueva tabla con variables numéricas y de texto con espacios:

```sas

data empleados;
    infile datalines dlm=' ' dsd;
    input id nombre :$20. departamento :$20. salario edad;
    datalines;
    1001 "Juan Pérez" "Ventas" 35000 28
    1002 "Ana García" "Marketing" 42000 32
    1003 "Luis Martín" "Recursos Humanos" 38000 29
;
run;


proc print data=empleados;
    title "Listado de Empleados";
run;
```

### Resultado:

<img width="383" height="116" alt="image" src="https://github.com/user-attachments/assets/8cad049f-1efd-436b-acd3-c7fe4e728f89" />



## 🧮 Operaciones con variables

### Con variables numéricas:
```sas
data calculos;
    input salario_base horas_extra;
    salario_total = salario_base + (horas_extra * 15);  /* Cálculo */
    datalines;
    2000 10
    2500 5
    ;
run;
```
<img width="305" height="80" alt="image" src="https://github.com/user-attachments/assets/8e6057fa-f134-41af-a92d-5f8792a193b3" />


### Con variables de texto:
```sas
data textos;
    input nombre $ apellido $;
    nombre_completo = catx(' ', nombre, apellido);  /* Concatenar */
    datalines;
    Juan Pérez
    Ana García
    ;
run;
```
<img width="318" height="121" alt="image" src="https://github.com/user-attachments/assets/dadef647-48a2-4a1d-ba2c-94eec1ae36a1" />


## 🔍 Cómo identificar el tipo de variable

Usa `PROC CONTENTS` para ver información sobre las variables de cualquier tabla, por ejemplo, la de empleados que acabamos de crear:

```sas
proc contents data=empleados; run;
```

Esto te mostrará mucha información sobre la tabla seleccionada (número de observaciones, variables, tamaño...), destacando especialmente el detalle de cada una de las variables:
- **Tipo**: Num (numérica) o Alfanumérica/Char (texto). 
- **Long**: Longitud de la variable.


## 💡 Consejos importantes

1. **Planifica tus variables**: Decide qué tipo necesitas antes de crearlas.
2. **Longitud suficiente**: Para texto como con la comida, mejor que sobre que no que falte. Si algún registro (o todos ellos) tiene mayor longitud de la especificada en la variable, el texto se truncará (se cortará). 
3. **Consistencia**: Usa el mismo tipo para variables similares.
4. **Nombres descriptivos**: `edad` es mejor que `var1`. Evita espacios, tildes y caracteres especiales como la ñ en los nombres de las variables para no tener problemas al utilizarlas posteriormente.

> 🚀 **¿Quieres conocer más variables?** Si quieres trabajar con fechas, formatos especiales y variables categóricas, ve al [8. Variables avanzadas](./08-variables-avanzadas.html).

## ⚡ Ejercicio práctico

Crea un dataset con información de productos:
- `codigo`: numérico (ej: 1001, 1002)
- `nombre`: texto (ej: "Seguro de Hogar")
- `categoria`: texto (ej: "Seguros")
- `prima`: numérico (ej: 499.99)
- `canal`: numérico (ej: 2)

## 🔗 Enlaces relacionados

- [← 1. Introducción a SAS](./01-introduccion.html)
- [3. Librerías y datasets →](./03-librerias.html)

---

[← Volver al inicio](./index.html)

*¿Te ha sido útil este tutorial? ¡Compártelo en LinkedIn!*
