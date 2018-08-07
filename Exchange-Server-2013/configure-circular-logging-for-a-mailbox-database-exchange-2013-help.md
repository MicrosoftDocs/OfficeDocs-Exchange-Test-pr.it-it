---
title: 'Configura registrazione circolare database cassette postale:Exchange 2013 Help'
TOCTitle: Configurare la registrazione circolare per un database di cassette postale
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la registrazione circolare per un database di cassette postale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-06-24_

Quando si abilita la registrazione circolare per un database di cassette postali, il tipo di registrazione circolare che si ottiene dipende dalla replica o meno del database di cassette postali tramite replica continua:

  - Se il database di cassette postali non viene replicato, utilizzerà la registrazione circolare JET. In questo caso, l'abilitazione o la disabilitazione della registrazione circolare JET richiede che il database venga smontato e montato.

  - Se viene replicato il database di cassette postali, utilizzerà la registrazione circolare a replica continua (CRCL). In questo caso, l'attivazione o la disattivazione di CRCL ha effetto in modo dinamico; non è necessario smontare e rimontare il database.

Per ulteriori informazioni sulla registrazione circolare e su CRCL, vedere [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni del database delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

## Utilizzare l'interfaccia di amministrazione di Exchange per configurare la registrazione circolare di un database

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **database**.

2.  Selezionare il database di cassette postali che si desidera configurare, quindi fare clic su ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Selezionare o deselezionare la casella di controllo **Attiva registrazione circolare**, quindi fare clic su **salva**.

4.  Se viene richiesto di eseguire un'operazione di smontaggio e montaggio, viene visualizzato un messaggio di avviso. Fare clic su **OK** per chiudere il messaggio di avviso.
    
    1.  Per smontare il database, fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi su **Smonta**. Fare clic su **sì** quando viene visualizzato il messaggio di avviso.
    
    2.  Per montare il database, fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi su **Monta**. Fare clic su **sì** quando viene visualizzato il messaggio di avviso.

## Utilizzare la shell per configurare la registrazione circolare di un database

In questo esempio viene attivata la registrazione circolare del database DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $True

In questo esempio viene disattivata la registrazione circolare del database DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $False

Consultare [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)) per visualizzare altri parametri del database di cassette postali che è possibile configurare.

