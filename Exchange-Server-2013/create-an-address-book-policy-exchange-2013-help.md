---
title: 'Creare un criterio della Rubrica: Exchange 2013 Help'
TOCTitle: Creare un criterio della Rubrica
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 50480808
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un criterio della Rubrica

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

I criteri della rubrica consentono di suddividere gli utenti in gruppi specifici per fornire viste personalizzate dell'Elenco indirizzi globale dell'organizzazione. Quando si crea un criterio delle rubriche, si assegna un Elenco indirizzi globale, una Rubrica offline, un elenco di sale e uno o più elenchi indirizzi al criterio. È quindi possibile assegnare il criterio delle rubriche agli utenti delle cassette postali, per consentire l'accesso a un Elenco indirizzi globale personalizzato in Outlook e Outlook Web App. Lo scopo è fornire un meccanismo più semplice per eseguire la segmentazione dell'Elenco indirizzi globale nelle organizzazioni locali che richiedono più Elenchi indirizzi globali. Per ulteriori informazioni sui criteri delle rubriche, vedere [Criteri delle rubriche](address-book-policies-exchange-2013-help.md).

Per ulteriori attività di gestione relative ai criteri della rubrica, consultare [Procedure relative al criterio della Rubrica indirizzi](address-book-policy-procedures-exchange-2013-help.md).

Per gli utenti interessati agli scenari in cui viene utilizzata questa procedura? vedere [Scenario: Distribuzione di criteri della Rubrica](scenario-deploying-address-book-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri delle rubriche" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - La creazione di criteri per la rubrica per un'organizzazione è una procedura complessa che si articola in diverse fasi e che richiede un'adeguata pianificazione. Per ulteriori informazioni, vedere [Scenario: Distribuzione di criteri della Rubrica](scenario-deploying-address-book-policies-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per creare i criteri della rubrica. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Creazione di un criterio della rubrica tramite Shell

In questo esempio viene creato un messaggio criterio della rubrica con le seguenti impostazioni:

  - **Nome:** All Fabrikam ABP

  - **Elenco indirizzi globale:** All Fabrikam

  - **Rubrica offline:** Fabrikam-All-OAB

  - **Elenco sale:** All Fabrikam Rooms

  - **Elenchi indirizzi:** All Fabrikam, All Fabrikam Mailboxes, All Fabrikam DLs e All Fabrikam Contacts

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-AddressBookPolicy](https://technet.microsoft.com/it-it/library/hh529913\(v=exchg.150\)).

## Ulteriori informazioni

[Assegnare un criterio della Rubrica per gli utenti di posta](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

