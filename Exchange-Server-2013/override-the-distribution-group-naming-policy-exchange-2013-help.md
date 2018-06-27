---
title: "Eseguire l'override del gruppo di distribuzione dei criteri di denominazione: Exchange 2013 Help"
TOCTitle: Eseguire l'override del gruppo di distribuzione dei criteri di denominazione
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 50479848
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire l'override del gruppo di distribuzione dei criteri di denominazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-13_

I criteri di denominazione dei gruppi per i gruppi di distribuzione sono applicati solo ai gruppi creati dagli utenti. Quando un amministratore utilizza Interfaccia di amministrazione di Exchange (EAC) per creare gruppi di distribuzione, i criteri di denominazione dei gruppi vengono ignorati e non vengono applicati al nome del gruppo.

Tuttavia, se si utilizza Exchange Management Shell per creare o rinominare un gruppo di distribuzione, i criteri di denominazione dei gruppi sono applicati anche ai gruppi creati dagli amministratori, a meno che non si utilizzi il parametro *IgnoreNamingPolicy* per eseguire l'override dei criteri di denominazione dei gruppi.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare Shell per eseguire l'override dei criteri di denominazione dei gruppi quando si crea un nuovo gruppo

Per eseguire l'override dei criteri di denominazione dei gruppi, eseguire il comando seguente.

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

Ad esempio, se i criteri di denominazione dei gruppi per l'organizzazione sono **DG\_\<Nome Gruppo\>\_Users**, eseguire il comando indicato di seguito per creare un gruppo denominato **All Administrators**:

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

Quando tramite Microsoft Exchange viene creato questo gruppo, viene utilizzato **All Administrators** per entrambi i parametri *Name* e *DisplayName*.

## Utilizzare Shell per eseguire l'override dei criteri di denominazione dei gruppi quando si rinomina un gruppo

Per eseguire l'override dei criteri di denominazione dei gruppi quando si rinomina un gruppo esistente con Shell, eseguire il comando indicato di seguito.

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

Ad esempio, si supponga che siano stati creati criteri di denominazione dei gruppi una sera tardi e il mattino successivo ci si rende conto di un errore ortografico nella stringa di testo nel prefisso. Il mattino successivo, si vedrà che è già stato creato un nuovo gruppo con il prefisso contenente l'errore ortografico. È possibile correggere i criteri di denominazione dei gruppi in EAC, ma è necessario utilizzare Shell per rinominare il gruppo con il nome sbagliato. Eseguire il comando riportato di seguito.

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy


> [!IMPORTANT]
> Assicurarsi di includere il parametro <EM>DisplayName</EM> quando si rinomina un gruppo. In caso contrario, verrà visualizzato ancora il vecchio nome nella rubrica condivisa e nelle righe A, Cc e Da nei messaggi di posta elettronica.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione o ridenominazione di un gruppo di distribuzione dinamico che ignora i criteri di denominazione dei gruppi, eseguire i seguenti comandi.

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

Se il formato del nome visualizzato per il gruppo è diverso da quello imposto dal criterio di denominazione dei gruppi dell'organizzazione, l'operazione ha avuto esito positivo.

