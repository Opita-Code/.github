# 🏛️ Opita Code — Reglas de Organización · Organization Rules

> **Vigente desde**: Mayo 2026 · Effective since May 2026
> **Última actualización**: 2026-05-08

---

## 🇨🇴 Principios / 🇺🇸 Principles

1. **Productos privados, infraestructura pública** — El código de producto (apps, lógica de negocio) es privado. Frameworks, runtimes y herramientas reutilizables pueden ser públicos.
2. **Auditar antes de publicar** — Todo repo que pase a público DEBE pasar una auditoría de secretos, credenciales y referencias a productos.
3. **Colombiano-neutral** — Todo el código público usa español colombiano-neutral (tú/usted). CERO voseo. CERO spanglish innecesario.
4. **Conventional commits en español** — `tipo(scope): descripción`. Sin emojis en commits. Sin "Co-Authored-By".
5. **Nunca exponer secretos** — API keys, tokens, contraseñas y `.env` NUNCA se commitean.

---

## 📊 Clasificación de Repos

| Tipo | Visibilidad | Ejemplos | Regla |
|------|-------------|----------|-------|
| **Producto** | 🔒 Privado | opita-os, opita-vibe-studio, opita-sync | NUNCA público |
| **Framework / Runtime** | 🌐 Público | opita-runtime, opita-sync-framework | Auditoría previa requerida |
| **Landing / Web pública** | 🌐 Público | www.opitacode.com | Sin secretos en el repo |
| **Herramienta interna** | 🔒 Privado | opita-scout | NUNCA público |
| **Workspace / Meta** | 🔒 Privado | opitacode-workspace, v0 | NUNCA público |
| **Org profile** | 🌐 Público | .github | Perfil institucional |

---

## 🔐 Proceso para hacer público un repo

1. **Auditoría de secretos**: `rg` o `grep` buscando `api.?key`, `secret`, `token`, `password`, `credential`, `.env`
2. **Auditoría de referencias**: Buscar nombres de productos privados en el código
3. **Revisión de historial**: Asegurar que ningún commit contenga secretos
4. **Aprobación del owner**: El cambio de visibilidad requiere aprobación explícita
5. **Post-publicación**: Verificar que el repo es accesible y no expone nada indebido

---

## 🌐 Reglas para repos públicos

- El README debe estar en **español e inglés** (bilingüe)
- Incluir `LICENSE` (MIT o Apache 2.0)
- Incluir `CONTRIBUTING.md` si se aceptan contribuciones
- Issues y PRs pueden ser en español o inglés
- El código y documentación usan español colombiano-neutral
- No referenciar productos privados en documentación pública

---

## 🔒 Reglas para repos privados

- `AGENTS.md` debe incluir reglas de seguridad y visibilidad
- No exponer rutas o nombres de productos en lugares públicos
- `.env` y archivos de configuración local en `.gitignore`
- Usar SSM Parameter Store o Vault para secretos, nunca en el código

---

## 📝 Convenciones de commits

```
tipo(scope): descripción en español

- feat: nueva funcionalidad
- fix: corrección de bug
- refactor: refactorización sin cambio funcional
- test: solo tests
- docs: solo documentación
- chore: mantenimiento, dependencias, config
- style: formato, linting (sin cambio de lógica)
```

---

## 🏷️ Identidad de marca

- **Nombre**: Opita Code (no "OpitaCode", no "opita code")
- **Tagline**: *Software práctico para negocios reales*
- **Tono**: Claro, cercano, práctico
- **Ubicación**: Neiva, Huila, Colombia 🇨🇴
- **Website**: [opitacode.com](https://www.opitacode.com)
- **Colores**: Negro (#1a1a2e), Blanco (#ffffff), Acento corporativo definido en brand assets
