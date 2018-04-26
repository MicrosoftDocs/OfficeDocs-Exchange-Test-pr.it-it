---
title: Guida introduttiva a Exchange Server 2013 Management Pack
TOCTitle: Guida introduttiva a Exchange Server 2013 Management Pack
ms:assetid: 72d1609f-ab32-44d8-aa40-b1de587442d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn195908(v=EXCHG.150)
ms:contentKeyID: 53375447
ms.date: 08/30/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Guida introduttiva a Exchange Server 2013 Management Pack

 

_**Ultima modifica dell'argomento:** 2013-04-08_

Exchange Server 2013 Management Pack aggiunge un contenitore nella sezione **Monitoraggio** della console SCOM. Quando si espande il contenitore Exchange Server 2013, si visualizzeranno solamente tre viste.

![Contenitori di Exchange 2013 Management Pack](images/Dn195908.253b4ec5-2103-4b0c-a22e-5ebd24d08600(EXCHG.150).png "Contenitori di Exchange 2013 Management Pack")

## Avvisi attivi – Problemi con Exchange?

La vista **Avvisi attivi** mostra tutti gli avvisi generati e attualmente attivi nell'organizzazione Exchange. È possibile fare clic su qualsiasi avviso e visualizzare maggiori informazioni su di esso nel riquadro dei dettagli. In questa vista è possibile rispondere Sì/No alla domanda "Problemi con la distribuzione Exchange?" Ogni avviso corrisponde a uno o più problemi per una particolare impostazione di integrità. Inoltre, in base al tipo specifico di problema, potrebbe essere generato più di un avviso.

## Integrità dell'organizzazione – Qual è l'impatto?

Se si visualizza un avviso per la vista Avvisi attivi, per prima cosa controllare la vista **Integrità dell'organizzazione**. È la risorsa principale di informazioni relative allo stato generale di integrità dell'organizzazione. Fornisce dettagli su cosa è impattato nell'organizzazione, come i siti di Active Directory e i gruppi di disponibilità del database.

![Integrità dell'organizzazione](images/Dn195908.603c920b-7b88-4956-87d9-09d93fa6cba3(EXCHG.150).png "Integrità dell'organizzazione")

## Integrità server – Su quale server è necessario eseguire la risoluzione dei problemi?

La vista **Integrità server** fornisce dettagli sui singoli server dell'organizzazione. Di seguito è possibile visualizzare l'integrità individuale di ogni server. Tramite questa vista, è possibile limitare ogni tipo di problema in un determinato server.

![Integrità del server](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Integrità del server")

## Categorie di monitoraggio

Durante la visualizzazione di queste tre viste nella dashboard di Exchange Server 2013, potrebbe essere possibile notare che oltre alla colonna **Stato**, sono disponibili altri quattro indicatori di integrità.

![Indicatori di integrità di Exchange](images/Dn195908.dd10ed0b-abe5-41aa-8d43-b4fb10133984(EXCHG.150).png "Indicatori di integrità di Exchange")

Ciascuno di questi indicatori di integrità fornisce una panoramica degli aspetti specifici della distribuzione di Exchange.

  - **Punti tocco del cliente** Mostra l'esperienza degli utenti. Se questo indicatore mostra lo stato di integrità, significa che il problema probabilmente non ha impatto sugli utenti. Ad esempio, se un membro del gruppo di disponibilità dei database riscontra problemi, ma il database esegue correttamente il failover, gli indicatori mostreranno lo stato di assenza di integrità per quel determinato gruppo di disponibilità dei database. Tuttavia l'indicatore dei punti tocco del cliente mostreranno lo stato di integrità, poiché gli utenti non stanno riscontrando nessuna interruzione del servizio.

  - **Componenti del servizio** Mostra lo stato del servizio associato al componente. Ad esempio, l'indicatore del componente del servizio per OWA indica se il servizio OWA in generale è integro.

  - **Risorse del server** Mostra lo stato delle risorse fisiche che influiscono sulla funzionalità di un server.

  - **Dipendenze fondamentali** Mostra lo stato delle risorse esterne da cui dipende Exchange come la connettività di rete, DNS o Active Directory.

Le viste di Exchange Server 2013 Management Pack fornisco una visualizzazione semplice ma efficace che consente di determinare facilmente e rapidamente lo stato di integrità dell'organizzazione. Tuttavia, le viste sono anche strutturate in modo da guidare velocemente l'utente alla radice del problema in caso di avviso. Vedere [Utilizzo del Management Pack di Exchange Server 2013 per la risoluzione dei problemi](using-the-exchange-server-2013-management-pack-for-troubleshooting.md), per ulteriori informazioni sull'utilizzo di Exchange Server 2013 Management Pack per la risoluzione dei problemi.

