---
title: 'Posta elettronica attiva o Disattiva posta una cartella pubblica: Exchange 2013 Help'
TOCTitle: Posta elettronica attiva o Disattiva posta una cartella pubblica
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50480404
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Posta elettronica attiva o Disattiva posta una cartella pubblica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-06-15_

Cartelle pubbliche sono progettate per l'accesso condiviso e offrono un modo semplice ed efficace per raccogliere, organizzare e condividere informazioni con altre persone del gruppo di lavoro o dell'organizzazione. Abilitare alla posta una cartella pubblica consente agli utenti di inserire nella cartella pubblica inviando un messaggio di posta elettronica. Quando una cartella pubblica è abilitato alla posta ulteriori impostazioni saranno disponibili per la cartella pubblica nell'interfaccia di amministrazione Exchange (EAC), ad esempio gli indirizzi di posta elettronica e le quote di posta elettronica. In Shell, prima di una cartella pubblica è abilitati alla posta elettronica, è utilizzare il cmdlet **Set-PublicFolder** per gestire impostazioni delle relative. Dopo la cartella pubblica è abilitato alla posta, utilizzare cmdlet **Set-MailPublicFolder** e **Set-PublicFolder** per gestire le impostazioni.

Se si desidera utenti su Internet per inviare posta a una cartella pubblica abilitata alla posta elettronica, è necessario impostare autorizzazioni aggiunta utilizzando il cmdlet **Add-PublicFolderClientPermission** .

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per garantire che gli utenti su Internet possono inviare messaggi di posta elettronica a una cartella pubblica abilitata alla posta elettronica, la cartella pubblica deve disporre almeno *CreateItems* diritto di accesso concesso all'account anonimo. Se si desidera informazioni su come eseguire questa operazione, consultare Consenti agli utenti anonimi di inviare la posta elettronica a una cartella pubblica abilitati alla posta elettronica.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EAC per posta elettronica abilitare o disabilitare una cartella pubblica

1.  Accedere a **Cartelle pubbliche** \> **Cartelle pubbliche**.

2.  Nella visualizzazione elenco, selezionare la cartella pubblica che si desidera disabilitare o abilitare alla posta.

3.  Nel riquadro dei dettagli, in **Impostazioni posta elettronica**, scegliere **abilitare** o **disabilitare**.

4.  Verrà visualizzata una finestra di avviso in cui viene chiesto che se si è certi che si desidera abilitare o disabilitare la posta elettronica per la cartella pubblica. Fare clic su **Sì** per continuare.

Se si desidera che gli utenti esterni possano inviare posta a questa cartella pubblica, verificare che la procedura indicata in Consenti agli utenti anonimi di inviare la posta elettronica a una cartella pubblica abilitata alla posta elettronica.

## Utilizzo della Shell per abilitare alla posta una cartella pubblica

In questo esempio stampa abilita la cartella pubblica Help Desk.

    Enable-MailPublicFolder -Identity "\Help Desk"

Questo esempio viene abilitato posta i rapporti di cartelle pubbliche nella cartella pubblica Marketing, ma nascosto nella cartella dall'elenco degli indirizzi.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

Se si desidera che gli utenti esterni possano inviare posta a questa cartella pubblica, verificare che la procedura indicata in Consenti agli utenti anonimi di inviare la posta elettronica a una cartella pubblica abilitata alla posta elettronica.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Enable-MailPublicFolder](https://technet.microsoft.com/it-it/library/aa998824\(v=exchg.150\)).

## Utilizzo della Shell per disabilitare una cartella pubblica

Questo esempio viene disabilitata dalla posta elettronica della cartella pubblica Marketing\\Reports.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Disable-MailPublicFolder](https://technet.microsoft.com/it-it/library/bb123781\(v=exchg.150\)).

## Consentire agli utenti anonimi di inviare posta elettronica a una cartella pubblica abilitata alla posta elettronica

È possibile utilizzare Outlook o la Shell per impostare le autorizzazioni per l'account anonimo della cartella pubblica. È possibile utilizzare EAC per impostare autorizzazioni per l'account anonimo.

**Utilizzano Outlook per impostare le autorizzazioni per l'account anonimo**

1.  Aprire Outlook utilizzando un account che è stato concesso autorizzazioni proprietario per la cartella pubblica abilitata alla posta elettronica che per gli utenti anonimi di inviare la posta.

2.  Accedere a **cartelle pubbliche - \< nome \>**.

3.  Passare alla cartella pubblica che si desidera modificare.

4.  Pulsante destro del mouse su cartelle pubbliche, fare clic su **proprietà** e quindi selezionare la scheda **autorizzazioni**.

5.  Selezionare l'account **anonimo**, selezionare **Crea elementi** in **scrittura** e quindi fare clic su **OK**.

**Utilizzo della Shell per impostare le autorizzazioni per l'account anonimo**

In questo esempio viene impostato l'autorizzazione `CreateItems` per l'account anonimo per la cartella pubblica "Feedback dei clienti" abilitati alla posta elettronica.

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Add-PublicFolderClientPermission](https://technet.microsoft.com/it-it/library/bb124743\(v=exchg.150\)).

