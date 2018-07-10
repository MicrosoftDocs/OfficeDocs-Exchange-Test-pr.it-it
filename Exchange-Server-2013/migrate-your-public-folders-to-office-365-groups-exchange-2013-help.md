---
title: 'Eseguire la migrazione delle cartelle pubbliche nei gruppi di Office 365: Exchange 2013 Help'
TOCTitle: Eseguire la migrazione delle cartelle pubbliche nei gruppi di Office 365
ms:assetid: d89e727b-675a-4623-b572-260f8b44b966
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt843872(v=EXCHG.150)
ms:contentKeyID: 74468720
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire la migrazione delle cartelle pubbliche nei gruppi di Office 365

 

_**Si applica a:** Exchange Online, Exchange Server 2010, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-09-25_

**Sintesi:**  informazioni sui motivi per cui eseguire o non eseguire la migrazione delle cartelle pubbliche di Exchange ai gruppi di Office 365.

In questo articolo viene fornito un confronto tra le cartelle pubbliche e i gruppi di Office 365 e viene spiegato come l'una o l'altra soluzione potrebbe essere quella migliore per l'organizzazione. Le cartelle pubbliche sono state introdotte con Exchange, mentre i gruppi solo di recente. Se si desidera eseguire la migrazione di alcune o tutte le cartelle pubbliche ai gruppi, in questo articolo viene descritto il funzionamento di questo processo e vengono forniti collegamenti agli articoli che trattano la relativa procedura in modo dettagliato.

## Cosa sono le cartelle pubbliche?

[Cartelle pubbliche](public-folders-exchange-2013-help.md) contengono diversi tipi di dati e sono organizzate in una struttura gerarchica.

Le cartelle pubbliche non sono consigliate nelle seguenti situazioni:

  - **Archiviazione dati**. Gli utenti con limiti delle cassette postali talvolta utilizzano le cartelle pubbliche anziché le cassette postali per archiviare i dati. Questa pratica è sconsigliata perché influisce sulla quantità di dati archiviati nelle cartelle pubbliche e compromette l'obiettivo dei limiti delle cassette postali.

  - **Condivisione documenti e collaborazione**. Le cartelle pubbliche non forniscono funzioni di gestione dei documenti, come la funzione di controllo delle versioni, archiviazione ed estrazione controllata e la notifica automatica delle modifiche al contenuto.

## Cosa sono i gruppi di Office 365?

I gruppi di Office 365 consentono di scegliere un set di persone con cui si desidera collaborare e quindi di configurare facilmente una raccolta di risorse da condividere con tali persone. Non è necessario assegnare manualmente le autorizzazioni per quelle risorse perché l'aggiunta di membri al gruppo fornisce automaticamente ai membri le autorizzazioni necessarie per accedere agli strumenti e alle risorse forniti dal gruppo. I gruppi sono anche la nuova e migliorata esperienza per quelle attività che in precedenza erano gestite dalle liste di distribuzione e dalle cassette postali condivise.

Per informazioni dettagliate sullo sviluppo dei gruppi, vedere [Informazioni sui gruppi di Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521).

## È necessario eseguire la migrazione delle cartelle pubbliche nei gruppi di Office 365?

