
# 📸 01 - Obiettivi e Requisiti del Progetto

Ciao. Questo documento riassume gli obiettivi strategici, la struttura dei contenuti e i requisiti di sistema concordati per l'ecosistema web **Carusoarw**. L'obiettivo è coniugare un'interfaccia pubblica ad alto impatto emotivo con un sistema di gestione dei contenuti snello ed efficiente.

---

## 🎯 1. Visione d'Insieme & Obiettivi

L'applicazione web deve posizionarsi come un portfolio digitale di livello Premium. I pilastri fondamentali del progetto sono:
*   **Impatto Visivo:** Valorizzare la fotografia d'autore attraverso layout e transizioni fluide.
*   **Autonomia Totale:** Permettere al fotografo di gestire l'intero archivio pubblico (categorie, eventi e immagini) in totale indipendenza.
*   **Flessibilità Architetturale:** Strutturare il database in modo che l'aggiunta di nuove categorie o generi fotografici non richieda modifiche al codice sorgente.

---

## 👥 2. Esperienza Utente (Lato Pubblico)

L'utente esterno che visita il sito disporrà di una navigazione pulita incentrata su tre macro-aree: **Portfolio**, **About Me**, **Contact Me**.

### A. Il Flusso di Navigazione del Portfolio (Struttura a 3 Livelli)
Per evitare il sovraccarico visivo, l'esplorazione dei lavori segue un percorso logico:

1.  **Livello 1 - Selezione Macro-Categoria:** 
    L'utente atterra sulla sezione Portfolio e sceglie il genere fotografico di interesse tramite filtri o menu dedicati (es. *Weddings*, *Events*, *Concerts*, ecc.).
2.  **Livello 2 - Indice dei Soggetti / Racconti:** 
    Una volta cliccata la categoria, il sito mostra un'anteprima (copertina + titolo) dei singoli progetti o soggetti specifici legati a quel genere (es. *Matrimonio di Marco & Sofia*, *Concerto Rock 2026*).
3.  **Livello 3 - Galleria Fotografica d'Autore:** 
    Selezionando il singolo soggetto, l'utente accede alla galleria finale, dove può scorrere l'intero reportage fotografico (utilizzando il layout a scorrimento orizzontale/verticale dinamico).

### B. Sezioni di Supporto
*   **About Me:** Spazio editoriale dedicato alla biografia del fotografo, alla sua filosofia di scatto, alle pubblicazioni e alle informazioni professionali.
*   **Contact Me:** Un modulo di contatto minimale che permette ai potenziali clienti di inviare una richiesta direttamente alla mail del fotografo, integrando sistemi di protezione dallo spam.

---

## 🛠️ 3. Gestione Contenuti (Lato Admin / Fotografo)

Il pannello di amministrazione privato (Backoffice) deve essere strutturato per essere intuitivo anche per utenti non tecnici. Il fotografo deve poter eseguire le seguenti operazioni:

*   **Gestione Categorie:** Aggiungere, rinominare o eliminare le macro-categorie (es. creare una nuova categoria *Fashion* o *Sport*) senza rompere il layout del sito.
*   **Gestione Soggetti (Post/Eventi):** Creare un nuovo "Soggetto" (es. *Matrimonio di Giulia & Andrea*), associarlo a una macro-categoria esistente e impostare un'immagine di copertina.
*   **Caricamento Multiplo (Bulk Upload):** Trascinare e caricare in blocco decine di immagini all'interno di un soggetto per popolare istantaneamente la galleria finale.
*   **Ordinamento Visivo:** Poter riordinare la sequenza delle foto all'interno della galleria per decidere il ritmo del racconto visivo.

---

## 🔒 4. Vincoli e Requisiti Non Funzionali (Tecnici)

Per garantire prestazioni elevate, il sito dovrà rispettare i seguenti standard:
1.  **Ottimizzazione Immagini Automatica:** Il sistema deve comprimere e convertire le foto caricate dall'admin nei moderni formati web (WebP/AVIF) in tempo reale, per garantire caricamenti istantanei.
2.  **Protezione Diritto d'Autore:** Blocco nativo del click destro e del trascinamento delle immagini (drag-and-drop) per rendere più difficile il furto dei file protetti da copyright.
3.  **Architettura Serverless:** Sfruttare un Headless CMS (come Sanity.io o Strapi) unito a un hosting statico (Vercel) per azzerare i costi fissi mensili del server e garantire la massima sicurezza informatica.

---


## 🔒 5. Sistema di Consegna e Selezione Privata (Area Clienti)

Oltre al portfolio pubblico, la piattaforma deve integrare un portale privato e sicuro per la collaborazione diretta tra il fotografo e i suoi clienti commerciali/privati.

### A. Accesso Protetto e Cloud Isolation
*   **Link Univoci Temporanei:** Il fotografo non creerà account con password per i clienti (operazione frustrante per l'utente). Genererà dall'admin un link cifrato unico (es. `/condivisi/wedding-marco-sofia-2026`).
*   **Storage Dedicato:** Le immagini private risiederanno in un Bucket privato su e.g. **Cloudflare R2**, isolate dal resto del sito pubblico per garantire la massima protezione dei dati sensibili e della privacy.

### B. Strumenti di Culling & Feedback (Valutazione e Tagging)
L'interfaccia dell'area privata deve permettere al cliente di "lavorare" sulle foto consegnate per finalizzare il servizio:

1.  **Sistema di Votazione (Rating a Stelle):**
    Ogni immagine disporrà di un selettore rapido a stelle (da 1 a 5) per definire la priorità di post-produzione e stampa:
    *   **5 Stelle ($max$):** Stato *“Eccellente / Selezione per Stampa e Album”*.
    *   **4 Stelle:** Stato *“Approvata / Ottima”*.
2.  **Sistema di Tagging Dinamico:**
    Il cliente deve poter associare alle foto dei tag predefiniti dal fotografo o personalizzati (es. *#Social*, *#DaRitoccare*, *#Famiglia*, *#BiancoENero*) per raggruppare i file secondo le proprie esigenze.
3.  **Sincronizzazione in Tempo Reale:**
    Ogni voto o tag assegnato dal cliente deve essere salvato istantaneamente nel database di backend, notificando lo stato al fotografo senza bisogno di esportazioni manuali o invio di file di testo esterni.

### C. Dashboard di Riepilogo lato Fotografo (Admin)
Nel pannello di controllo, il fotografo deve poter monitorare le scelte del cliente tramite filtri avanzati:
*   Filtrare l'intero servizio privato per mostrare solo i file a 5 stelle per procedere all'impaginazione del fotolibro.
*   Visualizzare i tag inseriti dal cliente per capire quali foto necessitano di ulteriore ritocco o modifiche specifiche.