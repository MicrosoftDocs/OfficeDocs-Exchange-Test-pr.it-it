---
title: "Creare una relazione dell'organizzazione: Exchange 2013 Help"
TOCTitle: Creare una relazione dell'organizzazione
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 50480725
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una relazione dell'organizzazione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Configurare una relazione tra organizzazioni per condividere le informazioni del calendario con un partner aziendali esterni. È possibile configurare una relazione dell'organizzazione tra due organizzazioni federate Exchange 2013 o tra un'organizzazione federata Exchange 2013 e alle organizzazioni federate Exchange 2010. È inoltre possibile impostare backup di una relazione dell'organizzazione tra l'organizzazione di Exchange locale e un'organizzazione Office 365.


> [!IMPORTANT]
> La creazione di una relazione organizzativa è uno dei diversi passaggi della configurazione di una condivisione federata nell'organizzazione di Exchange e richiede la configurazione di una relazione di trust federativa per l'organizzazione locale di Exchange.



Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Calendario e le autorizzazioni di condivisione? sezione nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) .

  - È necessario configurare una relazione di trust federativa attiva per l'organizzazione Exchange locale. Per ulteriori informazioni, vedere [Configurazione di una relazione di trust federativa](configure-a-federation-trust-exchange-2013-help.md).

  - L'organizzazione esterna che si desidera configurare la relazione dell'organizzazione deve inoltre disporre di una relazione di trust federativa con il sistema di autenticazione Azure AD. Utilizzare il dominio federato principale per l'organizzazione di Exchange esterno quando si configura la relazione dell'organizzazione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per creare una relazione organizzativa

1.  Su un server Exchange 2013 della propria organizzazione locale, andare a **Organizzazione** \> **Condivisione**.

2.  In **Condivisione tra organizzazioni** e fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  In **Nuova relazione organizzativa**, nella casella **Nome relazione**, digitare un nome amico per la relazione organizzativa.

4.  Nella casella **Domini da condividere con**, immettere il dominio federato o il sottodominio federato per l'organizzazione federata esterna di Exchange o Office 365 che si desidera configurare per la condivisione federata. Se sono necessari più domini per l'organizzazione esterna, separarli con una virgola. Ad esempio, **contoso.com, service.contoso.com**.

5.  Selezionare la casella di controllo **Abilitare la condivisione delle informazioni di disponibilità calendario** per attivare la condivisione del calendario con i domini elencati. Impostare il livello di condivisione delle informazioni sulla disponibilità e impostare quale utente può condividerle.
    
    Per impostare il livello di accesso alle informazioni sulla disponibilità, selezionare una delle seguenti operazioni:
    
      - **Informazioni sulla disponibilità solo con l'ora**
    
      - **   Informazioni sulla disponibilità con ora, oggetto e posizione**
    
    Per impostare quali utenti condivideranno le informazioni sulla disponibilità, selezionare una delle voci seguenti:
    
      - **Tutti nell'organizzazione**
    
      - **Un gruppo di protezione specificato**
        
        Per specificare un gruppo di protezione, fare clic su **Sfoglia**.

6.  Fare clic su **Salva** per creare la relazione organizzativa.

## Utilizzare la shell per creare una relazione organizzativa

Con questo esempio viene creata una relazione organizzativa con Contoso, Ltd con le condizioni seguenti:

  - La relazione organizzativa è abilitata per contoso.com, northamerica.contoso.com e europe.contoso.

  - Opzioni sulla disponibilità abilitate.

  - L'organizzazione richiedente riceve l'ora di disponibilità, l'oggetto e le informazioni sulla posizione dall'organizzazione di destinazione.

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

In questo esempio si tenta di individuare automaticamente le informazioni di configurazione dall'organizzazione esterna di Exchange Contoso.com utilizzando i nomi di dominio indicati nel cmdlet **Get-FederationInformation**. Se viene utilizzato questo metodo per creare la relazione organizzativa, prima è necessario verificare che sia stato creato l'identificatore di organizzazione utilizzando il cmdlet **Set-FederatedOrganizationIdentifier**.

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-FederationInformation](https://technet.microsoft.com/it-it/library/dd351221\(v=exchg.150\)) e [New-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332357\(v=exchg.150\)).

In questo esempio viene creata una relazione organizzativa con Fourth Coffee. In questo esempio sono disponibili le impostazioni di connessione all'organizzazione esterna di Exchange. Vengono applicate le seguenti condizioni:

  - Viene stabilita la relazione organizzativa con il dominio fourthcoffee.com, un dominio federato di Fourth Coffee.

  - L'URL dell'applicazione per i servizi Web di Exchange è mail.fourthcoffee.com.

  - L'URL di individuazione automatica è https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity.

  - Opzioni sulla disponibilità abilitate.

  - L'organizzazione richiedente riceve solo le informazioni sulla disponibilità con l'ora.

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332357\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Il corretto completamento della procedura guidata **Nuova relazione organizzativa** è il primo segnale del fatto che la creazione delle relazioni dell'organizzazione è stata eseguita come previsto.

Per verificare ulteriormente che è stata creata correttamente la relazione organizzativa, eseguire il seguente comando Shell per verificare le informazioni sulla relazione organizzativa.

    Get-OrganizationRelationship | format-list


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


