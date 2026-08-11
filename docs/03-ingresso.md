# Ingresso di una persona

Da eseguire nell'ordine. Ogni riga o e' fatta o non lo e', e la colonna della verifica dice dove guardare per stabilirlo: non basta ricordarsi di aver fatto una cosa.

Il **giorno 0** e' il primo giorno di lavoro della persona.

## Chi esegue

Tre ruoli, che in un'azienda di dieci persone esistono sempre anche se nessuno li chiama cosi'.

| Ruolo | Chi e' |
| --- | --- |
| **Owner GitHub** | Chi ha il ruolo Owner sull'organizzazione. Sono almeno due persone |
| **Responsabile del team** | Chi guida il team in cui la persona entra e risponde di cosa quel team puo' toccare |
| **La persona** | Chi entra |

## La lista

| Cosa si fa | Chi | Entro quando | Come si verifica |
| --- | --- | --- | --- |
| La persona crea il proprio account GitHub con l'email di lavoro | La persona | Giorno -2 | L'account risponde all'indirizzo `github.com/UTENTE` e l'email di lavoro risulta verificata nel suo profilo |
| La persona attiva la verifica in due passaggi e salva i codici di recupero fuori dal computer di lavoro | La persona | Giorno -2 | In **People**, accanto al suo nome, compare l'etichetta **2FA**. Se manca, la riga non e' fatta |
| Si manda l'invito all'organizzazione con ruolo **Member** | Owner GitHub | Giorno -1 | In **People** la persona compare come **Member**, non come Owner. La scheda **Invitations** non deve piu' contenerla |
| Si inserisce la persona nei team che corrispondono al suo lavoro | Responsabile del team | Giorno 0, mattina | In **Teams** il suo nome compare nei team previsti e in nessun altro |
| Si controlla quale permesso concede davvero il team scelto | Responsabile del team | Giorno 0, mattina | Nella pagina del team, scheda **Repositories**, si legge il permesso sul repository. Vedi l'avvertenza sui team annidati qui sotto |
| Non si concede nessun accesso diretto ai repository | Owner GitHub | Giorno 0 | In **Settings** del repository, scheda **Collaborators and teams**, la persona non compare fra i collaboratori individuali. Devono esserci solo team |
| La persona legge `docs/01-come-lavoriamo.md` e questo documento | La persona | Giorno 0 | Non e' verificabile su GitHub. Il responsabile del team ne parla con lei e il controllo finale qui sotto lo dimostra sul campo |
| Prima attivita': aprire una segnalazione e chiuderla con una proposta di modifica, anche minima | La persona | Entro 48 ore | La segnalazione e la proposta esistono nel repository e portano il suo nome |

## L'avvertenza sui team annidati

Un team puo' essere figlio di un altro. In questa organizzazione **prodotto** e' figlio di **tecnologia**.

Chi sta nel team figlio compare automaticamente anche nell'elenco del team padre, e questo inganna: il padre **tecnologia** concede lettura sul repository, il figlio **prodotto** concede scrittura. Guardando la lista dei membri di **tecnologia** si conclude che quelle persone possono solo leggere, e per chi arriva da **prodotto** e' falso.

Quando iscrivi qualcuno, leggi il permesso del team dove lo stai iscrivendo davvero, mai quello del padre. Chi sbaglia qui se ne accorge il giorno dell'uscita, quando toglie la persona dal team sbagliato e il permesso non scende.

## Cosa non si fa

- Non si da' accesso "per sicurezza, cosi' non ci blocchiamo"
- Non si concede Owner a chi deve solo lavorare
- Non si concede un accesso diretto a un repository per sbloccare in fretta una situazione: e' l'accesso che nessuno si ricorda di togliere, perche' non compare in nessun team
- Non si aspetta il primo giorno per preparare gli accessi, e non si preparano settimane prima

## Il controllo finale

Non verifica che gli accessi siano stati concessi. Verifica che la persona **riesca a lavorare** e che **non riesca a fare cio' che non deve**.

Entro le prime 48 ore, la persona apre una segnalazione, la chiude con una proposta di modifica su una linea di lavoro dedicata, e chiede la revisione.

Il risultato atteso e' doppio:

1. La proposta di modifica viene creata e la revisione parte. Se non ci riesce, i permessi sono troppo bassi
2. La proposta **non si puo' unire** finche' non arriva l'approvazione prevista. Se si unisce da sola, la protezione del ramo non sta funzionando

Il secondo punto e' il piu' importante, ed e' la ragione per cui questa riga esiste. Una protezione che non funziona si scopre con il primo assunto oppure con il primo incidente. La differenza la decide questo controllo.
