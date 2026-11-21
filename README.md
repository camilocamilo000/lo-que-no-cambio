# LO QUE NO CAMBIÓ

Experiencia de realidad aumentada creada con Zence Inverse Reality.

**Modo:** World Effects (anclaje al suelo con SLAM)
**Hosting:** Cloudflare Pages
**En vivo:** la asigna Cloudflare Pages al conectar el repositorio

---

## Cómo se publica

En Cloudflare: **Workers & Pages → Create → Pages → Connect to Git**, elige este
repositorio y despliega. `wrangler.toml` declara el directorio de salida, pero el
comando de compilación no cabe en ese archivo, así que ese sí hay que escribirlo:

| Ajuste | Valor | De dónde sale |
| --- | --- | --- |
| Framework preset | None | — |
| Build command | `npm run build` | **hay que escribirlo** |
| Build output directory | `dist` | `wrangler.toml` |
| Project name | `lo-que-no-cambio` | `wrangler.toml` |
| Node | 22 | `.node-version` |

El nombre del proyecto **tiene que ser exactamente** `lo-que-no-cambio`: con otro,
el build falla. Se puede cambiar, pero entonces hay que cambiarlo también en
`wrangler.toml`.

Hecho eso, **cada `push` a `main` vuelve a desplegar**: editar y guardar desde Zence Inverse Reality
crea un commit, y el commit actualiza la experiencia.

## Cómo editarlo

**Desde el navegador**, con Zence Inverse Reality: abre el editor, conecta tu cuenta de GitHub y elige
este repositorio.

**En tu ordenador**, con el 8th Wall Studio de escritorio: este es el formato oficial
de proyecto, así que se abre sin conversiones.

**A mano**, si prefieres:

```bash
npm install
npm run serve     # servidor de desarrollo
npm run build     # compila en dist/
```

## Publicarlo en otro sitio

`dist/` es un sitio estático corriente. Sirve tal cual en Netlify, GitHub Pages o
cualquier hosting; la configuración de Vercel y de Cloudflare ya viene en el
repositorio, así que cambiar de una a otra es conectar el repositorio y nada más. Solo
dos requisitos:

- **HTTPS**, porque la cámara exige contexto seguro.
- No bloquear `cdn.jsdelivr.net`, de donde se carga el motor.

## Estructura

```
src/.expanse.json       la escena: objetos, materiales, luces, componentes
src/index.html          página de entrada; carga el motor
src/*.ts                componentes propios
src/inre-marcadores.ts  carga los marcadores en el motor; lo genera Zence Inverse Reality
src/assets/             modelos, texturas, vídeo, audio
image-targets/          marcadores de imagen
config/                 configuración de webpack (MIT, de 8th Wall)
vercel.json             despliegue en Vercel
wrangler.toml           despliegue en Cloudflare Pages
.node-version           versión de Node con la que se compila
```

## Licencias

El código de este proyecto es tuyo. El motor que usa, no:

- `@8thwall/ecs` 3.2.1 — MIT, © Niantic Spatial, Inc.
- `@8thwall/engine-binary` 1.0.0 — **XR Engine License Agreement**
- `@8thwall/landing-page` 1.0.0 — MIT

La XR Engine License prohíbe cobrar por un producto cuyo valor derive sustancialmente
de la funcionalidad del motor. Ver [NOTICE](./NOTICE).
