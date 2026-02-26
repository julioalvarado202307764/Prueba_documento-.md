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
