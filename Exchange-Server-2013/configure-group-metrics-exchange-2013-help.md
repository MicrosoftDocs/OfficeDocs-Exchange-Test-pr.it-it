---
title: 'Configurare le metriche di gruppo: Exchange 2013 Help'
TOCTitle: Configurare le metriche di gruppo
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 50481000
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le metriche di gruppo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

I suggerimenti messaggio che forniscono informazioni sulla dimensione dei gruppi di distribuzione e dei gruppi di distribuzione dinamici si basano sui dati della metrica di gruppo. I dati della metrica di gruppo vengono generati sui server Cassette postali. Per ulteriori informazioni sulla metrica di gruppo, vedere [Metriche del gruppo e i suggerimenti messaggio](group-metrics-and-https://docs.microsoft.com/it-it/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips).

È possibile abilitare o disabilitare la generazione della metrica del gruppo su un server Cassette postali.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Metrica del gruppo" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - I dati della metrica del gruppo vengono utilizzati solo per i suggerimenti messaggio. Verificare che nell'organizzazione siano stati abilitati i suggerimenti messaggio della metrica del gruppo. Per la procedura dettagliata, vedere [Gestire i suggerimenti per le relazioni dell'organizzazione](https://docs.microsoft.com/it-it/exchange/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Abilitazione o disabilitazione della creazione dei dati della metrica del gruppo tramite Shell


> [!NOTE]
> Per impostazione predefinita, i dati della metrica del gruppo vengono creati sullo stesso server su cui viene creata la Rubrica offline. Questi esempi sono necessari solo per le organizzazioni che non utilizzano le Rubriche offline.



Per abilitare o disabilitare la generazione della metrica di gruppo su un server Cassette postali, utilizzare il seguente comando:

```powershell
Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>
```

In questo esempio viene abilitata la generazione della metrica di gruppo sul server Cassette postali denominato MBX1.

```powershell
Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente abilitato o disabilitato la generazione della metrica di gruppo in un'organizzazione che non utilizza le Rubriche offline, fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
        Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration
    ```

2.  Verificare che l'impostazione visualizzata sia quella che è stata configurata.

