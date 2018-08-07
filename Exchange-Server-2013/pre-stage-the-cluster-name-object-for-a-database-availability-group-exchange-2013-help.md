---
title: 'Oggetto nome cluster per gruppo disponibilità del database: Exchange 2013 Help'
TOCTitle: Pregestione dell'oggetto nome cluster per un gruppo di disponibilità del database
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 50480596
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pregestione dell'oggetto nome cluster per un gruppo di disponibilità del database

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-08-14_

In ambienti in cui la creazione dell'account computer è limitato o in cui vengono creati account computer in un contenitore diverso dal contenitore di computer predefinito, è possibile pregestione cluster nome oggetto (CNO) e quindi eseguire il provisioning il CNO mediante l'assegnazione di autorizzazioni a esso. Pregestione il CNO è richiesto anche per Windows Server 2012 e Windows Server 2012 R2 DAG membri a causa di modifiche apportate alle autorizzazioni di Windows per gli oggetti computer. Quando si distribuisce un gruppo di disponibilità del database (DAG) utilizzando server cassette postali che eseguono Windows Server 2012 o Windows Server 2012 R2, è necessario pregestione e fornire il CNO, a meno che non si sta distribuendo un DAG senza un punto di accesso di amministrazione cluster. DAG senza punti di accesso amministrativo cluster inutilizzato CNOs; di conseguenza pregestione non sia necessario per tali DAG.

Creare e disabilitare un account computer per il CNO, quindi:

  - Assegnare il controllo completo dell'account computer all'account computer del primo server Cassette postali aggiunto al DAG.

  - Assegnare il controllo completo dell'account computer al gruppo di protezione universale Exchange Trusted Subsystem.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto

  - È necessario utilizzare una account che abbia le autorizzazione per creare gli oggetti computer in Active Directory.

  - Una volta completata la seguente procedura, attendere per la replica di Active Directory. Dopo aver replicato l'oggetto, è possibile aggiungere il primo membro al gruppo di disponibilità del database.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Pregestione dell'oggetto di rete cluster

1.  Aprire Utenti e computer di Active Directory.

2.  Espandere il nodo della foresta.

3.  Fare clic con il pulsante destro del mouse sull'unità organizzativa (OU) in cui si desidera creare il nuovo account, selezionare **Nuovo** e **Computer**.

4.  In **Nuovo oggetto - Computer**, digitare il nome dell'account computer per l'oggetto di rete cluster nella casella **Nome computer**. Questo nome verrà utilizzato anche per il gruppo di disponibilità del database. Fare clic su **OK** per creare l'account.

5.  Fare clic con il pulsante destro del mouse sul nuovo account computer e fare clic su **Disabilita account**. Fare clic su **Sì** per confermare l'azione, quindi fare clic su **OK**.

## Assegnazione delle autorizzazioni all'oggetto di rete cluster

1.  Aprire Utenti e computer di Active Directory.

2.  Se non sono abilitate, attivare le funzionalità avanzate facendo clic su **Visualizza**, quindi su **Funzionalità avanzate**.

3.  Fare clic con il pulsante destro del mouse sul nuovo account computer, quindi fare clic su **Proprietà**.

4.  In **Proprietà \<Nome computer\>**, nella scheda **Protezione**, fare clic su **Aggiungi** per aggiungere l'account computer per il primo nodo da aggiungere al gruppo di disponibilità del database o aggiungere il gruppo di protezione universale Exchange Trusted Subsystem:
    
      - Per aggiungere Exchange Trusted Subsystem, digitare **Exchange Trusted Subsystem** nel campo **Immettere i nomi degli oggetti da selezionare**. Fare clic su **OK** per aggiungere il gruppo di protezione universale. Selezionare il gruppo di protezione universale Exchange Trusted Subsystem e in **Autorizzazioni per il campo Exchange Trusted Subsystem**, selezionare **Controllo completo** nella colonna **Consenti**. Fare clic su **OK** per salvare le impostazioni delle autorizzazioni.
    
      - Per aggiungere l'account computer per il primo nodo da aggiungere al gruppo di disponibilità del database, fare clic su **Tipi di oggetto**. Nella finestra di dialogo **Tipi di oggetto**, deselezionare le caselle di controllo **Entità di sicurezza incorporate**, **Gruppi** e **Utenti**. Selezionare la casella di controllo **Computer**, quindi scegliere **OK**. Nel campo **Immettere i nomi degli oggetti da selezionare**, digitare il nome del primo server Cassette postali da aggiungere al gruppo di disponibilità del database, quindi fare clic su **OK**. Selezionare l'account computer del primo nodo e nel campo **Autorizzazioni per \<NodeName\>** selezionare **Controllo completo** nella colonna **Consenti**. Fare clic su **OK** per salvare le impostazioni delle autorizzazioni.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che il CNO sia stato creato correttamente, procedere come segue:

1.  Aprire Utenti e computer di Active Directory.

2.  Espandere il nodo della foresta.

3.  Aprire l'unità organizzativa (OU) in cui è stato creato l'account e verificare che l'account sia nell'elenco.

