---
title: 'Aggiungere o rimuovere utenti da un criterio cassetta postale per dispositivi mobili: Exchange 2013 Help'
TOCTitle: Aggiungere o rimuovere utenti da un criterio cassetta postale per dispositivi mobili
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 50480626
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere o rimuovere utenti da un criterio cassetta postale per dispositivi mobili

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-07-16_

Un criterio cassetta postale per i dispositivi mobili consente di applicare un set di impostazioni per il dispositivo mobile e la sicurezza a un gruppo di utenti. È possibile creare più criteri cassetta postale per dispositivi mobili.


> [!WARNING]
> Quando si installa Microsoft Exchange Server 2013, viene creato un criterio cassetta postale per il dispositivo mobile predefinito e a tutti gli utenti viene automaticamente assegnato questo criterio.



Per le altre attività di gestione correlate ai criteri delle cassette postali del dispositivo mobile, vedere [Criteri cassetta postale di dispositivo mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criterio cassetta postale per i dispositivi mobili" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - È necessario disporre di un Criterio cassetta postale per il dispositivo mobile nell''interfaccia di amministrazione di Exchange in **Mobile** \> **Criteri cassetta postale per dispositivi mobili**.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Modificare un criterio cassetta postale per il dispositivo mobile di un utente

È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per modificare un criterio cassetta postale per il dispositivo mobile di un utente.

## Utilizzo dell'interfaccia di amministrazione di Exchange per modificare un criterio cassetta postale per il dispositivo mobile di un utente

Si modifica un criterio cassetta postale per il dispositivo mobile di un singolo utente utilizzando l'interfaccia di amministrazione di Exchange.

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali** e quindi selezionare una cassetta postale.

2.  Nel riquadro Dettagli, scorrere verso il basso fino a **Funzionalità telefono e messaggistica vocale** e selezionare **Visualizza dettagli** per visualizzare lo schermo **Dettagli dispositivo mobile**.

3.  Viene visualizzato il criterio cassetta postale di dispositivo mobile attualmente assegnato. Per modificare i criteri cassetta postale di dispositivo mobile, fare clic su **Sfoglia**.

4.  Selezionare i corretti criteri cassetta postale di dispositivo mobile dall'elenco, fare clic su **OK** quindi fare clic su **Salva**.

## Utilizzo dell'interfaccia di amministrazione di Exchange per modificare un criterio cassetta postale per il dispositivo mobile di un utente

È possibile modificare criterio cassetta postale di dispositivo mobile un singolo utente utilizzando il cmdlet **Set-CASMailbox** in Shell.

1.  In Shell, utilizzare il seguente comando.
    
        Set-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stato cambiato un criterio cassetta postale per il dispositivo mobile di un utente, eseguire una di queste operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali** e quindi selezionare un destinatario specifico. Nel riquadro Dettagli, scorrere verso il basso fino a **Funzionalità telefono e messaggistica vocale** e fare clic su **Visualizza dettagli**.

2.  In Shell, utilizzare il seguente comando.
    
        Get-CASMailbox -Identity tony@contoso.com 

## Modifica dei criteri delle cassette postali del dispositivo mobile per più utenti allo stesso tempo

Se si desidera modificare i criteri delle cassette postali del dispositivo mobile per più utenti allo stesso tempo, è possibile utilizzare la funzionalità di modifica in blocco nell'interfaccia di amministrazione di Exchange o utilizzare Shell per modificare i criteri delle cassette postali del dispositivo mobile per un insieme filtrato di utenti.

## Utilizzo dello strumento della modifica in blocco nell'interfaccia di amministrazione di Exchange per modificare i criteri delle cassette postali del dispositivo mobile per più utenti

È possibile aggiornare i criteri delle cassette postali del dispositivo mobile per più utenti allo stesso tempo utilizzando la funzionalità Modifica in blocco.

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali**.

2.  Selezionare più utenti.

3.  Nel riquadro Dettagli, scorrere fino a **Exchange ActiveSync** e fare clic su **Aggiorna i criteri**.

4.  Fare clic su **Sfoglia** per scegliere un criterio cassetta postale di dispositivo mobile.

5.  Fare clic su **OK** e quindi scegliere **Salva**.

## Utilizzo di Shell per modificare i criteri cassetta postale per i dispositivi mobili per un gruppo di utenti filtrati

È possibile utilizzare Shell per modificare i criteri delle cassette postali del dispositivo mobile per un gruppo di utenti filtrati. È possibile filtrare gli utenti su una varietà di attributi.

1.  In Shell, utilizzare il seguente comando.
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    

    > [!NOTE]
    > È possibile sostituire <CODE>CustomAttribute1</CODE> per le proprietà dell'oggetto <STRONG>Get-Mailbox</STRONG>. Per visualizzare l'elenco completo, digitare quanto segue: <CODE>Get-Mailbox username |fl</CODE>.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stato cambiato un criterio cassetta postale per il dispositivo mobile di un utente, eseguire una di queste operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Cassette postali**, quindi selezionare un destinatario specifico. Nel riquadro Dettagli, scorrere verso il basso fino a **Funzionalità telefono e messaggistica vocale** e fare clic su **Visualizza dettagli**.

2.  In Shell, utilizzare il seguente comando.
    
        Get-CASMailbox -Identity tony@contoso.com

