---
title: 'Sospende/riprende copia database cassette postali: Exchange 2013 Help'
TOCTitle: Sospendere o riprendere una copia del database delle cassette postali
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 50481245
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sospendere o riprendere una copia del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-02_

Potrebbe essere necessario sospendere o riprendere una copia del database per vari motivi, ad esempio per una manutenzione del disco contenente una copia del database o per la sospensione dell'attivazione di una singola copia del database a fini di ripristino di emergenza.

Per informazioni sulle altre attività di gestione correlate alle copie del database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzare EAC per sospendere una copia del database delle cassette postali

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database di cui si desidera sospendere la copia.

3.  Nel riquadro Dettagli, sotto **Copie database**, fare clic su **Sospendi** sotto la copia del database da sospendere.

4.  Nel campo **Commenti**, aggiungere un commento facoltativo di massimo 512 caratteri specificando il motivo della sospensione.

5.  Per sospendere la copia del database dall'attivazione automatica, selezionare la casella di controllo **Questa copia può essere attivata solo con un intervento manuale**.

6.  Fare clic su **Salva** per rimuovere la copia del database.

## Utilizzare EAC per riprendere una copia del database delle cassette postali

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database di cui si desidera riprendere la copia.

3.  Nel riquadro Dettagli, sotto **Copie database**, fare clic su **Riprendi** sotto la copia del database da riprendere.

4.  Fare clic su **Sì** per riprendere la copia del database.

## Sospensione di una copia del database delle cassette postali tramite Shell

In questo esempio viene sospesa la replica continua di una copia del database DB1 ospitata sul server MBX1. È stato, inoltre, specificato un commento opzionale.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False
```

In questo esempio viene sospesa l'attivazione di una copia del database DB2 ospitata sul server MBX2.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False
```

## Ripresa di una copia del database delle cassette postali tramite Shell

In questo esempio viene ripresa una copia del database DB1 sul server MBX1.

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX1
```

In questo esempio viene ripresa una copia del database DB2 sul server MBX2 solo per la replica.

```powershell
Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly
```

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta sospensione o ripresa di una copia del database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database appropriato e, nel riquadro Dettagli, fare clic su **Visualizza dettagli** per visualizzare le proprietà di copia del database.

  - Nella shell, eseguire il comando riportato di seguito per visualizzare le informazioni sullo stato per una copia del database.
    
    ```powershell
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```
