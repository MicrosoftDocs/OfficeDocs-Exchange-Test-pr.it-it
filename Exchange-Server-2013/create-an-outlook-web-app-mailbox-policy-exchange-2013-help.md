---
title: 'Creare un criterio cassetta postale di Outlook Web App: Exchange 2013 Help'
TOCTitle: Creare un criterio cassetta postale di Outlook Web App
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 50480322
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un criterio cassetta postale di Outlook Web App

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-05-30_

È possibile creare un criterio cassetta postale di Outlook Web App per applicare un gruppo comune di impostazioni di criteri. I criteri delle cassette postali Outlook Web App sono utili per applicare e standardizzare le impostazioni, quali le impostazioni degli allegati, per un gruppo specifico di utenti.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per poter eseguire questo cmdlet, è necessario disporre delle autorizzazioni appropriate. Sebbene in questo argomento vengano elencati tutti i parametri relativi al cmdlet, è possibile che alcuni di essi non siano accessibili se non sono inclusi nelle autorizzazioni di cui si dispone. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di Outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di un criterio cassetta postale di Outlook Web App tramite Interfaccia di amministrazione di Exchange

1.  In EAC, fare clic su **Autorizzazioni** \> **Criteri di Outlook Web App**.

2.  Fare clic sul pulsante **Nuovo**.

3.  
    
    Immettere un nome per il criterio.

4.  
    
    Utilizzare le caselle di controllo per abilitare o disabilitare le funzionalità. Per impostazione predefinita sono visualizzate le funzionalità più comuni. Per vedere tutte le funzionalità che possono essere abilitate o disabilitate, fare clic su **Altre opzioni**.
    

    > [!NOTE]
    > Le impostazioni delle funzionalità per i criteri della cassetta postale Outlook Web App hanno precedenza sulle impostazioni della directory virtuale Outlook Web App. È possibile modificare le impostazioni di segmentazione per singoli utenti utilizzando il cmdlet <STRONG>Set-CASMailbox</STRONG> nella Shell.



5.  Fare clic su **Salva** per salvare il criterio.

## Creazione di un criterio cassetta postale di Outlook Web App tramite Shell

In questo esempio, viene creato un criterio cassetta postale di Outlook Web App denominato `Policy1`.

  - In Shell, utilizzare il seguente comando.
    
        New-OwaMailboxPolicy -Name Policy1

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-OwaMailboxPolicy](https://technet.microsoft.com/it-it/library/dd351067\(v=exchg.150\)). Per informazioni sull'uso di Shell per la configurazione di un criterio cassetta postale di Outlook Web App, vedere [Set-OwaMailboxPolicy](https://technet.microsoft.com/it-it/library/dd297989\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare l'avvenuta creazione di un criterio cassetta postale di Outlook Web App:

  - In Interfaccia di amministrazione di Exchange, fare clic su **Autorizzazioni** \> **Criteri di Outlook Web App** e cercare il nuovo criterio cassetta postale.

