# Práctica 1 - Sistema de Análisis Académico
**Curso:** Lenguajes Formales y de Programación
**Semestre:** 1S 2026

## Descripción del Proyecto
Este repositorio contiene el código fuente y la documentación de la Práctica 1. El proyecto es una aplicación de consola desarrollada en C++ que permite la lectura de archivos de texto plano (`.lfp`) con información académica (Estudiantes, Cursos y Notas). El sistema procesa estos datos dinámicamente en memoria y genera reportes estadísticos exportados automáticamente en formato HTML.

## ⚙️ Instrucciones de Ejecución
El proyecto está diseñado para compilarse y ejecutarse a través de la consola del sistema operativo (PowerShell, CMD, o terminal de MSYS2/Linux).

### Paso 1: Compilación
Abre una terminal, navega hasta la carpeta `Practica1` y ejecuta el compilador `g++`:
```bash
g++ main.cpp -o main.exe
```
*(Nota: Si usas Linux o Mac, el comando de salida puede ser `-o main` sin la extensión .exe).*

### Paso 2: Ejecución
Una vez generado el archivo ejecutable, lánzalo con el siguiente comando:
```bash
.\main.exe
```
*(En Linux/Mac utiliza `./main`)*

## 🚀 Ejemplos de Uso
Al iniciar el programa, se desplegará un menú interactivo del 1 al 9.

**1. Carga de datos:**
Para que el sistema funcione, primero debes cargar los archivos. Selecciona la opción `1` y escribe la ruta del archivo cuando el sistema lo solicite:
> `Seleccione una opcion: 1`
> `Ruta del archivo de estudiantes: estudiantes.lfp`

*(Repite este proceso con las opciones 2 y 3 para los cursos y las notas).*

**2. Generación de Reportes:**
Una vez cargados los tres archivos, selecciona cualquier opción del `4` al `8`. 
Por ejemplo, para ver a los mejores alumnos:
> `Seleccione una opcion: 6`
> `Generando Reporte 3: Top 10 Mejores Estudiantes...`

El sistema creará inmediatamente un archivo llamado `Reporte3_Top10.html` en la misma carpeta del proyecto. Ábrelo en cualquier navegador web para ver los resultados.

## Documentación
Dentro de la carpeta `Practica1` podrás encontrar la documentación detallada del proyecto:
* `Manual_Tecnico.md`: Arquitectura, estructuras de datos y lógica de parseo.
* `Manual_Usuario.md`: Guía paso a paso con capturas de pantalla del uso del sistema.
* `Informe_Desarrollo.md`: Retos técnicos, soluciones aplicadas y conclusiones.

```mermaid
flowchart TD
    Inicio([Inicio del Programa]) --> Menu[/Mostrar Menú Principal/]
    Menu --> LeerOpcion[/Usuario ingresa opción/]
    
    LeerOpcion --> |Opción 1, 2, 3| CargarArchivos
    LeerOpcion --> |Opción 4, 5, 6, 7, 8| GenerarReportes
    LeerOpcion --> |Opción 9| Salir([Fin del Programa])
    LeerOpcion --> |Otra| ErrorMenu[Mostrar: Opción no válida] --> Menu
    
    %% Flujo de Carga de Archivos
    subgraph CargarArchivos [Lectura y Separación de Datos]
        A1[Abrir archivo .lfp con ifstream] --> A2{¿Archivo existe?}
        A2 -- No --> A3[Mostrar Error]
        A2 -- Sí --> A4[Leer línea con getline]
        A4 --> A5{¿Línea vacía?}
        A5 -- Sí --> A4
        A5 -- No --> A6[Ejecutar función split por comas]
        A6 --> A7{¿Tiene 5 datos?}
        A7 -- Sí --> A8[Convertir tipos stoi/stof y guardar en vector]
        A7 -- No --> A4
        A8 --> A9{¿Fin del archivo?}
        A9 -- No --> A4
        A9 -- Sí --> A10[Cerrar archivo]
    end
    A10 --> Menu
    A3 --> Menu

    %% Flujo de Generación de Reportes
    subgraph GenerarReportes [Procesamiento y HTML]
        R1[Crear archivo .html con ofstream] --> R2[Escribir etiquetas y encabezados HTML]
        R2 --> R3[Iterar sobre vectores de datos en memoria]
        R3 --> R4[Calcular métricas estadísticas / Ordenar con Lambda]
        R4 --> R5[Escribir filas de datos en tabla HTML]
        R5 --> R6[Cerrar etiquetas body y html]
        R6 --> R7[Cerrar archivo ofstream]
        R7 --> R8[Notificar éxito al usuario]
    end
    R8 --> Menu
```
