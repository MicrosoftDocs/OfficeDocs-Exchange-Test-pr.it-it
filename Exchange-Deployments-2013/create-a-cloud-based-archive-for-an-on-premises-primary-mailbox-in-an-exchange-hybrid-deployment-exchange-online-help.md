---
title: 'Creare un archivio basato sul cloud per una cassetta postale principale locale in una distribuzione ibrida di Exchange: Exchange 2013 Help'
TOCTitle: Creare un archivio basato sul cloud per una cassetta postale principale locale in una distribuzione ibrida
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253380
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un archivio basato sul cloud per una cassetta postale principale locale in una distribuzione ibrida di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-01-20_

In una distribuzione ibrida di Exchange, è possibile configurare una cassetta postale principale locale con una cassetta postale di archiviazione basata sul cloud in Exchange Online.

Passaggio 1: abilitare una cassetta postale di archiviazione basata sul cloud per una cassetta postale locale principale

Passaggio 2: verificare che la cassetta postale di archiviazione basata sul cloud sia stata creata

(facoltativo) Eseguire la sincronizzazione delle directory.

## Prima di iniziare

  - L'utente con la cassetta postale principale locale deve disporre di un account utente nell'organizzazione di Office 365.

  - È necessario assegnare all'account utente di Office 365 una licenza di Archiviazione Exchange Online per Exchange Server. La procedura per l'assegnazione di una licenza è inclusa nella descrizione del passaggio 1.

  - Dopo aver abilitato la cassetta postale di archiviazione basata sul cloud nel passaggio 1, il provisioning della cassetta postale di archiviazione basata sul cloud potrebbe richiedere fino a 30 minuti. Ciò è dovuto al fatto che la cassetta postale di archiviazione basata sul cloud viene creata dalla procedura di sincronizzazione della directory, in cui il servizio Active Directory locale viene sincronizzato con Active Directory in Azure (Azure AD) in Office 365. Per impostazione predefinita, la sincronizzazione della directory viene eseguita ogni 30 minuti.

## Passaggio 1: abilitare una cassetta postale di archiviazione basata sul cloud per una cassetta postale locale principale

Utilizzare una delle procedure seguenti per abilitare una cassetta postale di archiviazione basata sul cloud per una cassetta postale principale locale. Eseguire questi passaggi nell'Interfaccia di amministrazione di Exchange dell'organizzazione di Exchange locale e nell'interfaccia di amministrazione di Office 365.

Creare una cassetta postale di archiviazione basata sul cloud per un nuovo utente

Creare una cassetta postale di archiviazione basata sul cloud per un utente esistente

## Creare una cassetta postale di archiviazione basata sul cloud per un nuovo utente

1.  Nell'Interfaccia di amministrazione di Exchange nell'organizzazione locale, accedere a **Destinatari**  \> **Cassette postali**.

