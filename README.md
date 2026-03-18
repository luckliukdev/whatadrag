# What a drag! - Global Leaderboard System

Questo repository ospita la classifica globale del gioco "What a drag!".
Il sistema utilizza un'architettura **Serverless** basata su **GitHub Actions** e **GitHub Pages**.

## Come Funziona

1.  **Invio:** L'app invia un evento `repository_dispatch` (tipo: `submit-score`) all'API di GitHub.
2.  **Elaborazione:** Una GitHub Action (`.github/workflows/update_leaderboard.yml`) si attiva.
3.  **Aggiornamento:** Lo script Python nella Action:
    *   Legge `leaderboard.json`.
    *   Aggiunge il nuovo punteggio.
    *   Ordina e pulisce la lista (mantiene solo il miglior punteggio per utente).
    *   Fa il commit del file aggiornato.
4.  **Visualizzazione:** La pagina `leaderboard.html` legge il JSON aggiornato e mostra la classifica.

## Struttura Dati

Il file `leaderboard.json` contiene la Top 100 dei giocatori.

## Sicurezza

Per prevenire l'invio di punteggi fraudolenti, le richieste di invio vengono validate tramite un meccanismo di firma, assicurando che provengano solo dal client di gioco ufficiale.

## Privacy

Vedi `index.html` per la Privacy Policy completa. Nessun dato personale oltre al nickname di gioco viene salvato.

## Configurazione

Per il corretto funzionamento, è necessario configurare i **GitHub Secrets** appropriati nel repository (es. token per la validazione della firma e permessi di scrittura per la Action).

## Note Tecniche e Limitazioni

Poiché il sistema utilizza Git come livello di persistenza, le scritture sono sequenziali. In caso di traffico molto elevato e simultaneo (race conditions), potrebbero verificarsi conflitti durante il commit del file JSON. Il sistema è ottimizzato per volumi di invio medio-bassi.