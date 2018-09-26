---
title: 'Installazione degli Strumenti di gestione di Exchange 2013: Exchange 2013 Help'
TOCTitle: Installazione degli Strumenti di gestione di Exchange 2013
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 50555606
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installazione degli Strumenti di gestione di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-01-28_

Con gli strumenti di gestione di Microsoft Exchange Server 2013 è possibile configurare e gestire l'organizzazione di Exchange in remoto. Gli strumenti di gestione di Exchange 2013 comprendono Exchange Management Shell e la casella degli strumenti di Exchange. In questo argomento viene spiegato come utilizzare Setup.exe o la modalità di installazione automatica per installare gli strumenti di gestione di Exchange 2013.


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire questa procedura in remoto. L'interfaccia di amministrazione di Exchange è una console basata sul Web ospitata su computer che eseguono il ruolo del server Accesso client di Exchange 2013. Per ulteriori informazioni sull'accesso all'interfaccia di amministrazione di Exchange in modalità remota, vedere <A href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Interfaccia di amministrazione di Exchange in Exchange 2013</A>.



Per ulteriori informazioni sulla gestione di Exchange 2013, vedere [Interfaccia di amministrazione di Exchange in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) e [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 10 minuti

  - Assicurarsi di aver letto le note di rilascio prima di eseguire l'installazione di Exchange 2013. Per ulteriori informazioni, vedere [Note sulla versione di Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Il computer in cui vengono installati gli strumenti di gestione deve utilizzare un sistema operativo supportato (come Windows Server 2012 o Windows 8), disporre di spazio sufficiente sul disco, essere membro di un dominio Active Directory e soddisfare altri requisiti. Per informazioni sui requisiti di sistema, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Per eseguire l'installazione di Exchange 2013, è necessario installare Microsoft .NET Framework 4.5, Windows Management Framework 3.0 e altri software richiesti. Per informazioni sui prerequisiti per tutti i ruoli server, vedere [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Installazione degli strumenti di gestione di Exchange 2013 tramite Setup.exe

1.  Accedere al computer su cui si desidera installare Exchange 2013.

2.  Andare al percorso di rete dei file di installazione di Exchange 2013.

3.  Fare doppio clic su `Setup.exe` per avviare l'installazione di Exchange 2013
    

    > [!IMPORTANT]
    > Se il controllo di accesso utente (User Access Control, UAC) è abilitato, fare clic con il pulsante destro del mouse su <CODE>Setup.exe</CODE> e selezionare <STRONG>Esegui come amministratore</STRONG>.



4.  Nella pagina **Verifica disponibilità aggiornamenti** scegliere se includere nell'installazione il download tramite Internet degli aggiornamenti del prodotto e della sicurezza per Exchange 2013. Se si seleziona **Connettersi a Internet e verificare la disponibilità di aggiornamenti**, gli aggiornamenti verranno scaricati e applicati prima di continuare durante la procedura di installazione. Se si seleziona **Non verificare la disponibilità degli aggiornamenti adesso**, è possibile scaricare e installare manualmente gli aggiornamenti in un secondo momento. anche se è consigliabile scaricarli e installarli subito. Fare clic su **Avanti** per continuare.

5.  Nella pagina **Introduzione** inizia il processo di installazione di Exchange nell'organizzazione. L'utente verrà guidato nel processo di installazione. Sono elencati diversi collegamenti a contenuti di distribuzione utili. Si consiglia di visitare tali collegamenti prima di continuare l'installazione. Fare clic su **Avanti** per continuare.

6.  Nella pagina **Contratto di licenza** leggere le condizioni di licenza software. Per accettare le condizioni, selezionare **Accetto i termini del contratto di licenza** e fare clic su **Avanti**.

7.  Nella pagina **Impostazioni consigliate** scegliere se utilizzare o meno le impostazioni consigliate. Se si seleziona **Usa impostazioni consigliate**, Exchange invierà automaticamente a Microsoft segnalazioni di errori e informazioni sull'hardware del computer e sull'utilizzo di Exchange. Se si seleziona **Non utilizzare le impostazioni consigliate**, le impostazioni rimangono disabilitate ma sarà possibile abilitarle in qualsiasi momento una volta completata l'installazione. Per ulteriori informazioni su tali impostazioni e sull'utilizzo delle informazioni inviate a Microsoft, fare clic su **?**.

8.  Nella pagina **Selezione ruolo server** verificare che **Strumenti di gestione** sia selezionato.
    
    Selezionare **Installazione automatica dei ruoli e delle funzionalità di Windows Server necessari per installare Exchange Server** per includere nell'installazione guidata anche l'installazione dei prerequisiti di Windows. Per completare l'installazione di alcune funzionalità di Windows, è probabile che sia necessario riavviare il computer. Se questa opzione non viene selezionata, sarà necessario installare le funzionalità di Windows manualmente.
    

    > [!NOTE]
    > Questa opzione consente di installare solo le funzionalità di Windows richieste da Exchange. È necessario installare manualmente gli altri prerequisiti. Per ulteriori informazioni, vedere <A href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</A>.

    
    Fare clic su **Avanti** per continuare.

9.  Nella pagina **Spazio e percorso di installazione** accettare il percorso di installazione predefinito o fare clic su **Sfoglia** per scegliere un percorso diverso. Assicurarsi di disporre di spazio sufficiente su disco nel percorso in cui si intende installare Exchange. Fare clic su **Avanti** per continuare.

10. Se si tratta della prima installazione di Exchange 2013 nell'organizzazione, nella pagina **Organizzazione di Exchange** digitare un nome per l'organizzazione di Exchange. Il nome dell'organizzazione di Exchange può contenere solo i seguenti caratteri:
    
      - Dalla A alla Z
    
      - Dalla a alla z
    
      - Da 0 a 9
    
      - Spazio (non iniziale né finale)
    
      - Linea o trattino
        

        > [!NOTE]
        > Il nome dell'organizzazione non può contenere più di 64 caratteri. Il nome dell'organizzazione non può essere vuoto.

    
    Per utilizzare il modello di autorizzazioni suddivise di Active Directory, selezionare **Applica modello di autorizzazioni suddivise di Active Directory all'organizzazione di Exchange**.
    

    > [!WARNING]
    > Nella maggior parte delle organizzazioni non è necessario applicare il modello delle autorizzazioni suddivise di Active Directory. Se è necessario separare la gestione delle entità di sicurezza di Active Directory e la configurazione di Exchange, le autorizzazioni suddivise con controllo degli accessi basato sui ruoli (RBAC) potrebbe essere la soluzione migliore. Per ulteriori informazioni, fare clic su <STRONG>?</STRONG>.

    
    Fare clic su **Avanti** per continuare.

11. Nella pagina **Controllo conformità** visualizzare lo stato per determinare se il controllo dei prerequisiti per l'organizzazione e per il ruolo del server è stato completato con esito positivo. Se non è stato completato correttamente, è necessario risolvere eventuali errori segnalati prima di installare Exchange 2013. Non è necessario uscire dal programma di installazione quando si risolvono alcuni errori relativi ai prerequisiti. Dopo aver risolto un errore segnalato, fare clic su **Indietro**, quindi scegliere **Avanti** per eseguire di nuovo il controllo dei prerequisiti. Esaminare inoltre tutti gli eventuali avvisi ricevuti. Se i controlli di conformità sono stati completati con esito positivo, fare clic su **Avanti** per installare Exchange 2013.

12. Nella pagina **Completamento** fare clic su **Fine**.

13. Riavviare il computer al termine dell'installazione di Exchange 2013.

## Utilizzo della modalità automatica per installare gli strumenti di gestione di Exchange 2013

1.  Accedere al computer in cui si desidera installare gli strumenti di gestione di Exchange 2013.

2.  Andare al percorso di rete dei file di installazione di Exchange 2013.

3.  Al prompt dei comandi, eseguire il comando.
    

    > [!IMPORTANT]
    > Se è attivato un controllo di accesso utente, è necessario eseguire <CODE>Setup.exe</CODE> da un prompt dei comandi elevato.

    
    ```powershell
        Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms
    ```

Per ulteriori informazioni, vedere [Installare Exchange 2013 utilizzando la modalità automatica](ge-2013-using-unattended-mode-exchange-2013-help 
Redirect to URL: https://review.docs.microsoft.com/zh-cn/office/exchange-server-2013/exchange-2013-client-access-server-configuration-exchange-2013-help).

