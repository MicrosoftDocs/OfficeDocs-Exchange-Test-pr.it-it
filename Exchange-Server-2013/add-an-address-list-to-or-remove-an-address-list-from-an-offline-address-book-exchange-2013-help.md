---
title: 'Aggiungere/rimuovere elenco indirizzi di Rubrica fuori rete:Exchange 2013 Help'
TOCTitle: Aggiungere un elenco di indirizzi o rimuovere un elenco di indirizzi di una Rubrica fuori rete
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 50481091
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere un elenco di indirizzi o rimuovere un elenco di indirizzi di una Rubrica fuori rete

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-16_

È possibile utilizzare Shell per aggiungere o rimuovere un elenco indirizzi da una rubrica offline. Per impostazione predefinita, esiste una Rubrica offline denominata Rubrica offline predefinita che contiene l'elenco indirizzi globale. Le Rubriche offline vengono generate in base agli elenchi di indirizzi che includono. Per creare Rubriche offline personalizzate scaricabili dagli utenti, è possibile aggiungere o rimuovere elenchi di indirizzi da tali rubriche.

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](https://docs.microsoft.com/it-it/exchange/address-books/offline-address-books/offline-address-book-procedures).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Le modifiche apportate all'elenco indirizzi saranno disponibili per il download da parte del client solo dopo la generazione della rubrica offline in cui si trova l'elenco indirizzi. Per ulteriori informazioni, vedere [Aggiornare una Rubrica fuori rete](https://docs.microsoft.com/it-it/exchange/address-books/offline-address-books/update-offline-address-book).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare Shell per aggiungere un elenco indirizzi a una rubrica offline

Quando si utilizza il parametro *AddressLists*, tutti gli elenchi di indirizzi correnti verranno sovrascritti. È necessario includere gli elenchi di indirizzi esistenti quando si utilizza il parametro *AddressLists* per continuare a generare tali elenchi di indirizzi nella propria Rubrica offline. In questo esempio, in cui si dispone di AddressList1 e AddressList2, si aggiunge AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OfflineAddressBook](https://technet.microsoft.com/it-it/library/aa996330\(v=exchg.150\)).

## Utilizzare Shell per rimuovere un elenco indirizzi da una rubrica offline

Per rimuovere un elenco indirizzi da una rubrica offline, è sufficiente ometterlo dall'elenco di elenchi indirizzi. In questo esempio, in cui si dispone di AddressList1, AddressList2 e AddressList3, si rimuove AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OfflineAddressBook](https://technet.microsoft.com/it-it/library/aa996330\(v=exchg.150\)).

