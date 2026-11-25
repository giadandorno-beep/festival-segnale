# Schema dati — Segnale

## Scheda dati

1. **Entità:** `Evento` e `Sede`.
2. **Campi delle entità:**
   - **Sede** (`dati/sedi.json`):
     - `id` (`number`): identificativo numerico univoco della sede, es. `1`.
     - `nome` (`string`): denominazione della sede nel festival, es. `"Officina Nord — Sede centrale"`.
     - `indirizzo` (`string`): via, numero civico e città della sede, es. `"Corso Duca degli Abruzzi 24, Torino"`.
   - **Evento** (`dati/eventi.json`):
     - `id` (`number`): identificativo numerico univoco dell’evento, es. `1`.
     - `titolo` (`string`): titolo dell’appuntamento, es. `"Lettere in movimento"`.
     - `data` (`string`): data dell’evento in formato ISO `YYYY-MM-DD`, es. `"2026-06-12"`.
     - `orario` (`string`): ora di inizio in formato `HH:MM`, es. `"10:00"`.
     - `categoria` (`string`): tipologia dell’appuntamento, es. `"Incontro"`.
     - `descrizione` (`string`): testo breve di presentazione dell’evento, es. `"Come cambia un messaggio quando cambiano le lettere? Un incontro su tipografia, ritmo e comunicazione visiva."`.
     - `immagine` (`string`): percorso relativo del file immagine, es. `"assets/lettere-in-movimento.svg"`.
     - `immagine_alt` (`string`): testo alternativo descrittivo per l’immagine, es. `"Lettere geometriche disposte su una griglia"`.
     - `sede_id` (`number`): identificativo della sede in cui si svolge l’evento, es. `1`.
3. **Chiave primaria:** `id` numerico, univoco all’interno della propria entità (`Sede` o `Evento`) e stabile nel tempo.
4. **Relazione:** uno-a-molti (`1:N`): una **Sede** può ospitare più **Eventi**, mentre ogni **Evento** si svolge in una sola **Sede**. Il campo `Evento.sede_id` fa riferimento a `Sede.id`. Nome e indirizzo della sede risiedono esclusivamente in `dati/sedi.json`.
5. **Quantità:** 6 eventi (`dati/eventi.json`) e 3 sedi (`dati/sedi.json`).
6. **Aggiornamento dei dati:** i file in `dati/` vengono modificati direttamente nella repository e resi pubblici tramite commit, push e pubblicazione su GitHub Pages.
7. **Cosa mostra la pagina:** `programma.html` carica `dati/eventi.json` e `dati/sedi.json`, abbina ogni evento alla relativa sede tramite `sede_id` e genera le schede del programma (con immagine, giorno/data, orario, categoria, titolo, descrizione e nome della sede, oppure *«Sede da definire»* se `sede_id` non corrisponde ad alcuna sede).

## Schema Evento–Sede

```mermaid
erDiagram
    SEDE ||--o{ EVENTO : "ospita"
    SEDE {
        number id PK
        string nome
        string indirizzo
    }
    EVENTO {
        number id PK
        string titolo
        string data
        string orario
        string categoria
        string descrizione
        string immagine
        string immagine_alt
        number sede_id FK
    }