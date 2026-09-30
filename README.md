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

**3. Cambia i caratteri** se serve. I font **non** si prendono da Google: stanno in `fonts/`, e i `@font-face` sono in cima allo `<style>`. Per cambiarli, scarica i `.woff2` e sostituisci quei blocchi. Vedi *Perché i font stanno qui* più sotto.

**4. Cancella le sezioni che non servono.** Ognuna è un blocco delimitato da un commento, si toglie intera senza rompere nulla. Ci sono:

hero · fascia richiamo · menu/listino · galleria · chi siamo · recensioni · prodotti · camere/appartamenti · listino a fasce · orari · dove siamo · contatti · informativa privacy

**5. Scrivi i testi.** Il croato sta nell'HTML, le altre lingue nel blocco `5 · TRADUZIONI` in fondo. Ogni testo ha una chiave (`data-i18n="menu.title"`): la cambi in tutti e quattro i posti e sei a posto.

**6. Compila i dati strutturati** nella testa del file — il blocco `application/ld+json`. È quello che fa uscire orari, mappa e recensioni dentro Google, e su un sito locale vale metà del lavoro SEO. Cambia `@type` in `Store`, `LodgingBusiness` o `CafeOrCoffeeShop` secondo il caso.

**7. Metti le foto** in `img/` — i nomi attesi sono elencati in `img/LEGGIMI.txt`.

**8. Compila la parte legale.** Vedi *Prima di pubblicare* più sotto: sono due cose e senza quelle il cliente rischia una multa.

## Hosting e dominio — tutto a nome del cliente

Questa è la regola, e non si deroga: **gli account sono del cliente, io ci vengo aggiunto.** Se sono miei, il suo sito dipende dalla mia carta di credito, dalla mia memoria e dal fatto che io esista ancora fra sette anni. Se sono suoi, non dipende da niente di mio.

### Cloudflare Pages, sull'account del cliente

1. Il cliente apre un account Cloudflare **gratuito** con la sua email
2. Mi invita come membro: *Manage Account → Members*. Sul piano gratuito i membri diventano Administrator, sono illimitati e non costano niente
3. Pubblico il sito su Pages dal suo account
4. Costo: zero, per sempre

Perché Cloudflare e non altro: le richieste ai file statici sono **gratuite e illimitate su ogni piano, free compreso** — è scritto nella loro documentazione, *"Requests to static assets are free and unlimited"*, e non ci sono costi di banda. Non c'è nessun contatore che si svuota e non c'è niente che si mette in pausa a fine mese.

> **Sul piano a pagamento.** Per un sito statico non cambia assolutamente nulla. Workers Paid (5 $/mese) alza i limiti del codice Worker, che qui non esiste; Cloudflare Pro (~20 $/mese per dominio) è un prodotto di sicurezza e prestazioni, non di continuità. Se il cliente vuole spendere per stare tranquillo, quei soldi rendono molto di più come piccolo canone annuale per le modifiche.

### Il dominio

**Un `.hr` non si può registrare su Cloudflare.** Cloudflare Registrar copre poco più di una dozzina di domini nazionali (`.ai .ca .co .io .me .uk .us` e pochi altri) e il croato non c'è. Quindi:

- **`.hr`** → resta presso un registrar croato, intestato al cliente col suo OIB. Su Cloudflare si spostano soltanto i nameserver. Due fornitori invece di uno, ma il dominio è comunque suo
- **`.com` / `.net` / `.org`** → si registrano direttamente dentro Cloudflare, a prezzo di costo e senza ricarico, nello stesso account del sito. Un pannello solo, una scadenza sola

In tutti e due i casi: **rinnovo automatico acceso**, carta del cliente, email del cliente. Il dominio è l'unica cosa che scade davvero, e l'unica che può spegnere il sito.

### GitHub: solo quando serve il pannello

