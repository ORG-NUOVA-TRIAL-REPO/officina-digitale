# Policy degli accessi

Questo documento esiste per una ragione sola: rendere le regole discutibili una volta, invece che ogni volta che qualcuno chiede un permesso.

Le decisioni qui sotto sono prese. Chi vuole cambiarne una apre una proposta di modifica su questo file e la discute li', non nella chat del momento.

## Dove sta il codice aziendale

Tutto il codice dell'azienda vive nell'organizzazione `ORG-NUOVA-TRIAL-REPO`. Nessun repository aziendale sta su account personali. Se ne trovi uno, va trasferito, non copiato.

Trasferito e non copiato perche' una copia crea due versioni che da quel momento in poi si allontanano, e nessuno sa piu' quale sia quella buona.

## Chi puo' essere Owner

Owner dell'organizzazione e' **1 persona: Giovanni Beggiato**.

Owner e' un potere totale: chi lo ha puo' cambiare ogni permesso, togliere ogni protezione e cancellare l'organizzazione. Non e' un potere che qualcun altro dall'interno possa fermare.

**La regola sarebbe almeno due**, per non restare chiusi fuori se una persona non e' raggiungibile. Oggi la regola non e' rispettata, e la conseguenza va scritta in chiaro invece che nascosta: **se Giovanni Beggiato perde l'accesso al proprio account, nessuno puo' piu' amministrare l'organizzazione**. Non esiste un modo per rientrare dall'interno, e ne' i team ne' gli altri membri ereditano il ruolo.

Finche' l'Owner resta uno solo, valgono due contromisure:

- La verifica in due passaggi sull'account dell'Owner deve essere attiva, e i codici di recupero vanno conservati fuori dal computer di lavoro
- Nominare un secondo Owner e' il primo punto della prossima revisione

Mai piu' Owner di quanti ne servono. Due sono la sicurezza, quattro sono un rischio moltiplicato per quattro.

## Il permesso di base

Il permesso di base dell'organizzazione e' **nessuno**.

Il permesso di base e' cio' che ogni membro riceve su ogni progetto per il solo fatto di far parte dell'organizzazione, senza che nessuno glielo abbia dato. Impostarlo su **nessuno** significa che entrare in azienda non apre da solo nessuna porta: ogni accesso e' una decisione presa da qualcuno.

L'alternativa, "lettura", darebbe a ogni nuovo assunto la possibilita' di leggere ogni progetto dal primo giorno, compresi quelli che non lo riguardano. Se fosse impostato su "scrittura", ognuno potrebbe anche modificarli.

## Come si concedono gli accessi

- L'accesso si da' ai **team**, non alle persone. Una persona entra in un team, il team ha un permesso su un progetto
- L'accesso diretto a una persona su un progetto e' l'eccezione e va motivato per iscritto
- Il permesso di partenza e' il piu' basso che permette di lavorare. Si sale su richiesta, non per precauzione

Il motivo per cui l'accesso passa dai team e' pratico, non ideologico: quando una persona cambia ruolo o lascia l'azienda, si cambia una cosa sola, la sua appartenenza al team. Un accesso dato alla singola persona invece non compare in nessuna lista di gruppo, e nessuno se lo ricorda il giorno in cui andrebbe tolto.

**Attenzione ai team dentro altri team.** Un team puo' essere contenuto in un altro: qui `prodotto` sta dentro `tecnologia`. Chi entra nel team interno compare automaticamente anche nell'elenco di quello esterno, ma **conta il permesso del team dove la persona e' iscritta davvero**. In questo caso il team esterno concede la sola lettura mentre quello interno concede la scrittura: leggendo l'elenco del team esterno si conclude che quelle persone possono solo leggere, e per chi arriva da `prodotto` e' falso.

## Chi approva cosa

I responsabili di zona sono definiti nel file `.github/CODEOWNERS`. Quel file stabilisce chi deve essere chiamato ad approvare quando una modifica tocca una certa parte del progetto.

Modificare quel file richiede l'approvazione di **un Owner dell'organizzazione**.

La ragione: quel file decide chi puo' bloccare una modifica. Se puo' cambiarlo chiunque, chi vuole evitare un controllo si toglie da solo il controllore, e tutte le altre regole di questo documento diventano facoltative.

## Le protezioni minime su ogni progetto

- Proposta di modifica obbligatoria sul ramo principale: nessuno scrive direttamente sulla versione buona
- Almeno **1** approvazione, da una persona diversa dall'autore
- Controlli automatici obbligatori: i test devono passare prima che si possa unire il lavoro
- Cancellazione del ramo principale vietata
- Scrittura forzata vietata, cioe' nessuno puo' riscrivere la storia gia' pubblicata

**Perche' una sola approvazione e non due.** In un'azienda di dieci persone, chiedere due approvazioni significa che ogni modifica aspetta due agende diverse. Il risultato non e' piu' qualita': e' che si impara ad aggirare la regola, per esempio approvando senza leggere pur di sbloccare un collega. Una approvazione, letta davvero, vale piu' di due firme di comodo. Il numero si alza quando l'azienda cresce, non prima.

## Fornitori esterni

I fornitori esterni non diventano membri dell'organizzazione. Ricevono accesso a un solo progetto, con scadenza **90 giorni**.

La scadenza si verifica il **primo giorno** di ogni mese, insieme al controllo del registro attivita' descritto in `docs/06-controllo-mensile.md`.

Novanta giorni coprono quasi ogni collaborazione reale e obbligano a una conferma esplicita per continuare. Un accesso senza scadenza non viene tolto da nessuno: semplicemente smette di essere usato, e resta aperto per anni.

Il rinnovo si chiede per iscritto e vale altri 90 giorni. Un fornitore che non risponde alla richiesta di rinnovo e' un fornitore il cui accesso va chiuso.

## Revisione periodica

Due volte l'anno, a **marzo** e a **settembre**, si rileggono tutti gli accessi e si toglie tutto cio' che non e' piu' giustificato.

Cosa si guarda, in concreto:

1. L'elenco delle persone dell'organizzazione: c'e' ancora qualcuno che ha lasciato l'azienda
2. L'elenco dei collaboratori esterni: e' il posto dove ricompare chi e' stato tolto male
3. I membri di ogni team, confrontati con il lavoro che quelle persone fanno davvero oggi
4. Gli accessi diretti ai progetti: dovrebbero essere zero, e ogni eccezione deve avere ancora la sua motivazione scritta
5. Gli accessi dei fornitori esterni scaduti e mai chiusi

Responsabile: **Giovanni Beggiato**.

---

## Revisione di questo documento

| | |
| --- | --- |
| **Ultima compilazione** | 11 agosto 2026 |
| **Prossima revisione** | 1 settembre 2026 |
| **Chi ne risponde** | Giovanni Beggiato |

Il primo punto della prossima revisione e' la nomina di un secondo Owner dell'organizzazione, che oggi manca.

Se la data della prossima revisione e' passata e nessuno ha aperto una proposta di modifica su questo file, il documento non descrive piu' l'azienda: descrive l'azienda di allora.
