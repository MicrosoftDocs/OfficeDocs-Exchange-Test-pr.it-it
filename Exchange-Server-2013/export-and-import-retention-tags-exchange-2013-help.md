---
title: 'Esportare e importare i tag di conservazione: Exchange 2013 Help'
TOCTitle: Esportare e importare i tag di conservazione
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51407341
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esportare e importare i tag di conservazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-11-15_

Esistono vari scenari in cui può essere necessario esportare o importare i tag di conservazione, inclusi:

  - Applicare gli stessi criteri di conservazione in tutti i server in un'organizzazione a più foreste Exchange

  - Applicazione degli stessi criteri di conservazione in una distribuzione ibrida in cui alcune cassette postali risiedono nell'organizzazione Exchange locale e altre risiedono in Exchange Online.

  - Applicazione di criteri di conservazione in uno scenario di archiviazione Exchange, cui gli utenti locali Exchange 2010 o versione successive cassette postali dispongono di un archivio basato su cloud.

In questi scenari, l'Assistente cartelle gestite può elaborare correttamente un elemento a cui è stato applicato un tag di conservazione dopo che l'elemento o la cassetta postale è stata spostata in un'altra organizzazione.


> [!WARNING]
> Per mantenere i tag di conservazione e i criteri di conservazione sincronizzati tra le due organizzazioni, ogni volta che si apportano modifiche ai tag o ai criteri di conservazione nell'organizzazione di origine, è necessario eseguire questa procedura per esportare i tag e i criteri di conservazione ed importarli nell'organizzazione di destinazione.<BR>Non è possibile selezionare per l'esportazione tag o criteri di conservazione specifici. Lo script Export-RetentionTags.ps1 esporta tutti i tag e i criteri di conservazione da un'organizzazione.



Per altre attività di gestione relative a Gestione record di messaggistica, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Le procedure descritte in questo argomento dipendono da questi tre file nella cartella `%ExchangeInstallPath%Scripts` sul serverExchange:
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - Non è possibile selezionare per l'esportazione tag o criteri di conservazione specifici. Lo script Export-RetentionTags.ps1 esporta tutti i tag e i criteri di conservazione da un'organizzazione. Lo script Import-RetentionTags.ps1 importa tutti i tag e criteri di conservazione nel file XML importato, sostituendo tutti i tag e criteri di conservazione nell'organizzazione di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Passaggio 1: Esportare i tag di conservazione da un'organizzazione di Exchange locale

1.  Eseguire questo comando Exchange Management Shell per passare alla sottodirectory **script** nel percorso di installazione Exchange directory.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Eseguire lo script Export-RetentionTags.ps1 per esportare i tag di conservazione in un file .xml.
    

    > [!IMPORTANT]
    > Se l'importazione o esportazione dei tag di conservazione e criteri di conservazione in Exchange Online, devi collegare la sessione Windows PowerShell per Exchange Online. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/jj984289(v=exchg.150)">Connessione a Exchange Online tramite Remote PowerShell</A>.

    
        .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver esportato correttamente i tag e criteri di conservazione, effettuare le seguenti operazioni:

1.  Navigare al percorso specificato nel comando per esportare e verificare che il file XML con il nome specificato sia stato creato.

2.  In alternativa, è possibile aprire il file XML in un un editor di testo per esaminarne i contenuti.

## Passaggio 2: Importare i tag di conservazione in un'organizzazione di Exchange

1.  Eseguire questo comando Exchange Management Shell per passare alla directory sottodirectory **script** nel percorso di installazione Exchange.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Eseguire lo script Import-RetentionTags.ps1 per importare i tag di conservazione precedentemente esportati in un file XML.
    

    > [!IMPORTANT]
    > Se l'importazione o esportazione dei tag di conservazione e criteri di conservazione in Exchange Online, devi collegare la sessione Windows PowerShell per Exchange Online. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/jj984289(v=exchg.150)">Connessione a Exchange Online tramite Remote PowerShell</A>.

    

    > [!NOTE]
    > Quando si esegue questo script su Exchange Online, è possibile che venga chiesto di confermare che si desidera eseguire il software da un editore attendibile. Verificare che il nome del server di pubblicazione viene visualizzato come <CODE>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</CODE>e quindi fare clic su <STRONG>R</STRONG> per consentire lo script essere eseguito una volta o <STRONG>A</STRONG> eseguire sempre.

    
        .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver importato correttamente i tag e criteri di conservazione, effettuare le seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Gestione della conformità** \> **Tag di conservazione**, quindi verificare che i tag di conservazione siano stati correttamente importati. Andare a **Gestione della conformità** \> **Criteri di conservazione**, quindi verificare che i criteri di conservazione siano stati correttamente importati.

2.  Utilizzare i cmdlet **Get-RetentionPolicy** e **Get-RetentionPolicyTag** per verificare che siano stati creati i tag e i criteri. Per un esempio su come recuperare i tag di conservazione e criteri di conservazione, vedere gli esempi in [Get-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd298009\(v=exchg.150\)) e [Get-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd298086\(v=exchg.150\)).

