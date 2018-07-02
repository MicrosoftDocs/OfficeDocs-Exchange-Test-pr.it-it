---
title: 'Gestione dei domini remoti: Exchange 2013 Help'
TOCTitle: Gestione dei domini remoti
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52057234
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: MT
---

# Gestione dei domini remoti

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-13_

I domini remoti rappresentano i domini SMTP esterni all'organizzazione Microsoft Exchange. È possibile creare voci dei domini remoti per definire le impostazioni per il trasferimento dei messaggi tra l'organizzazione di Exchange e i domini esterni specifici. Le impostazioni della voce di dominio remoto di un dominio esterno specifico sostituiscono le impostazioni del dominio remoto predefinito che normalmente vengono applicate a tutti i destinatari esterni. Le impostazioni di dominio remoto valgono per tutta l'organizzazione di Exchange.

Se si elimina una voce del dominio remoto, le impostazioni per il trasferimento dei messaggi non vengono più applicate ai messaggi inviati al dominio remoto. L'eliminazione di una voce di un dominio remoto non disabilita il flusso di posta per tale dominio remoto. Una volta eliminata una voce di dominio remoto, le impostazioni di configurazione del dominio remoto vengono applicate ai nuovi messaggi inviati a quel dominio. Non è possibile eliminare il dominio remoto predefinito.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere°"Domini remoti" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Non è possibile creare un dominio remoto per uno spazio di indirizzo configurato come dominio accettato nell'organizzazione. Ad esempio, se l'organizzazione accetta la posta per fabrikam.com, non è possibile creare un dominio remoto per fabrikam.com.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un dominio remoto tramite Shell

Per creare una nuova voce di dominio remoto, utilizzare la seguente sintassi.

    New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>

In questo esempio viene creata una voce di dominio remoto per i messaggi inviati al dominio contoso.com.

    New-RemoteDomain -Name Contoso -DomainName contoso.com

In questo esempio viene creata una voce di dominio remoto per i messaggi inviati al dominio fabrikam.com e a tutti i sottodomini.

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la creazione del dominio remoto sia stata eseguita correttamente, procedere come segue:

1.  Eseguire il comando **Get-RemoteDomain** e verificare se il dominio remoto viene elencato.

2.  Eseguire il comando `Get-RemoteDomain <Remote Domain Name> | Format-List` per verificare le impostazioni del nuovo dominio remoto. Inviare un messaggio ad un destinatario nello spazio di indirizzo specificato nella nuova voce di dominio remoto e verificare che le impostazioni del messaggio corrispondano a quelle specificate dalla nuova voce di dominio.

## Configurazione di un dominio remoto tramite Shell

È possibile configurare le impostazioni del dominio remoto utilizzando il cmdlet **Set-RemoteDomain**. Esistono diverse impostazioni relative alle risposte automatiche, al formato messaggi, alla codifica e ad altre impostazioni dei messaggi. Per ulteriori informazioni, vedere [Set-RemoteDomain](https://technet.microsoft.com/it-it/library/aa997857\(v=exchg.150\)).

Per configurare domini remoti in scenari specifici, consultare i seguenti argomenti:

  - [Configurare un dominio remoto risposte fuori sede](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [Configurare le risposte automatiche dominio remoto](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [Configurare le relazioni messaggio dominio remoto](configure-remote-domain-message-reporting-exchange-2013-help.md)

## Eliminazione di un dominio remoto tramite Shell

Per rimuovere una voce di dominio remoto, utilizzare la seguente sintassi.

    Remove-RemoteDomain <RemoteDomainName>

In questo esempio viene rimossa la voce di dominio remoto denominato Contoso

    Remove-RemoteDomain Contoso

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il dominio remoto sia stato rimosso correttamente, procedere come segue:

1.  Eseguire il comando **Get-RemoteDomain** e verificare se il dominio remoto viene elencato.

2.  Eseguire il comando `Get-RemoteDomain Default | Format-List` per verificare le impostazioni del dominio remoto predefinito. Inviare un messaggio ad un destinatario nello spazio di indirizzo specificato nel dominio remoto rimosso e verificare che le impostazioni del messaggio corrispondano a quelle specificate dal dominio remoto predefinito.

