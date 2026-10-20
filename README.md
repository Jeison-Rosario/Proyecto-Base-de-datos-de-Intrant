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

## Mapa del modelo

| Área | Tablas incluidas |
| --- | --- |
| Solicitantes | `SOLICITANTES`, `SOLICITANTES_CONTACTO` |
| Solicitudes y evaluaciones | `Pagos_SOLICITUDES_LICENCIAS`, `EXAMENES`, `CARNETS_APRENDIZAJE` |
| Documentos | `LICENCIAS`, `PERMISOS`, `CERTIFICACIONES`, `DOCUMENTO_EMITIDO` |
| Organización | `EMPLEADOS`, `CONTACTO_EMPLEADO`, `DIVISIONES`, `PUESTOS_EMPLEADOS` |
| Infracciones | `INFRACCION`, relacionada con LICENCIAS |

`SOLICITANTES` utiliza `cedulaID` como clave. Las tablas de contacto, solicitudes y documentos relacionan su titular con esa entidad. El bloque final normaliza los puestos de empleados; no representa una migración independiente lista para producción.

## Objetos programables

| Objeto | Función demostrada |
| --- | --- |
| `VistaLicencias` | Consulta de licencias |
| `Vista_Categoria_3` | Vista enfocada en una categoría |
| `Vista_solicitantes_licencias` | Combinación de solicitantes y licencias |
| `ObtenerLicenciasPorEdad` | Filtro por intervalo de edad |
| `ObtenerLicenciasPorEdadYCategoria` | Añade filtro opcional de categoría |
| `ObtenerInformacionSolicitanteSimple` | Parámetros de salida con conteo e información |
| `ObtenerInformacionSolicitanteCompleta` | Amplía los resultados de salida |

El script contiene el trigger `Aviso` sobre inserciones, un aviso al eliminar licencias y otro para operaciones de permisos. También incluye instrucciones para desactivar algunos triggers: su presencia en el archivo no garantiza que queden activos al terminar de ejecutarlo.

## Consultas de inspección

Solo después de preparar y comprobar los objetos en una base de pruebas:

```sql
USE INTRANT;
GO
SELECT name, type_desc
FROM sys.objects
WHERE is_ms_shipped = 0
ORDER BY type_desc, name;

SELECT TOP (10) * FROM dbo.SOLICITANTES;
SELECT TOP (10) * FROM dbo.LICENCIAS;

EXEC dbo.ObtenerLicenciasPorEdad
    @EdadMinima = 25, @EdadMaxima = 35;
```

Estas consultas no sustituyen la instalación: fallarán si no existen las tablas o el procedimiento correspondiente. El script mezcla definición, datos y ejemplos; separar los bloques antes de automatizarlo.

## Revisión recomendada antes de ejecutarlo

Comprobar sintaxis y separación de lotes, datos de ejemplo, restricciones y permisos. Hay creación repetida del usuario `digitador` y comandos de seguridad a nivel de servidor; no son necesarios para explorar únicamente las tablas en un laboratorio ya configurado. No reproducir credenciales del guion en un entorno compartido.

La edad está almacenada junto a la fecha de nacimiento y puede desactualizarse. El trigger de inserción debe revisarse con lotes de varias filas y con todos los atributos del solicitante. Los mensajes `PRINT` no constituyen un registro persistente de auditoría.

## Diagramas y validación manual

Los PDF originales están en `Diagramas/`: `Diagrama Relacional INTRANT BD.pdf` e `INTRANT BD diagrama E-R.pdf`. Compararlos con el esquema después de aplicar los bloques finales; no se ha verificado su correspondencia visual en esta revisión.

Para validar: preparar una base desechable, comprobar PK/FK, ejecutar consultas por edad y categoría y probar operaciones de varias filas dentro de transacciones de laboratorio. Registrar los resultados antes de afirmar que el guion completo es reproducible. Esta ampliación solo documenta objetos observados; no ejecuta SQL Server ni convierte el guion en migraciones.

## Autor

[Jeison Rosario](https://github.com/Jeison-Rosario)
