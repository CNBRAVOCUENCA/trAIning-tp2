# TrAIning · Tablero de trabajo (TP Tema 2 · ASI 2026)

Repositorio y tablero del **Trabajo Práctico Tema 2: Diseño de la Estructura Operativa, Procesos y Marcos de Trabajo** (Administración de Sistemas de Información, UTN FRSR, 2026).

**Startup:** TrAIning, Agentes de IA con *Document Grounding* para PyMEs.
**Integrantes:** Bravo, Carolina · Buttini, Cristóbal · Cardozo, Leandro Roque · López Laszuk, Juan Pablo · Peñalbé, Hernán · Piastrellini, Mariano · Sosa, Ricardo Alberto.

## Qué hay acá

| Elemento | Dónde |
| --- | --- |
| Backlog de escalado: 10 historias de usuario con INVEST y criterios Gherkin, 1 tarjeta Expedite y 1 de deuda técnica | [Issues](../../issues) |
| Tablero Kanban/Scrum con columnas, límites de WIP y carriles por clase de servicio | Pestaña [Projects](../../projects) del repositorio |
| Políticas explícitas (DoR, DoD, WIP, clases de servicio) | Este README |

## Épicas

| Épica | Etiqueta | Historias |
| --- | --- | --- |
| E1 · Plataforma multi-cliente segura y gobernanza de datos | `E1 Seguridad multi-cliente` | HU-01, HU-02, HU-03 |
| E2 · Motor de grounding escalable con control de alucinaciones | `E2 Motor de grounding` | HU-04, HU-05, HU-06, HU-07 |
| E3 · Autogestión del cliente y operación comercial escalable | `E3 Autogestion y operacion` | HU-08, HU-09, HU-10 |

## Políticas del tablero

### Columnas

Backlog → Refinamiento → Ready (DoR) → En progreso → Code Review → QA / Testing → Staging → Done (DoD)

### Límites de WIP (Ley de Little)

| Columna | Límite |
| --- | --- |
| Refinamiento | 6 |
| Ready (DoR) | mínimo 4 (order point) · máximo 10 |
| En progreso | 3 |
| Code Review | 2 |
| QA / Testing | 2 |
| Staging | 2 |

Cálculo: throughput ≈ 1 historia por día hábil × cycle time objetivo ≈ 6 días → 6 a 9 ítems en curso, repartidos entre las columnas activas. La tarjeta **Expedite** no suma al WIP.

### Clases de servicio

| Clase | Etiqueta | Qué entra | Política |
| --- | --- | --- | --- |
| Expedite | `Expedite` | Incidentes SEV1: caída de producción, fuga de datos | Máximo 1 a la vez; ignora el WIP; *swarming*; rollback primero; postmortem en 48 h |
| Fixed Date | `Fixed Date` | Vencimientos legales o contractuales | Se inicia con margen: fecha límite menos 2 × cycle time p85 |
| Standard | `Standard` | Historias del backlog priorizadas por WSJF | FIFO dentro del orden por WSJF (~60–65 % de la capacidad) |
| Intangible | `Intangible` | Deuda técnica, refactorización | 20 % de la capacidad reservada en cada sprint |

### Definition of Ready (DoR)

Una historia entra a **Ready** solo si:

1. Está escrita como *Como [persona], quiero [capacidad], para [beneficio]*.
2. Cumple **INVEST**; si supera 8 story points, se divide.
3. Tiene al menos **2 escenarios Gherkin** (camino feliz y caso de error o borde).
4. Está vinculada a una **épica** y a la métrica de outcome o KR que mueve.
5. Si tiene interfaz, los **mockups** fueron validados con un cliente piloto.
6. Las **dependencias** con otros equipos están resueltas o tienen contrato de API acordado.
7. Si toca datos personales o documentos del cliente, el **DPO** revisó el impacto.
8. Si toca el motor de IA, hay casos agregados al **golden set**.
9. Está **estimada** y tiene **clase de servicio** asignada.

### Definition of Done (DoD)

Una historia está **Done** solo si:

1. Todos los escenarios Gherkin están **automatizados y pasan**.
2. Tests unitarios con TDD y **cobertura ≥ 80 %** del código nuevo o modificado.
3. **Análisis estático** sin vulnerabilidades críticas ni altas, sin secretos expuestos ni dependencias con CVE críticos.
4. **Revisión de código** aprobada por al menos un par (dos si toca autenticación, aislamiento entre clientes o facturación).
5. **Tests de contrato** en verde si modifica una API.
6. Si afecta al agente: **tasa de alucinación < 2 %** en el golden set.
7. **Documentación** actualizada (OpenAPI, runbook, notas de versión).
8. **Métricas y alertas** instrumentadas.
9. **Desplegado en producción** por el pipeline y verificado con telemetría.
10. El PO **aceptó** la historia.
