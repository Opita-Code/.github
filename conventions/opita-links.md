# Opita Links — Convención de Uso

> **Estándar del ecosistema Opita Code para URLs externas.**
> Toda URL visible a usuarios finales DEBE usar `go.opitacode.com`.

## Servicio

| Recurso | URL |
|---------|-----|
| **Dominio** | `https://go.opitacode.com` |
| **API** | `https://go.opitacode.com/api/links` |
| **Repo** | `github.com/Opita-Code/opita-links` |

## Cuándo usar Opita Links

### ✅ OBLIGATORIO

| Contexto | Ejemplo |
|----------|---------|
| URLs en correos HTML (SES) | Magic links, trial emails, notificaciones |
| URLs en mensajes de texto/SMS | Cualquier URL enviada por SMS |
| URLs compartidas en redes sociales | Posts, campañas |
| URLs en documentación pública | QR codes, flyers, presentaciones |

### ❌ NO usar

| Contexto | Razón |
|----------|-------|
| Redirects funcionales del frontend | Query params dinámicos se pierden (`?userId=X&redirect=Y`) |
| CORS `allowOrigins` | Configuración técnica, no visible al usuario |
| `og:url`, `canonical`, SEO tags | Los crawlers necesitan la URL canónica real |
| URLs internas entre servicios (API→API) | Latencia innecesaria |

## Tipos de links

### Slugs permanentes (sin TTL)

Para URLs estáticas que nunca cambian. Se crean una vez y se usan directamente:

```bash
# Crear slug permanente
curl -X POST https://go.opitacode.com/api/links \
  -H "Content-Type: application/json" \
  -H "x-api-key: $OPITA_LINKS_API_KEY" \
  -d '{"url": "https://cuenta.opitacode.com/login", "slug": "login"}'
```

**Registry de slugs permanentes:**

| Slug | Destino | Uso |
|------|---------|-----|
| `home` | `https://opitacode.com` | Homepage |
| `login` | `https://cuenta.opitacode.com/login` | Login de cuenta |
| `vibe` | `https://vibe.opitacode.com/app` | Abrir Vibe Studio |
| `checkout` | `https://cuenta.opitacode.com/checkout.html` | Checkout de pagos |

### Links dinámicos (con TTL)

Para URLs únicas por sesión (magic links, tokens temporales):

```typescript
// Inline SDK — copiar en cada Lambda que lo necesite
async function shortenUrl(
  url: string,
  options?: { ttl?: number; meta?: Record<string, string> }
): Promise<string> {
  const baseUrl = process.env.OPITA_LINKS_BASE_URL || "https://go.opitacode.com";
  const apiKey = process.env.OPITA_LINKS_API_KEY;
  if (!apiKey) return url; // graceful fallback
  try {
    const res = await fetch(`${baseUrl}/api/links`, {
      method: "POST",
      headers: { "Content-Type": "application/json", "x-api-key": apiKey },
      body: JSON.stringify({
        url,
        ...(options?.ttl ? { ttl: options.ttl } : {}),
        ...(options?.meta ? { meta: options.meta } : {}),
      }),
    });
    if (!res.ok) { console.error(`[opita-links] ${res.status}`); return url; }
    return ((await res.json()) as any).shortUrl;
  } catch (e: any) { console.error("[opita-links]", e.message); return url; }
}
```

## Reglas de implementación

1. **Siempre fallback**: Si el servicio falla, devolver la URL original. NUNCA romper el flujo del usuario.
2. **TTL = duración del token**: Si el link contiene un JWT de 15 min, el TTL debe ser 900 segundos.
3. **Meta obligatoria**: Todo link dinámico debe incluir `meta.source` para trazabilidad (ej: `"magic-link"`, `"trial-email"`).
4. **Env var**: `OPITA_LINKS_API_KEY` en el `.env` de cada servicio que use links dinámicos.
5. **No publicar npm**: El SDK es un helper inline de ~15 líneas. Copiar, no importar cross-repo.

## Variables de entorno

```bash
# Obligatorio para links dinámicos
OPITA_LINKS_API_KEY=<api-key>

# Opcional (default: https://go.opitacode.com)
OPITA_LINKS_BASE_URL=https://go.opitacode.com
```

## Agregar un nuevo slug permanente

1. Crear el slug via API (o Cloudflare Workers admin panel cuando exista)
2. Agregar la entrada a la tabla de registry en ESTA convención
3. Actualizar los archivos que usan la URL directa
