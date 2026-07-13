# Opita Code

> 🇨🇴 **Software práctico para negocios reales.** Construido desde Colombia con identidad local y ambición global.
>
> 🇺🇸 **Practical software for real businesses.** Built from Colombia with local identity and global ambition.

---

## 🏗️ Ecosistema / Ecosystem

Construimos software gobernado por especificación (Spec-Driven Development) y persiguiendo un único criterio: que las máquinas ejecuten nuestra visión, no al revés. Todo nuestro código sigue estándares de arquitectura limpia y se construye sobre nuestro sistema central **OpenSpec** (`opita-os`, privado).

| Capa / Layer | Repositorio | Descripción / Description | Stack |
|--------------|-------------|---------------------------|-------|
| 🏛️ **Núcleo** | **[`opita-os`](https://github.com/Opita-Code/opita-os)** 🔒 | *(Privado)* El "sistema operativo" de la organización. Contiene la fuente de la verdad (**OpenSpec**), el motor de marca (**Brand Engine**), SSO y Facturación. | Node.js, SVGO, Sharp |
| 🔧 **Infra pública** | **[`dark-research-mcp`](https://github.com/Opita-Code/dark-research-mcp)** | Servidor MCP que entrega a un agente IA 45 herramientas especializadas: OSINT (15), vibe-flow CRUD (22) y dark-ssd LLM-as-judge (8). Binario Go único sobre stdio. SQLite-backed `dark.db` compartido con `dark-eval`. | Go 1.22+ |
| 🔧 **Infra pública** | **[`ocais`](https://github.com/Opita-Code/ocais)** | **OCAIS — Opita Code AI Stream.** SDK de streaming de IA para AWS Lambda. ~15 KB, zero deps, TypeScript-first. SSE first-class, AbortSignal + timeout, structured output (Zod), tool execution multi-step. | TypeScript, AWS Lambda |
| 🎨 **SaaS** | **[`opita-vibe-studio`](https://github.com/Opita-Code/opita-vibe-studio)** ([vibe.opitacode.com](https://vibe.opitacode.com)) | Vibe-coding **en español** para estudiantes y creadores. IDE con IA en navegador + desktop (Tauri v2). React 18, SST v4, multi-provider (DeepSeek + Gemini + OpenAI + Anthropic), BYOK. | Tauri v2, React, TypeScript |
| 🌐 **Apps verticales** | **[`opita-market`](https://github.com/Opita-Code/opita-market)** ([market.opitacode.com](https://market.opitacode.com)) | Marketplace multi-vertical colombiano. Dashboard de precios en tiempo real + directorio + comparador. B2B + B2C. Compliance Ley 1581/2012 (Habeas Data) desde el día 1. | Astro 6, SST Router, Aurora Postgres, DynamoDB |
| 🌐 **Apps verticales** | **[`sociedad-opita-app`](https://github.com/Opita-Code/sociedad-opita-app)** | **Monumento digital vivo** del opita (Tello, Huila). Preservación del dialecto con 41 perfiles psicométricos validados (Big Five, Lomnitz, Dunbar) y 10 diálogos en streaming con `@opita/ocais`. | Astro 6 + React 19 islands, SST v3, Hono 4 |
| 🌐 **Apps verticales** | **[`opita-developer-web`](https://github.com/Opita-Code/opita-developer-web)** | Portfolio y sitio de identidad de marca del *Opita Developer*. Astro con estética *cyberpunk/gamer* orientado a product architects y desarrolladores. Terminal interactiva + diagramas de arquitectura en vivo. | Astro, React, Framer Motion |
| 📚 **Web pública** | **[`www.opitacode.com`](https://github.com/Opita-Code/www.opitacode.com)** ([opitacode.com](https://www.opitacode.com)) | Superficie pública corporativa. Astro v2 (en migración) + frontend HTML plano legado + AWS SAM (contact form) + Supabase. Magic Link auth compartido con `vibe-ai-backend`. | Astro, HTML/CSS, AWS SAM, Supabase |

### 📦 Archivado — reemplazados por `opita-os` / Archived — superseded by `opita-os`

Repos congelados como referencia histórica. La lógica que contenían migró al núcleo privado.

| Repositorio | Estado | Descripción / Description | Stack |
|-------------|--------|---------------------------|-------|
| **[`opita-runtime`](https://github.com/Opita-Code/opita-runtime)** | 🔒 archive | Motor de ejecución gobernada. SDD workflow, provider chain, encrypted vault AES-256-GCM, plugin ecosystem con trust classes y risk tiers. 15+ stores. Rewrite in Rust (WIP, en `rust-runtime/`). Reemplazado por `opita-os`. | Node.js ESM, Rust (WIP) |
| **[`opita-sync-framework`](https://github.com/Opita-Code/opita-sync-framework)** | 🔒 archive | **Opita Sync Framework (OSF)** — kernel reusable de gobernanza: contracts, policy, runtime, evidence y operator surfaces. Opcional PostgreSQL (persistencia) y Cerbos (PDP). Reemplazado por `opita-os`. | Go 1.24+ |

---

## 🚀 Metodología y Gobernanza / Methodology & Governance

Trabajamos bajo los más estrictos estándares de ingeniería para la era de la IA, asegurando que las máquinas sigan nuestra visión, y no al revés.

### 🇨🇴 Gobernanza de IA
- **Spec-Driven Development (SDD):** Escribimos las especificaciones (*Specs* en OpenSpec) **antes** de generar cualquier línea de código. Cada cambio importante vive como un *change* versionado en `openspec/changes/`.
- **Agentes Contextuales:** Usamos registros centralizados de *skills* (Engram) y herramientas MCP (`dark-research-mcp`) para que la IA actúe bajo los estándares estrictos de nuestro workspace.
- **LLM-as-judge:** Antes de publicar artefactos críticos (videos sintéticos, contenido EU, generación de código), un juez LLM audita contra specs, jurisdicciones y compliance. Cada verdict queda persistido para auditoría.

### 🇺🇸 AI Governance
- **Spec-Driven Development (SDD):** We write technical specifications (*OpenSpecs*) before any code is generated. Every meaningful change lives as a versioned `openspec/changes/` artifact.
- **Contextual Agents:** We use centralized *skills* registries (Engram) and MCP tooling (`dark-research-mcp`) so AI acts strictly under our workspace standards.
- **LLM-as-judge:** Before publishing critical artifacts (synthetic video, EU-jurisdiction content, generated code), an LLM judge audits against specs, jurisdictions, and compliance. Every verdict is persisted for audit.

---

## 🌎 Conectá con nosotros / Connect with us

| Canal / Channel | Enlace / Link |
|-----------------|---------------|
| 🌐 **Sitio Web** | [opitacode.com](https://www.opitacode.com) |
| 🧑‍💻 **Founder** | [Nicolás Urrutia](https://www.linkedin.com/in/nicourrutia98/) |
| 📍 **Sede** | Neiva, Huila, Colombia |
| 💬 **WhatsApp** | [wa.me/573126126085](https://wa.me/573126126085) |

---

<p align="center">
  <br>
  © 2026 Opita Code · Juan Nicolás Urrutia Salcedo
  <br>
  <i>Hecho con orgullo colombiano 🇨🇴 · Made in Colombia</i>
</p>
