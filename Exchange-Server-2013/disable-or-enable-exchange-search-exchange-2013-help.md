---
title: 'Disabilitazione e abilitazione di Ricerca di Exchange: Exchange 2013 Help'
TOCTitle: Disabilitazione e abilitazione di Ricerca di Exchange
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52063048
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitazione e abilitazione di Ricerca di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-05-07_

Per impostazione predefinita, il servizio Ricerca di Exchange è abilitato per tutti i nuovi database delle cassette postali e non necessita di alcuna configurazione aggiuntiva. Tuttavia, se si desidera interrompere l'indicizzazione del contenuto delle cassette postali da parte di Ricerca di Exchange, è possibile disabilitare questo servizio per i singole database delle cassette postali o per l'intero server Cassette postali.


> [!WARNING]
> La disabilitazione del servizio Ricerca di Exchange avrà un impatto sulla funzionalità e sulle prestazioni delle ricerche full-text eseguite dagli utenti usando Outlook in modalità online o i dispositivi Windows Mobile.<BR>Anche <A href="in-place-ediscovery-exchange-2013-help.md">eDiscovery sul posto</A> si basa su Ricerca di Exchange. Se si disabilita&nbsp;Ricerca di Exchange per il database di una cassetta postale o per un server Cassette postali, le ricerche di eDiscovery locale non restituiranno alcun messaggio dal database o dal server.



Per le attività di gestione aggiuntive correlate a Ricerca di Exchange, vedere [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 1 minuto

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - È possibile abilitare o disabilitare il servizio Ricerca di Exchange per i server o i database delle cassette postali, ma non per i singoli utenti delle cassette postali.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Per saperne di più

## Disabilitazione/abilitazione di Ricerca di Exchange per il database di una cassetta postale

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ricerca di Exchange" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare o disabilitare Ricerca di Exchange per un database di cassette postali.



Questo comando disabilita Ricerca di Exchange per il database di una cassetta postale denominata EXCH01:

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

Questo comando abilita Ricerca di Exchange per il database di una cassetta postale di nome EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)).

## Disabilitazione/abilitazione di Ricerca di Exchange per un server Cassette postali

Per disabilitare Ricerca di Exchange per un server Cassette postali, è necessario disabilitare e arrestare il servizio Ricerca di Microsoft Exchange. Analogamente, per abilitare Ricerca di Exchange per un server Cassette postali, è necessario abilitare e avviare il servizio Ricerca di Microsoft Exchange. Per fare ciò è possibile utilizzare la console Servizi o Shell.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione del servizio Ricerca di Microsoft Exchange su un server Cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

**Utilizzo della console Servizi**

1.  Andare a **Start** \> **Strumenti di amministrazione** \> **Servizi**.

2.  Nel riquadro dei dettagli **Servizi**, fare clic con il pulsante destro del mouse su **Ricerca di Microsoft Exchange** e selezionare **Proprietà**.

3.  Nella scheda **Generale**, nell'elenco **Tipo di avvio** selezionare **Disabilitato** per disabilitare il servizio o **Automatico** per avviarlo automaticamente.
    

    > [!NOTE]
    > Il tipo di avvio scelto ha effetto sul servizio al successivo tentativo di avvio: il servizio verrà avviato automaticamente dopo il riavvio del server o manualmente. Nel passo successivo, il servizio verrà interrotto o avviato manualmente.



4.  Fare clic su **Interrompi** per interrompere il servizio o su **Avvia** per avviarlo.

5.  Fare clic su **OK** per salvare le modifiche.

**Utilizzo di Shell**

Utilizzare i seguenti comandi per arrestare e disabilitare il servizio Ricerca di Microsoft Exchange.
```
Stop-Service MSExchangeFastSearch
```
```
Set-Service MSExchangeFastSearch -StartupType Disabled
```

Utilizzare i seguenti comandi per configurare il servizio Ricerca di Microsoft Exchange per l'avvio automatico e quindi avviare il servizio.
```
Set-Service MSExchangeFastSearch -StartupType Automatic
```
```
Start-Service MSExchangeFastSearch
```
