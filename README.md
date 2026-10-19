# Base de datos de tránsito · Caso académico INTRANT

Proyecto académico en SQL Server que modela solicitantes, licencias, permisos, certificaciones, exámenes, empleados e infracciones. Es un ejercicio de diseño y programación T-SQL; no acredita afiliación con INTRANT ni cumplimiento de requisitos legales reales.

## Contenido

- `PROYECTO_FINAL..sql`: definición de esquema, datos de ejemplo, consultas, vistas, triggers, procedimientos y ejemplos de permisos.
- `Diagramas/`: diagramas entidad-relación y relacional en PDF.
- `LICENSE`: licencia del repositorio.

## Elementos presentes en el script

- Claves primarias y relaciones mediante claves foráneas.
- Vistas como `VistaLicencias` y `Vista_solicitantes_licencias`.
- Procedimientos de consulta por edad y categoría e información de solicitantes.
- Triggers para operaciones sobre licencias y permisos.
- Ejemplos de logins, usuarios y asignación de permisos.
- Normalización posterior de puestos de empleados.

## Revisión y ejecución

Requiere SQL Server y un editor compatible con T-SQL. Trabajar exclusivamente en una instancia de pruebas.

El archivo es un guion académico que mezcla creación, datos, demostraciones y modificaciones posteriores. No está validado como una migración ejecutable de principio a fin.

1. Leer el script completo y los diagramas.
2. Separar creación de esquema, datos de prueba, seguridad y demostraciones.
3. Revisar delimitación de lotes con `GO`, especialmente antes de crear vistas, procedimientos y triggers.
4. Revisar las creaciones repetidas de usuarios y reemplazar credenciales de ejemplo.
5. Ejecutar y comprobar cada bloque sobre una base nueva y desechable.
6. No volver a ejecutar indiscriminadamente bloques de creación, inserción o eliminación.

## Mejoras para convertirlo en una muestra de portafolio

- Crear scripts ordenados y reproducibles para esquema, seed y consultas.
- Añadir `NOT NULL`, restricciones de dominio y validaciones de fechas y montos según reglas explícitas.
- Calcular la edad desde la fecha de nacimiento para evitar inconsistencias.
- Revisar que los triggers procesen correctamente operaciones de varias filas.
- Documentar y probar permisos con usuarios de privilegios mínimos.
- Confirmar que los datos publicados sean sintéticos.
- Agregar pruebas de integridad y actualizar los diagramas al esquema final.

## Validación

La documentación se basa en revisión estática del script. No se ejecutó SQL Server ni se comprobaron los PDF o el cumplimiento de reglas del dominio. Las funcionalidades descritas son objetos presentes en el código, no una certificación de funcionamiento.

## Autor

[Jeison Rosario](https://github.com/Jeison-Rosario)
