<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/5.5.1/github-markdown.min.css">
<style>
    body {
        box-sizing: border-box;
        min-width: 200px;
        max-width: 980px;
        margin: 0 auto;
        padding: 45px;
    }
    @media (max-width: 767px) {
        .markdown-body { padding: 15px; }
    }
</style>
<div class="markdown-body">
# 🗺️ 02 - Attori e Casi d'Uso

Questo documento mappa gli utenti che interagiscono con il sistema (Attori) e le azioni specifiche che possono compiere (Casi d'Uso), con un focus particolare sul flusso di selezione delle foto nell'area privata.

---

## 👥 1. Identificazione degli Attori

Nel sistema operano tre attori principali:
* **Visitatore Pubblico:** Utente esterno (potenziale cliente) che naviga sul sito per visionare il portfolio pubblico o contattare il fotografo.
* **Cliente Privato:** Cliente commerciale o sposi che hanno ricevuto un link univoco per accedere alla propria galleria protetta su Cloudflare R2.
* **Admin (Fotografo):** Proprietario del sito che gestisce i contenuti pubblici e monitora le selezioni dei clienti privati.

---

## 📊 2. Diagramma dei Casi d'Uso (Flusso Generale)

Di seguito è descritto il flusso delle interazioni tra gli attori e il sistema. Il grafico evidenzia la separazione tra la navigazione del portfolio pubblico e la gestione della galleria privata.


```plantuml
skinparam packageStyle rectangle
skinparam actorStyle awesome
left to right direction

actor "Ale (Admin)" as Ale
actor "Esterno (Visitatore)" as Esterno
actor "Cliente (Privato)" as Cliente

rectangle "Sito Vetrina Carusoarw" {
    usecase "Gestire Clienti" as UC_GestClienti
    usecase "Caricare gallerie Clienti\n(con sottocategorie)" as UC_UploadClienti
    usecase "Creare/Modificare Portfolio\n(Wedding, Concert, etc.)" as UC_ModPortfolio
    usecase "Aggiungere Info Personali" as UC_ModInfo
    
    usecase "Visualizzare Portfolio\n(Categorie -> Soggetti -> Gallery)" as UC_ViewPort
    usecase "Contattare (Email)" as UC_Contact
    
    usecase "Accesso via Link Privato" as UC_AccessLink
    usecase "Valutazione Foto/Video\n(Stars & Tags)" as UC_Rating
    usecase "Download Foto/Video" as UC_Download
    
    usecase "Filtrare foto per stampa\n(Solo 4/5 stelle)" as UC_FilterStars
}

' Collegamenti Admin
Ale --> UC_GestClienti
Ale --> UC_UploadClienti
Ale --> UC_ModPortfolio
Ale --> UC_ModInfo
Ale --> UC_FilterStars

' Collegamenti Visitatore Esterno
Esterno --> UC_ViewPort
Esterno --> UC_Contact

' Collegamenti Cliente Privato
Cliente --> UC_AccessLink
Cliente --> UC_Rating
Cliente --> UC_Download

' Note esplicative
note left of UC_FilterStars : Ale filtra i file pronti\nin base ai voti del cliente
note right of UC_ViewPort : Struttura:\nCategoria > Soggetto > Gallery
note right of UC_UploadClienti : Es: Giorno prima,\nMatrimonio, etc.
```

</div>