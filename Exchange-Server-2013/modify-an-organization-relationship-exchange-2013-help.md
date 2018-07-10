---
title: "Modificare una relazione dell'organizzazione: Exchange 2013 Help"
TOCTitle: Modificare una relazione dell'organizzazione
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 50480338
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare una relazione dell'organizzazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-01_

Una relazione di organizzazione consente agli utenti nell'organizzazione di Exchange di condividere informazioni sulla disponibilità del calendario con un'organizzazione di Office 365 o un'altra organizzazione di Exchange locale. Potrebbe essere necessario modificare le impostazioni di una relazione organizzativa, come ad esempio, modificare il nome, disattivare temporaneamente la condivisione del calendario, modificare il livello di accesso o cambiare i gruppi di sicurezza che condivideranno i calendari.

Prima di poter condividere i calendari con un'altra organizzazione, è necessario configurare una relazione di autenticazione con il cloud (nota anche come "federazione") che deve soddisfare i requisiti software minimi. Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

Per altre attività di gestione relative alla federazione, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere La voce *Calendar and Sharing Permissions* nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - È necessario configurare una relazione di trust federativa attiva per l'organizzazione Exchange locale.

  - L'organizzazione esterna che si desidera configurare la relazione dell'organizzazione deve inoltre disporre di una relazione di trust federativa con il sistema di autenticazione Azure AD.

  - Le procedure descritte in questo argomento apportano modifiche a una relazione organizzativa denominata Contoso. Gli esempi mostrano come:
    
      - Aggiungere un dominio denominato service.contoso.com all'organizzazione esterna.
    
      - Disabilitare la condivisione delle informazioni sulla disponibilità per la relazione organizzativa.
    
      - Modificare il livello di accesso alle informazioni sulla disponibilità da *Calendar free/busy information with time, subject, and location* a *Calendar free/busy information with time only*.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata?

## Utilizzare EAC per aggiungere un dominio a una relazione organizzativa

1.  In un server Exchange 2013 nella propria organizzazione locale, andare a **Organizzazione** \> **Condivisione**.

2.  Nella visualizzazione elenco, sotto **Condivisione organizzativa**, selezionare la relazione organizzativa Contoso, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Relazione organizzativa**, **Generale** non cambiare il **nome** per la relazione organizzativa.

4.  Nella casella **Domini con cui condividere**, inserire il dominio **service.contoso.com**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Fare clic su **salva** per aggiornare la relazione organizzativa.

## Utilizzo dell'interfaccia di amministrazione di Exchange per la disabilitazione della condivisione delle informazioni sulla disponibilità per la relazione organizzativa

1.  Andare a **Organizzazione** \> **Condivisione**.

2.  Nella visualizzazione elenco, sotto **Condivisione organizzativa**, selezionare la relazione organizzativa Contoso, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Relazione organizzativa**, fare clic su **Condivisione**

4.  Selezionare **Informazioni sulla disponibilità solo con l'ora**.

5.  Fare clic su **salva** per aggiornare la relazione organizzativa.

## Utilizzo dell'interfaccia di amministrazione di Exchange per la modifica del livello di accesso alle informazioni sulla disponibilità per la relazione organizzativa

1.  Andare a **Organizzazione** \> **Condivisione**.

2.  Nella visualizzazione elenco, sotto **Condivisione organizzativa**, selezionare la relazione organizzativa Contoso, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Relazione organizzativa**, fare clic su **Condivisione**

4.  Selezionare **Informazioni sulla disponibilità solo con l'ora**.

5.  Fare clic su **salva** per aggiornare la relazione organizzativa.

## Utilizzo di Shell per la modifica della relazione organizzativa

  - In questo esempio, il dominio service.contoso.com viene aggiunto alla relazione organizzativa Contoso.
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - In questo esempio viene disabilitata la relazione organizzativa Contoso.
    
        Set-OrganizationRelationship -Identity Contoso -Enabled $false

  - In questo esempio, viene abilitato l'accesso alle informazioni sulla disponibilità del calendario per la relazione organizzativa WoodgroveBank e viene impostato il livello di accesso a `AvailabilityOnly` (informazioni sulla disponibilità del calendario solo con l'ora).
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332343\(v=exchg.150\)) e [Set-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332326\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta esecuzione dell'aggiornamento della relazione organizzativa, utilizzare il seguente comando Shell e verificare le informazioni sulla relazione organizzativa.

    Get-OrganizationRelationship | format-list


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


