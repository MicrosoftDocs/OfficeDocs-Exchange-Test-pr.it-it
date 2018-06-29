---
title: "Relazioni dell'organizzazione: Exchange 2013 Help"
TOCTitle: Relazioni dell'organizzazione
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 50480552
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Relazioni dell'organizzazione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-02-20_

Impostare una relazione organizzativa per condividere le informazioni del calendario con un partner commerciale esterno. Gli amministratori di Exchange possono impostare una relazione organizzativa con un'organizzazione di Office 365 o con un'altra organizzazione di Exchange in locale. Se si desidera condividere i calendari con un'altra organizzazione di Exchange in locale, gli amministratori di Exchange in locale devono impostare una relazione di autenticazione con il cloud (denominato inoltre "federazione") e devono soddisfare i requisiti software minimi.

Una relazione organizzativa è una relazione uno a uno tra aziende per consentire agli utenti di ciascuna organizzazione di visualizzare le informazioni di disponibilità del calendario. Quando si imposta la relazione organizzativa, si imposta il proprio lato della relazione e si specifica il livello di informazioni visualizzabile dagli utenti esterni all'organizzazione. L'organizzazione esterna può definire impostazioni uguali o diverse sul relativo lato. Ad esempio, se Contoso crea una relazione organizzativa con Tailspin Toys, gli utenti su Tailspin Toys potranno pianificare incontri con gli utenti su Contoso aggiungendo l'indirizzo di posta elettronica all'invio alla riunione. La disponibilità dell'utente di Contoso invitato viene visualizzata dall'utente di Tailspin Toys. Tuttavia, prima che Contoso possa anche vedere la disponibilità per utenti di Tailspin Toys, i loro amministratori devono impostare una relazione organizzativa con Contoso.

Esistono tre livelli di accesso che è possibile specificare:

  - Nessun diritto di accesso

  - Accesso al solo tempo di disponibilità (disponibilità)

  - Accesso alla disponibilità tra cui ora, oggetto e posizione


> [!NOTE]
> Se gli utenti non desiderano condividere le informazioni sulla disponibilità, possono modificare la voce di autorizzazione predefinita di Outlook. Per eseguire questa operazione, gli utenti accedono alla scheda <STRONG>Proprietà calendario</STRONG> &gt; <STRONG>Autorizzazioni</STRONG>, selezionare le autorizzazioni <STRONG>Predefinite</STRONG> e selezionare <STRONG>Nessuna</STRONG> dall'elenco <STRONG>Livello di autorizzazione</STRONG>. Le informazioni sulla disponibilità non saranno visibili agli utenti interni o esterni, anche se esiste una relazione organizzativa. Vengono applicate le autorizzazioni impostate dall'utente.



Negli argomenti a seguire vengono spiegate la configurazione e la gestione delle relazioni di organizzazioni come parte della condivisione nella relativa organizzazione:

[Creare una relazione dell'organizzazione](create-an-organization-relationship-exchange-2013-help.md)

[Modificare una relazione dell'organizzazione](modify-an-organization-relationship-exchange-2013-help.md)

[Rimuovere una relazione dell'organizzazione](remove-an-organization-relationship-exchange-2013-help.md)

Per ulteriori informazioni sulla condivisione federata vedere [Condivisione](sharing-exchange-2013-help.md).

