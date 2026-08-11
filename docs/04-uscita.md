# Uscita di una persona

Da eseguire lo stesso giorno in cui la persona smette di lavorare, non la settimana dopo.

Togliere la persona dall'organizzazione non basta. Restano attivi diversi accessi che sopravvivono alla rimozione, ed e' esattamente li' che si creano i problemi.

Il **giorno 0** e' l'ultimo giorno di lavoro della persona.

## L'ordine conta, e va contro l'istinto

L'istinto dice di rimuovere subito la persona dall'organizzazione e poi sistemare il resto. E' l'ordine sbagliato, per due ragioni.

La prima: finche' la persona e' dentro, la pagina degli accessi ti mostra **da dove arriva ogni permesso**, cioe' se da un team o da un accesso diretto. Appena e' fuori, quella informazione non la recuperi piu' e un accesso diretto dimenticato diventa invisibile.

La seconda: nel menu di rimozione GitHub offre **Convert to outside collaborator** accanto a **Remove from organization**. La prima voce sembra la scelta prudente e invece conserva l'accesso ai repository, togliendo solo l'appartenenza all'organizzazione. Chi ha fretta la sceglie.

Per questo gli accessi diretti si tolgono per primi, quando li vedi ancora.

## Chi esegue

| Ruolo | Chi e' |
| --- | --- |
| **Owner GitHub** | Chi ha il ruolo Owner sull'organizzazione |
| **Responsabile del team** | Chi guidava la persona che esce |
| **Chi tiene i server** | Chi ha accesso amministrativo alle macchine e ai servizi esterni. In dieci persone e' spesso lo stesso Owner GitHub, e va scritto chi e' |

## La lista

| Cosa si fa | Chi | Entro quando | Come si verifica |
| --- | --- | --- | --- |
| Elencare gli accessi **diretti** della persona su ogni repository, prima di toccare qualsiasi cosa | Owner GitHub | Giorno 0, prima di tutto il resto | In **Settings** di ogni repository, scheda **Collaborators and teams**, si guarda l'elenco dei collaboratori individuali. Quello che compare li' non arriva da un team |
| Rimuovere gli accessi diretti trovati | Owner GitHub | Giorno 0 | Lo stesso elenco non contiene piu' il suo nome |
| Rimuovere la persona da tutti i team | Responsabile del team | Giorno 0 | In **People**, accanto al suo nome, il contatore dei team dice **0 teams** |
| Verificare che non fosse l'unico responsabile di una zona di `.github/CODEOWNERS`, e sostituirla | Responsabile del team | Giorno 0, prima della rimozione | Per ogni zona che la nominava, il file indica ora un'altra persona o un team che ha ancora almeno permesso Write |
| Verificare che non fosse l'unico Owner dell'organizzazione | Owner GitHub | Giorno 0, prima della rimozione | In **People**, filtrando per ruolo Owner, resta almeno un'altra persona. Se era l'unico, il ruolo va passato prima di rimuoverlo |
| Rimuovere la persona dall'organizzazione scegliendo **Remove from organization** | Owner GitHub | Giorno 0 | In **People** il suo nome non compare piu'. La scheda **Outside collaborators** non deve averlo acquisito |
| Revocare i **fine-grained personal access token** che avevano accesso all'organizzazione | Owner GitHub | Giorno 0 | In **Settings**, **Personal access tokens**, **Active tokens**, nessun token risulta intestato a lei. Sui token classici questa pagina non puo' nulla: vedi la sezione sui limiti |
| Trasferire i repository di lavoro che aveva creato sul proprio account personale | Owner GitHub | Entro 7 giorni | Il repository risponde all'indirizzo dell'organizzazione e compare in **Repositories** |
| Riassegnare le segnalazioni e le proposte di modifica ancora aperte a suo nome | Responsabile del team | Entro 48 ore | Una ricerca `is:open assignee:UTENTE` nel repository non restituisce nulla |
| Rileggere il registro attivita' degli ultimi trenta giorni cercando azioni amministrative che non riconosci | Owner GitHub | Entro 48 ore | Le cinque ricerche di `docs/06-controllo-mensile.md` non restituiscono nulla di nuovo oltre alle rimozioni appena fatte |

