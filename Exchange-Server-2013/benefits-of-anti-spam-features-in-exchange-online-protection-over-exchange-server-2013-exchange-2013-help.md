---
title: 'Vantaggi antivirus in EOP su Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Vantaggi delle funzionalità antivirus in Exchange Online Protection su Exchange Server 2013
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 50479896
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Vantaggi delle funzionalità antivirus in Exchange Online Protection su Exchange Server 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-05-26_

Di seguito sono vantaggi derivanti dall'utilizzo della protezione anti-spam Exchange nel cloud (Microsoft Exchange Online o Microsoft Exchange Online Protection ) oppure Microsoft Exchange Server 2013, che include la maggior parte delle stesse caratteristiche protezione da posta indesiderate incorporati di Microsoft Exchange Server 2010:

  - **Ulteriori controllo e la configurazione più semplice**   Gli amministratori possono utilizzare la console di gestione basata sul web Interfaccia di amministrazione di Exchange (EAC) per personalizzare la posta indesiderata impostazioni in modo che indicata soddisfino le esigenze dell'organizzazione. Non esiste alcuna interfaccia utente di protezione da posta indesiderata in Exchange Server 2013. Sono disponibili le funzionalità di protezione da posta indesiderata di EOP in Exchange Online

  - **Il filtro connessioni più affidabile**   Nel Exchange 2013 connessione elenchi di indirizzi IP consentiti filtri ed elenchi di indirizzi IP bloccati sono disponibili solo se si installa un server Trasporto Edge nella rete perimetrale. Per ulteriori informazioni, vedere [Server Trasporto Edge](edge-transport-servers-exchange-2013-help.md). Nel cloud, è possibile scegliere di ignorare la posta indesiderata in messaggi di posta elettronica inviati da mittenti attendibili (dati raccolti da diverse origini di terze parti), assicurarsi che questi messaggi non siano inavvertitamente contrassegnati come posta indesiderata. Inoltre, il servizio di filtraggio ospitato utilizza elenchi aggregati dai fornitori e gli elenchi di blocco di Microsoft per fornire il filtro IP a livello superiore.

  - **Filtro contenuto più affidabile**   È possibile configurare facilmente il criterio del filtro contenuto per:
    
      - Filtrare i messaggi scritti in determinate lingue.
    
      - Filtrare i messaggi inviati da determinati paesi o aree geografiche.
    
      - Contrassegnare i messaggi inviati in blocco (ad esempio, quelli di marketing e pubblicità) come posta indesiderata.
    
      - Esaminare gli attributi di un messaggio e, se si rileva uno specifico attributo di posta indesiderata, agire di conseguenza sul messaggio. Per contrastare il phishing, alcune di queste opzioni offrono una combinazione di tecnologie SPF e ID mittente per autenticare i messaggi e verificare che non siano falsificati.
    
    Oltre alle suddette opzioni per il filtro contenuto che è possibile configurare nell'interfaccia di amministrazione di Exchange, il servizio di filtraggio ospitato utilizza altri elenchi di URL per bloccare i messaggi sospetti che contengono determinati URL nel corpo del messaggio.

  - **Aggiornamenti più veloci**   Gli aggiornamenti di protezione da posta indesiderata vengono propagati più velocemente nella rete. In Exchange Server 2013 gli aggiornamenti vengono eseguiti due volte al mese, mentre il servizio viene aggiornato più volte ogni ora.

  - **Filtro in uscita**   Il filtro di protezione da posta indesiderata in uscita è sempre abilitato se si utilizza il servizio ospitato per inviare la posta. Di conseguenza, consente di proteggere le organizzazioni utilizzando il servizio e i destinatari desiderati.

