---
title: 'Testare una regola del flusso di posta elettronica: Exchange Online Protection Help'
TOCTitle: Testare una regola del flusso di posta elettronica
ms:assetid: 3d949e2a-8ba4-4261-8cfb-736fd2446ea1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn831862(v=EXCHG.150)
ms:contentKeyID: 63145424
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testare una regola del flusso di posta elettronica

 

_**Si applica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Ogni volta che si crea una regola del flusso di posta elettronica Exchange, noto anche come una regola di trasporto, è consigliabile testarlo prima di averla attivata. In questo modo, se si crea accidentalmente una condizione che non è esattamente ciò che desideri o interagisce con altre regole in modo imprevisto, non sarà necessario le conseguenze impreviste.


> [!IMPORTANT]
> Attendere 30 minuti dopo la creazione di una regola prima che il testing. Se si verifica subito dopo aver creato la regola, è possibile che si verifichi un comportamento coerente. Se si utilizza Exchange Server, sono presenti più server Exchange può essere anche superiore per tutti i server ricevere la regola.



## Passaggio 1: Creare una regola in modalità test

È possibile valutare le condizioni di una regola senza eseguire le azioni che influiscono su flusso di posta scegliendo una modalità di test. È possibile impostare una regola in modo da ottenere una notifica tramite posta elettronica ogni volta che la regola viene soddisfatta oppure è possibile esaminare la traccia dei messaggi per i messaggi che potrebbe essere corrispondono alla regola. Esistono due modalità di test:

  - **Verifica senza i suggerimenti sui criteri**    Utilizzare questa modalità insieme a un'azione rapporto operazioni non consentite ed è possibile ricevere un messaggio di posta elettronica ogni volta che un messaggio di posta elettronica corrispondente alla regola.

  - **Test con suggerimenti sui criteri**    Questa modalità è disponibile solo se si utilizza [Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) (DLP), disponibile con alcuni Exchange Online e Exchange Online Protection (EOP) piani di sottoscrizione. Con questa modalità, un messaggio viene impostato al mittente quando un messaggio che sta inviando corrisponde a un criterio, ma non le azioni del flusso di posta vengono eseguite.

Ecco cosa puoi trovare quando una regola viene soddisfatta se si include l'azione rapporto operazioni non consentite:

![Messaggio inviato quando viene rilevata la regola](images/Dn831862.c1a2db60-3fb9-4ddc-86d5-1757e2250f59(EXCHG.150).png "Messaggio inviato quando viene rilevata la regola")

Utilizzare la modalità di test con un'azione rapporto operazioni non consentite

1.  In Interfaccia di amministrazione di Exchange (EAC), andare a **flusso di posta** \> **regole**.

2.  Creare una nuova regola o selezionare una regola esistente e quindi scegliere **Modifica**.

3.  Scorrere fino alla sezione **scegliere una modalità per la regola** e quindi selezionare **Test senza suggerimenti sui criteri** o **Test con suggerimenti sui criteri**.

4.  Aggiungere un'azione rapporto operazioni non consentite:
    
    1.  Selezionare **Aggiungi azione** oppure, se non è visibile, selezionare **altre opzioni** e quindi selezionare **Aggiungi azione**.
    
    2.  Selezionare **incidente generazione di report e invialo a**.
    
    3.  Fare clic su **Selezionare una...** e selezionare se stessi o un utente.
    
    4.  Selezionare **Includi proprietà del messaggio** e quindi selezionare le proprietà del messaggio che si desidera includere nel messaggio di posta elettronica che viene visualizzato. Se non viene selezionato alcun si ricevono un messaggio di posta elettronica quando la regola viene soddisfatta.

5.  Selezionare **Salva**.

## Passaggio 2: Valutare se la regola viene si intende

Per testare una regola, è possibile inviare sia sufficiente messaggi di prova per verificare che cosa si prevede che succede o visualizzare il messaggio di traccia per i messaggi che persone incluse nei invia organizzazione. Assicurarsi di valutare i tipi di messaggi seguenti:

  - Messaggi che si prevede di corrispondono alla regola

  - Messaggi non desiderati per la corrispondenza della regola

  - Messaggi inviati da e verso gli utenti dell'organizzazione

  - Messaggi inviati a e da utenti esterni all'organizzazione

  - Risposte ai messaggi che corrispondono alla regola

  - Messaggi che possono causare interazioni tra più regole

## Suggerimenti per l'invio di messaggi di prova

