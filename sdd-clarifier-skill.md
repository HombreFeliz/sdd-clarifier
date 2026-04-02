---
name: sdd-clarifier
description: >-
  Guia el proceso completo de clarificacion de un proyecto digital antes de
  escribir codigo y genera los artefactos de especificacion en formato compatible
  con OpenSpec. Usar SIEMPRE que el usuario mencione nuevo proyecto, quiero
  construir, tengo una idea, clarificar proyecto, especificar proyecto, generar
  specs, preparar specs, SDD, spec-driven, o cuando pida ayuda para definir un
  producto digital desde cero o desde una idea vaga. Tambien usar cuando el
  usuario quiera generar artefactos de planificacion (PRD, arquitectura, design
  system, modelo de negocio) para un proyecto nuevo o existente. Esta skill cubre
  lo que OpenSpec NO cubre - decisiones de negocio, diseno visual y la fase
  exploratoria previa a la especificacion tecnica.
---

# Skill: SDD Clarifier

## Qué hace esta skill

Transforma una idea vaga o un briefing de proyecto en un conjunto completo de artefactos de especificación, siguiendo un proceso de clarificación progresiva. El output final es compatible con la estructura de OpenSpec pero extendido con capas de negocio y diseño visual.

## Filosofía

Esta skill implementa el principio de "80% planificación, 20% ejecución". La IA no decide por el usuario: pregunta, confronta, propone opciones y espera decisiones. El usuario mantiene el control y la comprensión total del proyecto en todo momento.

La potencia sin control no sirve de nada.

---

## Fases del proceso

El proceso tiene 3 fases secuenciales. No se salta ninguna. El usuario puede avanzar y retroceder libremente.

### FASE 1 — EXPLORACIÓN (conversacional)

Objetivo: extraer del usuario todas las decisiones necesarias para especificar el proyecto. No se genera ningún archivo en esta fase, solo conversación.

#### 1.1 Captura inicial

A partir del briefing del usuario (puede ser una frase, un párrafo, un audio transcrito o un documento), identificar:

- Qué quiere construir (producto/servicio/herramienta)
- Para quién (usuario objetivo)
- Qué problema resuelve
- Por qué ahora (motivación/urgencia)

Si falta información, preguntar. Máximo 3 preguntas por turno. No hacer más de las necesarias.

#### 1.2 Clarificación de negocio

Resolver estas preguntas con el usuario (no todas aplican siempre, usar criterio):

- Modelo de monetización (gratis, freemium, pago único, suscripción, por uso)
- Competidores o referencias conocidas
- Métricas de éxito (qué significa que "funcione")
- Restricciones (presupuesto, tiempo, tecnología impuesta, regulación)
- MVP vs visión completa (qué entra en v1 y qué no)

#### 1.3 Clarificación de diseño

Resolver con el usuario:

- Plataforma(s) objetivo (web, móvil, desktop, PWA)
- Estilo visual de referencia (minimalista, corporativo, lúdico, brutalista, etc.)
- Paleta de colores (si tiene preferencia o marca existente)
- Tipografía (si tiene preferencia)
- Tono de comunicación con el usuario final (formal, casual, técnico, cercano)
- Referencias visuales (webs, apps o diseños que le gusten)

Si el usuario no tiene opinión formada sobre diseño, proponer 2-3 opciones concretas con razonamiento. No dejar campos vacíos por defecto.

#### 1.4 Clarificación técnica

Resolver con el usuario:

- Stack tecnológico (si tiene preferencia o si se debe recomendar)
- Integraciones necesarias (APIs, servicios terceros, auth providers)
- Requisitos de datos (qué se almacena, dónde, esquema inicial)
- Requisitos de despliegue (hosting, dominio, CI/CD)
- Requisitos no funcionales (rendimiento, accesibilidad, i18n, SEO)

#### 1.5 Validación de alcance

Antes de pasar a la Fase 2, presentar al usuario un resumen ejecutivo de todas las decisiones tomadas. Formato: lista de decisiones agrupadas por categoría (negocio, diseño, técnica). Pedir confirmación explícita.

Si el usuario dice "ok" o equivalente, avanzar a Fase 2.
Si el usuario corrige algo, ajustar y volver a validar.

---

### FASE 2 — FORMALIZACIÓN (generación de artefactos)

Objetivo: generar los archivos Markdown del proyecto. Se generan todos de una vez, en una carpeta estructurada.

#### Estructura de salida

```
[nombre-proyecto]/
├── openspec/
│   ├── specs/
│   │   └── [dominio]/
│   │       └── spec.md          ← Specs funcionales (formato OpenSpec)
│   ├── changes/                  ← Vacío (para uso posterior con OpenSpec CLI)
│   └── config.yaml              ← Config básica de OpenSpec
├── docs/
│   ├── prd.md                   ← Product Requirements Document
│   ├── business.md              ← Modelo de negocio y decisiones comerciales
│   ├── design-system.md         ← Sistema de diseño visual
│   ├── architecture.md          ← Arquitectura técnica
│   ├── data-model.md            ← Modelo de datos
│   └── roadmap.md               ← Fases de desarrollo priorizadas
└── CLAUDE.md                    ← Instrucciones para agentes de codificación
```