- **Cliente che non modifica da solo** → pubblico con caricamento diretto (trascinando la cartella su Pages, o con `wrangler pages deploy`). Nel mondo del cliente GitHub non esiste proprio. Il repository resta mio, come banco di lavoro, e il sito non ne dipende
- **Cliente che vuole il pannello di modifica** → allora un repository serve, e va aperto sull'account GitHub **del cliente**, con me invitato come collaboratore. Gratis, e non lascia niente intestato a me

## Prima di pubblicare

Due cose senza le quali il cliente rischia una sanzione, e la paga lui, non tu.

**1. I dati obbligatori.** La legge croata vuole che sul sito siano visibili: nome completo dell'obrt o della tvrtka, sede, registro e numero d'iscrizione, OIB, banca e IBAN, e se è in regime di PDV. Per una d.o.o. anche tribunale, capitale sociale e se è versato. Nel template c'è già il posto: la chiave `foot.legal` nel piede. Riempila sul serio, non lasciare gli zeri.

**2. L'informativa sulla privacy.** C'è già, si apre dal piede, ed è in quattro lingue. Va adattata per ogni cliente:

- `priv.p1` — nome, indirizzo, OIB, telefono veri
- `priv.p2` — **dove arrivano davvero i messaggi**. Il template dice che il modulo apre il programma di posta del visitatore. Se per quel cliente usi Formspree, Netlify Forms o WhatsApp, quella riga va riscritta, altrimenti dice una cosa falsa
- Se aggiungi Google Analytics o qualsiasi cosa che traccia, `priv.p4` non è più vera e serve una barra dei cookie vera

## Cosa funziona già

- **Quattro lingue** (HR · EN · DE · IT) con selettore, memoria della scelta e rilevamento della lingua del browser
- **Navigazione** che si raccoglie in pillola allo scroll, menu a tutto schermo su mobile
- **Orari** con il giorno corrente evidenziato da solo
- **Modulo contatti** che apre l'app di posta
- **Foto gradate in CSS** via `--grade`: nessun ritocco esterno, si cambia un numero
- Comparsa allo scroll, `prefers-reduced-motion`, focus da tastiera, meta tag social
- **Nessuna richiesta a terzi all'apertura**, quindi nessuna barra dei cookie da mettere

## Perché il sito non contatta nessuno

Aprendo una pagina di questo template, il browser del visitatore parla solo col server del sito. Zero host esterni, zero cookie. Non è un vezzo: è quello che permette di **non avere la barra dei cookie**, che è la cosa più brutta che si possa mettere sulla prima pagina di un ristorante.

**I font stanno in `fonts/`.** Caricarli da `fonts.gstatic.com` manda l'indirizzo IP di ogni visitatore a Google a ogni pagina aperta, senza che lui possa rifiutare. Se rigeneri i font, **tieni sia `latin` sia `latin-ext`**: è `latin-ext` che porta č, ć, š, ž, đ, e senza quello il croato si rompe.

**La mappa non parte da sola.** Qualunque mappa incorporata contatta un server esterno e gli passa l'IP del visitatore nel momento in cui si carica; quella di Google mette anche un cookie di tracciamento. Qui c'è un pannello con un pulsante, e l'iframe nasce solo se il visitatore lo chiede. Per cambiare mappa basta sostituire il `data-src` su `#mapAsk`.

**L'informativa si apre senza JavaScript**, col selettore `:target`. Funziona anche se qualcosa va storto negli script.

## Cose da non dimenticare

- Sostituire `info@esempio.hr` e `+385 00 000 0000` — compaiono in più punti
- Sostituire il `data-src` della mappa con la posizione vera
- Le recensioni devono essere **vere**, prese da Google o TripAdvisor. Non inventarle
- Le foto devono essere del cliente o licenziate. Le immagini prese da internet le paga lui, non tu
- Il modulo apre l'app di posta del visitatore. Se il cliente vuole riceverle su un server, usa Formspree o Netlify Forms, sostituisci quel pezzo di script **e aggiorna `priv.p2`**

## Aggiungere una lingua

Un blocco nuovo dentro `T` col codice della lingua, e il codice aggiunto a `LANGS`. Il selettore si costruisce da solo.
