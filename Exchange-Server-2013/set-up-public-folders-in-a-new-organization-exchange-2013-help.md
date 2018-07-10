---
title: 'Configurare cartelle pubbliche in una nuova organizzazione: Exchange 2013 Help'
TOCTitle: Configurare cartelle pubbliche in una nuova organizzazione
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 50480955
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare cartelle pubbliche in una nuova organizzazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-11-09_

**Riepilogo:**  come configurare le cartelle pubbliche, inclusa l'assegnazione delle autorizzazioni a tali in EAC.

Nel presente argomento viene illustrato come scaricare le cartelle pubbliche configurate e in esecuzione in una nuova organizzazione o in un'organizzazione che non ha mai avuto cartelle pubbliche in precedenza.


> [!NOTE]
> Per ulteriori informazioni sulle quote di archiviazione e sui limiti relativi alle cartelle pubbliche, consultare i seguenti argomenti: 
> <UL>
> <LI>
> <P>Per ulteriori informazioni sulle cartelle pubbliche di Office 365, vedere <A href="https://go.microsoft.com/fwlink/?linkid=391188">Limiti di Exchange Online</A>.</P>
> <LI>
> <P>Per informazioni sulle cartelle pubbliche su Exchange Server 2013 locale, vedere <A href="limits-for-public-folders-exchange-2013-help.md">Limiti per le cartelle pubbliche</A>.</P></LI></UL>



Per ulteriori attività di gestione relative alle cartelle pubbliche Exchange Server 2013, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per ulteriori attività di gestione relative alle cartelle pubbliche in Exchange Online, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 30 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Creare la cassetta postale delle cartelle pubbliche primaria

La cassetta postale delle cartelle pubbliche principale contiene una copia scrivibile della gerarchia delle cartelle pubbliche più il contenuto ed è la prima cassetta postale delle cartelle pubbliche che viene creata per l'organizzazione. Le cassette postali delle cartelle pubbliche create successivamente saranno le cassette secondarie, che conterranno una copia di sola lettura della gerarchia più contenuto.

Per la procedura dettagliata, vedere [Creazione di una cassetta postale di cartelle pubbliche](create-a-public-folder-mailbox-exchange-2013-help.md).

## Passaggio 2: Creare la prima cartella pubblica

Per la procedura dettagliata, vedere [Creare una cartella pubblica](create-a-public-folder-exchange-2013-help.md).

## Passaggio 3: Assegnare le autorizzazioni per la cartella pubblica

Dopo aver creato la cartella pubblica, sarà necessario assegnare le autorizzazioni di **Proprietario** in modo che almeno un utente possa accedere alla cartella pubblica dal client e creare le sottocartelle. Tutte le cartelle pubbliche create dopo la prima erediteranno le autorizzazioni della cartella pubblica genitore.

1.  In Interfaccia di amministrazione di Exchange accedere a **Cartelle pubbliche** \> **Cartelle pubbliche**.

2.  Nell'elenco, selezionare la cartella pubblica.

3.  Nel riquadro dei dettagli, in **Autorizzazioni cartella** fare clic su **Gestione**.

4.  In **Autorizzazioni per le cartelle pubbliche**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Fare clic su **Sfoglia** per selezionare un utente.

6.  Nell'elenco **Livello di autorizzazione**, selezionare un livello. Almeno un utente deve essere impostato come **Proprietario**.

7.  Fare clic su **Salva**.

8.  È possibile aggiungere più utenti facendo clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e assegnare loro le autorizzazioni appropriate seguendo le procedure illustrate in precedenza. È inoltre possibile personalizzare il livello di autorizzazione selezionando o deselezionando le caselle di controllo. Quando si modifica un livello di autorizzazione predefinito (ad esempio, **Proprietario**), il livello di autorizzazione diventa **Personalizzato**.

Per informazioni sull'utilizzo della shell per assegnare le autorizzazioni a una cartella pubblica, vedere [Add-PublicFolderClientPermission](https://technet.microsoft.com/it-it/library/bb124743\(v=exchg.150\)).

## (Facoltativo) Procedura 4: Abilitare la cartella pubblica per la posta

Se si desidera che gli utenti possano inviare dei messaggi alla cartelle pubblica, è possibile abilitarla per la posta. Questo passaggio è facoltativo. Se non si abilita la cartella pubblica per la posta, gli utenti possono pubblicare i messaggi nella cartella trascinandoli da Outlook.

1.  Nell'Interfaccia di amministrazione di Exchange, accedere a **Cartelle pubbliche** \> **Cartelle pubbliche**.

2.  Nell'elenco, selezionare la cartella pubblica che si desidera abilitare per la posta.

3.  Nel riquadro dei dettagli, in **Impostazioni della posta – Disabilitata**, fare clic su **Abilita**.
    
    Verrà visualizzato un avviso che richiede se si è certi di voler abilitare la posta per la cartella pubblica. Fare clic su **Sì**.

La cartella pubblica sarà abilitata per la posta e il suo nome sarà utilizzato come alias. Se sono già presenti più destinatari con quel nome, all'alias della cartella pubblica verrà aggiunto un numero. Ad esempio, se è già presente un gruppo di distribuzione denominato SalesTeam, quando si crea una cartella pubblica denominata SalesTeam e la si abilita per la posta, il suo alias sarà SalesTeam1.

Per informazioni sull'utilizzo della shell per abilitare alla posta una cartella pubblica, vedere [Enable-MailPublicFolder](https://technet.microsoft.com/it-it/library/aa998824\(v=exchg.150\)).

