---
title: 'Creare una ricerca dei registri di controllo delle cassette postali: Exchange 2013 Help'
TOCTitle: Creare una ricerca dei registri di controllo delle cassette postali
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 50480579
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una ricerca dei registri di controllo delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-11_

È possibile creare una ricerca nel registro di controllo di una cassetta postale in modo che una ricerca asincrona venga eseguita in una o più cassette postali e i risultati ottenuti vengano inviati sotto forma di file XML agli indirizzi di posta elettronica specificati.

Per effettuare la ricerca nei registri di controllo delle cassette postali per una singola cassetta postale e visualizzare i risultati nella finestra Shell, vedere [Il Registro di controllo delle cassette postali per una cassetta postale di ricerca](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

Per altre attività di gestione relative alla registrazione di controllo delle cassette postali, vedere [Procedure di registrazione di controllo delle cassette postali](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo delle cassette postali" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, la registrazione del controllo delle cassette postali è disabilitato per tutte le cassette postali. Per ciascuna cassetta postale in cui si desidera eseguire il controllo, è necessario abilitare la registrazione del controllo e specificare le azioni (del proprietario, del delegato o dell'amministratore) da controllare. Per ulteriori dettagli, vedere [Abilitare o disabilitare la registrazione per una cassetta postale di controllo delle cassette postali](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per cercare gli accessi da parte dei proprietari nel registro di controllo delle cassette postali. La sezione di controllo nell'interfaccia di amministrazione di Exchange include dei rapporti relativi all'accesso alle cassette postali da parte di utenti diversi dai proprietari e consente di cercare ed esportare questi eventi di accesso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di una ricerca nei registri di controllo delle cassette postali

1.  Accedere a **Gestione conformità** \> **Controllo**.

2.  Nell'elenco, selezionare **Esporta i registri di controllo della cassetta postale**.

3.  In **Esporta i registri di controllo della cassetta postale**, completare i seguenti campi, quindi fare clic su **Esporta**:
    
      - **Data di inizio**
    
      - **Data di fine**
    
      - **Cerca in queste cassette postali o lascia il campo vuoto per trovare tutte le cassette postali a cui accedono utenti non proprietari**
        

        > [!WARNING]
        > A seconda del numero di cassette postali nell'organizzazione e della quantità di dati nei registri di controllo delle cassette postali, la ricerca potrebbe richiedere molto tempo.

    
      - **Cerca accesso eseguito da**
        
        Selezionare gli eventi di accesso che si desidera cercare:
        
          - **Tutti i non proprietari**
        
          - **Utenti esterni**
        
          - **Amministratori e utenti delegati**
        
          - **Amministratori**
    
      - **Invia il rapporto di verifica a**

## Creazione di una ricerca nei registri di controllo delle cassette postali tramite Shell

Per un esempio sull'utilizzo di Shell per la creazione di una ricerca nel registro di controllo di una cassetta postale, vedere [Example 1](https://technet.microsoft.com/it-it/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1) in **New-MailboxAuditLogSearch**.

