---
title: "Installazione di Exchange 2013 utilizzando l'installazione guidata: Exchange 2013 Help"
TOCTitle: Installazione di Exchange 2013 utilizzando l'installazione guidata
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 50481813
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# Installazione di Exchange 2013 utilizzando l'installazione guidata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-06-19_

L'argomento spiega come utilizzare l'installazione guidata di Microsoft Exchange Server 2013 per installare la cassetta postale Exchange 2013 e il ruolo server Client Access su un computer. Per ulteriori informazioni sulla pianificazione e la distribuzione di Exchange 2013, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Se si desidera installare il ruolo trasporto Edge Exchange 2013 su un computer, vedere [Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md). Il ruolo trasporto Edge non può essere installato sullo stesso computer come i ruoli cassetta postale o server Client access.


> [!TIP]
> Informazioni sull'Assistente per la distribuzione di Exchange Server Si tratta di uno strumento in linea gratuito che facilita la rapida distribuzione di Exchange 2013 all'interno dell'organizzazione richiedendo alcune domande e creando un elenco di controllo per la distribuzione personalizzato. Per ulteriori informazioni, vedere <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente per la distribuzione di Exchange Server</A>.




> [!NOTE]
> Dopo aver installato qualsiasi ruolo del server su un computer in cui viene eseguitoExchange 2013, non è possibile utilizzare l'installazione guidata di Exchange 2013 per aggiungere altri ruoli del server sullo stesso computer. Se si desidera aggiungere altri ruoli del server a un computer, è necessario utilizzare Installazione applicazioni nel Pannello di controllo oppure il file Setup.exe da una finestra del prompt dei comandi.



Per informazioni sulle attività da completare dopo l'installazione, vedere [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 60 minuti

  - Assicurarsi di aver letto le note di rilascio prima di eseguire l'installazione di Exchange 2013. Per ulteriori informazioni, vedere [Note sulla versione di Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Ciascuna organizzazione deve disporre di almeno un server Accesso client e un server Cassette postali nella foresta di Active Directory. Inoltre, ogni sito di Active Directory che contiene un server Cassette postali deve contenere anche almeno un server Accesso client. Se si separano i ruoli del server, è consigliabile installare per primo il ruolo Cassette postali.

  - Il computer su cui si installa Exchange 2013 deve avere un sistema operativo supportato (quale Windows Server 2008 R2 con Service Pack 1 (SP1) o Windows Server 2012), disporre di spazio su disco sufficiente, essere membro di un dominio Active Directory e soddisfare altri requisiti. Per informazioni sui requisiti di sistema, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Per eseguire l'installazione di Exchange 2013, è necessario installare Microsoft .NET Framework 4.5, Windows Management Framework 3.0 e altri software richiesti. Per informazioni sui prerequisiti per tutti i ruoli server, vedere [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - È necessario utilizzare un account che disponga della delega di appartenenza al gruppo Schema Admins, se non è stato precedentemente preparato lo schema di Active Directory. Se si sta installando il primo server Exchange 2013 nell'organizzazione, l'account utilizzato deve essere membro del gruppo Enterprise Admins. Se lo schema è già stato preparato e non si sta installando il primo server Exchange 2013 nell'organizzazione, è necessario utilizzare un account membro del gruppo di ruoli Gestione organizzazione di Exchange 2013.
    
    Gli amministratori membri del gruppo di ruoli Configurazione delegata possono distribuire i server Exchange 2013 precedentemente sottoposti a provisioning da un membro del gruppo di ruoli Gestione organizzazione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Dopo aver installato Exchange su un server, non modificare il nome del server. Non è infatti consentito assegnare un nuovo nome a un server dopo l'installazione di un ruolo server Exchange.



## Installazione di Exchange Server 2013

Se si sta installando il primo server Exchange 2013 nell'organizzazione, e non è stata eseguita la procedura di preparazione per Active Directory, l'account utilizzato deve essere membro del gruppo Enterprise Administrators. Se lo schema di Active Directory non è stato preparato in precedenza, l'account utilizzato deve essere membro del gruppo Schema Admins. Per informazioni sulla preparazione di Active Directory per Exchange 2013, vedere [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md). Se le procedure di preparazione dello schema e di Active Directory sono già state eseguite, l'account utilizzato deve essere membro del gruppo di ruolo Delegated Setup management o Organization Management.


> [!NOTE]
> Per scaricare l'ultima versione di Exchange 2013, vedere <A href="updates-for-exchange-2013-exchange-2013-help.md">Aggiornamenti per Exchange 2013</A>.



1.  Accedere al computer su cui si desidera installare Exchange 2013.

2.  Andare al percorso di rete dei file di installazione di Exchange 2013.

3.  Fare doppio clic su `Setup.exe` per avviare l'installazione di Exchange 2013
    

    > [!IMPORTANT]
    > Se il controllo di accesso utente (User Access Control, UAC) è abilitato, fare clic con il pulsante destro del mouse su <CODE>Setup.exe</CODE> e selezionare <STRONG>Esegui come amministratore</STRONG>.



4.  Nella pagina **Verifica disponibilità aggiornamenti** scegliere se includere nell'installazione il download tramite Internet degli aggiornamenti del prodotto e della sicurezza per Exchange 2013. Se si seleziona **Connettersi a Internet e verificare la disponibilità di aggiornamenti**, gli aggiornamenti verranno scaricati e applicati prima di continuare durante la procedura di installazione. Se si seleziona **Non verificare la disponibilità degli aggiornamenti adesso**, è possibile scaricare e installare manualmente gli aggiornamenti in un secondo momento anche se è consigliabile scaricarli e installarli subito. Fare clic su **Avanti** per continuare.

