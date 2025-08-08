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

## ⚠️ Longitud de las variables de texto

Si tu texto tiene más de 8 caracteres, debes especificar la longitud:

```sas
data ejemplo_longitud;
    input nombre $15. apellidos $25. ciudad $20.;
    datalines;
    Roberto "García López" "Las Palmas de Gran Canaria"
    Ana "Fernández Ruiz" Barcelona
    ;
run;
```

**Nota**: Usa comillas cuando el texto contiene espacios para que lo trate como información de la misma variable.

## 🔄 Ejemplo mixto (números y texto)

```sas
data empleados;
    input id nombre $12. departamento $15. salario edad;
    datalines;
    1001 "Juan Pérez" Ventas 35000 28
    1002 "Ana García" Marketing 42000 32
    1003 "Luis Martín" "Recursos Humanos" 38000 29
    ;
run;

proc print data=empleados;
    title "Listado de Empleados";
run;
```

### Resultado:
```
Listado de Empleados

Obs     id    nombre        departamento        salario    edad
 1     1001   Juan Pérez    Ventas              35000      28
 2     1002   Ana García    Marketing           42000      32
 3     1003   Luis Martín   Recursos Humanos    38000      29
```

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

## 🔍 Cómo identificar el tipo de variable

Usa `PROC CONTENTS` para ver información sobre las variables de cualquier tabla, por ejemplo, la de empleados que acabamos de crear:

```sas
proc contents data=empleados;
run;
```

Esto te mostrará:
- **Type**: Num (numérica) o Char (texto). 
- **Len**: Longitud de la variable.
- **Format**: Formato de visualización.

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
