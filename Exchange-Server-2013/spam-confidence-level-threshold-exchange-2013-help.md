---
title: 'Soglia del livello di probabilità di posta indesiderata: Exchange 2013 Help'
TOCTitle: Soglia del livello di probabilità di posta indesiderata
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 50479883
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Soglia del livello di probabilità di posta indesiderata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-11-17_


> [!NOTE]
> Dal 1° novembre 2016, Microsoft ha interrotto gli aggiornamenti delle definizioni spam per i filtri SmartScreen in Exchange e Outlook. Le definizioni spam SmartScreen esistenti non verranno eliminate, ma la loro efficacia si ridurrà progressivamente. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange (Eliminazione del supporto per SmartScreen in Outlook ed Exchange)</A>.



In Microsoft Exchange Server 2013, è possibile definire azioni specifiche in base alle soglie del livello di probabilità di posta indesiderata (SCL). Ad esempio, è possibile definire diverse soglie per il rifiuto, l'eliminazione o la messa in quarantena dei messaggi su un server Exchange in cui è in esecuzione l'agente Filtro contenuti.

La combinazione di questa configurazione della soglia SCL dell'agente Filtro contenuti e della configurazione della cartella Posta indesiderata di SCL nella cassetta postale utente consente di implementare una strategia per la protezione da posta indesiderata più ampia ed efficace. La funzione di regolazione della soglia SCL più precisa e dettagliata in Exchange 2013 può aiutare a ridurre il costo totale della distribuzione e gestione di una soluzione di protezione da posta indesiderata nell'organizzazione Exchange.

L'agente Filtro contenuti assegna una valutazione SCL ai messaggi in uno stadio avanzato del ciclo di protezione da posta indesiderata, dopo che i messaggi in ingresso sono stati elaborati da altri agenti protezione posta indesiderata. Molti degli altri agenti protezione posta indesiderata che elaborano i messaggi in ingresso prima dell'agente Filtro contenuti agiscono su un messaggio in modo deterministico. Ad esempio, su un server Trasporto Edge l'agente Filtro connessioni rifiuta tutti i messaggi inviati da un indirizzo IP incluso nell'elenco indirizzi bloccati in tempo reale. Anche l'agente Filtro mittente e l'agente Filtro destinatario elaborano i messaggi in modo deterministico.

In Exchange 2013, questi agenti di protezione da posta indesiderata deterministici elaborano prima i messaggi e quindi riducono significativamente il numero di messaggi che l'agente Filtro contenuto deve elaborare. Per ulteriori informazioni sull'ordine in cui gli agenti protezione posta indesiderata elaborano i messaggi, vedere [Protezione anti-spam](anti-spam-protection-exchange-2013-help.md).

Poiché il filtro contenuto non è un processo preciso e deterministico, la possibilità di regolare l'azione dell'agente Filtro contenuto su diversi valori SCL è importante. Regolando con attenzione la configurazione della soglia SCL, è possibile ridurre al minimo i seguenti valori:

  - La dimensione dell'archivio per la quarantena per la posta indesiderata

  - Il numero di messaggi di posta elettronica legittimi erroneamente messi in quarantena

  - Il numero di messaggi di posta elettronica legittimi che raggiungono la cartella Posta indesiderata degli utenti Microsoft Outlook

  - Il numero di messaggi di posta elettronica indesiderati e offensivi arrivati nella cartella Posta indesiderata o Posta in arrivo dell'utente di Outlook

  - Il numero di messaggi di posta elettronica indesiderati arrivati nella cartella Posta in arrivo dell'utente di Outlook

## Azioni della soglia SCL

