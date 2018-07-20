---
title: 'Gestione record di messaggistica: Exchange 2013 Help'
TOCTitle: Gestione record di messaggistica
ms:assetid: 0dd92e9c-881e-43c0-9bbf-f41fdc9dfd87
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335093(v=EXCHG.150)
ms:contentKeyID: 50479985
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestione record di messaggistica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-02-01_

Gli utenti inviano e ricevono messaggi di posta elettronica ogni giorno. Se non viene gestito, il volume di messaggi generati e ricevuti giornalmente può "sommergere" gli utenti, influenzare negativamente la loro produttività ed esporre l'organizzazione a dei rischi. Di conseguenza, la gestione del ciclo di vita dei messaggi di posta elettronica è una componente fondamentale per la maggior parte delle organizzazioni.

Gestione record di messaggistica è la tecnologia per la gestione dei record di Exchange Server 2013 e Exchange Online che consente alle organizzazioni di gestire il ciclo di vita dei messaggi di posta elettronica e ridurre i rischi legali ad essa associati. La distribuzione della funzionalità Gestione record di messaggistica può contribuire a migliorare la gestione dell'organizzazione in diversi modi:

  - **Soddisfare i requisiti aziendali**   In base ai criteri di messaggistica dell'organizzazione, potrebbe essere necessario conservare alcuni messaggi di posta elettronica per un determinato periodo. Ad esempio, la cassetta postale di un utente potrebbe contenere messaggi essenziali relativi alla strategia aziendale, alle transazioni e allo sviluppo di prodotti o alle interazioni con i clienti.

  - **Soddisfare i requisiti legali e normativi**   Numerose organizzazioni hanno un requisito legale o normativo a cui attenersi che prevede l'archiviazione dei messaggi per un determinato periodo di tempo e la loro rimozione una volta terminato quel periodo. Archiviare i messaggi per un periodo di tempo superiore a quello richiesto potrebbe aumentare i rischi legali e finanziari per l'organizzazione.

  - **Aumentare la produttività degli utenti**   Se non gestito correttamente, il costante aumento del volume di messaggi di posta elettronica nelle cassette postali degli utenti può influire negativamente sulla loro produttività. Ad esempio, anche se, quando vengono ricevute, le sottoscrizioni ai notiziari e alle notifiche automatiche, potrebbero avere valore informativo, gli utenti potrebbero non eliminarle dopo averle lette (spesso non vengono neanche mai lette). Molti di questi tipi di messaggi non vengono memorizzati per più di alcuni giorni. L'utilizzo della funzionalità Gestione record di messaggistica per eliminare questi messaggi potrebbe contribuire a ridurre la quantità di informazioni nelle cassette postali degli utenti, aumentandone in tal modo la produttività.

  - **Migliorare la gestione dell'archiviazione**   A causa delle aspettative legate ai servizi di posta elettronica di tipo consumer completamente gratuiti, sono sempre più numerosi gli utenti che scelgono di conservare i messaggi per lunghi periodi di tempo o addirittura di non rimuoverli mai. Conservare cassette postali di grandi dimensioni è un'usanza sempre più diffusa e gli utenti non dovrebbero essere forzati a modificare le loro abitudini lavorative per rispettare delle quote particolarmente restrittive. Tuttavia, conservare i messaggi oltre il periodo di archiviazione necessario per motivi aziendali, legali o normativi potrebbe aumentare i costi di archiviazione.

La funzionalità Gestione record di messaggistica offre la flessibilità necessaria per implementare il criterio di gestione dei record più adatto ai requisiti dell'organizzazione. Con una buona comprensione delle funzionalità di Gestione record di messaggistica, Archivio locale e Conservazione locale, è possibile gestire l'archiviazione delle cassette postali e nel contempo soddisfare i requisiti normativi di conservazione.

Per informazioni sulle attività di gestione relative a MRM? vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Gestione record di messaggistica in Exchange Server 2013 ed Exchange Online

