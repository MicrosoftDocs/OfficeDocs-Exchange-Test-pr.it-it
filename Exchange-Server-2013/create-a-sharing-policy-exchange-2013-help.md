---
title: 'Creare un criterio di condivisione: Exchange 2013 Help'
TOCTitle: Creare un criterio di condivisione
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 50481666
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un criterio di condivisione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

I criteri di condivisione possono essere utilizzati per controllare il modo in cui gli utenti all'interno dell'organizzazione di Exchange condividono le informazioni del calendario con gli utenti all'esterno dell'organizzazione di . I criteri di condivisione forniscono la condivisione stabilita dall'utente e tra utenti delle informazioni di calendario con tipi diversi di utenti esterni. Supportano la condivisione delle informazioni del calendario con organizzazioni federative esterne (ad esempio, Office 365 o altre organizzazioni locali di Exchange), organizzazioni non federative esterne e con individui che dispongono di accesso a Internet. Per applicare un criterio di condivisione specifico agli utenti, vedere [Applicare un criterio di condivisione alle cassette postali](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md).


> [!IMPORTANT]
> Creazione di un criterio di condivisione è una delle numerose operazioni di configurazione di condivisione federativa nell'organizzazione di Exchange. È necessario impostare una relazione di trust federativa con il sistema di autenticazione Azure Active Directory per l'organizzazione di Exchange locale per poter condividere le informazioni del calendario con altre organizzazioni Exchange federate. Una relazione di trust federativa non è necessario per i criteri di condivisione per Internet.



Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

Per altre attività di gestione relative alla federazione, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Calendario e le autorizzazioni di condivisione? sezione nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) .

  - Per i criteri di condivisione tra organizzazioni di Exchange federate, è necessario che:
    
      - Un server Accesso Client di Exchange 2013 sia presente in ogni organizzazione di Exchange. Criteri di condivisione sono supportati anche tra organizzazioni di Exchange in un'organizzazione sono presenti server di accesso Client Exchange 2013 e un'organizzazione ha Exchange 2010 SP3 o versioni successive dei server Accesso Client.
    
      - Ogni organizzazione di Exchange ha creato una relazione di trust federativa con il sistema di autenticazione Azure AD. Per ulteriori informazioni, vedere [Configurazione di una relazione di trust federativa](configure-a-federation-trust-exchange-2013-help.md).
    
      - Ogni organizzazione di Exchange abbia configurato un identificatore di organizzazione federativa. I domini utilizzati per la generazione degli indirizzi di posta elettronica degli utenti siano stati aggiunti agli identificatori di organizzazione.
    
      - Cassette postali degli utenti si trovino sui server cassette postali Exchange 2013 o Exchange 2010 delle cassette postali in ogni organizzazione di Exchange.
    
      - Solo gli utenti di Outlook 2010 o versioni successive e di Outlook Web App possano creare inviti di condivisione.

  - Per i criteri di condivisione con organizzazioni di Exchange non federate o con singoli utenti, è necessario che:
    
      - Un server Accesso client di Exchange 2013 sia presente nell'organizzazione di Exchange che utilizza la condivisione delle informazioni sul calendario dell'utente.
    
      - Le cassette postali degli utenti si trovino sui server Cassette postali di Exchange 2013 nell'organizzazione di Exchange che utilizza la condivisione delle informazioni sul calendario dell'utente.
    
      - Il server Accesso client Exchange 2013 sia abilitato all'accesso di Outlook Web App.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata?

## Creazione di un criterio di condivisione tramite EAC

1.  Accedere a **organizzazione**\> **condivisione**.

2.  Nella visualizzazione elenco, sotto **Condivisione singola**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella finestra di dialogo **nuovo criterio di condivisione** digitare il nome descrittivo per il criterio di condivisione nella casella **nome criterio**.

4.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per specificare le regole di condivisione per il criterio di condivisione.

