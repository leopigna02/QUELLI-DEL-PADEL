# Quelli del padel

App del campionato individuale di padel: classifica, calendario di 45 giornate, voto MVP, schede dei giocatori con avatar.
La pagina sta su GitHub Pages, i dati (risultati, voti, date, bonus, schede) su Cloud Firestore di Firebase.
Funziona senza abbonamenti: GitHub Pages e il piano gratuito Spark di Firebase bastano.

## File

- `index.html` — l'app (una sola pagina)
- `firebase-config.js` — il collegamento al progetto Firebase: va completato una volta
- `firestore.rules` — le regole dell'archivio: vanno incollate in Firebase
- `icon-180.png`, `icon-512.png`, `manifest.webmanifest` — icona e nome per la schermata Home del telefono

## Messa online (una volta sola)

1. **Firebase**: su console.firebase.google.com crea un progetto (Google Analytics non serve).
   Poi Firestore Database → Crea database → scegli un'area in Europa → modalità di produzione.
2. **Regole**: in Firestore → Regole, sostituisci tutto con il contenuto di `firestore.rules` e pubblica.
3. **Collegamento**: Impostazioni progetto → Le tue app → icona Web `</>` → registra l'app (Firebase Hosting non serve).
   Copia i valori di `firebaseConfig` dentro `firebase-config.js`.
4. **GitHub**: crea un repository pubblico, carica tutti questi file nella cartella principale.
5. **GitHub Pages**: nel repository, Settings → Pages → Branch `main`, cartella `/ (root)` → Save.
   Dopo un paio di minuti l'app è su `https://<tuo-utente>.github.io/<nome-repository>/`.

## Uso

- Ognuno entra scrivendo il proprio nome (è la parola d'ordine). Non protegge nulla: chi ha il link può segnare risultati e voti.
- Su iPhone: apri il link in Safari → Condividi → Aggiungi alla schermata Home.
- Se l'archivio non risponde, l'app mostra la copia dei dati salvata dentro `index.html` e permette di mandare risultati e voti nel gruppo.

## Archivio

Ogni dato è un documento a sé, così più persone salvano insieme senza sovrascriversi:

| Raccolta | Documento | Contenuto |
|---|---|---|
| `league` | `main` | nome, giocatori `p0`…`p5`, regole del punteggio |
| `results` | quattro cifre della partita, es. `0123` | game `a` e `b` |
| `votes` | partita-chi vota, es. `0123-2` | `p`, il giocatore votato |
| `dates` | `g` + giornata, es. `g14` | data `d` |
| `extras` | id libero | giocatore `p`, punti `pts`, motivo `note` |
| `profiles` | `p0`…`p5` | scheda `profile` e `avatar` |

I giocatori sono numerati da 0 a 5 nell'ordine della Lega. Nella partita `0123` la coppia 0+1 gioca contro 2+3.
