# Definiciones, usos y comparación

Material de apoyo para elaborar los diagramas del laboratorio.

---

## 1. ArchiMate

### Definición

**ArchiMate** es un lenguaje de modelado de **arquitectura empresarial** estandarizado por The Open Group. Describe de forma integrada la estructura y el comportamiento de una organización a través de capas (negocio, aplicación, tecnología) y aspectos (activa, comportamiento, pasiva).

### ¿Para qué sirve?

- Alinear estrategia de negocio con sistemas de información e infraestructura.
- Comunicar a stakeholders no técnicos (gerencia, procesos) y técnicos en un mismo lenguaje visual.
- Mostrar **trazabilidad**: un servicio de negocio → aplicaciones que lo soportan → nodos/tecnologías que los hospedan.
- Documentar el *as-is* y el *to-be* de la arquitectura empresarial.

### Capas

ArchiMate organiza el modelo en **capas**. Una capa agrupa elementos del mismo nivel de abstracción:

| Capa | Color típico | Qué representa |
|------|--------------|----------------|
| **Business** | Amarillo | Personas, roles, procesos y servicios de la organización |
| **Application** | Azul | Software que soporta el negocio (sistemas, APIs, interfaces) |
| **Technology** | Verde | Infraestructura donde corre el software (servidores, BD, redes) |

### Conceptos de la capa de negocio

| Concepto | Definición | Símbolo típico |
|----------|------------|----------------|
| **Business Actor** | Entidad concreta (persona, grupo u organización) capaz de realizar comportamiento | Caja con figura de persona |
| **Business Role** | Responsabilidad o papel que un actor puede asumir al participar en un proceso | Rectángulo redondeado |
| **Business Process** | Secuencia de comportamientos de negocio que produce un resultado | Rectángulo redondeado con flecha |
| **Business Service** | Unidad de funcionalidad que el negocio ofrece a su entorno (qué valor se entrega, no cómo se implementa) | Rectángulo con “mordida” superior |
| **Business Object** | Información relevante para el negocio, independiente de la tecnología | Documento / hoja |

### Conceptos de la capa de aplicación

| Concepto | Definición | Símbolo típico |
|----------|------------|----------------|
| **Application Component** | Bloque de software encapsulado y desplegable que realiza parte de la funcionalidad | Rectángulo con icono de componente |
| **Application Service** | Capacidad expuesta por una o más aplicaciones para ser usada por el negocio u otras apps | Servicio con mordida (azul) |
| **Application Interface** | Punto de acceso a un componente o servicio de aplicación (UI, API, canal) | Conector / interfaz |
| **Data Object** | Dato tratado por las aplicaciones | Caja de datos |

### Conceptos de la capa de tecnología

| Concepto | Definición | Símbolo típico |
|----------|------------|----------------|
| **Node** | Recurso computacional sobre el cual se pueden desplegar artefactos y software | Cubo / nodo 3D |
| **Device** | Recurso físico o lógico de hardware | Dispositivo |
| **System Software** | Entorno de ejecución o software de infraestructura (SO, motor de BD, runtime) | Rectángulo |
| **Technology Service** | Capacidad que ofrece la infraestructura a las aplicaciones | Servicio con mordida (verde) |
| **Artifact** | Pieza física de datos o software desplegada en un nodo | Artefacto / archivo |

### Relaciones

Una **relación** conecta elementos y dice *cómo* se vinculan:

| Relación | Definición | Dibujo típico |
|----------|------------|---------------|
| **Composition** | Un elemento es parte inseparable de otro | Rombo negro + línea |
| **Aggregation** | Un elemento agrupa a otros, sin ownership fuerte | Rombo blanco + línea |
| **Assignment** | Asigna responsabilidad o despliegue (quién hace / dónde corre) | Línea con punto |
| **Realization** | Un elemento implementa o concreta otro más abstracto | Flecha punteada + triángulo vacío |
| **Serving** | Un elemento ofrece su funcionalidad a otro (lo “sirve”) | Flecha hacia quien recibe |
| **Access** | Un elemento de comportamiento lee o escribe un objeto de datos | Línea punteada |
| **Triggering** | Un elemento dispara el inicio de otro | Flecha sólida |
| **Flow** | Transferencia de información o valor entre elementos | Flecha (a menudo punteada) |

**Trazabilidad típica entre capas:** Business Service ← Realization — Application Component ← Assignment — Node / System Software.

---

## 2. UML (Unified Modeling Language)

### Definición

**UML** es un lenguaje visual estandarizado (OMG) para especificar, visualizar y documentar artefactos de sistemas de **software**. No es un proceso de desarrollo: es una notación.

### ¿Para qué sirve?

- Modelar estructura (clases, componentes, despliegue) y comportamiento (casos de uso, secuencia, actividad, estados).
- Facilitar el diseño detallado entre desarrolladores, analistas y arquitectos de software.
- Servir de contrato de diseño antes o durante la implementación.

### Diagramas más usados en arquitectura junior