2.  Fare clic su **Nuovo**![Icona Aggiungi](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") \> **Cassetta postale utente**.

3.  Nella pagina **Nuova cassetta postale utente**, creare una cassetta postale per un utente nuovo o esistente. Per ulteriori informazioni sulla creazione di una cassetta postale utente, vedere [Creazione di cassette postali utente](https://technet.microsoft.com/it-it/library/jj991919\(v=exchg.150\)).

4.  Fare clic su **Altre opzioni** per abilitare una cassetta postale di archiviazione basata sul cloud.

5.  In **Archivio**, fare clic sulla casella di controllo **Crea un archivio sul posto per questo utente**, quindi selezionare **Archivio basato su cloud**. Viene visualizzato il nome del dominio in cui verrà eseguito il provisioning della cassetta postale di archiviazione.
    
    ![In archivio, fare clic sulla casella di controllo e su Archivio basato sul cloud](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "In archivio, fare clic sulla casella di controllo e su Archivio basato sul cloud")  

6.  Fare clic su **Salva** per creare la cassetta postale e l'archivio basato sul cloud.
    
    Nella pagina **Cassette postali**, il valore **Utente (archivio)** viene visualizzato nella colonna **Tipo di cassetta postale** per la cassetta postale selezionata.

7.  Attendere fino a 30 minuti affinché la sincronizzazione della directory crei un account utente corrispondente in Office 365.
    

    > [!TIP]
    > Nell'interfaccia di amministrazione di Office 365, andare a <STRONG>Integrità</STRONG> &gt; <STRONG>Stato sincronizzazione directory</STRONG> per visualizzare l'ultima sincronizzazione della directory effettuata.



8.  Dopo aver verificato che la sincronizzazione della directory si è verificata in seguito alla creazione della nuova cassetta postale locale, nell'interfaccia di amministrazione di Office 365 andare a **Utenti** \> **Utenti attivi**, quindi selezionare il nuovo account utente di Office 365 precedentemente creato per la nuova cassetta postale locale.

9.  Nella pagina delle proprietà dell'utente visualizzata, fare clic su **Modifica** nella sezione **Licenze per i prodotti**.
    
    ![Fare clic su Modifica nel riquadro dei dettagli per assegnare una licenza all'utente selezionato](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Fare clic su Modifica nel riquadro dei dettagli per assegnare una licenza all'utente selezionato")  

10. Nel menu a discesa **Percorso**, selezionare un percorso per l'utente.

11. Espandere l'elenco delle licenze di Office 365 Enterprise, quindi assegnare la licenza **Archiviazione Exchange Online per Exchange Server** e infine salvare le modifiche.
    
    Nella colonna **Stato** dell'elenco di utenti, notare che ora una licenza è assegnata all'utente.

12. Di nuovo, attendere fino a 30 minuti affinché la sincronizzazione della directory esegua il provisioning di una cassetta postale di archiviazione basata sul cloud. Per informazioni su come verificare che sia stata creata la cassetta postale di archiviazione basata sul cloud, andare al passaggio 2. Dopo aver creato la cassetta postale di archiviazione, l'utente può accedervi mediante Outlook o Outlook sul Web.

Inizio pagina

## Creare una cassetta postale di archiviazione basata sul cloud per un utente esistente

1.  Nell'interfaccia di amministrazione di Office 365, andare a **Utenti** \> **Utenti attivi**, quindi selezionare l'account utente per il quale si desidera creare una cassetta postale di archiviazione basata sul cloud.

2.  Nella pagina delle proprietà dell'utente visualizzata, fare clic su **Modifica** nella sezione **Licenze per i prodotti**.
    
    ![Fare clic su Modifica nel riquadro dei dettagli per assegnare una licenza all'utente selezionato](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Fare clic su Modifica nel riquadro dei dettagli per assegnare una licenza all'utente selezionato")  

3.  Nel menu a discesa **Percorso**, selezionare un percorso per l'utente.

4.  Espandere l'elenco delle licenze di Office 365 Enterprise, quindi assegnare la licenza **Archiviazione Exchange Online per Exchange Server** e infine salvare le modifiche.
    
    Nella colonna **Stato** dell'elenco di utenti, notare che ora una licenza è assegnata all'utente.

5.  Nell'Interfaccia di amministrazione di Exchange nell'organizzazione locale, accedere a **Destinatari**  \> **Cassette postali**.

6.  Nell'elenco delle cassette postali, selezionare l'utente al quale è appena stata assegnata la licenza.

7.  Nel riquadro dei dettagli, sotto **Archivio locale**, fare clic su **Abilita**.
    
    ![Fare clic su Abilita nel riquadro dei dettagli per abilitare la cassetta postale di archiviazione per l'utente selezionato](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "Fare clic su Abilita nel riquadro dei dettagli per abilitare la cassetta postale di archiviazione per l'utente selezionato")  

8.  Nella pagina **Crea archivio sul posto**, fare clic su **Archivio basato sul cloud**, quindi fare clic su **OK**. Viene visualizzato il nome del dominio in cui verrà eseguito il provisioning della cassetta postale di archiviazione.
    
    ![Nella pagina Crea archivio sul posto, fare clic su Archivio basato sul cloud](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "Nella pagina Crea archivio sul posto, fare clic su Archivio basato sul cloud")  
    
    Nella pagina **Cassette postali**, il valore **Utente (archivio)** viene visualizzato nella colonna **Tipo di cassetta postale** per la cassetta postale selezionata.

9.  Attendere fino a 30 minuti affinché la sincronizzazione della directory crei la cassetta postale di archiviazione basata sul cloud. Per informazioni su come verificare che sia stata creata la cassetta postale di archiviazione basata sul cloud, andare al passaggio 2. Dopo aver creato la cassetta postale di archiviazione, l'utente può accedervi mediante Outlook o Outlook sul Web.
    

    > [!TIP]
    > Nell'interfaccia di amministrazione di Office 365, andare a <STRONG>Integrità</STRONG> &gt; <STRONG>Stato sincronizzazione directory</STRONG> per visualizzare l'ultima sincronizzazione della directory effettuata.



Inizio pagina

## Passaggio 2: verificare che la cassetta postale di archiviazione basata sul cloud sia stata creata

Come descritto in precedenza, potrebbe esserci un ritardo tra il momento in cui viene abilitata una cassetta postale di archiviazione basata sul cloud e il momento in cui viene effettivamente creata Ciò è dovuto al fatto che è necessario eseguire la sincronizzazione della directory per creare la cassetta postale di archiviazione basata sul cloud. Sono disponibili diversi modi per verificare che sia stata creata la cassetta postale di archiviazione basata sul cloud.

Nella propria organizzazione Exchange Online, eseguire il seguente comando di PowerShell per visualizzare le proprietà relative alla cassetta postale di archivio dell'utente. Per connettersi a Exchange Online utilizzando PowerShell remoto, vedere [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554).

    Get-MailUser <cloud mail user> | FL *archive*

Nella screenshot seguente vengono mostrate le proprietà che vengono restituite quando il provisioning della cassetta postale di archiviazione basata sul cloud è in sospeso e dopo la creazione della cassetta postale di archiviazione.

**Proprietà dell'utente di posta elettronica precedenti al provisioning della cassetta postale di archiviazione eseguito dalla sincronizzazione della directory**

![Proprietà della cassetta postale basata sul cloud prima del provisioning dell'archivio basato sul cloud](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "Proprietà della cassetta postale basata sul cloud prima del provisioning dell'archivio basato sul cloud")

Prima che la sincronizzazione della directory esegua il provisioning dell'archivio basato sul cloud, la proprietà *ArchiveStatus* viene impostata su `None`. Tenere presente che le proprietà *ArchiveGuid* e *ArchiveName* sono vuote.

**Proprietà dell'utente di posta elettronica successive al provisioning della cassetta postale di archiviazione eseguito dalla sincronizzazione della directory**

![Proprietà della cassetta postale basata sul cloud in seguito al provisioning dell'archivio basato sul cloud](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "Proprietà della cassetta postale basata sul cloud in seguito al provisioning dell'archivio basato sul cloud")

Dopo che la sincronizzazione della directory esegue il provisioning dell'archivio basato sul cloud, la proprietà *ArchiveStatus* viene impostata su `Active` e le proprietà *ArchiveGuid* e *ArchiveName* vengono popolate. A questo punto, l'utente è in grado di accedere alla cassetta postale di archiviazione basata sul cloud in Outlook o Outlook sul Web.

![L'utente può accedere alla cassetta postale di archiviazione basata sul cloud in Outlook oppure in Outlook sul web](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "L'utente può accedere alla cassetta postale di archiviazione basata sul cloud in Outlook oppure in Outlook sul web")

È anche possibile eseguire il comando PowerShell seguente nell'organizzazione locale di Exchange al fine di visualizzare le proprietà correlate alla casetta postale di archiviazione basata sul cloud dell'utente.

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**Proprietà della cassetta postale locale precedenti al provisioning della cassetta postale di archiviazione eseguito dalla sincronizzazione della directory**

![Proprietà della cassetta postale prima del provisioning dell'archivio basato sul cloud](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "Proprietà della cassetta postale prima del provisioning dell'archivio basato sul cloud")

Prima che la sincronizzazione della directory esegua il provisioning dell'archivio basato sul cloud, la proprietà *ArchiveStatus* viene impostata su `None` e la proprietà *ArchiveState* viene impostata su `HostedPending`.

**Proprietà della cassetta postale locale successive al provisioning della cassetta postale di archiviazione eseguito dalla sincronizzazione della directory**

![Proprietà della cassetta postale in seguito al provisioning dell'archivio basato sul cloud](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "Proprietà della cassetta postale in seguito al provisioning dell'archivio basato sul cloud")

Dopo che la sincronizzazione della directory esegue il provisioning dell'archivio basato sul cloud, la proprietà *ArchiveStatus* viene impostata su `Active` e la proprietà *ArchiveState* viene impostata su `HostedProvisioned`. A questo punto, l'utente è in grado di accedere alla cassetta postale di archiviazione basata sul cloud in Outlook o Outlook sul Web.

Inizio pagina

## (facoltativo) Eseguire la sincronizzazione delle directory

Come descritto in precedenza, la cassetta postale di archiviazione basata sul cloud viene creata dal processo di sincronizzazione della directory. Per impostazione predefinita, l'ambiente Active Directory locale viene sincronizzato con Azure AD in Office 365 una volta ogni 30 minuti. È possibile consultare l'orario dell'ultima sincronizzazione della directory andando a **Integrità** \> **Stato sincronizzazione directory** nell'interfaccia di amministrazione di Office 365.

In alcuni casi, potrebbe essere necessario avviare la sincronizzazione della directory per eseguire il provisioning della cassetta di archiviazione basata sul cloud, prima della prossima sincronizzazione programmata. A tale scopo, eseguire il comando PowerShell seguente nel server in cui Azure AD Connect è installato.

    Start-ADSyncSyncCycle -PolicyType Delta

Per ulteriori informazioni, vedere [Sincronizzazione di Azure AD Connect: Utilità di pianificazione](https://go.microsoft.com/fwlink/p/?linkid=836813).

Inizio pagina

