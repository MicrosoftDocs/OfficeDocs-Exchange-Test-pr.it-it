---
title: "Il computer locale è responsabile dell'espansione gruppo membership_ServerIsDynamicGroupExpansionServer: Exchange 2013 Help"
TOCTitle: Il computer locale è responsabile dell'espansione gruppo membership_ServerIsDynamicGroupExpansionServer
ms:assetid: f6fdd8e1-fda1-45be-b8a2-0d356dbe7d83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.serverisdynamicgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 50482081
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il computer locale è responsabile dell'espansione gruppo membership\_ServerIsDynamicGroupExpansionServer

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft® Exchange Server 2007 non può continuare il tentativo di disinstallare un responsabile per espandere l'appartenenza al gruppo di ruolo Trasporto Hub.

Richiede l'installazione di Exchange 2007 che espansione della lista di distribuzione da rimuovere dal server testa di ponte corrente prima che il ruolo Trasporto Hub può essere disinstallato.

Espansione delle liste di distribuzione attiva l'identificazione dei singoli destinatari che appartengono alla lista di distribuzione che deve essere identificato o l'identificazione della distribuzione aggiuntiva sono elencate per l'espansione. Una lista di distribuzione espanse può restituire il percorso per qualsiasi necessari stato recapito (DSN). DSN avvisare l'amministratore di Microsoft Exchange o del mittente di posta elettronica dello stato di un messaggio di posta elettronica specifico. Espansione della lista di distribuzione, inoltre, indica se i messaggi fuori sede o risposte generate automaticamente devono essere inviate al mittente del messaggio originale.

Per risolvere questo problema, spostare l'espansione dei gruppi di distribuzione in un altro server e rieseguire il programma di installazione di Microsoft Exchange.

Per modificare il server di espansione di un gruppo di distribuzione o gruppo di distribuzione dinamico

1.  Aprire Exchange Management Console.

2.  Nell'albero della console espandere **Configurazione destinatario**.

3.  Nell'albero della console, fare clic su **Gruppo di distribuzione**.

4.  Creare un filtro per visualizzare tutti i gruppi di distribuzione e i gruppi di distribuzione dinamico che utilizzano il server testa di ponte corrente come un server di espansione.
    
    1.  Nel riquadro azioni fare clic su **Crea filtro**.
    
    2.  Nell'elenco a discesa proprietà, fare clic su **Server di espansione**.
    
    3.  Nell'elenco a discesa operatore, fare clic su **è uguale a**.
    
    4.  Nella casella valore, fare clic sul pulsante **Sfoglia** per selezionare il server testa di ponte che attualmente funge da server di espansione.


> [!NOTE]
> Il passaggio seguente è facoltativo.



1.  Fare clic su **Aggiungi espressione** per specificare ulteriori criteri di filtro. Verranno visualizzati solo i messaggi che soddisfano tutti i criteri di filtro.

2.  Fare clic su **Applica filtro**. Vengono visualizzati i risultati che soddisfano i criteri di filtro.

<!-- end list -->

1.  Nel riquadro dei risultati fare clic sul gruppo di distribuzione che si desidera modificare il server di espansione e quindi fare clic su **proprietà** nel riquadro azioni.

2.  **Proprietà**, fare clic sulla scheda **Avanzate**.

3.  Nell'elenco a discesa server, l'espansione selezionare un server specifico dall'elenco oppure selezionare **qualsiasi server nell'organizzazione**.

4.  Ripetere i passaggi da 5 a 7 per tutti i gruppi di distribuzione o gruppi di distribuzione dinamico che utilizzano il server testa di ponte come server di espansione.

