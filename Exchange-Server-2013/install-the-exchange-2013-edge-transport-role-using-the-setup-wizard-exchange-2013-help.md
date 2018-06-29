---
title: "Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata: Exchange 2013 Help"
TOCTitle: Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61202271
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata

 

_**Si applica a:**Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-06-19_

In questo argomento viene descritto come utilizzare l'installazione guidata di Microsoft Exchange Server 2013 per installare il ruolo del server Trasporto Edge di Exchange 2013 in un computer. Il ruolo Trasporto Edge è disponibile con Exchange 2013 Service Pack 1 (SP1) o versione successiva. Per ulteriori informazioni sulla pianificazione e la distribuzione di Exchange 2013, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Si consiglia di installare il ruolo Trasporto Edge in una rete perimetrale esterna alla foresta interna di Active Directory dell'organizzazione. La possibilità di installare il ruolo del server Trasporto Edge in un computer aggiunto al dominio consente di abilitare solo la gestione del dominio di impostazioni e funzionalità di Windows. Il ruolo Trasporto Edge non utilizza Active Directory. Al contrario, utilizza la funzionalità Active Directory Lightweight Directory Services (AD LDS) Windows per archiviare le informazioni sui destinatari e sulla configurazione. Per ulteriori informazioni sul ruolo Trasporto Edge, vedere [Server Trasporto Edge](edge-transport-servers-exchange-2013-help.md).

