---
title: 'Abilitare o disabilitare Exchange ActiveSync per una cassetta postale: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare Exchange ActiveSync per una cassetta postale
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50555700
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Abilitare o disabilitare Exchange ActiveSync per una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-13_

È possibile utilizzare EAC oppure Shell per abilitare o disabilitare Microsoft Exchange ActiveSync per una cassetta postale utente. Exchange ActiveSync è un protocollo client che consente agli utenti di sincronizzare un dispositivo mobile con la propria cassetta postale di Exchange. Exchange ActiveSync viene abilitato per impostazione predefinita quando viene creata una cassetta postale utente. Per ulteriori informazioni, vedere [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni di Exchange ActiveSync" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Abilitazione o disabilitazione di Exchange ActiveSync tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale che si desidera abilitare o disabilitare a Exchange ActiveSync, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Dispositivi mobili** effettuare una delle seguenti operazioni:
    
      - Per disabilitare Exchange ActiveSync, fare clic su **Disabilita Exchange ActiveSync**.
        
        Viene visualizzato un messaggio di avviso che richiede all'utente di confermare la disabilitazione di Exchange ActiveSync. Fare clic su **Sì**.
    
      - Per abilitare Exchange ActiveSync, fare clic su **Abilita Exchange ActiveSync**.

5.  Fare clic su **Salva** per salvare la modifica.


> [!NOTE]
> È possibile abilitare e disabilitare Exchange ActiveSync per più cassette postali utente tramite la funzionalità di modifica in blocco di EAC. Per ulteriori informazioni su come eseguire questa operazione, vedere la sezione "Modifica in blocco delle cassette postali utente" in <A href="manage-user-mailboxes-exchange-2013-help.md">Gestire le cassette postali degli utenti</A>.



## Abilitazione o disabilitazione di Exchange ActiveSync tramite Shell

Con questo esempio viene disabilitato Exchange ActiveSync per la cassetta postale di Yan Li.

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

Con questo esempio viene abilitato Exchange ActiveSync per la cassetta postale di Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione o disabilitazione di Exchange ActiveSync per la cassetta postale utente, effettuare una delle seguenti operazioni:

  - In EAC accedere a **Destinatari** \> **Cassette postali**, fare clic sulla cassetta postale, quindi su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

  - Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

  - Sotto **Dispositivi mobili** verificare se Exchange ActiveSync è abilitato o disabilitato.

Oppure

  - Eseguire il seguente comando in Shell.
    
        Get-CASMailbox <identity>
    
    Se Exchange ActiveSync è abilitato, il valore della proprietà *ActiveSyncEnabled* è `True`. Se Exchange ActiveSync è disabilitato, il valore è `False`.