5.  
    
    Nella pagina **Introduzione** inizia il processo di installazione di Exchange nell'organizzazione. L'utente verrà guidato nel processo di installazione. Sono elencati diversi collegamenti a contenuti di distribuzione utili. Si consiglia di visitare tali collegamenti prima di continuare l'installazione. Fare clic su **Avanti** per continuare.

6.  
    
    Nella pagina **Contratto di licenza** leggere le condizioni di licenza software. Per accettare le condizioni, selezionare **Accetto i termini del contratto di licenza** e fare clic su **Avanti**.

7.  
    
    Nella pagina **Impostazioni consigliate** scegliere se utilizzare o meno le impostazioni consigliate. Se si seleziona **Usa impostazioni consigliate**, Exchange invierà automaticamente a Microsoft segnalazioni di errori e informazioni sull'hardware del computer e sull'utilizzo di Exchange. Se si seleziona **Non utilizzare le impostazioni consigliate**, le impostazioni rimangono disabilitate ma sarà possibile abilitarle in qualsiasi momento una volta completata l'installazione. Per ulteriori informazioni su tali impostazioni e sull'utilizzo delle informazioni inviate a Microsoft, fare clic su **?**.

8.  
    
    Nella pagina **Selezione ruolo server** scegliere se installare o meno il **ruolo Cassette postali**, il **ruolo Accesso client**, entrambi i ruoli o solo gli **Strumenti di gestione** nel computer in uso. I ruoli del server potranno essere aggiunti in seguito se si sceglie di non installarli nel corso dell'installazione corrente. In un'organizzazione deve essere installato almeno un ruolo Cassette postali e almeno un ruolo del server Accesso client. Possono essere installati nello stesso computer o in computer separati. Gli strumenti di gestione sono installati automaticamente se si installa qualsiasi ruolo del server.
    
    Selezionare **Installazione automatica dei ruoli e delle funzionalità di Windows Server necessari per installare Exchange Server** per includere nell'installazione guidata anche l'installazione dei prerequisiti di Windows. Per completare l'installazione di alcune funzionalità di Windows, è probabile che sia necessario riavviare il computer. Se questa opzione non viene selezionata, sarà necessario installare le funzionalità di Windows manualmente.
    

    > [!NOTE]
    > Questa opzione consente di installare solo le funzionalità di Windows richieste da Exchange. È necessario installare manualmente gli altri prerequisiti. Per ulteriori informazioni, vedere <A href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</A>.

    
    Fare clic su **Avanti** per continuare.

9.  Nella pagina **Spazio e percorso di installazione** accettare il percorso di installazione predefinito o fare clic su **Sfoglia** per scegliere un percorso diverso. Assicurarsi di disporre di spazio sufficiente su disco nel percorso in cui si intende installare Exchange. Fare clic su **Avanti** per continuare.

10. 
    
    Se si tratta del primo server Exchange dell'organizzazione, nella pagina **Organizzazione di Exchange** digitare un nome per l'organizzazione di Exchange. Il nome dell'organizzazione di Exchange può contenere solo i seguenti caratteri:
    
      - Dalla A alla Z
    
      - Dalla a alla z
    
      - Da 0 a 9
    
      - Spazio (non iniziale né finale)
    
      - Segno meno o trattino
        

        > [!NOTE]
        > Il nome dell'organizzazione non può contenere più di 64 caratteri. Il nome dell'organizzazione non può essere vuoto.

    
    Per utilizzare il modello di autorizzazioni suddivise di Active Directory, selezionare **Applica modello di autorizzazioni suddivise di Active Directory all'organizzazione di Exchange**.
    

    > [!WARNING]
    > Nella maggior parte delle organizzazioni non è necessario applicare il modello delle autorizzazioni suddivise di Active Directory. Se è necessario separare la gestione delle entità di sicurezza di Active Directory e la configurazione di Exchange, le autorizzazioni suddivise con controllo degli accessi basato sui ruoli (RBAC) potrebbe essere la soluzione migliore. Per ulteriori informazioni, fare clic su <STRONG>?</STRONG>.

    
    Fare clic su **Avanti** per continuare.

11. Se si sta installando il ruolo Cassette postali, nella pagina **Impostazioni protezione da malware** scegliere se abilitare o meno l'analisi malware. Se si disabilita l'analisi malware, potrà comunque essere abilitata in futuro. Fare clic su **Avanti** per continuare.

12. 
    
    Nella pagina **Controllo conformità** visualizzare lo stato per determinare se il controllo dei prerequisiti per l'organizzazione e per il ruolo del server è stato completato con esito positivo. Se non è stato completato correttamente, è necessario risolvere eventuali errori segnalati prima di installare Exchange 2013. Non è necessario uscire dal programma di installazione durante la risoluzione dei problemi relativi ai prerequisiti. Dopo aver risolto un errore segnalato, fare clic su **Indietro**, quindi scegliere **Avanti** per eseguire di nuovo il controllo dei prerequisiti. Assicurarsi di esaminare inoltre tutti gli avvisi segnalati. Se i controlli di conformità sono stati completati con esito positivo, fare clic su **Avanti** per installare Exchange 2013.

13. 
    
    Nella pagina **Completamento** fare clic su **Fine**.

14. Riavviare il computer al termine dell'installazione di Exchange 2013.

15. Completare la distribuzione eseguendo le operazioni descritte in [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che Exchange 2013 sia stato installato correttamente, vedere [Verificare un'installazione di Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.