I gruppi di Office 365 rappresentano l'ultima offerta di collaborazione da parte di Microsoft, e ciò significa che ci sono molti motivi per cui sarebbero una soluzione da preferire alle cartelle pubbliche, una tecnologia molto meno recente. In Outlook, ad esempio, i gruppi possono sostituire completamente le cartelle pubbliche abilitate alla posta elettronica. La compilazione di un elenco di tutti gli scenari in cui i gruppi di Office 365 funzionano meglio delle cartelle pubbliche è impossibile, ma di seguito sono riportati quelli principali:

  - **Collaborazione tramite posta elettronica**. I gruppi di Outlook presentano uno spazio **Conversazioni** dedicato che consente di archiviare tutti i messaggi di posta elettronica e di collaborare con gli altri utenti. Il gruppo può anche essere configurato in modo da ricevere messaggi da persone esterne al gruppo o all'organizzazione. Se sono attualmente in uso cartelle pubbliche abilitate alla posta per l'archiviazione di discussioni correlate ai progetti, ad esempio, o di ordini di acquisto che devono essere visualizzati da un team, l'utilizzo dei gruppi sarebbe un miglioramento. I gruppi sono più adatti, inoltre, alle situazioni in cui si desidera semplicemente trasmettere informazioni a un set di utenti.

  - **Collaborazione tramite documenti**. In Outlook, i gruppi presentano una scheda **File** dedicata che consente di visualizzare tutti i file di un sito del team di SharePoint del gruppo, oltre agli allegati di posta elettronica. Si ottiene una visualizzazione di tutti i file, quindi non è necessario eseguire una ricerca dei file come si farebbe nelle cartelle pubbliche. Anche la creazione condivisa diventerebbe più semplice. Se si usano le cartelle pubbliche per l'archiviazione di file che dovrebbero essere utilizzati da più persone, si prenda in considerazione la migrazione ai gruppi.

  - **Calendario condiviso**. Al momento della creazione, ogni gruppo viene dotato di un calendario condiviso. Qualsiasi membro del gruppo può creare eventi in tale calendario. Quando si preferisce un gruppo, il rispettivo calendario può essere visualizzato insieme al calendario personale. È anche possibile sottoscriversi a un evento del gruppo, nel caso in cui gli eventi creati in tale gruppo vengano visualizzati nel calendario personale. Se si usano le cartelle pubbliche per ospitare calendari per il team, come una pianificazione o un orario, i gruppi offrirebbero un'esperienza migliorata.

  - **Autorizzazioni semplificate**. Quando si assegnano gli utenti a un gruppo, tali utenti ricevono immediatamente le autorizzazioni necessarie, mentre con le cartelle pubbliche è necessario assegnare manualmente le autorizzazioni appropriate. Gli utenti possono essere aggiunti come "proprietari" o "membri". I proprietari hanno diritti completi nel gruppo, inclusa la possibilità di eseguire operazioni di gestione del gruppo. Anche i membri possono creare contenuti e modificare i file come i proprietari, ma non possono eliminare i contenuti che non hanno creato. Se il modello di autorizzazioni delle cartelle pubbliche è troppo complesso e si desidera qualcosa di semplice e veloce, i gruppi di Office 365 sono la scelta migliore.

  - **Presenza su dispositivi mobili e Web**. Le cartelle pubbliche non possono essere utilizzate tramite dispositivi mobili e dispongono di un set limitato di funzionalità sul Web. I gruppi di Office 365, al contrario, sono accessibili tramite le app mobili di Outlook e presentano una serie di funzionalità sul Web più ampia. Se il team è in viaggio e necessita dell'accesso mobile, occorre utilizzare i gruppi di Office 365.

  - **Accesso a un'ampia gamma di app di Office 365**. Quando viene creato un gruppo, si sblocca l'accesso a un'ampia gamma di app offerte dalla famiglia di prodotti Office 365. Si ottiene un sito del team di SharePoint per l'archiviazione di file e una pianificazione su Planner per tenere traccia delle attività. I gruppi di Office 365 sono il servizio di appartenenza che combina gli elementi dell'intera famiglia di prodotti di Office 365.

I gruppi di Office 365 offrono innumerevoli vantaggi, ma è bene tenere presente che si riscontreranno alcune differenze fondamentali dopo aver lasciato l'esperienza delle cartelle pubbliche. Le differenze principali sono le seguenti:

  - **Gerarchia delle cartelle**. Mentre le cartelle pubbliche sono spesso utilizzate per organizzare i contenuti in una gerarchia completa, i gruppi di Office 365 hanno una struttura piatta. Tutti i messaggi di posta elettronica nel gruppo si trovano nello spazio Conversazioni e tutti i documenti vengono inseriti nella scheda **File**. Inoltre, non è possibile creare sottocartelle nei gruppi di Office 365.

  - **Ruoli di autorizzazione granulari**. Mentre le cartelle pubbliche sono dotate di una serie di ruoli di autorizzazione, i gruppi di Office 365 ne forniscono soltanto due: proprietario e membro.

Prima di passare ai gruppi, è opportuno prendere nota dei diversi limiti derivanti dalla creazione e dalla gestione dei gruppi. Vedere *Come si gestiscono i propri gruppi?* in [Informazioni sui gruppi di Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521) per ulteriori informazioni.

## Eseguire la migrazione delle cartelle pubbliche ai gruppi di Office 365

Se si decide di passare ai gruppi di Office 365, è possibile utilizzare un processo noto come *migrazione batch* per spostare il contenuto dei messaggi di posta elettronica e del calendario dalle cartelle pubbliche esistenti ai gruppi. La procedura specifica per l'esecuzione di una migrazione batch dipende dalla versione di Exchange che attualmente ospita la gerarchia delle cartelle pubbliche. Alla fine di questo articolo, sono disponibili collegamenti a istruzioni che illustrano il processo di migrazione batch.


> [!NOTE]
> Al termine della migrazione di una cartella pubblica abilitata alla posta elettronica a un gruppo particolare in Office 365, tutti i messaggi di posta elettronica indirizzati alla cartella pubblica in quel momento verranno ricevuti dal gruppo.