Regolando le azioni della soglia SCL, è possibile applicare una diversa azione di filtro contenuto sui messaggi che presentano una maggiore probabilità di essere posta indesiderata. Per comprendere questa funzionalità, è utile conoscere le diverse azioni della soglia SCL e il modo in cui vengono applicate:

  - **Soglia di eliminazione SCL**   Quando un valore SCL per uno specifico messaggio è uguale o maggiore della soglia di eliminazione SCL, l'agente Filtro contenuti elimina il messaggio. Non sono previste comunicazioni al livello del protocollo per notificare al sistema di invio o al mittente che il messaggio è stato eliminato. Se il valore SCL per un messaggio è inferiore al valore della soglia di eliminazione SCL, l'agente Filtro contenuto non elimina il messaggio. L'agente Filtro contenuti, invece, confronta il valore SCL e la soglia di rifiuto SCL.

  - **Soglia di rifiuto SCL**   Quando un valore SCL per uno specifico messaggio è uguale o maggiore della soglia di rifiuto SCL, l'agente Filtro contenuti elimina il messaggio e invia una risposta di rifiuto al sistema mittente. La risposta di rifiuto può essere personalizzata. In alcuni casi, viene inviato un rapporto di mancato recapito (NDR, non-delivery report) al mittente originale del messaggio. Se il valore SCL per un messaggio è inferiore ai valori della soglia di eliminazione SCL e della soglia di rifiuto SCL, l'agente Filtro contenuto non elimina o rifiuta il messaggio. L'agente Filtro contenuti, invece, confronta il valore SCL e la soglia di quarantena SCL.

  - **Soglia di quarantena SCL**   Quando un valore SCL per uno specifico messaggio è uguale o maggiore della soglia di quarantena SCL, l'agente Filtro contenuti invia il messaggio alla cassetta postale della quarantena. Gli amministratori della posta elettronica devono controllare periodicamente la cassetta postale della quarantena. Se il valore SCL per un messaggio è inferiore ai valori della soglia di eliminazione, rifiuto e quarantena SCL, l'agente Filtro contenuto non elimina, rifiuta o mette in quarantena il messaggio. L'agente Filtro contenuti, invece, invia il messaggio al server Cassette postali appropriato in cui il valore della soglia della cartella Posta indesiderata SCL del messaggio viene valutato per ciascun destinatario.

  - **Soglia della cartella Posta indesiderata SCL**   Se il valore SCL di uno specifico messaggio supera la soglia della cartella Posta indesiderata SCL, il messaggio viene inviato alla cartella Posta indesiderata dell'utente. Se il valore SCL per un messaggio è inferiore ai valori della soglia di eliminazione, rifiuto, quarantena e della cartella Posta indesiderata SCL, il messaggio viene inviato alla cartella Posta in arrivo dell'utente.

L'agente filtro contenuto e la cartella della posta indesiderata elaborano il valore soglia SCL in modo diverso. L'agente Filtro contenuti agisce sul valore della soglia SCL configurato dall'utente. La cartella della posta indesiderata agisce sul valore della soglia SCL configurato dall'utente più 1. Ad esempio, se si configura l'azione di eliminazione su un valore SCL pari a 8 nell'agente filtro contenuto, tutti i messaggi con un valore SCL pari ad almeno 8 verranno eliminati. Se, tuttavia, la cartella della posta indesiderata viene configurata con una soglia SCL pari a 4, tutti i messaggi con un valore SCL uguale o maggiore di 5 verranno spostati nella cartella della posta indesiderata.

Ad esempio, se si imposta la soglia di eliminazione SCL su 8, la soglia di rifiuto SCL su 7, la soglia di quarantena SCL su 6 e la soglia della cartella Posta indesiderata SCL su 5, tutti i messaggi di posta elettronica con un valore SCL uguale o inferiore a 4 verranno recapitati nella cassetta postale dell'utente. Messaggi con un valore SCL di 5 vengono messi nella cartella Posta indesiderata dell'utente. Messaggi con un valore SCL di 4 vengono messi nella cartella Posta in arrivo dell'utente.

