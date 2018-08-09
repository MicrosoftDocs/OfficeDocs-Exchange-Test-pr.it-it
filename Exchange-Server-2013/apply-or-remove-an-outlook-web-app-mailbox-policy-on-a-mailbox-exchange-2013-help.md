---
title: 'Applic./rim. criteri Outlook Web App in cassetta postale: Exchange 2013 Help'
TOCTitle: Applicare o rimuovere un criterio cassetta postale di Outlook Web App in una cassetta postale
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 50480595
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Applicare o rimuovere un criterio cassetta postale di Outlook Web App in una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-12_

È possibile applicare un criterio cassetta postale Outlook Web App a uno o più cassette postali o rimuovere uno tramite EAC o Shell.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Criteri cassetta postale di outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md) .

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Applicare un criterio cassetta postale di Outlook Web App

## Utilizzare EAC per applicare un criterio cassetta postale di Outlook Web App

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali**.

2.  Nel riquadro di lavoro, fare clic per selezionare la cassetta postale che si desidera applicare un criterio cassetta postale Outlook Web App. È inoltre possibile selezionare più cassette postali.

3.  **Se sono state selezionate una cassetta postale:** 
    
    1.  Scorrere verso il basso nel riquadro dei dettagli per **La connettività di posta elettronica** e fare clic su **Visualizza dettagli**.
    
    2.  Fare clic su **Sfoglia** per visualizzare e selezionare i criteri cassetta postale disponibili.
    
    3.  Fare clic su **Salva** per assegnare il criterio selezionato per la cassetta postale selezionata.
    
    **Se sono state selezionate più cassette postali:** 
    
    1.  Scorrere verso il basso nel riquadro dei dettagli a **Outlook Web App** e fare clic su **Assegna un criterio**.
    
    2.  Fare clic su **Sfoglia** per visualizzare e selezionare i criteri cassetta postale disponibili.
    
    3.  Fare clic su **Salva** per assegnare il criterio selezionato a cassette postali selezionate.

## Utilizzo della Shell per applicare un criterio cassetta postale di Outlook Web App a una cassetta postale esistente

In questo esempio viene applicato il criterio cassetta postale Outlook Web App denominato "Calendario" alla cassetta postale dell'utente tony@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Rimuovere un criterio cassetta postale di Outlook Web App

## Utilizzo dell'interfaccia di amministrazione di Exchange per rimuovere un criterio cassetta postale di Outlook Web App

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali**.

2.  Nel riquadro di lavoro, fare clic per selezionare la cassetta postale che si desidera rimuovere un criterio cassetta postale Outlook Web App da.

3.  Scorrere verso il basso nel riquadro dei dettagli per **La connettività di posta elettronica** e fare clic su **Visualizza dettagli**.
    
    Se è stato assegnato un criterio cassetta postale, fare clic su **Cancella** per rimuovere dalla cassetta postale.

4.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzare Shell per rimuovere un criterio cassetta postale di Outlook Web App da una cassetta postale esistente.

In questo esempio viene rimosso il criterio cassetta postale di Outlook Web App dalla cassetta postale dell'utente tony@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

