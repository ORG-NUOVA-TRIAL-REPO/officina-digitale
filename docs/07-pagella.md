# Pagella degli accessi

Fotografia dello stato reale dell'organizzazione `ORG-NUOVA-TRIAL-REPO` all'**11 agosto 2026**.

Ogni voce riporta il valore trovato e dove e' stato verificato, in modo che chiunque possa rifare lo stesso controllo e ottenere lo stesso risultato. Nessun esito e' basato su cio' che il documento dichiara: solo su cio' che la configurazione risponde.

Piano dell'organizzazione al momento del controllo: **Free**. Alcune voci non passano per un limite del piano, ed e' indicato dove.

## Punteggio: 4 su 12

| # | Voce | Esito | Valore trovato | Dove e' stato verificato |
| --- | --- | --- | --- | --- |
| 1 | Nessun repository aziendale su account personali | **Non passa** | Sull'account personale `Giobebbe` esiste `officina-digitale-modello`, pubblico, cioe' il progetto da cui deriva quello dell'organizzazione | Elenco dei repository dell'account personale |
| 2 | Numero di Owner | **Non passa** | **1** (`Giobebbe`). La policy ne chiede almeno due | **People**, filtro sul ruolo Owner |
| 3 | Permesso di base | **Passa** | `none`, cioe' **No permission** | **Settings**, **Member privileges**, voce Base permissions |
| 4 | Verifica in due passaggi obbligatoria | **Non passa** | Non richiesta a livello di organizzazione | **Settings**, **Authentication security** |
| 5 | Accessi da team contro accessi a persone singole | **Passa** | `officina-digitale`: **3 da team**, **1 a persona singola**. `prova-token-secondo-repo`: **0 e 0** | **Settings** del repository, **Collaborators and teams** |
| 6 | Accessi diretti a persone | **Non passa** | Uno: `Giobebbe` con permesso `admin` su `officina-digitale` | Elenco dei collaboratori individuali del repository |
| 7 | Outside collaborator | **Passa** | Nessuno, quindi nessuna data di ingresso da riportare | **People**, scheda **Outside collaborators** |
| 8 | Pull request obbligatoria su `main` | **Non passa** | `officina-digitale`: **si**, ruleset `protezione-main`. `prova-token-secondo-repo`: **no**, i ruleset non sono disponibili sui repository privati nel piano Free | Ruleset del repository |
| 9 | Approvazioni richieste | **Non passa** | `officina-digitale`: **1**, con revisione obbligatoria dei responsabili di zona. `prova-token-secondo-repo`: **nessuna regola** | Regola `pull_request` del ruleset |
| 10 | Status check obbligatori | **Non passa** | `officina-digitale`: **1**, `Test del calcolo fatture`. `prova-token-secondo-repo`: **nessuno** | Regola `required_status_checks` del ruleset |
| 11 | Push protection sulle credenziali | **Non passa** | `officina-digitale`: **attiva**. `prova-token-secondo-repo`: **non disponibile**, il secret scanning non copre i repository privati nel piano Free | **Settings**, **Code security** di ciascun repository |
| 12 | I token devono essere approvati | **Passa** | **Require administrator approval** selezionato, e i token devono avere una scadenza | **Settings**, **Personal access tokens**, scheda **Settings** |

## Le voci non superate, in ordine di rischio

L'ordine non e' quello della lista: e' quello del danno che ciascuna provoca se qualcosa va storto.

### 1. Owner unico (voce 2)

Se l'unico Owner perde l'accesso al proprio account, l'organizzazione non e' piu' amministrabile da nessuno. Non esiste un modo di rientrare dall'interno: ne' i team ne' gli altri membri ereditano il ruolo. Blocca anche ogni altra riparazione di questo elenco, perche' tutte richiedono un Owner.

**Tempo:** 5 minuti, una volta scelta la persona. **Cambio di piano:** no.

### 2. Verifica in due passaggi non obbligatoria (voce 4)

