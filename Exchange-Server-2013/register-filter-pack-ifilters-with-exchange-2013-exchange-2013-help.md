---
title: 'Registrazione dei IFilter di Filter Pack con Exchange 2013: Exchange 2013 Help'
TOCTitle: Registrazione dei IFilter di Filter Pack con Exchange 2013
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50555532
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione dei IFilter di Filter Pack con Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Le regole di trasporto con condizioni di scansione degli allegati eseguono l'estrazione del testo durante l'analisi del contenuto degli allegati. Exchange 2013 può eseguire la scansione dei tipi di allegato più comuni localmente. È possibile aggiungere ulteriori tipi di allegato registrando IFilters con Exchange 2013. In questo argomento, viene illustrato come registrare IFilters rilasciato da Microsoft e da fornitori di terze parti.

Una volta registrato un IFilter per un determinato tipo di file, le regole di trasporto con condizioni di elaborazione degli allegati saranno in grado di eseguire la scansione di tali allegati. Di conseguenza, questi tipi di file non attiveranno più la condizione *AttachmentIsUnsupported*.


> [!WARNING]
> Le procedure riportate in questo argomento prevedono la modifica del Registro di sistema sui propri server Exchange. La modifica non corretta del Registro di sistema può causare gravi problemi che potrebbero richiedere la reinstallazione del sistema operativo. Eventuali problemi derivanti dalla modifica non corretta del Registro di sistema potrebbero essere irrisolvibili. Prima di modificare il Registro di sistema, eseguire il backup di tutti i dati importanti.<BR>Tali procedure richiedono anche l'arresto e il riavvio del servizio Trasporto di Microsoft Exchange sui propri server Cassette postali.



