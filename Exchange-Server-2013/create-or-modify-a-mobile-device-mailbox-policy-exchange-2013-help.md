---
title: 'Creare o modificare un criterio cassetta postale di dispositivo mobile: Exchange 2013 Help'
TOCTitle: Creare o modificare un criterio cassetta postale di dispositivo mobile
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 50481461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare o modificare un criterio cassetta postale di dispositivo mobile

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-16_

Un criterio cassetta postale per i dispositivi mobili consente di applicare un set di impostazioni per il dispositivo mobile e la sicurezza a un gruppo di utenti. È possibile creare più criteri cassetta postale per dispositivi mobili. A ciascun destinatario dell'organizzazione deve essere assegnato un criterio cassetta postale per il dispositivo mobile. Quando si installa Microsoft Exchange Server 2013, viene creato un criterio cassetta postale per il dispositivo mobile predefinito a cui vengono automaticamente assegnati i nuovi utenti. Per assegnare utenti specifici a un criterio cassetta postale per il dispositivo mobile, vedere [Aggiungere o rimuovere utenti da un criterio cassetta postale per dispositivi mobili](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md).

Per ulteriori informazioni relative al criterio cassetta postale per il dispositivo mobile, vedere [Criteri cassetta postale di dispositivo mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criterio cassetta postale per i dispositivi mobili" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di un nuovo criterio cassetta postale per il dispositivo mobile

È possibile utilizzare Interfaccia di amministrazione di Exchange per creare un nuovo criterio cassetta postale per il dispositivo mobile.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criterio cassetta postale per i dispositivi mobili" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Creazione di un nuovo criterio cassetta postale per il dispositivo mobile tramite EAC

È possibile creare un nuovo criterio cassetta postale per il dispositivo mobile tramite Interfaccia di amministrazione di Exchange.


> [!NOTE]
> In EAC è possibile configurare solo un sottoinsieme di impostazioni del criterio cassetta postale per il dispositivo mobile. Per configurare le impostazioni del criterio cassetta postale per il dispositivo mobile, è necessario utilizzare Shell.



1.  In Interfaccia di amministrazione di Exchange fare clic su **Mobile** \> **Criteri cassetta postale per dispositivo mobile** quindi su **Nuovo**.

2.  Utilizzare le varie caselle di controllo e gli elenchi a discesa per configurare le impostazioni per il criterio cassetta postale per il dispositivo mobile.
    

    > [!WARNING]
    > Selezionare <STRONG>Si tratta dei criteri predefiniti</STRONG> per rendere predefinito il nuovo criterio cassetta postale per il dispositivo mobile. Dopo aver impostato come predefinito il criterio cassetta postale per il dispositivo mobile, a tutti i nuovi utenti che vengono creati verrà automaticamente assegnato tale criterio.



3.  Fare clic su **Salva**.

## Creazione di un nuovo criterio cassetta postale per il dispositivo mobile tramite Shell

È possibile creare un nuovo criterio cassetta postale per il dispositivo mobile tramite il cmdlet New-MobileDeviceMailboxPolicy.


> [!WARNING]
> Sono presenti due cmdlet che possono essere utilizzati per creare un nuovo criterio cassetta postale per il dispositivo mobile. Il cmdlet <STRONG>New-ActiveSyncMailboxPolicy</STRONG> e il cmdlet <STRONG>New-MobileDeviceMailboxPolicy</STRONG> eseguono le stesse attività. In una versione futura di Microsoft Exchange Server verrà rimosso il cmdlet <STRONG>New-ActiveSyncMailboxPolicy</STRONG>. Si consiglia di aggiornare gli script e le procedure per utilizzare il cmdlet <STRONG>New-MobileDeviceMailboxPolicy</STRONG>.



1.  In Shell, utilizzare il seguente comando.
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione del criterio cassetta postale per il dispositivo mobile, utilizzare una delle seguenti opzioni:

1.  In Interfaccia di amministrazione di Exchange fare clic su **Mobile** \> **Criteri cassetta postale per dispositivo mobile** e verificare che il nuovo criterio sia presente nella visualizzazione Elenco.

2.  In Shell, utilizzare il seguente comando.
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## Modifica di un criterio cassetta postale per il dispositivo mobile esistente

Per modificare un criterio cassetta postale per il dispositivo mobile, è possibile utilizzare Interfaccia di amministrazione di Exchange oppure Shell.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criterio cassetta postale per i dispositivi mobili" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Modifica di un criterio cassetta postale per il dispositivo mobile tramite EAC

È possibile modificare un criterio cassetta postale per il dispositivo mobile tramite Interfaccia di amministrazione di Exchange.


> [!NOTE]
> In Interfaccia di amministrazione di Exchange è possibile modificare solo un sottoinsieme di impostazioni del criterio cassetta postale per il dispositivo mobile. Per modificare le impostazioni del criterio cassetta postale per il dispositivo mobile, è necessario utilizzare Shell.



1.  In Interfaccia di amministrazione di Exchange fare clic su **Mobile** \> **Criteri cassetta postale per dispositivo mobile**.

2.  Selezionare un criterio dalla visualizzazione Elenco e fare clic sul pulsante **Modifica**.

3.  Utilizzare le schede **Generale** e **Protezione** per modificare le impostazioni del criterio cassetta postale del dispositivo mobile.

4.  Fare clic su **Salva** per aggiornare il criterio.

## Modifica delle impostazioni del criterio cassetta postale per il dispositivo mobile tramite Shell

È possibile utilizzare Shell per modificare un criterio cassetta postale per il dispositivo mobile.


> [!WARNING]
> Sono presenti due cmdlet che possono essere utilizzati per modificare un criterio cassetta postale per il dispositivo mobile. Il cmdlet Set-ActiveSyncMailboxPolicy e il cmdlet Set-MobileDeviceMailboxPolicy eseguono le stesse attività. In una versione futura di Microsoft Exchange Server verrà rimosso il cmdlet <STRONG>Set-ActiveSyncMailboxPolicy</STRONG>. Si consiglia di aggiornare gli script e le procedure per utilizzare il cmdlet <STRONG>Set-MobileDeviceMailboxPolicy</STRONG>.



1.  In Shell, utilizzare il seguente comando.
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica del criterio cassetta postale per il dispositivo mobile, effettuare una delle seguenti operazioni:

1.  in Interfaccia di amministrazione di Exchange fare clic su **Mobile** \> **Criteri cassetta postale per dispositivo mobile**, quindi scegliere un criterio specifico. Nel riquadro Dettagli verrà visualizzato un elenco delle impostazioni del criterio.

2.  In Shell, utilizzare il seguente comando.
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName>

