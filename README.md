![Institución Universitaria Pascual Bravo](https://pascualbravo.edu.co/wp-content/uploads/2023/06/cropped-Imagotipo-horizontal_acreditados.png)

# Cuestionario III — Arquitectura de Software

**Curso:** Arquitectura de Software · 2026-II  
**Institución:** Institución Universitaria Pascual Bravo  
**Modalidad:** Grupal (un fork por equipo)  
**Ponderación:** Punto 1 = **70%** · Punto 2 = **30%**

---

## Integrantes

| # | Nombres | Apellidos |
|---|---------|-----------|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |

---

## Objetivo

Diagramar el caso InvestigaPB con ArchiMate, UML y BPMN; escribir una conclusión a partir de esos diagramas; y responder 6 preguntas de entrevista para arquitecto junior.

---

## Estructura del repositorio

```
cuestionarioiii/
├── README.md
├── docs/
│   ├── 01-definiciones-y-comparacion.md   ← apoyo teórico
│   └── 02-herramientas.md                 ← draw.io y alternativas
├── caso-estudio/
│   └── investiga-pb.md                    ← caso a modelar
├── entrevistas/
│   └── preguntas-arquitecto-junior.md     ← punto 2
├── entregas/
│   ├── punto1/respuestas.md               ← conclusión (punto 1)
│   ├── punto2/respuestas.md               ← respuestas entrevista
│   └── diagramas/
│       ├── bpmn/
│       ├── uml/
│       └── archimate/
```

---

## Paso a paso

### Paso 0 — Fork

1. Hacer fork del repositorio (un integrante) y colaborar en ese fork.
2. Completar la tabla **Integrantes** de este `README.md`.

### Paso 1 — Lectura y herramientas

1. Leer `docs/01-definiciones-y-comparacion.md`.
2. Revisar `docs/02-herramientas.md` (usar **draw.io**).

### Paso 2 — Diagramas y conclusión (punto 1 · 70%)

1. Leer `caso-estudio/investiga-pb.md` (incluye qué diagramar en cada notación).
2. Elaborar y subir **3 diagramas** (uno por notación):

| Notación | Carpeta | Nombre de archivo |
|----------|---------|-------------------|
| BPMN | `entregas/diagramas/bpmn/` | `Equipo_bpmn.png` |
| UML | `entregas/diagramas/uml/` | `Equipo_uml.png` |
| ArchiMate | `entregas/diagramas/archimate/` | `Equipo_archimate.png` |

3. Exportar en PNG o PDF (opcional: `.drawio`, Mermaid o PlantUML).
4. Escribir la **conclusión** en `entregas/punto1/respuestas.md`.

### Paso 3 — Entrevista (punto 2 · 30%)

Resolver las 6 preguntas de `entrevistas/preguntas-arquitecto-junior.md` en `entregas/punto2/respuestas.md`.

### Paso 4 — Entrega

Ejecutar `git add` · `git commit` · `git push` y enviar la URL del fork.

---

## Evaluación

| Bloque | Peso | Entregables |
|--------|------|-------------|
| Punto 1 | **70%** | 3 diagramas + conclusión |
| Punto 2 | **30%** | 6 respuestas de entrevista |

---

## Reglas

- Trabajar en **grupo** (un fork por equipo).
- Diagramar únicamente el caso **InvestigaPB**.
- Completar la tabla de integrantes.
- Plagio = **0**.
- Penalizar la conclusión del punto 1 si se detecta exceso de uso de IA.
