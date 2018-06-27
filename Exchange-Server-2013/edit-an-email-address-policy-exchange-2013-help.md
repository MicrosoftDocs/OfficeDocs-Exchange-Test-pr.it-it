---
title: 'Modificare un criterio indirizzo di posta elettronica: Exchange 2013 Help'
TOCTitle: Modificare un criterio indirizzo di posta elettronica
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 50481722
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# Modificare un criterio indirizzo di posta elettronica

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-12-10_

I criteri degli indirizzi di posta elettronica generano gli indirizzi di posta elettronica principali e secondari per i destinatari, inclusi utenti, contatti e gruppi, in modo che siano in grado di inviare e ricevere posta elettronica.

Per le attività di gestione aggiuntive correlate ai criteri degli indirizzi di posta elettronica, vedere [Procedure relative al criterio indirizzo posta elettronica](email-address-policy-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) per modificare un criterio degli indirizzi di posta elettronica creato utilizzando Shell.

  - Se l'indirizzo di posta elettronica è stato creato con un filtro destinatario, è necessario utilizzare Shell per modificare il criterio degli indirizzi di posta elettronica. Per ulteriori informazioni, vedere [Creare un criterio indirizzo di posta elettronica utilizzando i filtri destinatari](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri degli indirizzi di posta elettronica" nell'argomento [Indirizzi di posta elettronica e rubriche](email-addresses-and-address-books-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Modifica dei destinatari a cui si applica il criterio tramite EAC

1.  Passare a **Flusso di posta** \> **Criteri degli indirizzi di posta elettronica**.

2.  Nella visualizzazione elenco selezionare il criterio degli indirizzi di posta elettronica che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  
    
    In **Criterio dell'indirizzo e-mail** fare clic su **Applica a** e modificare le impostazioni.

## Modifica della priorità del criterio degli indirizzi di posta elettronica tramite EAC

Un utente può disporre di più indirizzi di posta elettronica proxy per lo stesso account (ad esempio, ayla@exchange.mail.contoso.com o ayla@contoso.com). Questi indirizzi di posta elettronica possono essere applicati in base alla priorità. Si consideri, ad esempio, lo scenario seguente: si dispone di due criteri di indirizzi di posta elettronica ai quali vengono assegnate le priorità 1 e 2. Se viene creato un altro criterio, gli verrà assegnata automaticamente la priorità 3. Si supponga tuttavia di avere due criteri, a uno dei quali si assegna la priorità 1 mentre all'altro è stata assegnata una priorità predefinita 2 al momento della creazione. In questo caso, il criterio creato successivamente, per impostazione predefinita, diventerà il criterio con priorità 2. Al criterio con priorità 2 precedente verrà assegnata una priorità pari a 3.

1.  Passare a **Flusso di posta** \> **Criteri degli indirizzi di posta elettronica**.

2.  Selezionare il criterio degli indirizzi di posta elettronica per il quale si desidera modificare la priorità, quindi fare clic su **Aumenta priorità**![Icona Freccia in su](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icona Freccia in su") o **Diminuisci priorità**![Icona Freccia in giù](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icona Freccia in giù").

## Modifica di un criterio degli indirizzi di posta elettronica tramite Shell

In questo esempio viene modificato il criterio degli indirizzi di posta elettronica per gli uffici del sud-est che attualmente include i destinatari in Georgia, Alabama e Louisiana per includere anche i destinatari nel Texas.

    Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"


> [!NOTE]
> Anche se il criterio degli indirizzi di posta elettronica è già stato applicato ai destinatari in Georgia, Alabama e Louisiana, è necessario includerli nel parametro perché questo non aggiunge i nuovi valori a quelli esistenti, ma li sovrascrive.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-EmailAddressPolicy](https://technet.microsoft.com/it-it/library/bb124517\(v=exchg.150\)).