| Diagrama | Pregunta que responde |
|----------|----------------------|
| Casos de uso | ¿Qué hace el sistema para quién? |
| Secuencia | ¿Cómo colaboran objetos/servicios en el tiempo? |
| Componentes | ¿Cuáles son los bloques desplegables y sus interfaces? |
| Despliegue | ¿Dónde corre cada cosa? |
| Clases | ¿Cuál es el modelo de dominio / estructura estática? |

> En este laboratorio no repasar los símbolos UML (asumir conocidos).

---

## 3. BPMN (Business Process Model and Notation)

### Definición

**BPMN** es una notación estándar (OMG) para modelar **procesos de negocio** de extremo a extremo: actividades, eventos, puertas de decisión (gateways), flujos y participantes (lanes/pools).

### ¿Para qué sirve?

- Documentar y mejorar flujos operativos.
- Alinear negocio y TI sobre el “cómo se trabaja” antes de automatizar.
- Servir de base para automatización (motores BPM) o para requisitos funcionales claros.
- Detectar cuellos de botella, excepciones y responsabilidades por rol.

### Conceptos BPMN

#### Evento (*Event*)

Un **evento** es algo que **ocurre** durante el proceso: lo inicia, lo interrumpe o lo termina. No es un trabajo que alguien “hace”; es un hecho.

| Tipo | Definición | Símbolo |
|------|------------|---------|
| **Start Event** | Punto donde comienza una instancia del proceso | ○ círculo línea delgada |
| **Intermediate Event** | Ocurre entre el inicio y el fin (espera, mensaje, temporizador, etc.) | ◎ círculo doble |
| **End Event** | Punto donde termina el recorrido del proceso | ⬤ círculo línea gruesa |

Si el evento es de **mensaje**, lleva un **sobre** dentro del círculo (llegó o se envió un mensaje).

#### Actividad (*Activity*)

Una **actividad** es una unidad de **trabajo** realizada en el proceso (por una persona o por un sistema).

| Tipo | Definición | Símbolo |
|------|------------|---------|
| **Task** | Actividad atómica: no se descompone más en el diagrama | ▢ rectángulo muy redondeado |
| **User Task** | Tarea ejecutada por un humano con ayuda de una aplicación | ▢ + icono de persona |
| **Service Task** | Tarea ejecutada automáticamente por un servicio/sistema | ▢ + engranaje |

#### Gateway (*Gateway*)

Un **gateway** controla **cómo se bifurcan o se unen** los caminos del flujo.

| Tipo | Definición | Símbolo |
|------|------------|---------|
| **Exclusive (XOR)** | Se elige **un solo** camino según una condición | ◆ con **X** (o vacío) |
| **Parallel (AND)** | Se activan **todos** los caminos a la vez (y luego suelen reunirse) | ◆ con **+** |
| **Inclusive (OR)** | Se activan **uno o varios** caminos según condiciones | ◆ con **O** |

#### Pool y Lane

| Concepto | Definición | Símbolo |
|----------|------------|---------|
| **Pool** | Contenedor que representa un **participante** completo del proceso (organización, área o sistema) | Rectángulo grande con título |
| **Lane** | Subdivisión dentro de un pool que asigna actividades a un **rol** o unidad responsable | Franja dentro del pool |

#### Flujos y artefactos de información

| Concepto | Definición | Símbolo |
|----------|------------|---------|
| **Sequence Flow** | Orden en que se ejecutan los elementos **dentro del mismo pool** | → línea sólida |
| **Message Flow** | Intercambio de mensajes **entre pools distintos** | ⇢ línea punteada |
| **Data Object** | Dato o documento que el proceso usa o produce | Documento doblado |
| **Text Annotation** | Nota explicativa; no altera el flujo | Corchete + texto |

---

## 4. Comparación

| Criterio | ArchiMate | UML | BPMN |
|----------|-----------|-----|------|
| **Enfoque** | Arquitectura empresarial (negocio + apps + tech) | Diseño de software | Procesos de negocio |
| **Audiencia principal** | Arquitectos empresariales, gerencia + TI | Desarrolladores, arquitectos de software | Analistas de negocio, operaciones, TI |
| **Nivel de abstracción** | Alto / transversal | Medio a detallado | Medio (flujo operativo) |
| **Fortaleza** | Trazabilidad entre capas | Precisión del diseño de software | Claridad del proceso end-to-end |
| **Debilidad** | Menos detalle de código/objetos | No modela bien toda la empresa | No describe arquitectura de sistemas |
| **Estándar** | The Open Group | OMG | OMG |
| **Complemento típico** | TOGAF / EA | Casos de uso + C4 + patrones | Historias de usuario / RPA / BPMS |

### Relación entre las tres

```
BPMN  →  “¿Cómo fluye el trabajo del negocio?”
UML   →  “¿Cómo se diseña e implementa el software que lo soporta?”
ArchiMate → “¿Cómo encaja ese software en la arquitectura de la empresa?”
```

No se sustituyen: cada una responde una pregunta distinta.
