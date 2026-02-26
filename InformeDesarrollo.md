# Informe de Desarrollo 
**Práctica 1: Sistema de Análisis Académico**
**Curso:** Lenguajes Formales y de Programación

---

## 1. Implementación de la Práctica
El sistema fue desarrollado íntegramente en **C++**, priorizando un manejo de memoria eficiente y una ejecución rápida por medio de la consola. La arquitectura se basó en los siguientes pilares:
* **Estructuras Base (`struct`):** Se definieron entidades claras para `Estudiante`, `Curso` y `Nota`, evitando la sobrecarga de clases complejas.
* **Vectores Dinámicos:** El uso de `std::vector` permitió almacenar los datos cargados desde los archivos `.lfp` en tiempo de ejecución, facilitando la iteración y el filtrado iterativo.
* **Manipulación de Cadenas:** Se implementó una función personalizada `split` utilizando `std::stringstream` para separar los datos separados por comas, simulando el comportamiento nativo de lenguajes de más alto nivel.
* **Exportación a HTML:** Se hizo uso de la librería `<fstream>` (`ofstream`) para escribir directamente la estructura de etiquetas HTML, tablas y datos iterados, construyendo reportes listos para visualizarse en cualquier navegador.

---

## 2. Retos Técnicos y Soluciones Aplicadas

Durante el desarrollo, la lógica de programación y el diseño de los algoritmos funcionaron a la perfección. Sin embargo, el principal reto técnico se presentó en la fase de compilación del entorno local.

* **Reto:** El compilador `g++` (mediante MSYS2) ejecutaba el comando de construcción sin arrojar errores en consola, pero fallaba silenciosamente en generar el archivo ejecutable (`main.exe`). Inicialmente, los síntomas apuntaban a una intercepción agresiva por parte de Windows Defender o conflictos de sincronización en directorios de la nube.
* **Diagnóstico:** Dado que el equipo de desarrollo cuenta con recursos de alto rendimiento y no sufre de bloqueos ni congelamientos, el proceso fallaba tan rápido que no dejaba rastro. Tras realizar pruebas de compilación detalladas (modo verbose `-v`), aislar el entorno en nuevas carpetas y confirmar que otros proyectos compilaban bien, se identificó una anomalía en el archivo fuente.
* **Solución:** Se detectó que el archivo `main.cpp` había acumulado un volumen anómalo de datos (alcanzando los 26 KB) debido a un error de copiado y pegado durante la integración del código. Esta sobrecarga de texto inválido ahogaba el proceso `cc1plus.exe` del compilador en silencio. La solución aplicada fue realizar una purga del archivo, limpiar el entorno de dependencias creadas por editores externos (como la carpeta `.vscode`) e insertar el bloque de código puro y final (~8 KB). Tras esto, la compilación por terminal nativa se ejecutó de manera exitosa e instantánea.

---

## 3. Evidencia de Ejecución

*(Nota: Reemplaza las rutas entre paréntesis con el nombre de tus imágenes. Ejemplo: `![Menú](imagenes/menu.png)`)*

### 3.1. Menú Principal en Consola
![Captura del menú principal en ejecución](RUTA_DE_TU_IMAGEN_DEL_MENU_AQUI)

### 3.2. Carga de Archivos (.lfp)
![Captura de la carga exitosa de archivos](RUTA_DE_TU_IMAGEN_DE_CARGA_AQUI)

### 3.3. Reportes Generados (HTML)
**Reporte 1: Estadísticas de Cursos**
![Captura del Reporte 1](RUTA_DE_TU_IMAGEN_REPORTE1_AQUI)

**Reporte 3: Top 10 Estudiantes**
![Captura del Reporte 3](RUTA_DE_TU_IMAGEN_REPORTE3_AQUI)

**Reporte 5: Análisis por Carrera**
![Captura del Reporte 5](RUTA_DE_TU_IMAGEN_REPORTE5_AQUI)

---

## 4. Conclusiones Finales
1. **El entorno es tan crítico como el código:** Un entorno de desarrollo local mal configurado o archivos fuente corruptos pueden generar errores fantasmas que la consola no reporta. Mantener la pureza del código y compilar desde terminales nativas (PowerShell / MSYS2) asegura la estabilidad del proyecto.
2. **C++ destaca por su eficiencia bruta:** Al contar con una máquina óptima, el procesamiento de arreglos, cruce de datos mediante funciones iterativas y generación de archivos externos se realiza en fracciones de segundo.
3. **Escalabilidad del Sistema:** La separación de la lógica en funciones independientes para lectura y generación de reportes permite que el sistema sea fácilmente escalable si en el futuro se requiriera agregar nuevos módulos o formatos de exportación (como JSON o CSV).