È possibile configurare l'impostazione dei valori di eliminazione, rifiuto, quarantena e della cartella Posta indesiderata SCL nelle seguenti posizioni:

  - **Nella configurazione dell'agente Filtro contenuti (configurazione SCL per server trasporto)**   Si utilizza il cmdlet **Set-ContentFilterConfig** per abilitare o disabilitare e impostare le soglie di eliminazione, rifiuto e quarantena SCL sul server Exchange dove è in esecuzione l'agente Filtro contenuti. Con il passare del tempo, analizzando la funzionalità e la metrica della posta indesiderata fornite dalle funzioni di registrazione e segnalazione di agenti di protezione da posta indesiderata, è possibile regolare ulteriormente la configurazione delle soglie SCL in base alle proprie esigenze.
    
    I parametri SCL disponibili nel cmdlet **Set-ContentFilterConfig** sono descritti nella tabella seguente.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parametro</th>
    <th>Descrizione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>Questo parametro abilita o disabilita l'eliminazione di un messaggio senza un rapporto di mancato recapito (NDR) quando il valore SCL del messaggio è uguale o superiore al valore specificato nel parametro <em>SCLDeleteThreshold</em>. L'input valido per questo parametro è <code>$true</code> o <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>L'input valido per questo parametro è un numero intero compreso tra 0 e 9. Il valore di questo parametro deve essere maggiore del valore di soglia degli altri parametri SCL. Questo parametro è significativo solamente se il valore del parametro <em>SCLDeleteEnabled</em> è <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>Questo parametro abilita o disabilita il rifiuto di un messaggio con un rapporto di mancato recapito (NDR) quando il valore SCL del messaggio è uguale o superiore al valore specificato nel parametro <em>SCLRejectThreshold</em>. L'input valido per questo parametro è <code>$true</code> o <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>L'input valido per questo parametro è un numero intero compreso tra 0 e 9. Il valore di questo parametro deve essere inferiore al valore del parametro <em>SCLDeleteThreshold</em> ma maggiore del valore di soglia degli altri parametri SCL. Questo parametro è significativo solo se il valore del parametro <em>SCLRejectEnabled</em> è <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>Questo parametro abilita o disabilita l'invio un messaggio in quarantena nella cassetta postale della posta indesiderata con un rapporto di mancato recapito (NDR) quando il valore SCL del messaggio è uguale o superiore al valore specificato nel parametro <em>SCLQuarantineThreshold</em>. L'input valido per questo parametro è <code>$true</code> o <code>$false</code>.</p>
    <p>Per ulteriori informazioni sulla cassetta postale di quarantena per la posta indesiderata, vedere <a href="spam-quarantine-exchange-2013-help.md">Quarantena posta indesiderata</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>L'input valido per questo parametro è un numero intero compreso tra 0 e 9. Il valore di questo messaggio deve essere inferiore al valore del parametro <em>SCLRejectThreshold</em>, ma superiore al valore specificato nel parametro <em>SCLJunkThreshold</em> nei cmdlet <strong>Set-OrganizationConfig</strong> o <strong>Set-Mailbox</strong>. Questo parametro è significativo solamente se il valore del parametro <em>SCLQuarantineThreshold</em> è <code>$true</code>.</p></td>
    </tr>
    </tbody>
    </table>


  - **Nelle impostazioni di configurazione dell'organizzazione(configurazione SCL a livello organizzazione)**   È possibile utilizzare il cmdlet **Set-OrganizationConfig** per impostare i valori di soglia della cartella Posta indesiderata SCL per tutte le cassette postali dell'organizzazione.
    
    I parametri SCL disponibili nel cmdlet **Set-OrganizationConfig** sono descritti nella tabella seguente. Per un esempio dell'utilizzo di SCLJunkThreshold, vedere [Configurare le impostazioni di protezione da posta indesiderata per cassette postali](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parametro</th>
    <th>Descrizione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>Questo parametro specifica il valore SCL che un messaggio deve superare per spostare il messaggio nella cartella Posta indesiderata della cassetta postale dell'utente. L'input valido per questo parametro è un numero intero compreso tra 0 e 9. Il valore di questo parametro deve essere inferiore al valore di soglia degli altri parametri SCL. Ad esempio, se si specifica un valore di 4, il messaggio con un valore SCL di 5 o superiore verrà spostato nella cartella Posta indesiderata dell'utente.</p></td>
    </tr>
    </tbody>
    </table>


  - **Nelle cassette postali utente (configurazione SCL specifica per destinatario)**   È possibile utilizzare il cmdlet **Set-Mailbox** per abilitare disabilitare o impostare le soglie di eliminazione, rifiuto, quarantena e della cartella Posta indesiderata SCL specifiche per destinatario nelle singole cassette postali utente. È possibile utilizzare solo il cmdlet **Set-Mailbox** per abilitare o disabilitare la soglia della cartella Posta indesiderata SCL su cassette postali individuali. Le soglie di eliminazione, rifiuto e quarantena SCL specifiche per destinatario sono memorizzate in Active Directory e vengono replicate dal servizio Microsoft Exchange EdgeSync nei server Trasporto Edge sottoscritti. Le configurazioni delle soglie SCL specifiche per destinatario vengono utilizzate dall'agente Filtro contenuto anche se sono state impostate configurazioni SCL specifiche per il server di trasporto. Pertanto, se sono state impostate le soglie SCL specifiche per destinatario, l'agente Filtro contenuto utilizza le soglie SCL per determinati utenti, anziché la configurazione SCL dell'agente Filtro contenuto. Per esempi, vedere [Configurare le impostazioni di protezione da posta indesiderata per cassette postali](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    

    > [!NOTE]
    > Le soglie SCL specifiche per destinatario non vengono applicate alla posta ricevuta attraverso i gruppi di distribuzione.

    
    Gli stessi parametri SCL sono disponibili nel cmdlet **Set-Mailbox** che è disponibile nei cmdlet **Set-ContentFilterConfig** e **Set-OrganizationConfig**:
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    Tuttavia, tutti i parametri nel cmdlet **Set-Mailbox** accettano anche il valore `$null`. Se in una cassetta postale una impostazione SCL è nulla (`$null`), alla cassetta postale verrà applicata la corrispondente impostazione dell'agente Filtro contenuto o l'impostazione per l'organizzazione. Se una impostazione SCL per la cassetta postale ha il valore di `$true` o `$false`, l'impostazione della cassetta postale sovrascrive la corrispondente impostazione per l'intera organizzazione sull'agente Filtro contenuto o nella configurazione per l'organizzazione.
    
    I parametri SCL disponibili solo nel cmdlet **Set-Mailbox** sono descritti nella tabella seguente.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parametro</th>
    <th>Descrizione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>Questo parametro abilita o disabilita l'invio di un messaggio nella cassetta postale della posta indesiderata quando il valore SCL del messaggio è superiore al valore specificato nel parametro <em>SCLQuarantineThreshold</em>. L'input valido per questo parametro è <code>$true</code>, <code>$false</code>o <code>$null</code>.</p>
    <p>Notare che il filtraggio della posta indesiderata è abilitato per scelta predefinita per tutte le cassette postali utente dell'organizzazione. Per scelta predefinita, il parametro <em>Enabled</em> è impostato sul valore <code>$true</code> nel cmdlet <strong>Set-MailboxJunkEmailConfiguration</strong> per tutte le cassette postali utente.</p></td>
    </tr>
    </tbody>
    </table>
    
    Per ulteriori informazioni sulla configurazione delle soglie SCL su una cassetta postale, vedere [Configurare le impostazioni di protezione da posta indesiderata per cassette postali](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).

## Monitoraggio delle soglie SCL

È possibile utilizzare numerosi script incorporati nella cartella `%ExchangeInstallPath%Scripts`, come **get-AntispamSCLHistogram.ps1**, per raccogliere i dati dei risultati del filtraggio. Se i dati indicano che è necessario apportare immediate modifiche, riconfigurare le soglie SCL. In caso contrario, raccogliere i dati e analizzare i rapporti per la posta indesiderata per determinare se è necessario impostare nuove regolazioni.

