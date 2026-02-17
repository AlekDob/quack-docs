# Brain dallo Store: guida rapida

Il Second Brain di Quack funziona grazie a un set di plugin installabili dal **Quack Store**. Questa pagina ti spiega quali sono, cosa fanno, e come metterli insieme in pochi minuti.

Pensa allo Store come a un negozio di app per i tuoi agenti AI. Alcune "app" insegnano all'agente come comportarsi (sono le **Rules**), altre gli danno competenze specifiche (le **Skills**), e altre ancora sono agenti specializzati pronti all'uso (i **Droids**).

## I 4 plugin del Brain

Aprendo il Quack Store e cercando "Brain" trovi 4 item principali:

| Nome | Tipo | Cosa fa |
|------|------|---------|
| **Quack Brain** | Skill | Il cuore del sistema — insegna all'agente a leggere e scrivere nel Brain |
| **Use Quack Brain** | Rule | Il promemoria automatico — ricorda all'agente di usare il Brain in ogni sessione |
| **Brain Migrate** | Skill | L'assistente al trasloco — converte documentazione sparsa nel formato Brain v2 |
| **Quack Brain Manager** | Droid | Il bibliotecario — mantiene la knowledge base ordinata nel tempo |

Vediamoli uno per uno.

---

## Quack Brain (Skill)

Questa e' la skill fondamentale. Senza di lei, l'agente non sa ne' dove cercare ne' come salvare le conoscenze.

Installando **Quack Brain** insegni all'agente:

- La struttura a due livelli (`documentation/` nel progetto + `~/.quack/brain/` globale)
- Il formato YAML obbligatorio per ogni file di conoscenza
- Come leggere, scrivere e cercare entry nel Brain
- Come scrivere i diary entry (il changelog giornaliero del progetto)
- Come usare le frecce di breadcrumb nel codice (`// Brain: slug`) per collegare codice e documentazione
- Come creare diagrammi Mermaid

:::callout[info]
Se installi solo un plugin, questo e' quello giusto. E' il fondamento su cui si appoggiano tutti gli altri.
:::

---

## Use Quack Brain (Rule)

Una Rule e' diversa da una Skill. Non insegna all'agente un'abilita' tecnica, ma gli dice **come comportarsi**.

**Use Quack Brain** e' il promemoria automatico che si attiva all'inizio di ogni sessione. Dice all'agente:

- Prima di fare qualsiasi cosa, cerca nel Brain se esiste gia' una soluzione
- Dopo aver scoperto qualcosa di utile, salvalo nel Brain
- Rispetta sempre il formato YAML (senza frontmatter, il Brain UI non mostra i file)

:::callout[warning]
La Rule non e' infallibile al 100%. A volte l'agente dimentica di seguirla, specialmente in sessioni molto lunghe o su task complessi. Ma copre la stragrande maggioranza dei casi e vale sempre la pena averla attiva.
:::

Senza questa Rule, l'agente conosce il Brain (grazie alla Skill) ma potrebbe non usarlo in modo sistematico. Con la Rule, il comportamento diventa un'abitudine automatica.

---

## Brain Migrate (Skill)

Hai un progetto con documentazione sparsa? File `.md` in giro per il repo, una cartella `.quack/brain/` dal vecchio formato, oppure docs in `.claude/docs/`?

**Brain Migrate** e' la skill che fa il trasloco. Scansiona tutte le posizioni note, classifica ogni file (bug fix, pattern, decisione, gotcha, diary...) e li sposta nella struttura corretta `documentation/`.

Il processo e' in 6 step e ti mostra un piano completo prima di toccare qualsiasi file. Nulla si sposta senza la tua approvazione.

:::callout[info]
Se stai partendo da zero con un progetto nuovo, non hai bisogno di Brain Migrate. E' pensata per chi ha gia' della documentazione e vuole portarla nel formato v2.
:::

Per tutti i dettagli sul processo di migrazione, vedi [Brain Migration](./brain-migration).

---

## Quack Brain Manager (Droid)

Un Droid e' un agente specializzato che puoi chiamare su richiesta. Non e' attivo in automatico come una Rule — lo invochi tu quando ne hai bisogno.

**Quack Brain Manager** e' il bibliotecario del tuo Brain. Lo usi per:

- Riorganizzare entry che si sono accumulate in modo caotico
- Trovare duplicati e consolidarli
- Aggiornare entry obsolete
- Fare una "pulizia di primavera" della knowledge base

E' un plugin opzionale, utile soprattutto su progetti maturi con molte entry accumulate nel tempo.

---

## Setup raccomandato

Ecco le tre configurazioni piu' comuni, dal minimo indispensabile all'avanzato.

:::steps
1. **Setup minimo** — Installa **Quack Brain** (Skill) + **Use Quack Brain** (Rule). Questo e' tutto quello che ti serve per iniziare. L'agente sa come usare il Brain e ha il promemoria automatico attivo.

2. **Setup per progetti esistenti** — Aggiungi **Brain Migrate** (Skill) se hai gia' documentazione da organizzare. Eseguila una volta, poi puoi anche disinstallarla se non ti serve piu'.

3. **Setup avanzato** — Aggiungi **Quack Brain Manager** (Droid) se vuoi manutenzione periodica della knowledge base senza farlo a mano.
:::

---

## Come installare i plugin

:::steps
1. Apri il **Quack Store** dall'interfaccia principale (puoi trovarlo nella barra laterale o nelle impostazioni dell'agente)

2. Cerca **"Brain"** nella barra di ricerca

3. Clicca su ciascun plugin che vuoi installare, poi clicca **Install**

4. Assegna le Rules e le Skills all'agente dal pannello laterale (vedi [Side Panel](./side-panel) per i dettagli)

5. Inizia una nuova sessione — i plugin sono attivi subito
:::

:::callout[info]
Quando installi una **Rule**, ricordati di assegnarla esplicitamente all'agente. Le Rules non si attivano da sole se non le assegni. Le Skills, invece, vengono usate dall'agente quando servono una volta che sono installate.
:::

---

## Come funzionano insieme

Se li hai tutti e tre attivi, il flusso tipico di una sessione e' questo:

1. L'agente parte, legge **Use Quack Brain** (Rule) e sa che deve cercare prima di agire
2. Usa **Quack Brain** (Skill) per sapere dove cercare e come interpretare i file trovati
3. Lavora sul tuo task
4. Prima di chiudere, usa di nuovo **Quack Brain** per salvare eventuali scoperte
5. Se convochi **Quack Brain Manager** (Droid), lui si occupa di tenere tutto ordinato

---

**Prossimo**: [Background Tasks](./background-tasks) — Esegui operazioni lunghe senza bloccare l'interfaccia

**Precedente**: [Brain Migration](./brain-migration) — Migra la tua documentazione esistente nel formato Brain v2
