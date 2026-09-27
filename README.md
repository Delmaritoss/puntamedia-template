# Template Puntamedia

Punto di partenza per i siti clienti. Un file solo, nessuna build, quattro lingue già funzionanti.

L'idea è arrivare al 60% prima ancora di scrivere una riga: parti da qui, cambi sei colori, cancelli le sezioni che non servono, riempi i testi.

## Come si fa un sito nuovo

**1. Copia la cartella** e rinominala col nome del cliente.

**2. Cambia i colori.** In cima a `index.html`, blocco `2 · CONFIGURAZIONE`. Sono sei valori:

| | |
|---|---|
| `--ink` | fondo scuro |
| `--ink-2` | fondo scuro alternativo |
| `--surface` | schede |
| `--text` | testo |
| `--muted` | testo secondario |
| `--acc` | **il colore del brand** — bottoni, dettagli, prezzi |

Gli altri sotto sono derivati: di solito non serve toccarli. Le sezioni chiare hanno il loro blocco `.light` subito sotto.

**3. Cambia i caratteri** se serve: il link a Google Fonts nella testa, più `--serif` e `--sans`.

**4. Cancella le sezioni che non servono.** Ognuna è un blocco delimitato da un commento, si toglie intera senza rompere nulla. Ci sono:

hero · fascia richiamo · menu/listino · galleria · chi siamo · recensioni · prodotti · camere/appartamenti · listino a fasce · orari · dove siamo · contatti

**5. Scrivi i testi.** Il croato sta nell'HTML, le altre lingue nel blocco `5 · TRADUZIONI` in fondo. Ogni testo ha una chiave (`data-i18n="menu.title"`): la cambi in tutti e quattro i posti e sei a posto.

**6. Compila i dati strutturati** nella testa del file — il blocco `application/ld+json`. È quello che fa uscire orari, mappa e recensioni dentro Google, e su un sito locale vale metà del lavoro SEO. Cambia `@type` in `Store`, `LodgingBusiness` o `CafeOrCoffeeShop` secondo il caso.

**7. Metti le foto** in `img/` — i nomi attesi sono elencati in `img/LEGGIMI.txt`.

## Cosa funziona già

- **Quattro lingue** (HR · EN · DE · IT) con selettore, memoria della scelta e rilevamento della lingua del browser
- **Navigazione** che si raccoglie in pillola allo scroll, menu a tutto schermo su mobile
- **Orari** con il giorno corrente evidenziato da solo
- **Modulo contatti** che apre l'app di posta
- **Foto gradate in CSS** via `--grade`: nessun ritocco esterno, si cambia un numero
- Comparsa allo scroll, `prefers-reduced-motion`, focus da tastiera, meta tag social

## Cose da non dimenticare

- Sostituire `info@esempio.hr` e `+385 00 000 0000` — compaiono in più punti
- Sostituire l'`iframe` della mappa con quello vero (Google Maps → Condividi → Incorpora)
- Le recensioni devono essere **vere**, prese da Google o TripAdvisor. Non inventarle.
- Il modulo apre l'app di posta del visitatore. Se il cliente vuole riceverle su un server, usa Formspree o Netlify Forms e sostituisci quel pezzo di script.

## Aggiungere una lingua

Un blocco nuovo dentro `T` col codice della lingua, e il codice aggiunto a `LANGS`. Il selettore si costruisce da solo.
