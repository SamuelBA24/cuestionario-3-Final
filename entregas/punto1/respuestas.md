# Punto 1 — Conclusión

Escribir una conclusión a partir de los diagramas elaborados (BPMN, UML y ArchiMate): qué aporta cada notación, en qué se complementan y qué se decidió o descubrió al modelar InvestigaPB.

> Penalizar si se detecta exceso de uso de IA.

Conclusión
# Conclusiones del modelado de InvestigaPB

Modelamos InvestigaPB con tres notaciones y vimos que ninguna alcanza sola. Juntas sí cubren todo: desde el trámite administrativo hasta la infraestructura de la universidad.

## Aporte de cada notación

### BPMN

Nos sirvió para dibujar el flujo real entre el Investigador, el Director de Grupo y el Comité de Investigación. Con las compuertas exclusivas (XOR) dejamos clara una regla: **ninguna propuesta llega al comité sin el aval del director**. También se ve qué pasa cuando una propuesta se devuelve.

### UML

Con UML pasamos esas reglas a piezas técnicas. Dividimos la solución en:

- Un **Portal Web SPA**
- Una **API REST** con módulos de autenticación, propuestas, avales, evaluación, auditoría y notificaciones
- Una **Base de Datos Relacional**

Así definimos cómo se comunican: JSON/REST, JDBC y SMTP. Con eso, el equipo de desarrollo sabe qué construir.

### ArchiMate

Nos dio la vista general por capas en la Institución Universitaria Pascual Bravo. Une los actores y procesos del negocio con el software de la capa de aplicación, y este con el servidor institucional y el correo de la capa de tecnología.

## Cómo se complementan

Las tres notaciones se complementan porque cada una responde una pregunta distinta:

| Notación | Pregunta que responde | Audiencia |
|----------|----------------------|-----------|
| BPMN | ¿Qué pasa y en qué orden? | Usuarios académicos y administrativos |
| UML | ¿Cómo se construye? | Programadores |
| ArchiMate | ¿Qué componente soporta cada proceso y dónde corre? | Directivos y área de soporte TI |

## Decisiones de arquitectura

Modelar también nos obligó a tomar decisiones:

1. **Motor de estados centralizado.** Lo pusimos en un módulo propio de la API REST, con los estados `BORRADOR`, `EN_AVAL`, `EN_EVALUACION`, `APROBADO` y `RECHAZADO`. Así el frontend no puede saltarse validaciones obligatorias, como el aval del director.
2. **Notificaciones y auditoría desacopladas.** Si el correo institucional falla un rato, la propuesta igual avanza y se guarda en la base de datos.
3. **Alcance delimitado.** Limitamos el sistema hasta la decisión del comité, para no cargarlo con etapas que vienen después.