#### Contenido de cada artefacto

**openspec/specs/[dominio]/spec.md** — Formato OpenSpec estándar:
```markdown
# [dominio] Specification

## Purpose
[Descripción del dominio/capability]

## Requirements

### Requirement: [nombre]
The system SHALL [comportamiento esperado].

#### Scenario: [nombre del escenario]
- GIVEN [precondición]
- WHEN [acción]
- THEN [resultado esperado]
```

Organizar por dominios funcionales (auth, dashboard, payments, etc.). Cada dominio tiene su propio spec.md.

**docs/prd.md** — Documento de requisitos del producto:
- Resumen ejecutivo (2-3 párrafos)
- Problema que resuelve
- Usuario objetivo (con persona si aplica)
- Funcionalidades core (priorizadas con MoSCoW)
- Flujos de usuario principales (descritos narrativamente)
- Requisitos no funcionales
- Fuera de alcance (explícito)

**docs/business.md** — Decisiones de negocio:
- Propuesta de valor (1 frase)
- Modelo de monetización (detallado)
- Competidores y diferenciación
- Métricas de éxito con valores objetivo
- Riesgos identificados y mitigación

**docs/design-system.md** — Sistema de diseño:
- Paleta de colores (con códigos hex, roles: primary, secondary, accent, background, text, error, success)
- Tipografía (fuentes, tamaños, pesos para headings, body, captions)
- Espaciado y grid
- Estilo de componentes (bordes redondeados vs sharp, sombras, densidad)
- Tono visual (descripción en prosa del look & feel)
- Referencias visuales mencionadas por el usuario

**docs/architecture.md** — Arquitectura técnica:
- Stack seleccionado con justificación
- Diagrama de componentes (en Mermaid)
- Estructura de carpetas del proyecto
- Integraciones y dependencias externas
- Estrategia de autenticación
- Estrategia de despliegue

**docs/data-model.md** — Modelo de datos:
- Entidades principales con campos y tipos
- Relaciones entre entidades (en Mermaid si aplica)
- Políticas de acceso (RLS si usa Supabase)
- Datos seed o iniciales si aplica

**docs/roadmap.md** — Fases de desarrollo:
- Fase 1 (MVP): funcionalidades mínimas para validar
- Fase 2: mejoras sobre validación
- Fase 3: escalado
- Cada fase con estimación de esfuerzo relativo

**CLAUDE.md** — Instrucciones para el agente de codificación:
- Resumen del proyecto (3-4 líneas)
- Stack y convenciones de código
- Estructura de carpetas esperada
- Referencia a los docs ("lee docs/prd.md antes de empezar", etc.)
- Reglas de estilo de código
- Qué NO hacer (antipatrones específicos del proyecto)

---

### FASE 3 — ENTREGA Y SIGUIENTE PASO

Una vez generados todos los archivos:

1. Presentar la estructura de carpetas al usuario
2. Ofrecer revisión de cualquier artefacto individual
3. Indicar el siguiente paso: "Ahora puedes inicializar OpenSpec en tu proyecto (`openspec init`) y los specs ya estarán en su sitio. Para nuevas features, usa `/opsx:propose`."

---

## Reglas de generación

- Idioma: el mismo que use el usuario (español por defecto si no se especifica)
- Tono de los artefactos: técnico pero accesible. Sin jerga innecesaria.
- Longitud: cada artefacto debe ser completo pero no redundante. Si algo ya está en el PRD, no repetirlo en architecture.md; referenciarlo.
- Los specs de OpenSpec usan SHALL/MUST/SHOULD según RFC 2119.
- Los diagramas Mermaid deben ser sintácticamente correctos.
- No inventar decisiones. Todo lo que aparezca en los artefactos debe haberse discutido en la Fase 1.
- Si durante la generación se detecta que falta una decisión, pausar y preguntar antes de asumir.

---

## Compatibilidad con OpenSpec

Los artefactos generados en `openspec/specs/` son directamente compatibles con OpenSpec CLI. Después de generar, el usuario puede:

1. Instalar OpenSpec: `npm install -g @fission-ai/openspec@latest`
2. Ejecutar `openspec init` en el directorio del proyecto (si no existe ya)
3. Los specs generados por esta skill se integran directamente como source of truth
4. Para nuevos cambios, usar el flujo estándar de OpenSpec: `/opsx:propose`, `/opsx:apply`, `/opsx:archive`

Los artefactos en `docs/` (business.md, design-system.md, etc.) son extensiones propias que complementan el framework. No interfieren con OpenSpec pero añaden contexto que los agentes de codificación pueden leer via CLAUDE.md.

---

## Ejemplo de uso

**Usuario:** "Quiero hacer una app para que la gente pueda compartir sus colecciones de vinilos"

**Skill (Fase 1):**
- Pregunta por modelo de negocio, usuario objetivo, plataforma
- Pregunta por estilo visual, referencias
- Pregunta por stack preferido, requisitos de datos
- Presenta resumen de decisiones para validar

**Skill (Fase 2):**
- Genera la carpeta completa con todos los artefactos
- Specs organizados por dominio: auth, collections, social, profile

**Skill (Fase 3):**
- Entrega los archivos
- Indica cómo continuar con OpenSpec para la implementación