Il furto di un account e' la via d'ingresso piu' comune, e senza obbligo basta una persona con una password debole per esporre tutta l'organizzazione. Oggi il rischio e' contenuto perche' il membro e' uno solo, e cresce con la prima persona che entra.

**Tempo:** 2 minuti. **Cambio di piano:** no. **Attenzione:** attivando l'obbligo, GitHub rimuove dall'organizzazione chi non ha la verifica attiva. Va annunciato prima.

### 3. Push protection assente su un repository (voce 11)

Una chiave scritta per sbaglio dentro `prova-token-secondo-repo` non verrebbe fermata da nessuno, e resterebbe nella storia del repository anche dopo la cancellazione dal file. E' il rischio con la riparazione piu' costosa a posteriori, perche' una credenziale esposta va sostituita, non nascosta.

**Tempo:** 1 minuto se si cancella quel repository, che la sua stessa descrizione dichiara temporaneo. Altrimenti il tempo del passaggio di piano. **Cambio di piano:** si, se il repository deve restare privato.

### 4. `main` non protetta su un repository (voci 8, 9, 10)

Le tre voci hanno una causa sola: nel piano Free i ruleset non si applicano ai repository privati. Su `prova-token-secondo-repo` chiunque abbia accesso in scrittura puo' scrivere direttamente sul ramo principale, senza proposta di modifica, senza approvazione e senza controlli automatici.

**Tempo:** 1 minuto cancellando il repository temporaneo, oppure 10 minuti per configurare il ruleset dopo il passaggio di piano. **Cambio di piano:** si, se il repository deve restare privato. Renderlo pubblico e' l'altra strada che GitHub indica, e per un repository di prova sui token non e' una buona idea.

### 5. Repository del progetto su un account personale (voce 1)

`officina-digitale-modello` vive sull'account personale invece che nell'organizzazione. Non e' un rischio di accesso ma di continuita': cio' che sta su un account personale segue quell'account, non l'azienda, e non compare in nessun controllo di questo elenco.

**Tempo:** 10 minuti per il trasferimento. **Cambio di piano:** no. **Nota:** se quel repository e' materiale didattico e non codice aziendale, la policy deve dirlo, altrimenti il controllo continuera' a segnalarlo a ogni revisione.

### 6. Un accesso diretto a persona (voce 6)

`Giobebbe` ha permesso `admin` su `officina-digitale` come collaboratore individuale. E' il rischio piu' basso dell'elenco, perche' si tratta dell'Owner, che ha comunque accesso amministrativo a tutti i repository grazie al ruolo. Proprio per questo l'accesso diretto e' **ridondante**: non concede niente in piu' e crea un'eccezione alla regola "l'accesso passa dai team" che nessun documento motiva.

**Tempo:** 1 minuto. **Cambio di piano:** no.

## La riparazione che vale piu' di tutte

Cancellare `prova-token-secondo-repo`, che la sua stessa descrizione dichiara temporaneo, fa passare in un colpo solo le voci 8, 9, 10 e 11 e porta il punteggio da **4 su 12** a **8 su 12**, senza cambiare piano e in circa un minuto.

Va detto con onesta': quelle voci passano perche' il repository non conforme smette di esistere, non perche' e' stato messo in regola. E' la scelta giusta solo se quel repository ha davvero esaurito il suo scopo.

## Come rifare questa pagella

Le dodici voci si ricontrollano dalle stesse schermate elencate nella colonna di destra. La verifica va rifatta a ogni revisione periodica prevista da `docs/02-policy-accessi.md`, cioe' a marzo e a settembre, e il punteggio va confrontato con quello precedente: un punteggio che scende senza che nessuno se ne sia accorto e' l'informazione piu' utile che questo documento possa dare.

| | |
| --- | --- |
| **Data del controllo** | 11 agosto 2026 |
| **Prossimo controllo** | 1 settembre 2026 |
| **Chi ne risponde** | Giovanni Beggiato |
