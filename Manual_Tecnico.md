# Manual Técnico - Sistema de Análisis Académico (Práctica 1)

## 1. Descripción General
El Sistema de Análisis Académico es una aplicación desarrollada en C++ que se ejecuta en la consola del sistema operativo. Su objetivo principal es procesar información académica proveniente de archivos de texto plano (`.lfp`), almacenar los datos dinámicamente en memoria, realizar cálculos estadísticos y exportar reportes analíticos en formato HTML.

## 2. Requerimientos Técnicos
El desarrollo y ejecución del sistema requiere los siguientes componentes:
* **Lenguaje:** C++ (Estándar C++11 o superior).
* **Compilador:** `g++` (Recomendado entorno MSYS2 UCRT64 en Windows).
* **Librerías Estándar Utilizadas:**
  * `<iostream>`: Entrada y salida estándar en consola.
  * `<fstream>`: Lectura y escritura de archivos en disco (HTML y `.lfp`).
  * `<sstream>`: Procesamiento y tokenización de cadenas de texto.
  * `<vector>`: Almacenamiento dinámico de las estructuras de datos.
  * `<string>`: Manipulación de texto.
  * `<algorithm>`: Uso de la función `std::sort` para ordenamiento de datos.
  * `<cmath>`: Operaciones matemáticas avanzadas (`pow`, `sqrt`) para la desviación estándar.

## 3. Estructuras de Datos (`struct`)
Para mantener el programa ligero y eficiente, se utilizaron estructuras base en lugar de clases complejas para modelar la información de los archivos:

* **`Estudiante`**: Almacena `carnet` (int), `nombre` (string), `apellido` (string), `carrera` (string) y `semestre` (int).
* **`Curso`**: Almacena `codigo` (int), `nombre` (string), `creditos` (int), `semestre` (int) y `carrera` (string).
* **`Nota`**: Almacena `carnet` (int), `codigo_curso` (int), `nota` (float), `ciclo` (string) y `anio` (int).

Adicionalmente, se implementaron estructuras auxiliares (`EstudiantePromedio`, `CursoReprobacion`, `InfoCarrera`) exclusivamente para facilitar el cruce de datos y el ordenamiento mediante funciones Lambda en la generación de reportes.

## 4. Métodos y Funciones Principales

### 4.1. Funciones de Lectura y Parseo
* **`vector<string> split(const string& linea, char delimitador)`**
  Emula el comportamiento de funciones de separación de cadenas en otros lenguajes. Utiliza `stringstream` para iterar sobre una línea de texto y extraer los fragmentos separados por el delimitador (una coma), limpiando posibles espacios en blanco.
* **`cargarEstudiantes()`, `cargarCursos()`, `cargarNotas()`**
  Abren el archivo especificado utilizando `ifstream`. Leen el archivo línea por línea con `getline()`, omiten líneas vacías y aplican la función `split()`. Finalmente, convierten los tipos de datos de string a int/float usando `stoi()` y `stof()`.

### 4.2. Funciones de Generación de Reportes
* **`generarReporte1(...)` a `generarReporte5(...)`**
  Cada función recibe por referencia constante (`const vector&`) los arreglos de datos necesarios. Ejecutan la lógica matemática correspondiente (promedios, conteos, ordenamientos) y construyen secuencialmente un archivo `.html` utilizando la clase `ofstream` para inyectar etiquetas HTML puras concatenadas con las variables calculadas.

## 5. Lógica de Lectura y Procesamiento de Archivos (Pseudocódigo)
La lectura de los archivos `.lfp` sigue este flujo estructurado para garantizar que no se procesen datos corruptos:

## 6. Observaciones Relevantes del Desarrollo
Ordenamiento Eficiente: Se integró el uso de funciones Lambda dentro del método std::sort() de la librería <algorithm>. Esto permitió ordenar vectores de estructuras complejas basándose en un atributo específico (como el porcentaje de reprobación) sin necesidad de escribir algoritmos de ordenamiento manuales extensos.

Robustez en la Compilación: El proyecto demostró que la compilación directa en terminal mediante comandos (ej. g++ main.cpp -o main.exe) es fundamental para evitar conflictos con archivos temporales o restricciones de seguridad de IDEs de terceros.

```text
INICIO funcion cargarArchivo(ruta_archivo)
    Intentar abrir el archivo(ruta_archivo)
    SI NO se pudo abrir:
        Imprimir error y retornar vector vacio
    
    MIENTRAS existan lineas por leer en el archivo:
        Leer linea
        SI linea esta vacia:
            Continuar a la siguiente linea
        
        arreglo_datos = split(linea, ',')
        
        SI tamano(arreglo_datos) == 5 (formato correcto):
            Crear nueva estructura
            Convertir arreglo_datos[0] a entero
            Convertir arreglo_datos[2] a decimal (si aplica)
            Asignar datos a la estructura
            Agregar estructura al vector principal
    FIN MIENTRAS
    
    Cerrar archivo
    Retornar vector principal
FIN