Se si desiderano installare i ruoli Accesso client e Cassette postali di Exchange 2013 in un computer, vedere [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Non è possibile installare il ruolo Trasporto Edge sullo stesso computer dei ruoli server Accesso client e Cassette postali.


> [!TIP]
> Informazioni sull'Assistente per la distribuzione di Exchange Server Si tratta di uno strumento in linea gratuito che facilita la rapida distribuzione di Exchange 2013 all'interno dell'organizzazione richiedendo alcune domande e creando un elenco di controllo per la distribuzione personalizzato. Per ulteriori informazioni, vedere <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente per la distribuzione di Exchange Server</A>.



Per informazioni sulle attività da completare dopo l'installazione, vedere [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 40 minuti

  - Assicurarsi di aver letto le note di rilascio prima di eseguire l'installazione di Exchange 2013. Per ulteriori informazioni, vedere [Note sulla versione di Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - È necessario che il computer in cui si è installato Exchange 2013 disponga di un sistema operativo supportato (come Windows Server 2008 R2 con SP1, Windows Server 2012 R2 oWindows Server 2012), di spazio su disco sufficiente e soddisfi altri requisiti. Per informazioni sui requisiti di sistema, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Per eseguire l'installazione di Exchange 2013, è necessario installare Microsoft .NET Framework 4.5, Windows Management Framework e altri software richiesti. Per informazioni sui prerequisiti per tutti i ruoli server, vedere [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - È necessario configurare il suffisso DNS primario nel computer. Ad esempio, se il nome di dominio completo del computer in uso è edge.contoso.com, il suffisso DNS per il computer è contoso.com. Per ulteriori informazioni, vedere [Suffisso DNS primario manca](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - I server Trasporto Hub di Exchange 2007 e Exchange 2010 richiedono un aggiornamento prima della creazione di una sottoscrizione di EdgeSync con un server Trasporto Edge di Exchange 2013. Se non viene installato tale aggiornamento, la sottoscrizione di EdgeSync non funzionerà correttamente. Per ulteriori informazioni, vedere la sezione "Scenari di coesistenza supportati" in [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Assicurarsi che l'account in uso sia un membro del gruppo Administrators locale del computer in cui è in corso l'installazione del ruolo Trasporto Edge.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Dopo aver installato Exchange su un server, non modificare il nome del server. Non è infatti consentito assegnare un nuovo nome a un server dopo l'installazione di un ruolo server Exchange.



## Installazione di Exchange Server 2013


> [!NOTE]
> Per scaricare la versione più recente di Exchange 2013, vedere <A href="updates-for-exchange-2013-exchange-2013-help.md">Aggiornamenti per Exchange 2013</A>.



1.  Accedere al computer su cui si desidera installare Exchange 2013.

2.  Andare al percorso di rete dei file di installazione di Exchange 2013.

3.  Fare doppio clic su `Setup.exe` per avviare l'installazione di Exchange 2013
    

    > [!IMPORTANT]
    > Se il controllo di accesso utente (User Access Control, UAC) è abilitato, fare clic con il pulsante destro del mouse su <CODE>Setup.exe</CODE> e selezionare <STRONG>Esegui come amministratore</STRONG>.



4.  Nella pagina **Verifica disponibilità aggiornamenti** scegliere se includere nell'installazione il download tramite Internet degli aggiornamenti del prodotto e della sicurezza per Exchange 2013. Se si seleziona **Connettersi a Internet e verificare la disponibilità di aggiornamenti**, gli aggiornamenti verranno scaricati e applicati prima di continuare durante la procedura di installazione. Se si seleziona **Non verificare la disponibilità degli aggiornamenti adesso**, è possibile scaricare e installare manualmente gli aggiornamenti in un secondo momento anche se è consigliabile scaricarli e installarli subito. Fare clic su **Avanti** per continuare.

5.  
    
    Nella pagina **Introduzione** ha inizio il processo di installazione di Exchange nell'organizzazione. L'utente verrà guidato nel processo di installazione. Sono elencati diversi collegamenti a contenuti di distribuzione utili. Si consiglia di visitare tali collegamenti prima di continuare l'installazione. Fare clic su **Avanti** per continuare.

6.  
    
    Nella pagina **Contratto di licenza** leggere le condizioni di licenza software. Per accettare le condizioni, selezionare **Accetto i termini del contratto di licenza** e fare clic su **Avanti**.

7.  
    
    Nella pagina **Impostazioni consigliate** scegliere se utilizzare o meno le impostazioni consigliate. Se si seleziona **Usa impostazioni consigliate**, Exchange invierà automaticamente a Microsoft segnalazioni di errori e informazioni sull'hardware del computer e sull'utilizzo di Exchange. Se si seleziona **Non utilizzare le impostazioni consigliate**, le impostazioni rimangono disabilitate ma sarà possibile abilitarle in qualsiasi momento una volta completata l'installazione. Per ulteriori informazioni su tali impostazioni e sull'utilizzo delle informazioni inviate a Microsoft, fare clic su **?**.

8.  
    
    Nella pagina **Selezione ruolo server** selezionare **Trasporto Edge**. Ricordare che non è possibile aggiungere ruoli server Cassette postali e Accesso client a un computer in cui è installato il ruolo Trasporto Edge. Gli strumenti di gestione sono installati automaticamente se si installa qualsiasi ruolo del server.
    
    Selezionare **Installazione automatica dei ruoli e delle funzionalità di Windows Server necessari per installare Exchange Server** per includere nell'installazione guidata anche l'installazione dei prerequisiti di Windows. Per completare l'installazione di alcune funzionalità di Windows, è probabile che sia necessario riavviare il computer. Se questa opzione non viene selezionata, sarà necessario installare le funzionalità di Windows manualmente.
    

    > [!NOTE]
    > Questa opzione consente di installare solo le funzionalità di Windows richieste da Exchange. È necessario installare manualmente gli altri prerequisiti. Per ulteriori informazioni, vedere <A href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</A>.

    
    Fare clic su **Avanti** per continuare.

9.  Nella pagina **Spazio e percorso di installazione** accettare il percorso di installazione predefinito o fare clic su **Sfoglia** per scegliere un percorso diverso. Assicurarsi di disporre di spazio sufficiente su disco nel percorso in cui si intende installare Exchange. Fare clic su **Avanti** per continuare.

10. 
    
    Nella pagina **Controllo conformità** visualizzare lo stato per determinare se il controllo dei prerequisiti per l'organizzazione e per il ruolo del server è stato completato con esito positivo. Se non è stato completato correttamente, è necessario risolvere eventuali errori segnalati prima di installare Exchange 2013. Non è necessario uscire dal programma di installazione durante la risoluzione dei problemi relativi ai prerequisiti. Dopo aver risolto un errore segnalato, fare clic su **Indietro**, quindi scegliere **Avanti** per eseguire di nuovo il controllo dei prerequisiti. Assicurarsi di esaminare inoltre tutti gli avvisi segnalati. Se i controlli di conformità sono stati completati con esito positivo, fare clic su **Avanti** per installare Exchange 2013.

11. 
    
    Nella pagina **Completamento** fare clic su **Fine**.

12. Riavviare il computer al termine dell'installazione di Exchange 2013.

13. Completare la distribuzione eseguendo le operazioni descritte in [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che Exchange 2013 sia stato installato correttamente, vedere [Verificare un'installazione di Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.

