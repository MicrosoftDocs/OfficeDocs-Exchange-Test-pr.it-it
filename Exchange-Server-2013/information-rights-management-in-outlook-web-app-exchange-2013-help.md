---
title: 'Information Rights Management in Outlook Web App: Exchange 2013 Help'
TOCTitle: Information Rights Management in Outlook Web App
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 50480739
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Information Rights Management in Outlook Web App

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Gli Information Worker utilizzano sempre di più la posta elettronica per scambiare informazioni riservate. Per proteggere queste informazioni, le organizzazioni possono utilizzare Information Rights Management (IRM) per applicare una protezione permanente al contenuto dei messaggi. Prima di Microsoft Exchange Server 2010, l'utilizzo della protezione IRM era limitato ai client Outlook. In Exchange Server 2007, veniva richiesto agli utenti di Microsoft Outlook Web Access di scaricare il componente aggiuntivo Rights Management per Microsoft Internet Explorer in modo da poter accedere al contenuto protetto con IRM.

In Exchange 2013, IRM in Outlook Web App consente agli utenti di accedere alla funzionalità IRM offerta da Exchange per applicare la protezione IRM permanente al contenuto dei messaggi.

La seguente funzionalità IRM è disponibile in Outlook Web App:

  - **Invio messaggi protetti con IRM**   Come mostrato nella figura seguente, gli utenti di Outlook Web App possono utilizzare l'elenco a discesa relativo alle autorizzazioni e selezionare un modello dei criteri per i diritti da applicare al messaggio. Ciò consente agli utenti di inviare messaggi protetti con IRM da Outlook Web App. I messaggi sono protetti con IRM dai server Accesso client.
    
    ![Invio di un messaggio protetto con IRM da OWA](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "Invio di un messaggio protetto con IRM da OWA")  

  - **Allegati protetti con IRM**   Quando gli utenti inviano un messaggio protetto con IRM da Outlook Web App, qualsiasi file allegato al messaggio riceverà la stessa protezione IRM e verrà protetto utilizzando lo stesso modello dei criteri per i diritti del messaggio. In Exchange 2013, la protezione IRM viene applicata ai file associati a Microsoft Office Word, Excel e PowerPoint, così come ai file .xps e ai messaggi di posta elettronica. La protezione IRM viene applicata a un allegato solo se non è già protetto da IRM. Per ulteriori informazioni su Active Directory Modelli di criteri dei diritti AD RMS (Rights Management Services), vedere [Information Rights Management](information-rights-management-exchange-2013-help.md).
    

    > [!NOTE]
    > IRM in Outlook Web App consente di proteggere solo gli allegati file supportati illustrati in questa sezione. Non vengono protetti gli allegati che utilizzano formati file non supportati. Quando gli utenti di Outlook Web App proteggono un messaggio e allegano un tipo di file non supportato, viene visualizzata una notifica in cui viene indicato agli utenti che sono protetti solo i tipi di file supportati.

    

    > [!IMPORTANT]
    > La protezione IRM non può essere applicata ad un messaggio già firmato o crittografato utilizzando S/MIME. Per applicare la protezione IRM, la crittografia e la firma S/MIME devono essere rimosse dal messaggio. Lo stesso vale per i messaggi protetti con IRM. Gli utenti non possono firmarli o crittografarli utilizzando S/MIME.



  - **Lettura dei messaggi protetti con IRM**   I messaggi protetti dai mittenti utilizzando il cluster AD RMS dell'organizzazione vengono visualizzati nel riquadro di anteprima in Outlook Web App. Non è necessario installare alcun componente aggiuntivo e registrare il computer nella distribuzione di AD RMS. Quando un utente apre un messaggio o lo visualizza nel riquadro di anteprima, il messaggio viene decrittografato utilizzando la licenza di utilizzo aggiunta dall'agente di prelicenza. Dopo aver eseguito la decrittografia, il messaggio viene visualizzato nel riquadro di anteprima. Se una prelicenza non è disponibile, Outlook Web App ne richiede una dal server AD RMS, quindi esegue il rendering del messaggio. Durante la lettura degli allegati protetti con IRM in Outlook Web App, Visualizzazione documenti WebReady non è disponibile.
    

    > [!NOTE]
    > IRM in Outlook Web App non è in grado di impedire agli utenti acquisire immagini dallo schermo utilizzando la funzionalità Stamp nel modo utilizzato da Outlook e altre applicazioni Office. Ciò ha impatto sul diritto EXTRACT, che impedisce di copiare il contenuto del messaggio, se specificato nel modello dei criteri per i diritti AD&nbsp;RMS.



  - **Browser diversi, piattaforma più supporto di IRM**   IRM in Outlook Web App disponibili e browser piattaforma più supportare IRM. IRM in Outlook Web App è supportata in tutti i browser supportati da Exchange 2013, inclusi nei sistemi operativi Linux e Apple Macintosh. Per ulteriori informazioni sui sistemi operativi e browser supportati, vedere [Outlook Web App Supported Browsers](https://go.microsoft.com/fwlink/p/?linkid=129362).

  - **WebReady Document Viewing**   In Exchange 2013, gli utenti possono visualizzare gli allegati protetti con IRM utilizzando WebReady Document Viewing. Ciò consente agli utenti di visualizzare gli allegati supportati con l'applicazione associata senza dover scaricare l'allegato.

Per informazioni sulle attività relative alla gestione IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Abilitazione di IRM in Outlook Web App

Per abilitare IRM in Outlook Web App, è necessario aggiungere la cassetta postale di recapito federativo, una cassetta postale di sistema creata dal programma di installazione di Exchange 2013 al gruppo di utenti con privilegi avanzati in AD RMS. Per i dettagli, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md). Ciò consente ai server Exchange 2013 di accedere ai messaggi protetti da IRM.

È anche possibile abilitare IRM in Outlook Web App utilizzando il cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)) in Exchange Management Shell. Ciò consente di abilitare IRM in Outlook Web App per l'organizzazione Exchange 2013. È possibile disabilitare o abilitare IRM in Outlook Web App per una directory virtuale di Outlook Web App. È inoltre possibile controllare IRM in Outlook Web App ai seguenti livelli di granularità:

  - **Directory virtuale di Outlook Web App**   Per abilitare o disabilitare IRM in Outlook Web App per una directory virtuale di Outlook Web App, utilizzare il cmdlet **Set-OWAVirtualDirectory** e impostare il parametro *IRMEnabled* su `$false` o `$true` (predefinito). Ciò consente di disabilitare IRM in Outlook Web App per una directory virtuale su un server Accesso client di Exchange 2013, tenendolo abilitato su un'altra directory virtuale su un diverso server Accesso client.

  - **Criteri cassetta postale per Outlook Web App**   Per abilitare o disabilitare IRM in Outlook Web App per i criteri delle cassette postali di Outlook Web App, usare il cmdlet **Set-OWAMailboxPolicy** e impostare il parametro *IRMEnabled* su `$false` o `$true` (predefinito). Ciò consente di abilitare IRM in Outlook Web App per un gruppo di utenti e disabilitarlo per un altro gruppo assegnando loro criteri di cassetta postale diversi per Outlook Web App.

Per ulteriori informazioni, vedere [Attivare o disattivare Information Rights Management sui server Accesso Client](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

