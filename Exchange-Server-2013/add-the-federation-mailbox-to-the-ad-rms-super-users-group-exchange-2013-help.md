---
title: 'Agg. cass. post. feder. gruppo utenti privilegi av. AD RMS: Exchange 2013 Help'
TOCTitle: Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 50480528
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Per le seguenti Microsoft Exchange Server 2013 Information Rights Management (IRM) funzionalità da abilitare, aggiungere la cassetta postale di federazione (una cassetta postale di sistema creata da Exchange 2013 il programma di installazione) al gruppo di utenti con privilegi avanzati in cluster di [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) dell'organizzazione:

  - IRM in Microsoft Office Outlook Web App

  - IRM in Exchange ActiveSync

  - Decrittografia dei rapporti del journal

  - Decrittografia di trasporto

È possibile configurare un gruppo di distribuzione abilitato all'utilizzo della posta come gruppo di utenti con privilegi avanzati. Ai membri del gruppo di distribuzione viene concessa una licenza d'uso con diritti di proprietario quando richiedono una licenza dal cluster AD RMS. Ciò consente di decrittografare tutto il contenuto protetto con RMS pubblicato dal cluster. Sia che si utilizzi un gruppo di distribuzione esistente o che si crei un gruppo di distribuzione e lo si configuri come gruppo di utenti con privilegi avanzati in AD RMS, si consiglia di dedicare il gruppo di distribuzione a tale scopo e di configurare le corrette impostazioni per approvare, controllare e monitorare le modifiche ai membri.


> [!WARNING]
> Configurazione di un gruppo di utenti con privilegi avanzati in AD RMS consente ai membri di gruppo decrittografare i contenuti protetti tramite IRM. È consigliabile misure appropriate per controllare e monitorare l'appartenenza al gruppo e abilitare il controllo tenere traccia delle modifiche di appartenenza. È inoltre possibile limitare modifiche indesiderate all'appartenenza al gruppo configurando il gruppo di un gruppo con restrizioni mediante criteri di gruppo. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/en-us/library/cc756802(v=ws.10).aspx">Impostazioni dei criteri gruppi con restrizioni</A>.



Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Un cluster AD RMS deve essere distribuito nella foresta di Active Directory.

  - Se un gruppo di utenti con privilegi avanzati è già configurato su un cluster AD RMS, qualsiasi modifica ai membri del gruppo di distribuzione può impiegare fino a 24 ore per essere visualizzata dal cluster AD RMS. Ciò è dovuto alla memorizzazione nella cache dei membri del gruppo sul cluster.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Aggiunta della cassetta postale di recapito federativo in un gruppo di distribuzione tramite Shell

Se un gruppo di distribuzione viene creato e configurato come gruppo di utenti con privilegi avanzati nel cluster AD RMS, è possibile aggiungervi, come componente, la cassetta postale di recapito federativo di Exchange 2013. Se non è stato configurato alcun gruppo di utenti con privilegi avanzati, occorrerà creare un gruppo di distribuzione e aggiungervi la cassetta postale di recapito federativo come componente.

1.  Creare un gruppo di distribuzione dedicato per utilizzarlo come gruppo di utenti con privilegi avanzati in AD RMS. Per ulteriori informazioni, vedere [Creazione e gestione dei gruppi di distribuzione](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups).

2.  Aggiungere l'utente di **FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042** al nuovo gruppo di distribuzione. Dal momento che è una cassetta postale di sistema, la cassetta postale di recapito federativo non è visibile nell'interfaccia di amministrazione di Exchange. Per aggiungerla ad un gruppo di distribuzione, è necessario utilizzare il cmdlet di [Add-DistributionGroupMember](https://technet.microsoft.com/it-it/library/bb124340\(v=exchg.150\)) da Shell.
    
    In questo esempio viene mostrato come aggiungere la cassetta postale di recapito federativo nel gruppo di distribuzione ADRMSSuperUsers.
    ```powershell
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042
    ```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Add-DistributionGroupMember](https://technet.microsoft.com/it-it/library/bb124340\(v=exchg.150\)).

## Passaggio 2: Utilizzo di AD RMS per impostare un gruppo di utenti con privilegi avanzati

Eseguire la procedura riportata di seguito in un cluster AD RMS. L'account utilizzato per eseguire questa procedura deve essere un membro del gruppo locale AD RMS Enterprise Administrators sul server AD RMS.

1.  Aprire la console di Active Directory Rights Management Services ed espandere il cluster AD RMS.

2.  Nell'albero della console, espandere i **Criteri di sicurezza**, quindi scegliere **Utenti con privilegi avanzati**.

3.  Nel riquadro azioni, fare clic su **Attiva utenti con privilegi avanzati**.

4.  NeI riquadro dei risultati, fare clic su **Modifica gruppo utenti con privilegi avanzati** per aprire la finestra delle proprietà **Utenti con privilegi avanzati**.

5.  Nella casella **Gruppo di utenti con privilegi avanzati**, digitare l'indirizzo di posta elettronica del gruppo di distribuzione creato nella precedente procedura oppure fare clic su **Sfoglia** per selezionare un gruppo di distribuzione.

## Come verificare se l'operazione ha avuto esito positivo?

Dopo aver aggiunto la cassetta postale di recapito federativo ad un gruppo di distribuzione nuovo o esistente, utilizzare il cmdlet [Get-DistributionGroupMember](https://technet.microsoft.com/it-it/library/aa996367\(v=exchg.150\)) per verificare l'appartenenza del gruppo.

Per un esempio di come controllare l'appartenenza ad un gruppo di distribuzione, vedere [Examples](https://technet.microsoft.com/it-it/aa996367\(exchg.150\)#examples) in **Get-DistributionGroupMember**.

Dopo aver utilizzato AD RMS per configurare un gruppo di utenti con privilegi avanzati, è possibile utilizzare i seguenti metodi per verificare che il gruppo di utenti con privilegi avanzati sia stato configurato correttamente. Inoltre, è possibile utilizzare i cmdlet di [Test-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979798\(v=exchg.150\)) per verificare la funzionalità IRM.

  - Utilizzare la console AD RMS per verificare che il gruppo corretto sia stato configurato come gruppo di utenti con privilegi avanzati.

  - Utilizzare il seguente comando PowerShell su un server AD RMS per recuperare il gruppo di utenti con privilegi avanzati.
    

    > [!IMPORTANT]
    > Il modulo ADRMSAdmin PowerShell è disponibile in Windows Server 2008 R2 e versioni successive.

    ```powershell
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser
    ```
