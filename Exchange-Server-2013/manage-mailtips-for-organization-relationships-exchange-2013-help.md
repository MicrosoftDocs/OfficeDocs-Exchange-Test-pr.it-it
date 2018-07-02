---
title: "Gestire i suggerimenti per le relazioni dell'organizzazione: Exchange 2013 Help"
TOCTitle: Gestire i suggerimenti per le relazioni dell'organizzazione
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 50480841
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i suggerimenti per le relazioni dell'organizzazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Exchange Management Shell per configurare le impostazioni personalizzate per gli avvisi messaggio tra diverse organizzazioni.

Una relazione organizzativa consente di ottimizzare il lavoro degli utenti di entrambe le organizzazioni grazie alla condivisione di informazioni sulla disponibilità, alla configurazione di flussi di messaggi sicuri e all'abilitazione della verifica dei messaggi. Per ulteriori informazioni sulle relazioni organizzative, vedere [Suggerimenti messaggio tramite le relazioni dell'organizzazione](mailtips-over-organization-relationships-exchange-2013-help.md).

Sono disponibili diverse impostazioni per controllare l'utilizzo dei suggerimenti messaggio tra due organizzazioni che hanno dato vita a una relazione organizzativa. Le procedure descritte in questa sezione illustrano i diversi controlli disponibili. In tutti gli esempi, l'organizzazione on-premises è contoso.com, l'organizzazione remota è online.contoso.com e la relazione tra le due si chiama Contoso Online.

Utilizzare il cmdlet **Set-OrganizationRelationship** per configurare queste impostazioni.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Suggerimenti messaggio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione dei suggerimenti messaggio tra due organizzazioni tramite Shell

In questo esempio, la relazione organizzativa viene configurata in modo che i mittenti nell'organizzazione remota ricevano i suggerimenti messaggio quando indirizzano dei messaggi a destinatari nell'organizzazione principale.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

In questo esempio, la relazione organizzativa viene configurata in modo che i mittenti nell'organizzazione remota non ricevano alcun suggerimento messaggio quando indirizzano dei messaggi a destinatari nell'organizzazione principale.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332326\(v=exchg.150\)).

## Configurazione della tipologia di suggerimenti messaggio ricevuti dall'organizzazione remota tramite Shell

Per ciascuna relazione organizzativa, è possibile definire quali tipi di suggerimenti debbano essere inviati ai mittenti nell'altra organizzazione. In questo esempio, la relazione organizzativa viene configurata in modo che i suggerimenti vengano inviati.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

In questo esempio, la relazione organizzativa viene configurata in modo che vengano inviati solo i suggerimenti di tipo Risposte automatiche, Messaggio di dimensioni eccessive, Destinatario con limitazioni, Cassetta postale piena.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

In questo esempio, la relazione organizzativa viene configurata in modo che non venga inviato alcun suggerimento.


> [!NOTE]
> Non utilizzare questo metodo per disabilitare i suggerimenti per la relazione. Per disabilitare i suggerimenti, impostare il parametro <EM>MailTipsAccessEnabled</EM> su <CODE>$false</CODE>.



    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332326\(v=exchg.150\)).

## Configurazione di uno specifico gruppo di utenti a cui inviare suggerimenti messaggio specifici del destinatario tramite Shell

È possibile limitare l'invio di suggerimenti specifici del destinatario a uno specifico gruppo di utenti. Per impostazione predefinita, quando si abilitano i suggerimenti per una relazione organizzativa, a tutti gli utenti vengono inviati i seguenti suggerimenti specifici del destinatario:

  - Risposte automatiche

  - Cassetta postale piena

  - Suggerimento personalizzato

È possibile specificare un gruppo di accesso ai suggerimenti nella relazione organizzativa. Una volta specificato questo gruppo, i suggerimenti specifici del destinatario vengono inviati solo alle cassette postali, ai contatti di posta e agli utenti di posta che sono membri di questo gruppo. In questo esempio, la relazione organizzativa viene configurata in modo che invii i suggerimenti specifici del destinatario solo ai membri del gruppo ShareMailTips@contoso.com.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332326\(v=exchg.150\)).

