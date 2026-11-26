# Cómo publicar meriden.com.ar

El sitio es HTML estático y se publica gratis con **GitHub Pages**. El dominio se maneja desde **Cloudflare** (DNS gratis), que además permite configurar después los correos `@meriden.com.ar`.

Recorrido: **NIC Argentina** (dueño del dominio) → **Cloudflare** (DNS) → **GitHub Pages** (aloja el sitio).

---

## 1. Activar GitHub Pages

1. En GitHub, entrá al repositorio `meriden-web` → **Settings** → **Pages**.
2. En **Source** elegí **Deploy from a branch**, rama `main`, carpeta `/ (root)` → **Save**.
3. En **Custom domain** escribí `meriden.com.ar` → **Save**. (El archivo `CNAME` del repositorio ya lo tiene cargado.)
4. Por ahora va a decir que el DNS no está configurado. Es normal; se resuelve en el paso 3.

## 2. Crear la cuenta de Cloudflare y agregar el dominio

1. Creá una cuenta gratis en https://dash.cloudflare.com/sign-up
2. **Add a domain** → `meriden.com.ar` → plan **Free**.
3. Cloudflare te muestra **dos servidores de nombres** (nameservers), algo como `xxx.ns.cloudflare.com` y `yyy.ns.cloudflare.com`. Anotalos.

## 3. Delegar el dominio en NIC Argentina

1. Entrá a https://nic.ar con tu clave fiscal (Trámites a Distancia / Mi Nic).
2. Andá a **Dominios** → `meriden.com.ar` → **Delegaciones** (o "Administrar delegaciones").
3. Borrá las delegaciones que haya y cargá los dos nameservers de Cloudflare (solo el nombre del host, sin IP).
4. Confirmá. NIC suele aplicar el cambio en pocas horas, aunque puede tardar hasta 24–48 h.
5. Cloudflare te avisa por mail cuando el dominio queda **Active**.

## 4. Apuntar el dominio a GitHub Pages (en Cloudflare)

En Cloudflare → `meriden.com.ar` → **DNS** → **Records**, cargá estos registros:

| Tipo  | Nombre | Contenido                        | Proxy           |
|-------|--------|----------------------------------|-----------------|
| A     | `@`    | `185.199.108.153`                | DNS only (gris) |
| A     | `@`    | `185.199.109.153`                | DNS only (gris) |
| A     | `@`    | `185.199.110.153`                | DNS only (gris) |
| A     | `@`    | `185.199.111.153`                | DNS only (gris) |
| CNAME | `www`  | `segundoperezalisedo.github.io`  | DNS only (gris) |

> Dejá la nubecita en **gris (DNS only)** al principio, así GitHub puede emitir el certificado HTTPS. Si el repositorio queda en otra cuenta u organización de GitHub, cambiá `segundoperezalisedo` por ese nombre.

## 5. Activar HTTPS

1. Volvé a GitHub → **Settings** → **Pages**. Cuando el chequeo de DNS dé OK, tildá **Enforce HTTPS** (puede tardar hasta una hora en habilitarse).
2. Probá https://meriden.com.ar y https://www.meriden.com.ar

## 6. (Después) Correos @meriden.com.ar

Con Google Workspace o Zoho Mail: el proveedor te da registros **MX** y **TXT** (SPF, DKIM) que se cargan en la misma pantalla de DNS de Cloudflare. No afectan al sitio web.

---

## Cómo actualizar el sitio

Cualquier cambio que se suba a la rama `main` se publica solo en 1–2 minutos.

- **Logo:** reemplazá los archivos de `assets/img/` manteniendo los mismos nombres (si cambia el logo, rehacer también `compartir.png`, la imagen que aparece al compartir el link, y `apple-touch-icon.png`):
  `logo.svg` (positivo, header), `logo-negativo.svg` (footer), `simbolo.svg` (favicon), `simbolo-negativo.svg` (marca de agua del inicio).
- **Textos:** están en `index.html`.
- **Colores y tipografías:** al principio de `assets/css/styles.css`.
- **Datos de contacto:** sección `CONTACTO` de `index.html` (mail, WhatsApp, Instagram).
