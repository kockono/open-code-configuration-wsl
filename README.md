# 🧠 OpenCode Agents System — App-Menu

Guía para crear y usar **Agents, Commands y Skills** dentro de OpenCode.
Este documento define cómo estructurar automatizaciones inteligentes para desarrollo.

---

# 🚀 ¿Qué es cada cosa?

## 🤖 Agents

Son inteligencias especializadas que ejecutan una tarea concreta.

Ejemplos:

* commit-agent → crea commits
* code-review-agent → revisa código
* refactor-agent → sugiere mejoras

👉 Piensa en ellos como **roles (senior devs virtuales)**
---
### Modes

mode: **primmary**
  Build es el agente principal predeterminado con todas las herramientas habilitadas. Este es el agente estándar para trabajos de desarrollo en los que necesita acceso completo a las operaciones de archivos y comandos del sistema.
  
mode: **subagent**
  Un agente de uso general para investigar preguntas complejas y ejecutar tareas de varios pasos. Tiene acceso completo a las herramientas (excepto tareas pendientes), por lo que puede realizar cambios en los archivos cuando sea necesario. Utilícelo para ejecutar varias unidades de trabajo en paralelo.
  
mode: **All**
  Permite ser sub y primmary


### Models
model: inherit 
  inherit le dice al subagente que use el mismo modelo que el agente padre (el que está corriendo Claude Code en ese momento), en lugar de forzar uno específico. Así si cambias de modelo en Claude Code, el subagente lo hereda automáticamente sin tocar el archivo.
## ⚙️ Commands

Son instrucciones rápidas que ejecutan un flujo.

Ejemplos:

* `/commit`
* `/review`
* `/refactor`

👉 Son atajos para invocar agentes

---

## 🧩 Skills

Son capacidades reutilizables que los agentes pueden usar.

Ejemplos:

* análisis de código
* detección de patrones
* validación de arquitectura

👉 Son como “superpoderes” internos

---

# 📁 Estructura recomendada

```id="x5q7kz"
.opencode/
│
├── agents/
│   ├── commit-agent.md
│   ├── code-review-agent.md
│
├── commands/
│   ├── commit.md
│   ├── review.md
│
├── skills/
│   ├── analyze-code.md
│   ├── detect-patterns.md
│
└── README.md
```

---

# 🤖 Cómo crear un Agent

Un agent es un archivo `.md` con configuración + instrucciones.

## 📌 Ejemplo

```md id="c7w2bq"
---
description: Smart commit generator
mode: **all**
model: google/gemini-3-flash-preview
temperature: 0.1

permission:
  read: allow
  glob: allow
  grep: allow
  bash: deny
---

# 🧠 Commit Agent

Sos un experto en Git y conventional commits.

Tu tarea:
- analizar cambios
- generar commits limpios
- usar formato estándar del proyecto
```

---

## 🧠 Buenas prácticas

* Un agent = una responsabilidad
* Ser específico (no genérico)
* Definir reglas claras
* Incluir ejemplos

---

# ⚙️ Cómo crear un Command

Un command invoca un agent.

## 📌 Ejemplo `/commit`

```md id="n1nh9o"
Usa el agent: commit-agent

Analizá los cambios actuales y generá commits siguiendo el estándar del proyecto.
```

---

## 📌 Ejemplo `/review`

```md id="6r8q0m"
Usa el agent: code-review-agent

Revisá el código nuevo y validá arquitectura, consistencia y buenas prácticas.
```

---

# 🧩 Cómo crear Skills

Las skills son bloques reutilizables.

## 📌 Ejemplo

```md id="bdcvv2"
# Skill: Analyze Code

- Detecta duplicación
- Identifica malas prácticas
- Sugiere mejoras
```

---

## 🧠 Cuándo usar skills

* lógica repetida entre agentes
* validaciones comunes
* patrones de análisis

---

# 🧠 Cómo usar @ en OpenCode

Puedes invocar agentes directamente con `@`.

---

## 🔥 Ejemplos

### Ejecutar commit agent

```id="tqt7g1"
@commit-agent analiza los cambios y crea commits
```

---

### Ejecutar code review

```id="1d1v6r"
@code-review-agent revisa este archivo
```

---

### Pasar contexto

```id="3qg9vy"
@code-review-agent revisa este diff:

<pegar código aquí>
```

---

## 🧠 Tip importante

Mientras más contexto le des:

* mejores resultados obtienes

---

# 🔄 Flujo recomendado

```id="t1b1ux"
1. Escribir código
2. @code-review-agent
3. Corregir
4. @commit-agent
5. Ejecutar comandos generados
```

---

# ⚠️ Limitaciones de OpenCode

* ❌ No ejecuta bash real
* ❌ No corre git directamente
* ❌ No accede al sistema operativo

👉 Los agentes:

* analizan
* generan comandos
* NO ejecutan

---

# 🚀 Mejores prácticas

* Mantener agents pequeños y enfocados
* Usar nombres claros
* Evitar lógica ambigua
* Documentar reglas del proyecto
* Usar ejemplos reales

---

# 🧠 Filosofía

> "Los agentes no reemplazan al developer, amplifican su criterio"

---

# 🔥 Ejemplo completo

```id="p9y0lc"
@code-review-agent revisa este código

@commit-agent crea commits basados en estos cambios
```

---

# 🚀 Siguientes mejoras

* Integrar commitlint
* Automatizar changelog
* Crear agentes por dominio (auth, api, db)
* Pipeline automático (review → commit)

---

# 🧩 Conclusión

Con este sistema puedes:

* Automatizar tareas repetitivas
* Mantener consistencia
* Mejorar calidad del código
* Escalar tu flujo de desarrollo

---
Reglas por agente
<img width="1402" height="401" alt="image" src="https://github.com/user-attachments/assets/0d75db3f-feff-4c9e-85b4-a8f8d0e31f83" />


## Agentes
### FREE
opencode/mimo-v2-pro-free
opencode/nemotron-3-super-free
opencode/big-pickle


## Dependencias
https://github.com/rtk-ai/rtk