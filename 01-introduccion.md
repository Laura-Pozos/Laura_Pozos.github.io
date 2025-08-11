# 1. Introducción a SAS - Primeros pasos

[← Volver al inicio](./index.html)

## ¿Qué es SAS?

SAS (Statistical Analysis System) es una herramienta potente para:
- **Gestión de datos**: Importar, limpiar y transformar datos.
- **Análisis estadístico**: De todo tipo, desde descriptivos hasta modelos complejos. 
- **Automatización**: Crear procesos que se ejecuten automáticamente.
- **Reportes**: Generar informes profesionales.

## Mi primer programa SAS

Empecemos con algo sencillo. Desde la pestaña Archivo vamos a crear un nuevo programa:

<img width="517" height="128" alt="image" src="https://github.com/user-attachments/assets/a10cb947-a103-49ef-9a9a-704acba2dbca" />



Este programa crea un dataset y muestra su contenido:

```sas
/* Mi primer programa SAS */
data mi_primer_dataset;
    input nombre $ edad ciudad $;
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

⭐ Lee la siguiente [guía sobre tipos de variables](./02-tipos-variables.html) para dominar las variables numéricas y de texto.

### ¿Qué hace este código?

1. **`data mi_primer_dataset;`** - Crea un nuevo set de datos o dataset.
2. **`input`** - Define las variables y sus tipos ($ = texto)
3. **`datalines;`** - Inicia la sección de datos.
4. **`run;`** - Ejecuta el paso DATA
5. **`proc print`** - Muestra el contenido del dataset.

## Resultado 

<img width="223" height="117" alt="image" src="https://github.com/user-attachments/assets/cf371d3b-e494-40c7-b9fc-dd08751a8991" />

Como veréis, se ha truncado la ciudad de Barcelona porque tiene más de 8 caracteres. Si no especificamos un número mayor al crear la variable de texto, por defecto SAS la crea con un máximo de 8 caracteres.
En la guía [2. Tipos de variables](./02-tipos-variables.html) aprenderemos cómo crear variables de texto con mayor longitud para evitar que esto ocurra.

## Conceptos clave 

- **Dataset**: Una tabla de datos en SAS
- **Variables**: Las columnas de nuestros datos
- **Observaciones**: Las filas de nuestros datos
- **DATA step**: Para crear y manipular datos
- **PROC step**: Para analizar y mostrar datos

## 💡 Consejo práctico

Siempre termina cada instrucción con `;`. Al decirle a SAS `run;`, es como decirle "ejecuta esto ahora".

## ⚡ Ejercicio práctico

Intenta crear un dataset con información sobre ti:
- Tu nombre
- Tu edad  
- Tu ciudad
- Tu trabajo

## 🔗 Próximo tutorial

En [2. Tipos de variables](./02-tipos-variables.html) aprenderemos en detalle sobre variables numéricas y de texto en SAS.

---

[← Volver al inicio](./index.html) | [Siguiente →](./02-tipos-variables.html)

*¿Te ha sido útil este tutorial? ¡Compártelo en LinkedIn!*
