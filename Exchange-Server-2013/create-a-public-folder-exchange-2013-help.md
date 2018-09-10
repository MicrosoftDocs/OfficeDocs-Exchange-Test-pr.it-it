---
title: 'Creare una cartella pubblica: Exchange 2013 Help'
TOCTitle: Creare una cartella pubblica
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 50480944
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# Creare una cartella pubblica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-24_

Le cartelle pubbliche sono progettate per l'accesso condiviso e offrono un metodo semplice ed efficace per raccogliere, organizzare e condividere le informazioni con altre persone del gruppo di lavoro o dell'organizzazione.

Per impostazione predefinita, una cartella pubblica eredita le impostazioni della cartella principale, incluse le impostazioni delle autorizzazioni.


> [!NOTE]
> Per ulteriori informazioni sulle quote di archiviazione e sui limiti relativi alle cartelle pubbliche, consultare i seguenti argomenti: 
> <UL>
> <LI>
> <P>Per ulteriori informazioni sulle cartelle pubbliche di Office 365, vedere <A href="https://go.microsoft.com/fwlink/?linkid=391188">Limiti di Exchange Online</A>.</P>
> <LI>
> <P>Per informazioni sulle cartelle pubbliche su Exchange Server 2013 locale, vedere <A href="limits-for-public-folders-exchange-2013-help.md">Limiti per le cartelle pubbliche</A>.</P></LI></UL>



Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Non è possibile creare una cartella pubblica prima di aver creato una cassetta postale delle cartelle pubbliche. Per ulteriori informazioni su come creare una cassetta postale delle cartelle pubbliche, vedere [Creazione di una cassetta postale di cartelle pubbliche](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/create-public-folder-mailbox).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Per saperne di più

## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di una cartella pubblica

Quando si utilizza l'interfaccia di amministrazione per creare una cartella pubblica, è possibile impostarne solamente il nome e il percorso. Per configurare altre impostazioni, è necessario modificare la cartella pubblica dopo averla creata.

1.  Accedere a **Cartelle pubbliche** \> **Cartelle pubbliche**.

2.  Se si desidera creare questa cartella pubblica come elemento figlio di una cartella pubblica esistente, fare clic sulla cartella pubblica esistente nell'elenco. Se si desidera creare una cartella pubblica di livello superiore, ignorare questo passo.

3.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  In **Cartella pubblica**, digitare il nome della cartella pubblica.
    

    > [!IMPORTANT]
    > Non utilizzare la barra rovesciata (\) nel nome durante la creazione di una cartella pubblica.



5.  Nella casella **Percorso**, verificare il percorso per questa cartella pubblica. Se non è quello desiderato, fare clic su **Annulla** e seguire il passo 2 di questa procedura.

6.  Fare clic su **Salva**.

## Creazione di una cartella pubblica tramite Shell

In questo esempio, nel percorso Marketing\\2013 viene creata una cartella pubblica denominata Rapporti.

    New-PublicFolder -Name Reports -Path \Marketing\2013


> [!IMPORTANT]
> Non utilizzare la barra rovesciata (\) nel nome durante la creazione di una cartella pubblica.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-PublicFolder](https://technet.microsoft.com/it-it/library/aa996405\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver creato correttamente una cartella pubblica, fare quanto segue:

  - Nell'interfaccia di amministrazione di Exchange, fare clic su **Aggiorna** per aggiornare l'elenco delle cartelle pubbliche. La nuova cartella pubblica verrà visualizzata nell'elenco.

  - In Shell, utilizzare uno dei seguenti comandi:
    ```
    Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    ```
    ```
    Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    ```
    ```
    Get-PublicFolder -Recurse
    ```


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


