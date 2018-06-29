---
title: 'Cancellazione remota dati nel dispositivo: Exchange 2013 Help'
TOCTitle: Cancellazione remota dati nel dispositivo
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 50481726
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cancellazione remota dati nel dispositivo

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-09-19_

I dispositivi mobili, i tablet e altri dispositivi possono archiviare i dati riservati aziendali e consentire l'accesso a molte risorse aziendali. Se un dispositivo mobile viene perso o rubato, tali dati possono essere compromessi. Mediante i criteri cassetta postale per i dispositivi mobili di Exchange Microsoft, è possibile aggiungere la richiesta di una password ai dispositivi mobili. Questa operazione richiede agli utenti di immettere una password per accedere ai loro dispositivi mobili. Oltre alla richiesta di una password, si consiglia di configurare i dispositivi mobili per la richiesta automatica della password dopo un periodo di inattività. La combinazione di password del dispositivo e blocco dopo un periodo di inattività garantisce una maggiore sicurezza dei dati aziendali.

Oltre a queste funzionalità, Exchange Server 2013 mette a disposizione una funzionalità di cancellazione remota dati nel dispositivo. È possibile inviare un comando di cancellazione remota dati nel dispositivo da Exchange Management Shell o Interfaccia di amministrazione di Exchange. Gli utenti possono inviare i comandi di cancellazione remota dati nel dispositivo dall'interfaccia utente di MicrosoftOutlook Web App.

La funzionalità di cancellazione remota dati nel dispositivo include anche una funzione di conferma che scrive un timestamp nei dati dello stato di sincronizzazione della cassetta postale dell'utente. Questo timestamp viene visualizzato in Outlook Web App e nella finestra di dialogo delle proprietà del dispositivo mobile dell'utente in EAC.


> [!IMPORTANT]
> Un comando di cancellazione remota può ripristinare il dispositivo mobile alle impostazioni predefinite. Anche se il protocollo di cancellazione remota come implementato in Exchange 2013 richiede solo l'eliminazione dei dati aziendali personali, tutti i produttori attuali dei dispositivi mobili interpretano il comando come se cancellasse tutti i dati del telefono. Molti sistemi operativi dei dispositivi mobili cancellano anche tutti i dati archiviati su una scheda di memoria inserita nel dispositivo mobile. Se si esegue la cancellazione remota dati nel dispositivo su un telefono cellulare di cui si è in possesso e si desidera mantenere i dati presenti nella scheda di memoria, rimuovere la scheda di memoria prima di iniziare la cancellazione remota dati nel dispositivo.




> [!WARNING]
> Dopo la cancellazione remota dati nel dispositivo è particolarmente difficile recuperare i dati. Tuttavia, nessun processo di rimozione dei dati cancella integralmente i dati residui da un dispositivo mobile restituendolo come nuovo. Il ripristino dei dati potrebbe essere ancora possibile utilizzando strumenti avanzati.



## Cancellazione remota dati nel dispositivo e cancellazione locale dati nel dispositivo

La cancellazione locale dati nel dispositivo si verifica quando il dispositivo cancella automaticamente i dati senza la richiesta generata dal server. Se l'organizzazione ha implementato i criteri cassetta postale per i dispositivi mobili che specificano il numero massimo di tentativi con errore di immissione password, in caso di superamento di tale limite massimo, il dispositivo mobile esegue la cancellazione locale dati. Il risultato della cancellazione locale dati nel dispositivo è lo stesso della cancellazione remota dati nel dispositivo: il dispositivo ritorna alla condizione predefinita di fabbrica. Quando un dispositivo mobile esegue la cancellazione locale dati nel dispositivo, non viene inviata alcuna conferma al server di Exchange.