Per eseguire il test deve effettuare l'accesso di mittente e destinatario di un messaggio di prova.

  - Se non si dispone di più account di accesso all'interno dell'organizzazione, è possibile testare un [account di valutazione di Office 365](https://go.microsoft.com/fwlink/p/?linkid=402791) o creare pochi utenti fittizi temporanei nell'organizzazione.

  - Poiché un web browser in genere non è possibile disporre di sessioni aperte contemporaneamente nello stesso computer effettuato l'accesso a più account, è possibile utilizzare l' [Esplorazione InPrivate di Internet Explorer](https://go.microsoft.com/fwlink/p/?linkid=402784)o un altro computer, dispositivi o browser web per ogni utente.

## Esaminare la traccia dei messaggi

L'analisi del messaggio include una voce per ogni regola corrispondente per il messaggio e richiede una voce per ogni azione della regola. Ciò è utile per tenere traccia di cosa accade ai messaggi di prova, nonché per tenere traccia di cosa accade ai messaggi reali intermediazione nell'organizzazione.

![Traccia messaggi che visualizza azioni delle regole di trasporto](images/Dn831862.64179f28-5c8c-421b-b630-cc1f7de9a34f(EXCHG.150).png "Traccia messaggi che visualizza azioni delle regole di trasporto")

1.  In EAC, andare a **flusso di posta** \> **traccia dei messaggi**.

2.  Individuare i messaggi che si desidera traccia in base ai criteri, ad esempio il mittente e la data di invio. Per informazioni sull'impostazione di criteri, vedere [Esecuzione di Ritrova messaggio e Visualizza risultati](https://technet.microsoft.com/it-it/library/jj200712\(v=exchg.150\)).

3.  Dopo aver individuato il messaggio che si desidera traccia, fare doppio clic per visualizzarne i dettagli del messaggio.

4.  Cercare nella colonna di **evento** per la **regola di trasporto**. Nella colonna **azione** viene eseguita l'azione specifica.

## Passaggio 3: Al termine test, impostare la regola da applicare

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Flusso di posta** \> **Regole**.

2.  Selezionare una regola e quindi scegliere **Modifica**.

3.  Selezionare **Imponi**.

4.  Se è stato utilizzato per generare un rapporto sull'incidente un'azione, selezionare l'azione e quindi scegliere **Rimuovi**.

5.  Selezionare **Salva**.


> [!TIP]
> Per evitare causare risultati imprevisti, informare gli utenti sulle nuove regole.



## Suggerimenti sulla risoluzione dei problemi

Ecco alcuni problemi comuni e risoluzioni:

  - **Tutto il contenuto appaia corretto, ma non funziona la regola.**
    
    Occasionalmente impiegato più di 15 minuti per un nuovo flusso di posta elettronica sia disponibile. Attendere qualche ora e poi provare nuovamente. Verificare anche se potrebbe interferire un'altra regola. Provare a modificare la regola a livello di priorità 0 per lo spostamento all'inizio dell'elenco.

  - **Dichiarazione di non responsabilità viene aggiunto al messaggio originale e tutte le risposte, anziché solo per il messaggio originale.**
    
    Per evitare questo problema, è possibile aggiungere un'eccezione alla regola dichiarazione di non responsabilità per cercare una frase univoca nella dichiarazione di non responsabilità.

  - **La regola ha due condizioni e desidera che l'azione da eseguire quando si verifica una delle condizioni, ma solo viene confrontato quando vengono soddisfatte le condizioni.**
    
    È necessario creare due regole, uno per ogni condizione. Consente di copiare facilmente la regola selezionando **Copia** e quindi rimuovere una condizione da originale e l'altra condizione dalla copia.

  - **si lavora con i gruppi di distribuzione e** **Il mittente è** (**SentTo** ) **non sembra funzionare.**
    
    **SentTo** genera una corrispondenza per i messaggi in cui uno dei destinatari è una cassetta postale, utente abilitato alla posta o contatto, ma è possibile specificare un gruppo di distribuzione con tali condizioni. Utilizzare invece **per casella contiene un membro del gruppo** (**SentToMemberOf** ).

## Altre opzioni di test

Se si utilizza Exchange Online o Exchange Online Protection, è possibile controllare il numero di volte in cui che ogni regola viene soddisfatta utilizzando un rapporto sulle regole. Per poter essere incluse nei report, una regola deve disporre selezionata la casella di controllo **Controlla questa regola con livello di gravità**. Questi rapporti consentono di individuare le tendenze di utilizzo delle regole e identificare le regole che non sono associate.

Per visualizzare un report, le regole in interfaccia di amministrazione di Office 365, selezionare **rapporti**.


> [!NOTE]
> Mentre la maggior parte dei dati viene visualizzata nel rapporto entro 24 ore, per alcuni dati potrebbero essere necessari 5 giorni.



![Report che visualizza l'utilizzo della regola](images/Dn831862.df5bf202-741d-432a-b71d-b37143f0ec0a(EXCHG.150).png "Report che visualizza l'utilizzo della regola")

Per ulteriori informazioni, vedere [visualizzare i report di protezione posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Per informazioni dettagliate,

[Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md)

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Regole del flusso di posta (regole di trasporto in Exchange Online Protection](https://technet.microsoft.com/it-it/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server)

