# Punto 1 — Conclusión

Escribir una conclusión a partir de los diagramas elaborados (BPMN, UML y ArchiMate): qué aporta cada notación, en qué se complementan y qué se decidió o descubrió al modelar InvestigaPB.

> Penalizar si se detecta exceso de uso de IA.

Conclusión:

Modelamos InvestigaPB con tres notaciones y vimos que ninguna alcanza sola. Juntas sí cubren todo: desde el trámite administrativo hasta la infraestructura de la universidad.

BPMN nos sirvió para dibujar el flujo real entre el Investigador, el Director de Grupo y el Comité de Investigación. Con las compuertas exclusivas (XOR) dejamos clara una regla: ninguna propuesta llega al comité sin el aval del director. También se ve qué pasa cuando una propuesta se devuelve.

Con UML pasamos esas reglas a piezas técnicas. Dividimos la solución en un Portal Web SPA, una API REST con módulos (autenticación, propuestas, avales, evaluación, auditoría y notificaciones) y una Base de Datos Relacional. Así definimos cómo se comunican: JSON/REST, JDBC y SMTP. Con eso, el equipo de desarrollo sabe qué construir.

ArchiMate nos dio la vista general por capas en la Institución Universitaria Pascual Bravo. Une los actores y procesos del negocio con el software de la capa de aplicación, y este con el servidor institucional y el correo de la capa de tecnología.

Las tres notaciones se complementan porque cada una responde una pregunta distinta. BPMN dice qué pasa y en qué orden, y por eso los usuarios académicos y administrativos pueden validar el trámite. UML dice cómo se construye, y le sirve a los programadores. ArchiMate muestra qué componente soporta cada proceso y dónde corre, y ayuda a hablar con los directivos y con el área de soporte TI.

Modelar también nos obligó a tomar decisiones. Pusimos el motor de estados (BORRADOR, EN_AVAL, EN_EVALUACION, APROBADO y RECHAZADO) en un módulo propio de la API REST. Así el frontend no puede saltarse validaciones obligatorias, como el aval del director. Además, separamos las notificaciones y la auditoría del resto. Si el correo institucional falla un rato, la propuesta igual avanza y se guarda en la base de datos. Por último, limitamos el alcance hasta la decisión del comité, para no cargar el sistema con etapas que vienen después.