Per le attività di gestione aggiuntive relative alle regole di trasporto, vedere [Gestire le regole di flusso di posta elettronica](https://docs.microsoft.com/it-it/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti per ogni server.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni di configurazione del server Exchange" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - È necessario eseguire le seguenti procedure su server su cui è già installato il ruolo del server Cassette postali di Exchange 2013. Se si aggiungono ulteriori server Cassette postali dopo aver eseguito queste procedure, è necessario eseguirle nuovamente sui server appena aggiunti.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Registrazione di Microsoft Office 2010 Filter Pack

Per impostazione predefinita, i seguenti tipi di file Office non sono supportati dalle regole di trasporto di Exchange:

  - Office OneNote

  - Office Publisher

Se si desidera supportare questi file, è necessario distribuire Microsoft Office 2010 Filter Pack. La funzionalità Filter Pack non viene distribuita durante l'installazione di Exchange 2013 e non è un prerequisito per la distribuzione.

## Distribuzione di Microsoft Office 2010 Filter Pack

La distribuzione di Office 2010 Filter Pack consiste in due passaggi principali:

  - Download e installazione di Filter Pack, che registra gli IFilter con Windows (Search).

  - Modifica del Registro di sistema affinché gli IFilters vengano registrati anche con Exchange 2013. Ciò consente a Exchange di supportare la scansione degli allegati per i formati file.


> [!IMPORTANT]
> È necessario eseguire questa procedura su tutti i server Cassette postali dell'organizzazione.



1.  Scaricare e salvare Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`) dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/?linkid=191548).

2.  Eseguire il file `FilterPack64bit.exe` sul proprio server Cassette postali e seguire le istruzioni per completare l'installazione.

3.  Avviare Editor del Registro di sistema e individuare la seguente sottochiave del registro:
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID
    ```

4.  Sotto **CLSID**, aggiungere una sottochiave per i file OneNote, come indicato di seguito:
    
    1.  Fare clic con il pulsante destro del mouse su **CLSID**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    2.  Modificare il nome della nuova chiave in `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.
    
    3.  Fare clic sulla chiave appena creata e impostare il valore **(Predefinito)** utilizzato per l'installazione di Office 2010 Filter Pack. Per impostazione predefinita, la funzionalità Filter Pack viene installato in `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll`.
    
    4.  Fare clic con il pulsante destro del mouse su **{B8D12492-CE0F-40AD-83EA-099A03D493F1}**, scegliere **Nuovo**, quindi fare clic su **Valore stringa**.
    
    5.  Denominare il nuovo valore della stringa `ThreadingModel` e impostarlo su `Both`.

5.  Sotto **CLSID**, aggiungere una sottochiave per i file Publisher, come indicato di seguito:
    
    1.  Fare clic con il pulsante destro del mouse su **CLSID**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    2.  Modificare il nome della nuova chiave in `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.
    
    3.  Fare clic sulla chiave appena creata e impostare il valore **(Predefinito)** utilizzato per l'installazione di Office 2010 Filter Pack. Per impostazione predefinita, la funzionalità Filter Pack viene installato in `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll`.
    
    4.  Fare clic con il pulsante destro del mouse su **{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}**, scegliere **Nuovo**, quindi fare clic su **Valore stringa**.
    
    5.  Denominare il nuovo valore della stringa `ThreadingModel` e impostarlo su `Both`.

6.  Individuare la seguente chiave del Registro di sistema:
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters
    ```

7.  Sotto **filtri**, aggiungere una sottochiave per le estensioni .one, come indicato di seguito.
    
    1.  Fare clic con il pulsante destro del mouse su **filtri**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    2.  Modificare il nome della nuova chiave in `.one`.
    
    3.  Fare clic sulla chiave appena creata e impostare il valore **(Predefinito)** su `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.

8.  Sotto **filtri**, aggiungere una sottochiave per le estensioni .pub, come indicato di seguito:
    
    1.  Fare clic con il pulsante destro del mouse su **filtri**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    2.  Modificare il nome della nuova chiave in `.pub`.
    
    3.  Fare clic sulla chiave appena creata e impostare il valore **(Predefinito)** su `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.

9.  Chiudere l'Editor del Registro di sistema.

10. Sul server Cassette postali, arrestare e, quindi, riavviare i seguenti servizi nell'ordine specificato:
    
    1.  Arrestare il Servizio di trasporto di Microsoft Exchange.
    
    2.  Arrestare il servizio di gestione del filtraggio di Microsoft.
    
    3.  Avviare il servizio di gestione del filtraggio di Microsoft.
    
    4.  Avviare il servizio di trasporto di Microsoft Exchange.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta registrazione degli IFilter Microsoft Office 2010 Filter Pack, effettuare le seguenti operazioni:

1.  Creare una regola di trasporto con le seguenti proprietà. Per istruzioni dettagliate su come creare le regole di trasporto, vedere [Gestire le regole di flusso di posta elettronica](https://docs.microsoft.com/it-it/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).
    
      - Il mittente è la propria cassetta postale.
    
      - Il contenuto di qualsiasi allegato include "Verifica di IFilter".
    
      - Generare un rapporto sull'incidente e inviarlo alla cassetta postale.

2.  Creare un file OneNote file contenente la frase "Verifica di IFilter", allegarlo a un nuovo messaggio di posta elettronica e inviarlo al proprio indirizzo di posta elettronica.

3.  Verificare di aver ricevuto un rapporto sull'incidente per le regole di trasporto per la regola appena creata. Ciò conferma che il motore delle regole è stato in grado di analizzare il contenuto del file OneNote.

4.  Ripetere i passaggi 2 e 3 con un file Publisher.

## Registro di IFilter di terze parti per il supporto di ulteriori formati file

È possibile estendere la funzionalità di scansione degli allegati per ulteriori tipi di file registrando IFilters di terze parti aggiuntivi. È possibile aggiungere il supporto per altri file installando e registrando IFilter del tipo di file su ciascun server Cassette postali.


> [!IMPORTANT]
> Microsoft non ha verificato gli IFilter di terze parti con regole di trasporto, pertanto, si consiglia di distribuire e verificare tutti gli IFilter di terze parti in un ambiente di testing prima di distribuirli nel proprio ambiente di produzione.



## Distribuzione di Adobe PDF IFilter

Questa procedura viene illustrato come distribuire [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) per supportare l'elaborazione di allegati PDF nelle regole di trasporto.


> [!NOTE]
> Per impostazione predefinita, Exchange 2013 supporta la scansione di file PDF nelle regole di trasporto. In questo caso, l'esempio di PDF viene utilizzato semplicemente per illustrare come sia possibile estendere il supporto di ulteriori tipi di file utilizzando gli IFilter di terze parti.



1.  Scaricare [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025)e quindi seguire le istruzioni di installazione.

2.  Avviare Editor del Registro di sistema e individuare la seguente sottochiave:
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID
    ```

3.  Sotto **CLSID**, aggiungere una sottochiave per i file PDF, come indicato di seguito:
    
    1.  Fare clic con il pulsante destro del mouse su **CLSID**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    2.  Modificare il nome della nuova chiave in `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.
        

        > [!NOTE]
        > Ogni IFilter ha un ID di classe univoco (CLSID). È possibile individuare il CLSID nella documentazione di installazione per l'IFilter che si sta registrando o ricercando l'estensione file sotto la chiave <CODE>HKEY_CLASSES_ROOT\CLSID</CODE> nel Registro di sistema.

    
    3.  Fare clic sulla chiave appena creata e impostare il valore **(Predefinito)** utilizzato per l'installazione di PDF IFilter. Per impostazione predefinita, PDF IFilter viene installato in `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll`.

4.  Individuare la seguente chiave del Registro di sistema:
    
    ```powershell
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters
    ```

5.  Sotto **filtri**, aggiungere una sottochiave per le estensioni. pdf, come indicato di seguito:
    
    1.  Fare clic con il pulsante destro del mouse su **filtri**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    2.  Modificare il nome della nuova chiave in `.pdf`.
    
    3.  Fare clic sulla chiave appena creata e impostare il valore **(Predefinito)** su `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.

6.  Chiudere l'Editor del Registro di sistema.

7.  Sul server Cassette postali, arrestare e riavviare i seguenti servizi nell'ordine specificato:
    
    1.  Arrestare il Servizio di trasporto di Microsoft Exchange.
    
    2.  Arrestare il servizio di gestione del filtraggio di Microsoft.
    
    3.  Avviare il servizio di gestione del filtraggio di Microsoft.
    
    4.  Avviare il servizio di trasporto di Microsoft Exchange.

## Come verificare se l'operazione ha avuto esito positivo?

Utilizzare la stessa procedura riportata nella precedente sezione How do you know this worked? di questo argomento, sostituendo i file Publisher con file Adobe PDF.

## Ulteriori informazioni

[Utilizzare le regole di trasporto per esaminare messaggi con allegati](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Azioni della regola di trasporto](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