## Quello che GitHub non puo' verificare al posto tuo

Le righe qui sotto non hanno una schermata che le dimostri. Nessuna rimozione su GitHub le tocca, e sono quelle che restano aperte per mesi.

| Cosa si fa | Chi | Entro quando | Come si verifica |
| --- | --- | --- | --- |
| Rimuovere le **chiavi SSH** della persona dai server aziendali | Chi tiene i server | Giorno 0 | Su ogni macchina, la sua chiave non compare piu' nel file delle chiavi autorizzate. Le chiavi stanno sui server, non su GitHub: toglierla dall'organizzazione non ne rimuove nemmeno una |
| Rimuovere le **deploy key** che aveva installato sui repository | Owner GitHub | Giorno 0 | In **Settings** del repository, scheda **Deploy keys**, non restano chiavi che solo lei sapeva a cosa servissero |
| **Ruotare** i segreti condivisi che ha visto: password di servizi, chiavi API, credenziali comuni | Chi tiene i server | Entro 24 ore | Ogni credenziale ha un valore nuovo e il vecchio non funziona piu'. Va cambiato il valore, non l'accesso: revocare un permesso non cancella cio' che una persona ha gia' letto e magari copiato negli appunti |
| Chiudere gli accessi ai **servizi esterni collegati con l'account GitHub** | Chi tiene i server | Giorno 0 | Nel pannello di ogni servizio la persona non compare piu' fra gli utenti. Entrare con GitHub e' una porta indipendente: continua a funzionare anche dopo la rimozione dall'organizzazione |
| Chiedere la restituzione o la cancellazione delle **copie locali** del codice | Responsabile del team | Giorno 0 | Non e' verificabile. Va chiesto per iscritto e messo agli atti: chi ha clonato un repository ha quei file sul proprio computer e nessuna azione su GitHub li rimuove |

Tre limiti da conoscere, perche' cambiano cosa puoi promettere:

- **I token classici non li vedi.** Un Owner puo' revocare i fine-grained personal access token che toccano l'organizzazione, ma i token classici non compaiono in quella pagina. Perdono l'accesso quando la persona esce dall'organizzazione, e questo e' l'unico motivo per cui il punto si chiude
- **I fork dentro un account privato sono invisibili.** Se la persona ha copiato il repository dentro un proprio repository privato, nessuno fuori dal suo account puo' vederlo
- **Le chiavi SSH e i token del suo account personale restano suoi.** GitHub non da' a un Owner nessuna visibilita' sulle credenziali personali di un membro

## Il controllo finale

Non verifica che i passi siano stati eseguiti. Verifica che la persona **non abbia piu' accesso**, che e' una cosa diversa.

Il giorno dopo, due controlli:

1. **Per ogni repository dell'organizzazione**, aprire **Settings**, scheda **Collaborators and teams**, e cercare il suo nome. Non deve comparire ne' fra i collaboratori individuali ne' dentro un team
2. **Aprire la scheda Outside collaborators** in **People**. E' l'unico posto dove riappare chi e' stato convertito invece che rimosso, e non compare nella lista dei membri

Un'avvertenza che evita una conclusione sbagliata. Su un repository **pubblico**, GitHub attribuisce a chiunque un permesso di lettura, anche a una persona che non ha mai avuto niente a che fare con l'azienda. Trovare `read` accanto al suo nome quindi non significa che le e' rimasto un accesso: e' la lettura che ha chiunque su Internet. La prova che l'uscita e' andata a buon fine e' l'**assenza del nome dall'elenco dei collaboratori**, non il valore del permesso.

Non usare come controllo la ricerca del suo nome nel registro attivita'. Il registro contiene il suo nome proprio perche' l'hai rimossa, e l'evento `org.remove_member` la cita per esteso: quella ricerca segnala un problema ogni volta, anche quando e' filato tutto liscio.
