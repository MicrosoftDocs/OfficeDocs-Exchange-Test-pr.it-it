---
title: 'Config. criteri attiv. per copia database cassette postali: Exchange 2013 Help'
TOCTitle: Configurare i criteri di attivazione per una copia del database delle cassette postali
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 50480828
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare i criteri di attivazione per una copia del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-02_

L'*attivazione* è il processo di modifica di una copia di database delle cassette postali che da passiva diventa attiva. L'attivazione avviene automaticamente come parte di un'operazione di failover del server o del database e può essere eseguita manualmente da un amministratore come parte di un'operazione di cambiamento del server o del database. Bloccare il database per l'attivazione fa sì che il database non diventi la copia attiva durante un failover del server o del database.

Per informazioni sulle altre attività di gestione relative alle copie di database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzo dell'interfaccia di amministrazione di Exchange per la configurazione del criterio di attivazione di una copia del database delle cassette postali

1.  
    
    Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database da configurare.

3.  
    
    Nel riquadro Dettagli, sotto **Copie del database**, individuare la copia del database da configurare e fare clic su **Sospendi**.

4.  Facoltativamente, aggiungere un commento e selezionare la casella **Per attivare questa copia è necessario un intervento manuale**.

5.  Fare clic su **Salva** per salvare le modifiche alla configurazione della copia del database delle cassette postali.

## Utilizzo di Shell per la sospensione o la ripresa dell'attivazione di una copia del database

In questo esempio viene bloccata la copia del database DB1 sul server MBX2 per l'attivazione.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly
```

In questo esempio viene ripresa la copia del database DB1 sul server MBX2 per l'attivazione.

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX2
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)) o [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335220\(v=exchg.150\)).

## Utilizzo di Shell per la configurazione del criterio di attivazione di un server

In questo esempio, le copie del database sul server MBX2 vengono configurate come bloccate per l'attivazione.

```powershell
Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked
```

In questo esempio, le copie del database sul server MBX3 vengono configurate come bloccate per l'attivazione esterna al sito.

```powershell
Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly
```

In questo esempio, le copie del database sul server MBX4 vengono configurate come sbloccate per l'attivazione.

```powershell
Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)), [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335220\(v=exchg.150\)) e [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che il criterio di attivazione sia stato configurato correttamente, fare quanto segue:

  - In Shell, utilizzare il seguente comando per visualizzare le impostazioni di attivazione per una copia del database.
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended
```

  - In Shell, utilizzare il seguente comando per visualizzare le impostazioni di attivazione per un membro del gruppo di disponibilità del database.
    
    ```powershell
Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy
```

