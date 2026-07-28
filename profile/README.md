# Opita Code

> **Software práctico para negocios reales.** Construido desde Colombia con identidad local y ambición global.
>
> **Practical software for real businesses.** Built from Colombia with local identity and global ambition.

---

## El kernel: dark-memory-mcp + Vibe-Flow

Toda la organización gira en torno a **un par de productos canónicos**: **dark-memory-mcp** (el servidor MCP que entrega governance + memory + research + vibe-flow como un set unificado de 34+ herramientas) y **Vibe-Flow** (la modalidad de desarrollo: *spec → artifact → drift → reconcile → publish*, con cada cambio versionado en OpenSpec y cada artefacto auditado por un juez LLM antes de publicarse).

El resto de la organización son **productos verticales** que demuestran ese kernel, o **SDKs** que lo extienden. No construimos software sin pasar por el kernel.

### Estado actual del kernel (2026-07-28)

| Componente | Repositorio | Estado |
|---|---|---|
| **Kernel MCP canónico** | [`dark-memory-mcp`](https://github.com/Opita-Code/dark-memory-mcp) | **Activo** — v2.2.0. 34 herramientas canónicas + 3 opcionales L7-REDTEAM. Schema v18. Policy Gateway + Agent Memory data plane. |
| **Backend OSINT + jueces LLM** | [`dark-research-mcp`](https://github.com/Opita-Code/dark-research-mcp) | **Consolidándose** — v0.7.2 (2026-07-28 README-restoration). v0.7.0 introdujo 38 deprecation shims que delegan al namespace `RESEARCH` de dark-memory-mcp. Los backends OSINT y los jueces LLM viven aquí todavía; la superficie canónica vive en dark-memory-mcp. |
| **Runtime privado** | `opita-os` (privado) | SSOT, OpenSpec, Brand Engine, vault cifrado, SSO. Sostiene a todos los productos verticales. |
| **SDK streaming IA** | [`ocais`](https://github.com/Opita-Code/ocais) | **Activo** — `@opitacode/ocais` v3.0.1 (publicado en npm). SDK de streaming para AWS Lambda, consumido por vibe-studio y sociedad-opita-app. |

```mermaid
graph TD
    OS["opita-os (privado)<br/>OpenSpec · Brand Engine · Vault · SSO"]
    DM["dark-memory-mcp<br/>34+ herramientas canónicas<br/>(RESEARCH · JUDGE · VIBE · AGENT_MEMORY)"]
    DR["dark-research-mcp<br/>13 OSINT backends<br/>(shims hacia dark-memory-mcp)"]
    SDK["@opitacode/ocais<br/>Streaming SDK para AWS Lambda"]
    VS["opita-vibe-studio<br/>IDE de vibe-coding en español"]
    SO["sociedad-opita-app<br/>Monumento digital del opita"]
    DEV["opita-developer-web<br/>Portfolio del Opita Developer"]
    WEB["www.opitacode.com<br/>Landing corporativa"]
    MK["opita-market (privado)<br/>Marketplace colombiano B2B+B2C"]

    OS -.runtime + specs.-> DM
    DR -.deprecation shims v0.7.0+ consolidate into.-> DM
    DM -.consume kernel.-> VS
    DM -.consume kernel.-> MK
    DM -.consume kernel.-> SO
    SDK -.streamText.-> VS
    SDK -.streamText.-> SO
    VS -.embed.-> WEB
    MK -.serve.-> WEB
    SO -.serve.-> WEB
    DEV -.stand-alone.-> WEB
```

---

## Productos verticales (consumen el kernel)

Cada producto demuestra una faceta distinta del kernel. Ninguno se construye fuera de la metodología vibe-flow.

| Producto | Repositorio | Demo en vivo | Qué demuestra del kernel |
|----------|-------------|--------------|---------------------------|
| **Vibe Studio** | [`opita-vibe-studio`](https://github.com/Opita-Code/opita-vibe-studio) | [vibe.opitacode.com](https://vibe.opitacode.com) | IDE de vibe-coding **en español** para estudiantes y creadores. Browser + desktop (Tauri v2). Consume el kernel MCP para governar cada generación. |
| **Opita Market** | `opita-market` *(privado)* | [market.opitacode.com](https://market.opitacode.com) | Marketplace multi-vertical colombiano (B2B + B2C). Dashboard de precios en tiempo real, directorio y comparador. Compliance Ley 1581/2012 (Habeas Data) desde el día 1 — el primer producto donde vibe-flow gates un MVP regulado. *(Repo privado desde 2026-07-28.)* |
| **Sociedad Opita** | [`sociedad-opita-app`](https://github.com/Opita-Code/sociedad-opita-app) | [sociedad.opitacode.com](https://sociedad.opitacode.com) | **Monumento digital vivo** del opita (Tello, Huila). Preservación del dialecto con 41 perfiles psicométricos validados (Big Five, Lomnitz, Dunbar) y diálogos en streaming con `@opitacode/ocais`. Astro + SST, monolito `web/` + `api/`. |
| **Developer Web** | [`opita-developer-web`](https://github.com/Opita-Code/opita-developer-web) | [developer.opitacode.com](https://developer.opitacode.com) | Portfolio y sitio de identidad del *Opita Developer*. Estética cyberpunk/gamer, terminal interactiva, diagramas de arquitectura en vivo. Construido con vibe-flow como vitrina del kernel. |
| **Web pública** | [`www.opitacode.com`](https://github.com/Opita-Code/www.opitacode.com) | [opitacode.com](https://www.opitacode.com) | Superficie pública corporativa. |

---

## Repositorios archivados

Repos congelados como referencia histórica. La lógica que contenían migró al runtime privado (`opita-os`) o a otro repo. No los usamos activamente.

### Públicos (código público congelado, referencia histórica)

| Repositorio | Qué contenía | Reemplazo |
|---|---|---|
| [`opita-runtime`](https://github.com/Opita-Code/opita-runtime) | Motor de ejecución gobernada. SDD workflow, provider chain, encrypted vault AES-256-GCM, plugin ecosystem con trust classes y risk tiers. | `opita-os` (privado) |
| [`opita-sync-framework`](https://github.com/Opita-Code/opita-sync-framework) | Opita Sync Framework (OSF) — kernel reusable de gobernanza: contracts, policy, runtime, evidence y operator surfaces. Opcional PostgreSQL (persistencia) y Cerbos (PDP). | `opita-os` (privado) |

### Privados (workspace / scratch interno)

| Repositorio | Qué contenía |
|---|---|
| `dev.opitacode.com` | Dev environment del landing corporativo; consolidado en `www.opitacode.com`. |
| `opitacode-workspace` | Workspace contenedor de proyectos experimentales. |
| `v0` | Bootstrap inicial del org (antes de Opita-Code ser opita-code.com). |

---

## Cómo producimos cada producto

```
   spec  →  artifact  →  drift  →  reconcile  →  publish
    │          │            │          │            │
 OpenSpec   log/upload   judge   spec ↔ artifact   has_disclosure=true
                                                    │
                                          judge.eval_type:
                                          compliance_check
                                          pii_detect
                                          prompt_injection_scan
```

### Gobernanza de IA

- **dark-memory-mcp es nuestro sistema nervioso.** Cada agente que escribe código — sea para OpenSpec, Vibe Studio, o cualquier producto vertical — tiene acceso al mismo set de herramientas MCP via el namespace `RESEARCH` (OSINT), `JUDGE` (LLM-as-judge), `VIBE` (CRUD de ciclo), o `AGENT_MEMORY` (state cross-session). No duplicamos lógica entre repos.
- **Vibe-Flow es nuestra modalidad de desarrollo.** Escribimos la *spec* (en OpenSpec) **antes** de generar una sola línea. Cada artefacto se *loggea* con `dark_memory_vibe_artifact_log`. Un juez LLM (`dark_memory_judge(eval_type=drift_judge)`) compara artefacto contra spec y emite verdict (`aligned | drift_detected | needs_human`). Sin `reconciled_at`, no hay publish.
- **LLM-as-judge, no LLM-as-author.** Publicamos artefactos críticos (synthetic media, contenido EU, código generado) solo después de que un juez LLM los audite contra specs, jurisdicciones y compliance. Cada verdict queda persistido en `judgment_history` para auditoría.
- **dark-research-mcp está en consolidación hacia dark-memory-mcp.** Los nombres legacy (`dark_research_*`, `dark_ssd_*`) emiten `X-Deprecation` headers y siguen funcionando como shims; los nombres canónicos ahora viven en el namespace `dark_memory_*`.

---

## Conectá con nosotros

| Canal | Enlace |
|-------|--------|
| **Sitio Web** | [opitacode.com](https://www.opitacode.com) |
| **Founder** | [Nicolás Urrutia](https://www.linkedin.com/in/nicourrutia98/) |
| **Sede** | Neiva, Huila, Colombia 🇨🇴 |
| **WhatsApp** | [wa.me/573126126085](https://wa.me/573126126085) |

---

<p align="center">
  <br>
  © 2026 Opita Code · Juan Nicolás Urrutia Salcedo
  <br>
  <i>Hecho con orgullo colombiano 🇨🇴 · Made in Colombia</i>
  <br>
  <sub>Última revisión del README: 2026-07-28 (audit hygiene pass + URL canonicalization de sociedad.opitacode.com y developer.opitacode.com)</sub>
</p>
