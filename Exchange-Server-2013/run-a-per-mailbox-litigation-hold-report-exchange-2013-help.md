---
title: 'Esegue rapp. attesa conserv. controversia cassetta postale: Exchange 2013 Help'
TOCTitle: Eseguire un rapporto di attesa di conservazione per controversia per cassetta postale
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 50479763
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire un rapporto di attesa di conservazione per controversia per cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-13_

Se l'organizzazione è coinvolta in un'azione legale, potrebbe essere necessario intraprendere i passaggi per conservare i dati rilevanti, ad esempio i messaggi di posta elettronica, che potranno essere utilizzati come prove. In queste situazioni, è possibile utilizzare la conservazione per controversia legale per conservare tutti i messaggi di posta elettronica inviati e ricevuti da utenti specifici o nell'intera organizzazione per un periodo specificato. Per ulteriori informazioni sulla condizione di una cassetta postale in conservazione per controversia legale e sull'abilitazione e la disabilitazione di questa funzionalità, vedere la sezione "Funzionalità delle cassette postali" in [Gestire le cassette postali degli utenti](manage-user-mailboxes-exchange-2013-help.md).

Utilizzare il rapporto sulla conservazione per controversia legale per tenere traccia dei seguenti tipi di modifiche apportate a una cassetta postale in un periodo di tempo specificato:

  - Abilitazione della conservazione per controversia legale.

  - Disabilitazione della conservazione per controversia legale.

Per ciascun tipo di modifica, nel rapporto viene indicato l'utente che l'ha apportata e la data e l'ora in cui è stata effettuata.

## Che cosa è necessario sapere prima di iniziare

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo dell'amministratore in sola visualizzazione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare EAC per eseguire un rapporto sulla conservazione per controversia legale

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Gestione conformità** \> **Controllo**.

2.  Fare clic su **Esegui un rapporto di conservazione per controversia legale per cassetta postale**.
    
    In Microsoft Exchange il rapporto viene eseguito per le modifiche alla conservazione per controversia legale apportate a qualsiasi cassetta postale nelle ultime due settimane.

3.  Per visualizzare le modifiche per una cassetta postale specifica, selezionarla nel riquadro dei risultati della ricerca. I risultati della ricerca vengono visualizzati nel riquadro dei dettagli.


> [!TIP]
> Come limitare i risultati della ricerca Selezionare la data di inizio e la data di fine, o entrambe, e selezionare le cassette postali specifiche in cui eseguire la ricerca. Fare clic su <STRONG>Cerca</STRONG> per eseguire nuovamente il rapporto.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta esecuzione di un rapporto sulla conservazione per controversia legale, nel riquadro dei risultati della ricerca vengono visualizzate le cassette postali in cui sono state apportate modifiche alla conservazione per controversia legale nell'intervallo di date specificato. Se non sono visibili risultati, non sono avvenute modifiche alla conservazione per controversia legale nell'intervallo di date, oppure le modifiche apportate non hanno avuto esito positivo.


> [!NOTE]
> Quando una cassetta postale viene inserita nella conservazione per controversia legale, potrebbero essere necessari fino a 60&nbsp;minuti perché la conservazione abbia effetto.


