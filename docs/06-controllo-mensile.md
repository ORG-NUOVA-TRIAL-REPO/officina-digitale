# Controllo mensile del registro attivita'

Una volta al mese, dieci minuti. Si apre l'**Audit log** dell'organizzazione e si eseguono le cinque ricerche qui sotto, una alla volta. Non e' un controllo sulle persone: e' la verifica che le regole configurate siano ancora quelle decise.

Dove: `github.com/organizations/ORG-NUOVA-TRIAL-REPO/settings/audit-log`

Il registro conserva gli eventi degli ultimi centottanta giorni. Ogni espressione si incolla nella casella di ricerca cosi' com'e' scritta.

## Le cinque ricerche

### 1. Qualcuno e' diventato Owner

```
action:org.update_member
```

Mostra ogni cambio di ruolo di un membro dell'organizzazione, in entrambe le direzioni: da Member a Owner e viceversa. Il campo `permission` nel dettaglio dell'evento dice il ruolo nuovo, `old_permission` quello precedente.

Se trovi un risultato che non riconosci: qualcuno ha ottenuto o perso il potere totale sull'organizzazione senza che tu lo sapessi. Chiama subito chi compare nel campo `actor` e chiedi chi lo ha autorizzato. Finche' non hai la risposta, riporta il ruolo com'era.

### 2. Una protezione e' stata creata, modificata o cancellata

```
action:repository_ruleset.create
action:repository_ruleset.update
action:repository_ruleset.destroy
```

Tre ricerche separate, una per verbo: creazione, modifica e cancellazione di un ruleset. Il registro non permette di cercarle in una volta sola. Se in azienda vengono usate anche le protezioni di ramo classiche, gli eventi corrispondenti iniziano con `protected_branch.` (ad esempio `action:protected_branch.destroy`).

Se trovi un risultato che non riconosci: il processo di revisione che avete costruito e' stato toccato. La modifica puo' essere legittima, ma la persona nel campo `actor` deve saperti dire perche'. Se la protezione e' stata cancellata, va ricreata prima di chiudere il controllo.

### 3. Il permesso di base e' cambiato

```
action:org.update_default_repository_permission
```

Mostra ogni cambio del permesso di base dell'organizzazione. Nel dettaglio, `old_permission` e' il valore precedente e `permission` quello nuovo.

Se trovi un risultato che non riconosci: una riga in una pagina di impostazioni ha concesso o tolto accesso a tutti su tutto. Se il valore nuovo e' piu' alto di quello scritto nella policy degli accessi (`docs/02-policy-accessi.md`), riportalo al valore di policy e poi chiedi all'autore perche' lo aveva alzato.

### 4. Un repository ha cambiato visibilita'

```
action:repo.access
```

Mostra ogni cambio di visibilita' di un repository dell'organizzazione, in entrambe le direzioni. Il caso che conta e' il passaggio da privato a pubblico: nel dettaglio dell'evento, il campo `visibility` vale `public`.

Se trovi un passaggio a pubblico che non riconosci: tutta la storia di quel repository e' gia' uscita di casa, e riportarlo a privato non la fa rientrare. Riporta comunque il repository a privato per fermare l'esposizione, poi verifica se conteneva credenziali o dati di clienti e trattali come compromessi.

### 5. Un'applicazione e' stata installata o ha ottenuto permessi nuovi

```
action:integration_installation.create
action:integration_installation.version_updated
```

La prima mostra ogni **GitHub App** installata sull'organizzazione, la seconda ogni volta che a un'App gia' installata sono stati concessi permessi nuovi. Due ricerche separate.

Se trovi un risultato che non riconosci: un programma esterno ha accesso ai vostri progetti. Apri **Settings** > **GitHub Apps**, guarda quali permessi ha l'applicazione e chi l'ha installata. Se nessuno la reclama, disinstallala: un'App legittima si puo' sempre reinstallare, un accesso non reclamato no.

## Il punto di partenza

Conteggi al primo controllo, eseguito l'11 agosto 2026:

| Ricerca | Risultati | Nota |
| --- | --- | --- |
| `org.update_member` | 0 | Nessun cambio di ruolo dalla creazione dell'organizzazione |
| `repository_ruleset.create` / `.update` / `.destroy` | 1 / 0 / 0 | Il ruleset creato durante il percorso |
| `org.update_default_repository_permission` | 2 | I due cambi fatti durante il percorso, il 3 agosto 2026 |
| `repo.access` | 0 | Nessun repository ha cambiato visibilita' |
| `integration_installation.create` / `.version_updated` | 0 / 0 | Nessuna applicazione installata |

Al prossimo controllo, ogni risultato in piu' rispetto a questa tabella deve avere un nome e una ragione.
