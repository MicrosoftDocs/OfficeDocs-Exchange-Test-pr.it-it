---
title: 'Importare un modello di criteri DLP personalizzato da un file: Exchange 2013 Help'
TOCTitle: Importare un modello di criteri DLP personalizzato da un file
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 50479838
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importare un modello di criteri DLP personalizzato da un file

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-08-09_

È possibile gestire le informazioni riservate tramite i criteri DLP importando un file che contiene le impostazioni di criteri informazioni. Modelli di criteri DLP possono essere sviluppati indipendentemente dal programma di Exchange come file XML. Tuttavia, è necessario che soddisfino i requisiti di formato specifico per il funzionamento. In alternativa, è possono importare criteri che vengono esportati da una versione precedente di Exchange in Microsoft Exchange Server 2013.


> [!WARNING]
> È opportuno abilitare i criteri DLP in modalità di test prima di eseguirli nell'ambiente di produzione vero e proprio. Durante i test, si consiglia di configurare delle cassette postali campione e di inviare dei messaggi di prova che richiamino i criteri di test in modo da poterne verificare i risultati.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Prevenzione della perdita di dati (DLP)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EAC per importare un modello di criteri DLP personalizzato da un file

Utilizzare la procedura seguente per importare un modello di criteri DLP personalizzato da un file. Per evitare confusione, specificare un nome univoco per ogni parte del criterio o regola quando si ha la possibilità di rendere disponibile il proprio nome.

1.  In EAC, individuare **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare clic sulla freccia accanto all'icona **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi fare clic su **Importa criteri**.

3.  Nella pagina **Importa criteri** completare i seguenti campi:
    
    1.  **Selezionare il file da importare**   Aggiungere il nome del file di criteri che si desidera installare.
    
    2.  **Nome**   Aggiungere un nome che consenta di distinguere questo criterio dagli altri.
    
    3.  **Descrizione**   Aggiungere una descrizione facoltativa che riassuma il criterio.
    
    4.  **Altre opzioni**   Selezionare la modalità o lo stato per questo criterio. Il nuovo criterio non viene abilitato in toto fino a una richiesta specifica. La modalità predefinita per un criterio è il test senza notifiche.
    
    5.  Fare clic su **Avanti** per convalidare e importare i criteri.

## Utilizzo della Shell per importare un modello di criteri DLP personalizzato da un file

In questo esempio consente di importare un file modello dei criteri DLP personalizzato nel file C:\\My Documents\\DLP la. Importazione di un insieme di criteri DLP da un file XML consente di rimuovere o sovrascrive tutti i criteri DLP esistenti che sono stati definiti all'interno dell'organizzazione. Assicurarsi di avere una copia di backup della raccolta di criteri DLP corrente prima di importare e sovrascrivere i criteri DLP correnti.

    Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

