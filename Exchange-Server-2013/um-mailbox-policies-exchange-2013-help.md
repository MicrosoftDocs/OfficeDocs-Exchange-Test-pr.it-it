---
title: 'Criteri cassetta postale di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Criteri cassetta postale di messaggistica unificata
ms:assetid: dfae629e-ee89-4494-a3ed-9655b67eb87e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124909(v=EXCHG.150)
ms:contentKeyID: 50555704
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri cassetta postale di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-15_

I criteri cassetta postale di messaggistica unificata sono richiesti quando vengono abilitati utenti al servizio Messaggistica unificata. Vengono creati per applicare un insieme comune di criteri o impostazioni di protezione a un insieme di cassette postali degli utenti delle caselle vocali. I criteri cassetta postale di messaggistica unificata vengono utilizzati per specificare le impostazioni di messaggistica unificata come segue:

  - Criteri PIN

  - Restrizioni di composizione

  - Altre proprietà generali dei criteri cassetta postale di messaggistica unificata

Ad esempio, è possibile creare un criterio cassetta postale di messaggistica unificata per incrementare il livello di protezione del PIN riducendo il numero massimo di errori di accesso consentiti per un gruppo specifico di utenti abilitati alla messaggistica unificata, come i dirigenti.

## Criteri cassetta postale di messaggistica unificata

Prima di abilitare gli utenti alla messaggistica unificata, è necessario che almeno un criterio cassetta postale di messaggistica unificata sia stato creato. È possibile creare ulteriori criteri cassetta postale di messaggistica unificata per applicare un insieme comune di impostazioni per gruppi di utenti.

I criteri cassetta postale di messaggistica unificata vengono creati utilizzando Exchange Management Shell o Interfaccia di amministrazione di Exchange (EAC). Per impostazione predefinita, ogni volta che si crea un dial plan di messaggistica unificata viene creato un singolo criterio cassetta postale di messaggistica unificata. Il nuovo criterio cassetta postale di messaggistica unificata è associato automaticamente al dial plan di messaggistica unificata e parte del nome del dial plan sarà incluso nel nome visualizzato del criterio. È possibile modificare questo criterio cassetta postale di messaggistica unificata predefinito.

È possibile associare più utenti abilitati alla messaggistica unificata a un singolo criterio cassetta postale di messaggistica unificata. La cassetta postale di ogni utente abilitato alla messaggistica unificata deve tuttavia essere collegata a un singolo criterio cassetta postale di messaggistica unificata. Questo consente di controllare le impostazioni di sicurezza PIN, quali il numero minimo di cifre in un PIN o il numero massimo di tentativi di accesso per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. È inoltre possibile controllare le impostazioni del testo dei messaggi o le restrizioni di composizione per le stesse cassette postali abilitate alla messaggistica unificata.

