---
title: 'Modificare le impostazioni di un criterio della Rubrica: Exchange 2013 Help'
TOCTitle: Modificare le impostazioni di un criterio della Rubrica
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 50481538
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare le impostazioni di un criterio della Rubrica

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-03-30_

Dopo aver creato un criterio della rubrica è possibile visualizzare o modificarne il nome, nonché l'Elenco indirizzi globale, la Rubrica offline, l'elenco sale e gli elenchi di indirizzi assegnati.

Per ulteriori attività di gestione relative ai criteri della rubrica, consultare [Procedure relative al criterio della Rubrica indirizzi](address-book-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri delle rubriche" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - La creazione di criteri per la rubrica per un'organizzazione è una procedura complessa che si articola in diverse fasi e che richiede un'adeguata pianificazione. Per ulteriori informazioni, vedere [Scenario: Distribuzione di criteri della Rubrica](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per configurare i criteri della rubrica. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Operazione desiderata?

## Modificare la rubrica offline, l'elenco delle sale e l'elenco indirizzi globale per un criterio della rubrica

In questo esempio vengono modificati la Rubrica offline, l'elenco delle sale e l'Elenco indirizzi globale che verranno utilizzati dagli utenti delle cassette postali assegnatoi al criterio della rubrica All Fabrikam ABP.

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## Sostituire elenchi di indirizzi in un criterio della Rubrica

Gli elenchi di indirizzi specificati per un criterio della Rubrica esistente sostituire tutti gli elenchi di indirizzi nel ABP.

In questo esempio sostituisce gli elenchi di indirizzi esistente con gli elenchi di indirizzi denominati GovernmentAgencyA Atlanta e Mosca GovernmentAgencyA per il criterio della Rubrica denominata a ente pubblico.

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## Aggiungere gli elenchi di indirizzi per un criterio della Rubrica

Per mantenere gli elenchi di indirizzi già definiti in un criterio della Rubrica, è necessario specificare tali elenchi di indirizzi quando si aggiungono nuove strutture per la ABP.

In questo esempio viene aggiunto l'elenco di indirizzi denominato Contoso Chicago per il criterio della Rubrica denominato Contoso criterio della Rubrica, che è già configurata per utilizzare l'elenco di indirizzi denominato Contoso Seattle.

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## Rimuovere gli elenchi di indirizzi da un criterio della Rubrica

Per rimuovere elenchi di indirizzi esistente che già definiti in un criterio della Rubrica, è necessario specificare gli elenchi di indirizzi che si desidera mantenere.

Ad esempio, il criterio della Rubrica denominata Fabrikam ABP utilizza gli elenchi di indirizzi denominati risorse Umane di Fabrikam e Fabrikam-Finance. Per rimuovere l'elenco di indirizzi Fabrikam-HR dal criterio della Rubrica, specificare l'elenco di indirizzi Fabrikam-Finance che si desidera mantenere.

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## Ulteriori informazioni

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-AddressBookPolicy](https://technet.microsoft.com/it-it/library/hh529945\(v=exchg.150\)).

