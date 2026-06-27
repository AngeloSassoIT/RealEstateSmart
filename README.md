# RealEstateSmart — Sito pubblico

Statici HTML per pubblicare Privacy Policy + Pagina di supporto su GitHub Pages.
URL richiesti da App Store Connect quando carichi l'app.

## File inclusi

| File | Scopo | Dove usarlo in App Store Connect |
|---|---|---|
| `index.html` | Landing page (cosa fa l'app + link a Privacy e Support) | (Opzionale) Marketing URL |
| `privacy.html` | Informativa privacy bilingue IT/EN | **Privacy Policy URL** (obbligatorio) |
| `support.html` | FAQ + contatto email | **Support URL** (obbligatorio) |

Tutti i file sono autonomi, senza dipendenze CSS/JS esterne, con dark mode automatico.

## Deploy su GitHub Pages — passo per passo

### 1. Crea il repository

```bash
cd /Users/angelo/Desktop/TodoRES
git init
git add .
git commit -m "Initial site"
```

Su GitHub crea un nuovo repository **pubblico** chiamato per esempio `realestatesmart-site` (deve essere pubblico per Pages gratuito; col piano Pro puoi tenerlo privato).

```bash
git remote add origin https://github.com/<TUO_USERNAME>/realestatesmart-site.git
git branch -M main
git push -u origin main
```

### 2. Abilita GitHub Pages

1. Apri il repo su github.com
2. **Settings → Pages** (sidebar sinistra)
3. **Source**: "Deploy from a branch"
4. **Branch**: `main`, **Folder**: `/ (root)`
5. **Save**

Aspetta 1-2 minuti. GitHub mostrerà l'URL pubblico, tipo:
`https://<TUO_USERNAME>.github.io/realestatesmart-site/`

### 3. Verifica gli URL

Apri nel browser e controlla:

- `https://<TUO_USERNAME>.github.io/realestatesmart-site/` → landing
- `https://<TUO_USERNAME>.github.io/realestatesmart-site/privacy.html` → privacy
- `https://<TUO_USERNAME>.github.io/realestatesmart-site/support.html` → support

Tutti devono restituire **HTTP 200**, niente 404, niente lockscreen.

### 4. Inserisci in App Store Connect

App Store Connect → la tua app → tab **App Information** (sidebar):

| Campo | Valore |
|---|---|
| **Privacy Policy URL** | `https://<USERNAME>.github.io/realestatesmart-site/privacy.html` |
| **Support URL** | `https://<USERNAME>.github.io/realestatesmart-site/support.html` |
| **Marketing URL** (opzionale) | `https://<USERNAME>.github.io/realestatesmart-site/` |

Save in alto a destra.

## Cose da personalizzare prima del deploy

Cerca e sostituisci in tutti i file:

- `angelosassopp93@gmail.com` → email di supporto definitiva (se diversa)
- `privacy@simplebuild.it` → email privacy definitiva (se diversa)
- `simplebuild.it` → eventuale dominio diverso

Le date `23 giugno 2026` / `23 June 2026` nella privacy: aggiornale a ogni revisione sostanziale.

## Aggiornamenti futuri

Quando cambi la privacy policy **dentro l'app** (`Localizable.xcstrings`, sezione `privacy.*`), aggiorna anche `privacy.html` in questo repo per tenerli allineati. App Review controlla che combacino.

Procedura:

```bash
cd /Users/angelo/Desktop/TodoRES
# modifica privacy.html, support.html ecc.
git add .
git commit -m "Update privacy policy: <descrivi cambiamento>"
git push
```

GitHub Pages ridistribuisce automaticamente in pochi secondi.

## (Opzionale) Dominio personalizzato

Se in futuro vuoi usare un dominio tipo `realestatesmart.app`:

1. Aggiungi un file `CNAME` nel repo con il dominio dentro (es. `realestatesmart.app`)
2. Sul registrar del dominio crea un CNAME verso `<USERNAME>.github.io`
3. In Settings → Pages → Custom domain inserisci il dominio
4. Aggiorna gli URL in App Store Connect

## Validazioni utili

Prima di sottomettere all'App Review:

- [ ] Apri `privacy.html` da Safari mobile e verifica che si legga bene su iPhone
- [ ] Apri il link `mailto:` dal browser per controllare che apra l'app di posta
- [ ] Verifica con [W3C HTML Validator](https://validator.w3.org/) che non ci siano errori di markup
- [ ] Se attivi il sito su un dominio custom, controlla che il certificato HTTPS sia attivo (GitHub Pages lo gestisce automatico, ma può richiedere fino a 24h)
