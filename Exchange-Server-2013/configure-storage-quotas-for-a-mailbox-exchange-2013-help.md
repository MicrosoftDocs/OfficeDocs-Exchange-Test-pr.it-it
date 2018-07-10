---
title: 'Configurazione delle quote di archiviazione per una cassetta postale: Exchange 2013 Help'
TOCTitle: Configurazione delle quote di archiviazione per una cassetta postale
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50555602
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione delle quote di archiviazione per una cassetta postale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-07-07_

**Riepilogo:**  utilizzare l'interfaccia di amministrazione di Exchange (EAC) o Shell per impostare le quote di archiviazione per cassette postali specifiche.

Le quote di spazio di archiviazione consentono di controllare la dimensione delle cassette postali e di gestire l'incremento dei database che queste contengono. Quando viene raggiunto o superato il limite specificato delle quote di archiviazione della cassetta postale, Exchange invia una notifica descrittiva al proprietario della cassetta postale.


> [!NOTE]
> Le quote di spazio di archiviazione si applicano rispetto alla dimensione di una determinata cassetta postale definita dalla proprietà <CODE>TotalItemSize</CODE> quando viene eseguito il cmdlet <CODE>Get-MailboxStatistics</CODE>. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/bb124612(v=exchg.150)">Get-MailboxStatistics</A>.



Le quote di spazio di archiviazione vengono generalmente configurate per ciascun database. Ciò vuol dire che le quote configurate per un database di una cassetta postale sono applicabili a tutte le cassette postali di quel database. Per ulteriori informazioni sulla gestione delle impostazioni delle cassette postali per database, vedere [Gestire il database delle cassette postali in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

L'argomento illustra come personalizzare le impostazioni di archiviazione per una cassetta postale specifica invece di utilizzare le impostazioni di archiviazione del database delle cassette postali. Per le altre attività di gestione relative alle cassette postali degli utenti, vedere [Gestire le cassette postali degli utenti](manage-user-mailboxes-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione delle quote di archiviazione per una cassetta postale tramite l'interfaccia di amministrazione di Exchange

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale di cui si desidera cambiare le quote di archiviazione, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà delle cassette postali, fare clic su **Utilizzo cassetta postale**, quindi fare clic su **Altre opzioni**.

4.  Fare clic su **Personalizza le impostazioni per questa cassetta postale**, quindi configurare le seguenti caselle. L'intervallo di valori per le impostazioni della quota di archiviazione è compreso tra 0 e 2047 GB.
    
      - **Invia un avviso in corrispondenza di (GB)**   Questa casella indica il limite massimo di archiviazione che è possibile raggiungere prima che venga inviato un messaggio di avviso. Se la dimensione della cassetta postale raggiunge o supera il valore specificato, Exchange invia un avviso all'utente.
        

        > [!IMPORTANT]
        > Il messaggio associato alla quota <STRONG>Invia avviso</STRONG> non verrà inviato all'utente, a meno che il valore di questa impostazione non superi il 50% di quello specificato dalla quota <STRONG>Proibisci invio</STRONG>. Se si imposta la quota <STRONG>Proibisci invio</STRONG> su 8 MB, per la quota <STRONG>Invia avviso</STRONG> è necessario impostare almeno 4 MB. In caso contrario, il messaggio relativo alla quota <STRONG>Invia avviso</STRONG> non verrà inviato.

    
      - **Non consentire l'invio di (GB)**   Questa casella indica il limite di *invio non consentito* per la cassetta postale. Se la dimensione della cassetta postale raggiunge o supera il limite specificato, Exchange impedisce all'utente di inviare nuovi messaggi e visualizza un messaggio di errore descrittivo.
    
      - **Non consentire l'invio e la ricezione di (GB)**   Questa casella indica il limite di *invio e ricezione non consentiti* per la cassetta postale. Se la dimensione della cassetta postale raggiunge o supera il limite specificato, Exchange impedisce all'utente della cassetta postale di inviare nuovi messaggi e non recapiterà i nuovi messaggi alla cassetta postale. Tutti i messaggi inviati alla cassetta postale vengono restituiti al mittente con un messaggio di errore descrittivo.

5.  Fare clic su **Salva** per salvare le modifiche.

## Configurazione delle quote di archiviazione per una cassetta postale tramite Shell

In questo esempio vengono impostati i limiti di avviso, di invio non consentito e di invio e ricezione quote non consentiti per la cassetta postale di Joe Healy rispettivamente a 24,5 GB, 24,75 GB e 25 G.


> [!NOTE]
> Per assicurarsi che vengano utilizzate le impostazioni personalizzate per la cassetta postale, anziché i valori predefiniti del database delle cassette postali, è necessario impostare il parametro <EM>UseDatabaseQuotaDefaults</EM> su <CODE>$false</CODE>.



    Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false

In questo esempio viene impostata la quota minima per l'emissione di un avviso, di invio non consentito e di invio e ricezione quote non consentiti per la cassetta postale di Ayla Kol rispettivamente a 900 MB, 950 MB e 1 GB e viene configurata la cassetta postale per utilizzare le impostazioni personalizzate.

    Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che le quote di archiviazione della cassetta postale siano state impostate correttamente, effettuare una delle seguenti operazioni:

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale di cui si desidera verificare le quote di archiviazione, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà delle cassette postali, fare clic su **Utilizzo cassetta postale**, quindi fare clic su **Altre opzioni**.

4.  Verificare che **Personalizza le impostazioni per questa cassetta postale** sia selezionata.

5.  Verificare le impostazioni delle quote di archiviazione.

Oppure

Eseguire il seguente comando in Shell.

    Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

