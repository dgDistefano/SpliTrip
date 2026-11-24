# Splitrip — Gestione Itinerari e Spese Condivise Multivaluta in EUR

**Splitrip** è una Progressive Web App (PWA) *local-first* progettata per organizzare viaggi di gruppo, monitorare il tasso di cambio giornaliero verso l'Euro e calcolare automaticamente i rimborsi minimi tra partecipanti.

---

## Caratteristiche Principali

* **Architettura Single-File Zero-Dependency**: interamente contenuta in `index.html` (HTML5, CSS3 Variables, Vanilla ES2022), senza framework esterni né backend obbligatorio.
* **Persistenza Locale e Portabilità**:
  * Salvataggio automatico su `localStorage` (`splitrip_data_v5`) con migrazione trasparente dalle versioni precedenti (`v1`–`v4`).
  * Esportazione e importazione completa in formato **JSON**.
  * Esportazione tabellare delle spese in formato **CSV** (separatore `;`, codifica UTF-8 BOM per apertura diretta in Microsoft Excel).
  * Condivisione rapida del riepilogo conti tramite Web Share API o copia negli appunti.
* **Motore Multivaluta (160+ valute ISO 4217)**:
  * Recupero automatico del tasso di cambio giornaliero verso `EUR` tramite API pubbliche (`frankfurter.app`, `frankfurter.dev` con fallback su `open.er-api.com`).
  * **Snapshot storico del cambio**: ogni spesa in valuta estera congela il tasso applicato al momento dell'inserimento (`fxRateApplied` e `fxDateApplied`).
  * **Cambio manuale e riallineamento**: possibilità di inserire un tasso personalizzato (es. cambio reale applicato dalla carta/banca) e di riallineare retroattivamente le spese esistenti.
* **Ripartizione Intelligente delle Spese**:
  * Supporto alla divisione equa o **selettiva per sotto-gruppi** (`splitAmong`).
  * **Algoritmo Greedy di compensazione dei debiti**: riduce al minimo il numero di bonifici/trasferimenti necessari per azzerare i saldi.
  * Pulsante **Salda** su ogni rimborso consigliato per registrare istantaneamente il pagamento avvenuto.
* **Pianificazione & Controllo Budget**:
  * Categorizzazione spese (*Alloggio, Ristoranti & Bar, Trasporti, Attività & Biglietti, Shopping & Varie*) con grafico a barre percentuale.
  * Monitoraggio del budget massimo stimato in EUR.
  * Checklist itinerario ordinata cronologicamente con stato di completamento.
  * 5 temi cromatici (`Dark`, `Light`, `Ocean`, `Sunset`, `Forest`) e copertine personalizzabili con compressione automatica delle immagini lato client (`Canvas API`).

---

## Struttura del Progetto

```text
WayLocal/
├── index.html        # Applicazione completa (UI, Stili CSS, Logica JS, Icona SVG dinamica)
├── manifest.json     # Manifest PWA (nome app, icone, display standalone)
├── sw.js             # Service Worker per caching offline e installabilità
├── icon-192.png      # Icona PWA 192x192
└── README.md         # Documentazione tecnica e guida utente
