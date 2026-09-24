# Biblioteca Francesc v9 · PWA + OneDrive

Aquesta versió separa **aplicació** i **dades**.

## Què resol
- L'app s'instal·la com a PWA des d'una URL HTTPS fixa.
- Les actualitzacions es publiquen a la mateixa URL; l'app mostra “Nova versió disponible” i s'actualitza sense tocar les dades.
- Les dades es guarden sempre localment per funcionar offline.
- Opcionalment, cada canvi es sincronitza a `biblioteca.json` dins la carpeta privada de l'app a OneDrive.
- Si dos dispositius canvien dades alhora, la versió més nova guanya i l'altra es guarda com a fitxer de conflicte a OneDrive.

## 1. Publicar una sola vegada
Publica **tots els fitxers d'aquesta carpeta** en un hosting estàtic HTTPS (GitHub Pages, Netlify, Cloudflare Pages, etc.).
La URL ha de quedar estable. Exemple: `https://usuari.github.io/biblioteca-francesc/`

## 2. Configurar Microsoft OneDrive una sola vegada
1. Entra a Microsoft Entra > App registrations > New registration.
2. Nom: `Biblioteca Francesc`.
3. Tipus de comptes: permet comptes personals Microsoft si el teu OneDrive és personal.
4. A Authentication, afegeix plataforma **Single-page application (SPA)**.
5. Com a Redirect URI posa EXACTAMENT la URL que l'app mostra a `Més > OneDrive`.
6. A API permissions, Microsoft Graph > Delegated permissions, afegeix `Files.ReadWrite.AppFolder`.
7. Copia `Application (client) ID`.
8. A l'app: `Més > OneDrive`, enganxa el Client ID i prem “Connectar amb Microsoft”.

No cal cap client secret.

## Actualitzacions futures (v10, v11...)
Substitueix els fitxers del hosting pels de la nova versió mantenint la mateixa URL.
El `service worker` detectarà la nova versió i l'app oferirà **Actualitzar ara**.
Les dades no formen part del codi de l'app: continuen a OneDrive + còpia local.

## Fitxers
- `index.html`: aplicació
- `manifest.webmanifest`: instal·lació PWA
- `sw.js`: offline i actualitzacions
- `version.json`: detecció de versió
- `icon-192.png`, `icon-512.png`: icones
