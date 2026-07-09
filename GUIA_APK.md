# Entrena en Casa v2.0 — Guía del APK

App de entrenamiento con **138 ejercicios** (111 con fotos reales), rutinas automáticas, nutrición, progreso y logros. Archivo único de ~15 MB (las fotos van dentro).

---

## Opción A — GitHub Actions (recomendada, sin gastar RAM del PC)

1. Crea un repositorio nuevo en GitHub (por ejemplo `entrena-en-casa`).
2. Sube **todo el contenido de esta carpeta** (incluida la carpeta oculta `.github`).
   Desde CMD:
   ```
   cd entrena-en-casa-apk
   git init
   git add .
   git commit -m "Entrena en Casa v2.0 con fotos"
   git branch -M main
   git remote add origin https://github.com/luengof67/entrena-en-casa.git
   git push -u origin main
   ```
3. En el repositorio: **Settings → Secrets and variables → Actions** y añade tus 4 secrets de siempre (los mismos de PLANEA):
   - `KEYSTORE_BASE64`
   - `KEYSTORE_PASSWORD`
   - `KEY_ALIAS`
   - `KEY_PASSWORD`
4. Al hacer push, el workflow arranca solo. Cuando termine (~5-8 min), el APK firmado aparece en **Releases** y también en **Actions → artefactos**.
5. Descarga `entrena-en-casa.apk` al móvil e instala (acepta "orígenes desconocidos" si lo pide).

> Al usar el mismo keystore, si ya tenías la versión anterior instalada, esta se actualiza encima **conservando todos tus datos** (perfil, sesiones, peso, logros...).

## Opción B — Compilar en tu PC con Android Studio

1. En CMD, dentro de esta carpeta:
   ```
   npm install
   npx cap add android
   npx capacitor-assets generate --android
   npx cap sync android
   npx cap open android
   ```
2. En Android Studio, recuerda el ajuste que ya hiciste la otra vez:
   **File → Settings → Build, Execution → Build Tools → Gradle → Gradle JDK = 17**.
3. **Build → Build App Bundle(s) / APK(s) → Build APK(s)** → el APK debug sale en
   `android/app/build/outputs/apk/debug/app-debug.apk`.

## Actualizar la app en el futuro

Cuando cambies el HTML: sustituye `www/index.html`, ejecuta `npx cap sync android` (opción B) o simplemente haz push (opción A). Sube también la versión del `sw.js` (v5 → v6) si publicas la web en GitHub Pages.

## Notas sobre el peso

- El APK rondará los **16-18 MB** por las 222 fotos incrustadas. Normal y esperado.
- Las fotos se cargan bajo demanda: el arranque no las decodifica todas.
- La primera apertura de la pestaña **Ejercicios** puede tardar un instante mientras pinta la cuadrícula; después va fluida.
