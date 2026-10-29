# Landing de servicios de infraestructura IT

Sitio estático generado con **Hugo** (binario único) y el tema
[Up Business](https://github.com/writeonlycode/hugo-up-business), desplegado en
**GitHub Pages**.

- Producción: https://juancarbone.github.io/infra-services-landing/
- Repositorio: https://github.com/juancarbone/infra-services-landing

## Requisitos

| Herramienta | Versión | Nota |
| --- | --- | --- |
| Hugo extended | 0.169.0 | Debe ser *extended* (el tema usa Tailwind vía Hugo) |
| Node.js | 22 (ver `.nvmrc`) | Solo para compilar Tailwind en build; no se publica |

Node 22 es necesario porque Hugo usa `module.registerHooks` al invocar Tailwind.
Si usás `nvm`: `nvm use` (toma `.nvmrc`).

## Uso local

```bash
npm ci
nvm use            # Node 22
hugo server -D     # http://localhost:1313/infra-services-landing/
```

Build de producción:

```bash
npm run build      # equivale a hugo --gc --minify -> public/
```

## Dónde se edita cada cosa

- `data/home/*.yaml`: bloques de la home (hero, marcas, portfolio, servicios,
  testimonios, CTA). Cada bloque tiene `enable: true|false` para mostrarlo u
  ocultarlo.
- `assets/images/`: imágenes de los bloques (se optimizan a WebP en build).
- `hugo.toml`: título, descripción, contacto, ubicación, menús y `baseURL`.
- `content/_index.md`: metadatos de la home.
- `layouts/`: solo dos overrides locales del tema:
  - `baseof.html`: corrige `lang` a `es-ES`.
  - `_partials/shared/footer.html`: traduce los títulos del footer.

El tema está versionado como submódulo en `themes/hugo-up-business` (commit
`33d421f`). Para actualizarlo:

```bash
git submodule update --remote themes/hugo-up-business
```

## Deploy

Cada push a `main` dispara `.github/workflows/hugo.yml`, que instala Hugo +
Node 22, ejecuta `npm ci`, compila y publica en GitHub Pages. No hay pasos
manuales.

## Pendiente (contenido y marca)

El contenido actual es el de demostración del tema (Lorem ipsum, marcas de
ejemplo y datos de contacto ficticios). Falta reemplazar:

- Nombre/marca, logo (`assets/images/logo.png`) e imágenes propias.
- Textos de hero, servicios, casos y testimonios (`data/home/`).
- Email, teléfono y ubicación reales (`hugo.toml`).
- Favicon y metadatos SEO.
