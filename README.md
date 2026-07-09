# AR viewer stile Artivive — image tracking

Il 3D appare **ancorato sopra l'immagine-opera** e la segue (modo B).
Tutto statico: nessun backend. Solo tu carichi/modifichi i contenuti; gli utenti aprono un link e guardano.

## File

```
ar-app/
├─ index.html      → il VIEWER (il link che aprono gli utenti dal telefono)
├─ editor.html     → strumento TUO per sistemare i modelli e generare il manifest
├─ manifest.json   → il "database": collega ogni immagine al suo modello 3D
├─ targets.mind    → le tue immagini-opera compilate (lo generi tu, vedi sotto)
└─ models/         → i file .glb
```

## Procedura completa (la fai tu, una volta)

### 1. Prepara i materiali
Per ogni opera: una **foto nitida e dettagliata dell'immagine** da inquadrare + il suo **modello `.glb`**.
Le immagini devono essere "ricche" (dettaglio, contrasto, poco simmetriche): un quadro va benissimo, un logo semplice su fondo bianco no.

### 2. Compila le immagini in `targets.mind`
Vai su **https://hiukim.github.io/mind-ar-js-doc/tools/compile**
- trascina le foto **in ordine** (la 1ª = target 0, la 2ª = target 1, …),
- premi *Start*, scarica il file e rinominalo `targets.mind`,
- mettilo in questa cartella.

L'ordine qui è l'`indice target` che userai nell'editor e nel manifest.

### 3. Sistema i modelli e crea il manifest (`editor.html`)
Apri `editor.html`, e per ogni opera:
- imposta l'**indice target** (0, 1, 2…) uguale all'ordine del punto 2,
- trascina il `.glb`, regola scala / altezza / rotazione / luci sopra il marker,
- premi **Aggiungi al manifest**.

Alla fine premi **Scarica manifest.json** e mettilo in questa cartella.
Metti i `.glb` nella cartella `models/` con gli stessi percorsi che hai scritto.

### 4. Pubblica online (in HTTPS)
Carica l'intera cartella `ar-app/` su un hosting statico in **HTTPS** (obbligatorio per la fotocamera).
Opzioni gratuite: GitHub Pages, Netlify, Cloudflare Pages.

### 5. Uso da parte dell'utente
L'utente apre il link di `index.html` sul telefono → tocca **Avvia fotocamera** → inquadra l'opera → vede il 3D.
Puoi mettere quel link dentro un QR "generico" (uno qualsiasi generatore di QR da URL) da stampare accanto all'opera.

## Provarlo subito (demo)
Se apri `index.html` **senza** `targets.mind`/`manifest.json` validi, parte una **demo integrata**:
stampa o mostra questa immagine e inquadrala →
https://hiukim.github.io/mind-ar-js-doc/samples/assets/card.png

## Note tecniche
- Librerie da CDN: A-Frame 1.5.0 + MindAR 1.2.5 (image tracking).
- Test in locale: la fotocamera richiede HTTPS, quindi `index.html` va provato da telefono **sull'hosting**, non con doppio clic sul file. `editor.html` invece funziona in locale col doppio clic.
- 15 immagini in un solo `targets.mind` è fattibile; se sui telefoni lenti il riconoscimento rallenta, dividi in più file `.mind` (es. 3 da 5) con una schermata di scelta.
