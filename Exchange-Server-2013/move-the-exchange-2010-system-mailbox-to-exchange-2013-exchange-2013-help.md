---
title: 'Spostare la cassetta postale di sistema di Exchange 2010 in Exchange 2013: Exchange 2013 Help'
TOCTitle: Spostare la cassetta postale di sistema di Exchange 2010 in Exchange 2013
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54915151
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Spostare la cassetta postale di sistema di Exchange 2010 in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

In Exchange 2010 la cassetta postale di sistema di Microsoft Exchange è una cassetta postale di arbitraggio utilizzata per archiviare i dati relativi all'intera organizzazione, ad esempio i registri di controllo dell'amministratore, i metadati relativi alle ricerche eDiscovery e i dati di messaggistica unificata quali menu, dial plan e saluti personalizzati. La cassetta postale di sistema di Microsoft Exchange è denominata **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** e il nome visualizzato è **Microsoft Exchange**.

Quando si esegue l'aggiornamento dell'organizzazione di Exchange 2010 esistente a Exchange 2013, è necessario spostare la cassetta postale di sistema di Microsoft Exchange in un database delle cassette postali su un server Cassette postali di Exchange 2013. È necessario spostare la cassetta postale dopo avere installato e verificato Exchange 2013. Se la cassetta postale di sistema non viene spostata in Exchange 2013, la coesistenza di Exchange 2010 e Exchange 2013 nell'organizzazione di Exchange determina i seguenti problemi:

  - Le attività Exchange 2013 non vengono salvate nel registro di controllo dell'amministratore. Quando si esegue il cmdlet **Search-AdminAuditLog** o si tenta di esportare il registro di controllo dell'amministratore nell'interfaccia di amministrazione di Exchange, verrà visualizzato un messaggio di errore in cui si comunica che non è possibile creare una ricerca nel registro di controllo dell'amministratore perché la cassetta postale di sistema, SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, si trova su un server che non sta eseguendo Exchange 2013. Ogni volta che si esegue un comando, inoltre, nel registro applicazioni di Windows viene registrato un errore di Microsoft Exchange con ID evento 5000.

  - Non è possibile eseguire ricerche eDiscovery utilizzando Shell o l'interfaccia di amministrazione di Exchange in Exchange 2013. È possibile creare e mettere in coda ricerche nelle cassette postali, ma non è possibile avviarle. Nel registro di Microsoft Exchange Management viene registrato un errore con ID evento 6 in cui viene indicato che il cmdlet **Start-MailboxSearch** ha avuto esito negativo. È tuttavia possibile eseguire ricerche nelle cassette postali utilizzando Shell e il Pannello di controllo di Exchange (ECP) in Exchange 2010.

È necessario anche spostare la cassetta postale di sistema di Microsoft Exchange in Exchange 2013, come parte dell'aggiornamento di Messaggistica unificata di Exchange 2010 a Exchange 2013.

Per ulteriori informazioni sull'aggiornamento a Exchange 2013, vedere i seguenti argomenti:

  - [Aggiornamento da Exchange 2007 a Exchange 2010](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Aggiornamento dalla messaggistica unificata di Exchange 2007 alla messaggistica unificata di Exchange 2010](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## Informazioni preliminari

  - Tempo stimato per il completamento: 20 minuti. Il tempo effettivo può variare a seconda delle dimensioni della cassetta postale di sistema.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di migrazione e spostamento delle cassette postali" in [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Eseguire il seguente comando in Exchange 2013 per ottenere l'identità e la versione dei server di Exchange e dei database delle cassette postali contenenti le cassette postali di sistema dell'organizzazione.
    
        Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    
    La proprietà **AdminDisplayVersion** indica la versione di Exchange in esecuzione sul server. Il valore `Version 14.x` indica Exchange 2010, mentre il valore `Version 15.x` indica Exchange 2013.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per spostare le cassette postali di sistema

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Migrazione**.

2.  Fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi fare clic su **Sposta su un altro database**.

3.  Nella pagina **Nuovo spostamento cassetta postale locale**, fare clic su **Seleziona gli utenti da spostare** e selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella pagina **Seleziona cassetta postale**, aggiungere la cassetta postale con le seguenti proprietà:
    
      - Il nome visualizzato è **Microsoft Exchange**.
    
      - L'alias dell'indirizzo di posta elettronica della cassetta postale è **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**.

5.  Scegliere **OK**, quindi scegliere **Avanti**.

6.  Nella pagina **Configurazione spostamento**, digitare il nome del batch di migrazione, quindi fare clic su **Sfoglia** accanto a **Database di destinazione**.

7.  Nella pagina **Selezione del database delle cassette postali**, aggiungere il database delle cassette postali in cui spostare la cassetta postale del sistema. Verificare che la versione del database delle cassette postali selezionata sia la 15.x, che indica che il database si trova su un server Exchange 2013.

8.  Scegliere **OK**, quindi scegliere **Avanti**.

9.  Nella pagina **Avvia batch** selezionare le opzioni per avviare e completare automaticamente la richiesta di migrazione, quindi fare clic su **Nuovo**.

## Utilizzo di Shell per spostare le cassette postali di sistema

Eseguire innanzitutto il seguente comando in Exchange 2013 per ottenere i nomi e le versioni di tutti i database delle cassette postali presenti nell'organizzazione.

    Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion

Una volta identificato il nome dei database delle cassette postali dell'organizzazione, eseguire il seguente comando in Exchange 2013 per spostare la cassetta postale di sistema di Microsoft Exchange in un database delle cassette postali ubicato in un server di Exchange 2013.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## Verifica dell'esito positivo dell'operazione

Per verificare il corretto spostamento della cassetta postale di sistema di Microsoft Exchange in un database delle cassette postali ubicato in un server di Exchange 2013, eseguire il seguente comando in Shell.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

Se il valore della proprietà **AdminDisplayVersion** è **Versione 15.x (Build xxx.x)**, viene verificato che la cassetta postale del sistema risieda in un database delle cassette postali ubicato in un server Exchange 2013.

Una volta spostata la cassetta postale del sistema Microsoft Exchange su Exchange 2013, sarà possibile eseguire correttamente le seguenti attività amministrative:

  - Eseguire il cmdlet **Search-AdminAuditLog**.

  - Esportare il registro di controllo dell'amministratore nell'interfaccia di amministrazione di Exchange.

  - Creare e avviare correttamente le ricerche eDiscovery utilizzando Shell o l'interfaccia di amministrazione di Exchange in Exchange 2013.