I vantaggi principali delle migrazioni batch sono:

  - **Migrazione basata sul servizio di replica delle cassette postali**. Il processo di migrazione utilizza i cmdlet di migrazione batch. La migrazione a più gruppi può essere avviata contemporaneamente in una singola migrazione batch. Sono disponibili anche script che semplificano il processo di migrazione.

  - **Sono supportate le cartelle pubbliche per i calendari e la posta elettronica**. I post e i messaggi di posta elettronica copiati vengono visualizzati nei gruppi come conversazioni di gruppo, mentre gli elementi del calendario copiati saranno visibili nei calendari di gruppo. Altri tipi di cartelle pubbliche, come attività e contatti, non sono attualmente supportati per questa migrazione.

  - **Le cartelle pubbliche locali possono essere migrate direttamente ai gruppi di Office 365**. Per questa migrazione non è necessario spostare prima le cartelle pubbliche in Office 365 e quindi passare ai gruppi. I cmdlet di copia dei dati del servizio di replica delle cassette postali leggono i dati delle cartelle pubbliche direttamente dall'ambiente locale e quindi copiano i dati nei gruppi di Office 365. Si noti che le cartelle pubbliche di Exchange 2010 richiedono un endpoint di Outlook via Internet. Le cartelle pubbliche di Exchange 2013 ed Exchange 2016 richiedono un endpoint basato sul proxy del servizio di replica delle cassette postali.

  - **Non una migrazione "tutto o niente"**. È possibile scegliere cartelle pubbliche specifiche per cui eseguire la migrazione ai gruppi, e solo di queste cartelle pubbliche verrà eseguita la migrazione.

  - **Copia di dati singola**. Le migrazioni batch sono progettate per essere una copia di dati singola dalle cartelle pubbliche di origine ai gruppi di destinazione, senza la complessità della sincronizzazione incrementale e della finalizzazione.

  - **I dati delle cartelle pubbliche vengono uniti ai dati esistenti in un gruppo**. La copia dei dati unisce il contenuto delle cartelle pubbliche a quello del gruppo esistente, se presente. Se è necessaria la copia dei dati incrementale, è possibile eseguire la copia dei dati tutte le volte che è necessario. Ciò consente di copiare i dati incrementali nel gruppo.

## Panoramica delle migrazioni batch

Nella seguente procedura viene descritto il processo generale di migrazione dei contenuti delle cartelle pubbliche ai gruppi di Office 365 in una migrazione batch. I dettagli specifici sono contenuti negli articoli elencati di seguito.

1.  **Seleziona origine:**  scegliere le cartelle pubbliche che si desidera migrare. È possibile scegliere qualsiasi cartella con contenuti del calendario o della posta elettronica.

2.  **Crea destinazione:**  creare i gruppi corrispondenti per le cartelle, con le configurazioni desiderate come membri, impostazioni della privacy e classificazione dei dati.

3.  **Copia dati:**  usare i cmdlet di migrazione batch per copiare i dati dalle cartelle pubbliche ai gruppi.

4.  **Blocca origine:**  bloccare le cartelle pubbliche dopo aver verificato i dati nei gruppi.

5.  **Completa:**  copiare i nuovi dati che sono stati creati tra i passaggi 3 e 4.

Le cartelle pubbliche e i gruppi corrispondenti rimangono disponibili online per gli utenti durante i passaggi 1-3 sopra descritti. Dopo il passaggio 3, è possibile stabilire se procedere o no con il resto della migrazione, in base all'esperienza dei gruppi, e se tale soluzione è adatta o no agli utenti e all'organizzazione. A questo punto, è possibile eseguire il rollback della migrazione e ripristinare le cartelle pubbliche. Se si procede con la migrazione, dopo aver completato il passaggio 5, è possibile eliminare le cartelle pubbliche originali. Anche dopo la migrazione è possibile eseguire il rollback alle cartelle pubbliche, purché siano stati salvati i file di backup dal processo di migrazione e non siano state eliminate le cartelle pubbliche originali.

## Prerequisiti di migrazione batch e istruzioni dettagliate

I prerequisiti seguenti sono necessari nell'ambiente Exchange per poter eseguire una migrazione batch. I prerequisiti specifici dipendono dalla versione di Exchange attualmente in esecuzione.

1.  Se le cartelle pubbliche sono in locale, i server devono eseguire una delle versioni seguenti:
    
      - Exchange 2010 SP3 RU8 o versione successiva
    
      - Exchange 2013 CU15 o versione successiva
    
      - Exchange 2016 CU4 o versione successiva

2.  Se le cartelle pubbliche sono in locale, è necessario configurare un ambiente ibrido di Exchange. Per ulteriori informazioni, vedere [Distribuzioni ibride di Exchange Server](https://technet.microsoft.com/it-it/library/jj200581\(v=exchg.150\)).

**Istruzioni di migrazione**

Selezionare il collegamento appropriato indicato di seguito per istruzioni dettagliate sull'esecuzione di una migrazione batch.

  - [Use batch migration to migrate Exchange Online public folders to Office 365 Groups](https://technet.microsoft.com/it-it/library/mt843871\(v=exchg.150\))

  - [Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2010 nei gruppi di Office 365](use-batch-migration-to-migrate-exchange-2010-public-folders-to-office-365-groups-exchange-2013-help.md)

  - [Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 nei gruppi di Office 365](use-batch-migration-to-migrate-exchange-2013-public-folders-to-office-365-groups-exchange-2013-help.md)

  - [Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2016 ai gruppi di Office 365](https://go.microsoft.com/fwlink/p/?linkid=859171)