5.  In **regola di condivisione** selezionare uno dei seguenti pulsanti di opzione per specificare i domini per la condivisione:
    
      - **Condivisione con tutti i domini**
    
      - **Condivisione con uno specifico dominio**

6.  Se è stato selezionato **Condivisione con uno specifico dominio**, digitare il dominio per la condivisione. Se è necessario inserire più di un dominio per il criterio di condivisione, salvare le impostazioni del primo dominio, quindi modificare le regole di condivisione al fine di aggiungervi ulteriori domini.

7.  Per definire i livelli di condivisione del calendario da applicare al criterio, selezionare la casella di controllo **Condividi la tua cartella del calendario** e selezionare una delle opzioni seguenti:
    
      - **Informazioni sulla disponibilità solo con l'ora**
    
      - **Informazioni sulla disponibilità di calendario con ora, oggetto e posizione**
    
      - **Tutte le informazioni di calendario sull'appuntamento, incluse ora, oggetto, posizione e titolo**

8.  Fare clic su **salva** per impostare le regole per il criterio di condivisione.

9.  Per impostare come predefinito il criterio di condivisione per gli utenti nell'organizzazione di Exchange, selezionare la casella di controllo **Imposta questo criterio come predefinito per la condivisione**.

10. Fare clic su **salva** per creare il criterio di condivisione.

## Utilizzare l'interfaccia di amministrazione di Exchange per consentire a tutti gli utenti di condividere tutti i dettagli del calendario

È possibile modificare il criterio di condivisione predefinito per consentire a tutti gli utenti di condividere tutti i calendari del dettaglio con persone esterne all'organizzazione.

1.  Accedere a **organizzazione**\> **condivisione**.

2.  Nella visualizzazione elenco in **Condivisione singola**, selezionare **il criterio di condivisione predefinito**, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella casella di dialogo **Criterio di condivisione**, selezionare **Condivisione con tutti i domini**, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Nella finestra di dialogo **Regola di condivisione**, in **Specifica quali informazioni condividere**, selezionare **Tutte le informazioni di calendario sull'appuntamento, incluse ora, oggetto, posizione e titolo**, quindi fare clic su **salva**.

5.  Nella finestra di dialogo **Criterio di condivisione**, fare clic su **salva** per impostare le regole del criterio di condivisione.

## Utilizzare la shell per creare un criterio di condivisione

  - In questo esempio viene creato il criterio di condivisione Contoso per il dominio esterno federato contoso.com. Questo criterio consente agli utenti nel dominio contoso.com di visualizzare le informazioni dettagliate sulla disponibilità del calendario. Per impostazione predefinita, questo criterio è abilitato.
    
        New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail

  - In questo esempio viene creato il criterio di condivisione ContosoWoodgrove per due diversi domini federati (contoso.com e woodgrovebank.com) con azioni di condivisione differenti per ciascun dominio configurato. Il criterio è disabilitato.
    
        New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false

  - In questo esempio viene creato il criterio di condivisione anonimo per un'organizzazione di Exchange con il server Accesso client CAS01 e il server Cassette postali MAIL01 con l'azione di condivisione configurata per informazioni limitate sulla disponibilità del calendario. Questo criterio consente agli utenti dell'organizzazione di Exchange di invitare gli utenti con accesso a Internet a visualizzare le informazioni sulla disponibilità del calendario inviando un collegamento. Il criterio è abilitato.
    
    1.  Impostare l'URL del proxy Web per MAIL01.
        
            Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
    
    2.  Abilitare la pubblicazione di una directory virtuale in CAS01.
        
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
    
    3.  Creare il criterio di condivisione anonimo e configurare la condivisione limitata delle informazioni di calendario.
        
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [New-SharingPolicy](https://technet.microsoft.com/it-it/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/it-it/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la creazione corretta del criterio di condivisione, eseguire il comando Shell seguente per controllare le informazioni sul criterio di condivisione.

    Get-SharingPolicy <policy name> | format-list


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


