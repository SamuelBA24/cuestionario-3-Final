# Caso de estudio: InvestigaPB

Sistema web de la **Institución Universitaria Pascual Bravo** para gestionar **propuestas de proyectos de investigación**.

---

## Contexto

Hoy el trámite va por correo y Excel. **InvestigaPB** digitaliza el flujo hasta la decisión del comité.

---

## Actores

| Actor | Rol |
|-------|-----|
| Investigador | Registrar y enviar la propuesta |
| Director de grupo | Avalar o devolver la propuesta |
| Comité de investigación | Aprobar o rechazar |
| InvestigaPB | Sistema web |
| Correo institucional | Enviar notificaciones (externo) |

---

## Alcance

1. Registrar propuesta.
2. Avalar por el director (obligatorio para llegar al comité).
3. Evaluar en el comité: aprobar o rechazar.

**Fuera de alcance:** ejecución, reportes de avance, cierre, Minciencias, nómina.

---

## Reglas de negocio

- Sin aval del director → la propuesta no llega al comité.
- Estados: `BORRADOR` → `EN_AVAL` → `EN_EVALUACION` → `APROBADO` | `RECHAZADO`.
- Todo cambio de estado relevante dispara notificación por correo.

---

## Orientación técnica

Aplicación web + API + base de datos relacional + correo institucional + servidor de la universidad.

---

## Diagramas a entregar

| Notación | Entregable |
|----------|------------|
| **BPMN** | Modelar el proceso propuesta → aval → decisión del comité. Usar lanes: Investigador, Director, Comité (InvestigaPB opcional). Incluir gateways XOR de aval y de aprobación/rechazo. |
| **UML** | Elaborar **un** diagrama: casos de uso **o** secuencia (envío hasta la decisión) **o** componentes (Web, API, BD, Correo). |
| **ArchiMate** | Elaborar **una** vista layered: servicio de negocio ↔ aplicaciones (portal/API) ↔ tecnología (servidor, BD, correo). |

Subir los archivos a `entregas/diagramas/bpmn/`, `uml/` y `archimate/` con nombres `Equipo_bpmn`, `Equipo_uml`, `Equipo_archimate`.