In Exchange Server 2013 e Exchange Online, la funzionalità Gestione record di messaggistica viene eseguita con i tag di conservazione e i criteri di conservazione. I tag di conservazione vengono utilizzati per applicare le impostazioni di conservazione a un'intera cassetta postale e alle cartelle delle cassette postali predefinite, quali Posta in arrivo e Posta eliminata. È anche possibile creare e distribuire tag di conservazione che gli utenti di Outlook 2010 e versioni successive e Outlook Web App potranno applicare alle cartelle o ai singoli messaggi. Dopo essere stati creati, i tag di conservazione vengono aggiunti a un criterio di conservazione che a sua volta viene poi applicato agli utenti. L'Assistente cartelle gestite elabora le cassette postali e applica le impostazioni di conservazione nel criterio di conservazione dell'utente. Per ulteriori informazioni sui criteri di conservazione, vedere [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md).

Quando un messaggio raggiunge il termine del periodo di conservazione specificato nel tag di conservazione più adatto, l'Assistente cartelle gestite esegue l'attività di conservazione specificata nel tag. I messaggi possono essere eliminati con la possibilità di recuperarli oppure eliminati definitivamente. Se all'utente viene fornito un archivio, è possibile utilizzare i tag di conservazione anche per spostare gli elementi nell'archivio in locale dell'utente.

## Strategie di Gestione record di messaggistica

È possibile utilizzare i criteri di conservazione per forzare la conservazione dei messaggi di base nell'intera cassetta postale o in cartelle predefinite specifiche. Anche se ci sono diverse strategie per la distribuzione di Gestione record di messaggistica, le più comuni sono le seguenti:

**Rimuovere tutti i messaggi dopo un periodo specificato**   In questa strategia, viene implementato un unico criterio di Gestione record di messaggistica che rimuove tutti i messaggi dopo un determinato periodo. In questa strategia, non c'è nessuna classificazione dei messaggi. Questo criterio può essere implementato tramite la creazione di un unico tag del criterio predefinito per la cassetta postale. Tuttavia, questa soluzione non garantirà la conservazione dei messaggi per il tempo specificato. Gli utenti possono sempre eliminare i messaggi prima che venga raggiunto il periodo di conservazione.

