---
title: 'Crea criterio indirizzo posta con i filtri destinatari: Exchange 2013 Help'
TOCTitle: Creare un criterio indirizzo di posta elettronica utilizzando i filtri destinatari
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 50481945
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un criterio indirizzo di posta elettronica utilizzando i filtri destinatari

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-16_

Non è possibile creare un criterio dell'indirizzo di posta elettronica utilizzando i filtri destinatario nella shell. Per ulteriori informazioni sui criteri degli indirizzi di posta elettronica, vedere [Criteri degli indirizzi di posta elettronica](email-address-policies-exchange-2013-help.md).

Per le attività di gestione aggiuntive correlate ai criteri degli indirizzi di posta elettronica, vedere [Procedure relative al criterio indirizzo posta elettronica](email-address-policy-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per utilizzare il parametro *RecipientFilter* per creare un filtro personalizzato, è necessario specificare una stringa per il filtro. Shell utilizza OPath per la sintassi del filtro. OPath è un linguaggio di query progettato per eseguire query sulle origini dati degli oggetti.
    

    > [!IMPORTANT]
    > Se un criterio dell'indirizzo di posta elettronica viene creato o modificato utilizzando un filtro destinatario, non è possibile modificarlo nell'interfaccia di amministrazione di Exchange (EAC). È necessario utilizzare la shell. Per ulteriori informazioni sulla sintassi e sui parametri, vedere <A href="https://technet.microsoft.com/it-it/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</A>.



  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri degli indirizzi di posta elettronica" nell'argomento [Indirizzi di posta elettronica e rubriche](email-addresses-and-address-books-exchange-2013-help.md).

  - Prima di poter utilizzare un dominio con indirizzo SMTP in un criterio indirizzo di posta elettronica, è necessario configurare un dominio accettato. Per ulteriori informazioni, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creazione di un criterio dell'indirizzo di posta elettronica utilizzando i filtri destinatari tramite Shell

Per creare un criterio dell'indirizzo di posta elettronica utilizzando i filtri destinatari, utilizzare la seguente sintassi.

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

In questo esempio viene creato un criterio dell'indirizzo di posta elettronica applicabile a tutti i dirigenti e nel quale la parte locale dell'indirizzo è composta dalle prime due lettere del nome e dal cognome intero.

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-EmailAddressPolicy](https://technet.microsoft.com/it-it/library/aa996800\(v=exchg.150\)).

