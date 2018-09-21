---
title: 'Visualizza info. su dispos. mobili per utenti: Exchange 2013 Help'
TOCTitle: Visualizzare informazioni sui dispositivi mobili per gli utenti
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 50480585
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare informazioni sui dispositivi mobili per gli utenti

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-29_

Gli utenti possono configurare più dispositivi mobili per la sincronizzazione con MicrosoftExchange Server 2013. È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per visualizzare un elenco di dispositivi mobili associati a uno specifico utente.

Per altre attività di gestione relative ai dispositivi mobili, vedere [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criterio cassetta postale per i dispositivi mobili" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la visualizzazione delle informazioni sui dispositivi mobili degli utenti

L'interfaccia di amministrazione di Exchange visualizza l'elenco dei dispositivi mobili sincronizzati con la cassetta postale di un utente. È possibile visualizzare i dispositivi mobili raggruppati per famiglia, modello, numero di telefono o stato.

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali** e scegliere una cassetta postale.

2.  Nel riquadro Dettagli, scorrere fino a **Funzionalità telefoniche e vocali** e fare clic su **Visualizza dettagli** per visualizzare la schermata **Dettagli dispositivo mobile**.

## Utilizzo di Shell per la visualizzazione delle informazioni sui dispositivi mobili degli utenti

È possibile utilizzare il cmdlet **Get-MobileDevice** per visualizzare un elenco di dispositivi mobili per uno specifico utente.

1.  Eseguire il comando riportato di seguito.
    
    ```powershell
Get-MobileDevice -Mailbox useralias
```