**Spostare i messaggi nelle cassette postali di archiviazione**   In questa strategia, si implementano i criteri di Gestione record di messaggistica che spostano gli elementi sulla cassetta postale di archiviazione dell'utente. Una cassetta postale di archiviazione fornisce agli utenti uno spazio di archiviazione aggiuntivo dove conservare contenuti non aggiornati o a cui si accede di rado. I tag di conservazione che spostano gli elementi sono chiamati anche *criteri di conservazione*. Nello stesso criterio di conservazione, è possibile combinare un tag del criterio predefinito con dei tag personali per spostare gli elementi e un tag del criterio predefinito con dei tag dei criteri di conservazione e dei tag personali per eliminare gli elementi. Per ulteriori informazioni sui criteri di archiviazione, vedere:

  - **Exchange Server 2013:**  [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:**  [Cassette postali di archiviazione in Exchange Online](https://technet.microsoft.com/it-it/library/dn922147\(v=exchg.150\))


> [!NOTE]
> In una distribuzione ibrida di Exchange, è possibile configurare una cassetta postale di archiviazione basata su cloud per una cassetta postale principale locale. Se si assegnano criteri di archiviazione a una cassetta postale locale, gli elementi vengono spostati nell'archivio basato su cloud. Se un elemento viene spostato nella cassetta postale di archiviazione, non ne viene mantenuta una copia nella cassetta postale locale. Se la cassetta postale locale viene messa in attesa, i criteri di archiviazione sposteranno comunque gli elementi nella cassetta postale di archiviazione basata su cloud in cui vengono mantenuti per la durata specificata dal blocco.



**Rimuovere i messaggi in base al percorso della cartella**   In questa strategia, si implementano i criteri di Gestione record di messaggistica basati sulla collocazione del messaggio di posta elettronica. Ad esempio, è possibile specificare che i messaggi che si trovano in posta in arrivo vengano conservati per un anno e i messaggi che si trovano nella cartella Posta indesiderata vengano conservati per 60 giorni. È possibile implementare questo criterio utilizzando una combinazione di tag dei criteri di conservazione per ciascuna cartella predefinita per la quale si desidera configurare un tag del criterio predefinito per l'intera cassetta postale. Il tag dei criteri predefiniti si applica a tutte le cartelle personalizzate e a tutte le cartelle predefinite a cui non è applicato un tag dei criteri di conservazione.


> [!NOTE]
> In Exchange 2013, è possibile creare tag dei criteri di conservazione per le cartelle Calendario e Attività. Se non si desidera che gli elementi in queste cartelle o in altre cartelle predefinite scadano, è possibile creare un tag di conservazione disabilitato per queste cartelle predefinite.



**Consentire agli utenti di classificare i messaggi**   In questa strategia, si implementano i criteri di Gestione record di messaggistica che includono un'impostazione di conservazione di base per tutti i messaggi, ma consentono agli utenti di classificare i messaggi sulla base di requisiti normativi o aziendali. In questo caso, gli utenti diventano una parte importante della strategia di gestione dei record utilizzata - spesso hanno la miglior comprensione di un valore di conservazione dei messaggi.

Gli utenti possono applicare diverse impostazioni di conservazione ai messaggi che è necessario conservare per periodi più lunghi o più brevi. È possibile implementare questo criterio utilizzando una combinazione di:

  - Un tag del criterio predefinito per la cassetta postale

  - Tag personali che l'utente può applicare a cartelle personalizzate o a singoli messaggi

  - (Facoltativo) Altri tag del criterio di conservazione per assegnare una scadenza agli elementi in specifiche cartelle predefinite

Ad esempio, è possibile utilizzare un criterio di conservazione con tag personali che hanno un periodo di conservazione più breve (ad esempio, due giorni, una settimana o un mese) e tag personali con un periodo di conservazione più lungo (ad esempio, un anno, due anni, cinque anni). Gli utenti possono applicare tag personali con periodi di conservazione più brevi per elementi come sottoscrizioni ai notiziari che potrebbero perdere valore dopo alcuni giorni dal ricevimento e applicare le tag con periodi più lunghi per conservare gli elementi che hanno un elevato valore aziendale. È inoltre possibile automatizzare il processo utilizzando le regole Posta in arrivo in Outlook per applicare un tag personale ai messaggi che rispondono alle condizioni di una regola.

**Mantenere i messaggi per scopi legati a eDiscovery**   In questa strategia, si implementano i criteri Gestione record di messaggistica che rimuovono i messaggi dalle cassette postali dopo un periodo specificato ma li conservano anche nella cartella Elementi ripristinabili agli scopi di [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md), anche se i messaggi sono stati eliminati dall'utente o da un altro processo.

È possibile soddisfare questo requisito utilizzando una combinazione di criteri di conservazione e [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md) o un blocco per controversia legale. I criteri di conservazione rimuovono i messaggi dalla cassetta postale dopo il periodo specificato. Il blocco sul posto con scadenza o il blocco per controversia legale conserva i messaggi eliminati o modificati entro quel periodo. Ad esempio, per conservare i messaggi per sette anni, è possibile creare un criterio di conservazione con un tag del criterio predefinito che elimina i messaggi dopo sette anni e un blocco per controversia legale per conservare i messaggi per sette anni. I messaggi che non sono stati rimossi dagli utenti verranno eliminati dopo sette anni, mentre quelli rimossi dagli utenti prima del periodo di sette anni verranno conservati nella cartella Elementi ripristinabili per sette anni. Per ulteriori informazioni su questa cartella, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

Facoltativamente è possibile utilizzare tag del criterio di conservazione e tag personali per consentire agli utenti di pulire le cassette postali. Tuttavia, il blocco sul posto e il blocco per controversia legale continuano a conservare i messaggi eliminati fino alla scadenza del periodo.


> [!NOTE]
> Un blocco sul posto con scadenza o un blocco per controversia legale è simile a quello che veniva comunemente chiamato <EM>blocco a fini giudiziari</EM> in Exchange 2010. Il blocco a fini giudiziari è stato implementato configurando il periodo di conservazione degli elementi eliminati per un database delle cassette postali o una singola cassetta postale. Tuttavia, la conservazione degli elementi eliminati conserva gli elementi eliminati e modificati sulla base della data di eliminazione. Il blocco sul posto e il blocco per controversia legale conservano gli elementi sulla base della data in cui sono stati ricevuti o creati. Ciò garantisce che i messaggi vengano conservati per almeno il periodo specificato.



## Ulteriori informazioni

[Record di messaggistica terminologia relativa alla gestione di Exchange 2013](messaging-records-management-terminology-in-exchange-2013-exchange-2013-help.md)

[Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md)

