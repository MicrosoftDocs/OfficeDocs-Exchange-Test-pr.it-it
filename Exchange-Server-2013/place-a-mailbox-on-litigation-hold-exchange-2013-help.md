---
title: 'Conservazione in caso di dispute di una cassetta postale: Exchange 2013 Help'
TOCTitle: Conservazione in caso di dispute di una cassetta postale
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62269042
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conservazione in caso di dispute di una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-10-18_

Attivare un blocco per controversia legale in una cassetta postale per conservare tutto il contenuto della cassetta postale, tra cui elementi eliminati e versioni originali degli elementi modificati. Quando si attiva un blocco per controversia legale nella cassetta postale di un utente, anche il contenuto della cassetta postale di archiviazione dell'utente (se abilitata) viene messo in attesa. Gli elementi eliminati o modificati vengono conservati per un periodo specificato o fino a quando non viene rimosso il blocco per controversia legale dalla cassetta postale. Tutti questi elementi delle cassette postali vengono restituiti in una ricerca di [eDiscovery sul posto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery).


> [!IMPORTANT]
> Il blocco per controversia legale conserva gli elementi nella cartella Elementi ripristinabili nella cassetta postale dell'utente.A seconda del numero e della dimensione degli elementi eliminati o modificati, la dimensione della cartella Elementi ripristinabili della cassetta postale potrebbe aumentare rapidamente. Per impostazione predefinita, la cartella Elementi ripristinabili è configurata con una quota elevata. In Exchange Online, questa quota viene aumentata automaticamente quando si attiva un blocco per controversia legale in una cassetta postale. In Exchange Server 2013 si consiglia di monitorare le cassette postali con blocco per controversia legale attivato ogni settimana per verificare non venga raggiunto il limite delle quote di Elementi ripristinabili.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - L'impostazione Blocco per controversia legale potrebbe richiedere fino a 60 minuti per essere effettivo.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Blocco sul posto" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per attivare il blocco per controversia legale in una cassetta postale di Exchange Online, è necessario disporre di una licenza di Exchange Online (Piano 2). Se una cassetta postale dispone di una licenza di Exchange Online (Piano 1), occorre assegnarle una licenza di Exchange Online Archiving distinta per attivare il blocco.

  - Come descritto in precedenza, quando si esegue un blocco per controversia legale nella cassetta postale dell'utente, anche il contenuto nella cassetta postale di archiviazione dell'utente viene bloccato. Se si attiva un blocco per controversia legale in una cassetta postale principale locale in una distribuzione ibrida di Exchange, viene conservata anche la cassetta postale di archiviazione basata sul cloud (se abilitata).

  - In Exchange Online, la quota per la cartella Elementi ripristinabili viene automaticamente aumentata a 100 GB quando per una cassetta postale si attiva il blocco per controversia legale. La dimensione predefinita della cartella è 30 GB.

  - Il blocco per controversia legale preserva gli elementi eliminati e anche le versioni originali degli elementi modificati finché non viene rimosso il blocco. È possibile specificare in modo facoltativo la durata del blocco, che conserva un elemento della cassetta postale per il periodo di durata specificato. È possibile specificare un periodo della durata del blocco, viene calcolato dalla data di ricezione di un messaggio o dalla creazione dell'elemento della cassetta postale. Per mantenere gli elementi che soddisfano i criteri specificati, usare un blocco sul posto per creare un blocco *basato su query*. Per ulteriori dettagli, vedere [Creare o rimuovere un'archiviazione sul posto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/create-or-remove-in-place-holds).

  - Per attivare un blocco in una cassetta postale di Exchange Online tramite la shell, è necessario utilizzare Exchange Online PowerShell. Per ulteriori informazioni, vedere [Connessione a Exchange Online tramite Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\)).

  - L'impostazione di un blocco per controversia legale su una cassetta postale per le cartelle pubbliche non è supportata. Per applicare un blocco alle cartelle pubbliche, è necessario utilizzare il blocco sul posto.

## Utilizzo dell'interfaccia di amministrazione di Exchange per attivare un blocco per controversia legale in una cassetta postale

1.  Andare a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale per cui si desidera attivare il blocco per controversia legale, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Blocco per controversia legale: disabilitato**, fare clic su **Abilita** per attivare il blocco per controversia legale nella cassetta postale.

5.  Nella pagina **Blocco per controversia legale**, inserire le seguenti informazioni opzionali:
    
      - **Durata del blocco per controversia legale (giorni)**   Utilizzare questa casella per specificare la durata di conservazione degli elementi della cassetta postale quando viene attivato il blocco per controversia legale. La durata viene calcolata a partire dalla data di ricezione o creazione dell'elemento della cassetta postale. Se si lascia la casella vuota, gli elementi vengono conservati a tempo indeterminato o fino a quando non viene rimossa la conservazione. Usare un numero di giorni per specificare la durata.
    
      - **Nota**   Utilizzare questa casella per informare l'utente che nella sua cassetta postale è attivo il blocco per controversia legale. La nota viene visualizzata nella cassetta postale dell'utente se quest'ultimo utilizza Outlook 2010 o versione successiva.
    
      - **URL**   Utilizzare questa casella per indirizzare l'utente a un sito Web per ulteriori informazioni sul blocco per controversia legale. Questo URL viene visualizzato nella cassetta postale dell'utente se quest'ultimo utilizza Outlook 2010 o versione successiva.

6.  Fare clic su **Salva** nella pagina **Blocco per controversia legale**, quindi fare clic su **Save** nella pagina proprietà della cassetta postale.

Torna all'inizio

## Attivare un blocco per controversia legale a tempo indeterminato nella cassetta postale tramite la shell

In questo esempio viene attivato il blocco per controversia legale nella cassetta postale bsuneja@contoso.com. Gli elementi nella cassetta postale vengono conservati a tempo indeterminato o finché non viene rimosso il blocco.

```powershell
Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true
```


> [!NOTE]
> Quando si attiva un blocco per controversia legale per un tempo indefinito (senza specificarne la durata), il valore della proprietà <EM>LitigationHoldDuration</EM> è impostato su <CODE>Unlimited</CODE>.



## Utilizzo della shell per attivare il blocco per controversia legale nella cassetta postale e conservare gli elementi per una durata specifica

In questo esempio viene attivato il blocco per controversia legale nella cassetta postale bsuneja@contoso.com e gli elementi vengono conservati per 2555 giorni (circa 7 anni):

```powershell
Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555
```

## Utilizzo della shell per attivare il blocco per controversia legale in tutte le cassette postali per una durata specifica

L'organizzazione può richiedere che tutti i dati delle cassette postali siano conservati per un periodo di tempo specifico. Prima di attivare il blocco per controversia legale per tutte le cassette postali nell'organizzazione, considerare quanto segue:

In questo esempio viene attivato il blocco per controversia legale in tutte le cassette postali utente di un anno (365 giorni).
```powershell
    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365
```
In questo esempio viene utilizzato il cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) per recuperare tutte le cassette postali nell'organizzazione, si specifica un filtro destinatari per includere tutte le cassette postali utente e viene trasmesso un elenco di cassette postali al cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) per attivare il blocco per controversia legale e impostarne la durata.

Per impostare un blocco indefinito in tutte le cassette postali utente, eseguire il comando precedente senza includere il parametro *LitigationHoldDuration*.

Vedere la sezione Ulteriori informazioni per esempi relativi all'utilizzo di altre proprietà del destinatario in un filtro per includere o escludere una o più cassette postali.

## Rimozione dalla conservazione in caso di dispute di una cassetta postale tramite shell

In questo esempio, viene rimosso un blocco per controversia legale dalla cassetta postale bsuneja@contoso.com.

```powershell
Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false
```

Torna all'inizio

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta attivazione di un blocco per controversia legale in una cassetta postale, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange:
    
    1.  Andare a **Destinatari** \> **Cassette postali**.
    
    2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale di cui si desidera verificare le impostazioni del blocco per controversia legale, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.
    
    4.  In **Blocco per controversia legale**, verificare che il blocco sia attivato.
    
    5.  Fare clic su **Visualizza dettagli** per verificare quando è stato attivato il blocco per controversia legale e da chi. È inoltre possibile verificare o modificare i valori nelle caselle facoltative **Durata del blocco per controversia legale (giorni)**, **Nota** e **URL**.

  - In Shell, utilizzare uno dei seguenti comandi:
    ```powershell
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    ```
    oppure
    ```powershell
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    ```
    Se si attiva un blocco per controversia legale per un tempo indefinito, il valore della proprietà *LitigationHoldDuration* è impostato su `Unlimited`.

## Ulteriori informazioni

  - Se l'organizzazione richiede che tutti i dati delle cassette postali siano conservati per un periodo di tempo specifico, considerare quanto segue prima di attivare il blocco per controversia legale per tutte le cassette postali nell'organizzazione.
    
      - Quando si utilizza il comando precedente per attivare un blocco in tutte le cassette postali nell'organizzazione (oppure un set secondario di cassette postali corrispondenti a un filtro destinatario specificato), il blocco viene attivato solo per le cassette postali che esistono al momento dell'esecuzione del comando. Se si creano nuove cassette postali in un secondo momento, sarà necessario eseguire di nuovo il comando per attivare il blocco per le nuove cassette postali. Se si creano spesso nuove cassette postali, è possibile eseguire il comando come attività pianificata secondo la frequenza necessaria.
    
      - Attivare il blocco per controversia legale in tutte le cassette postali può influire notevolmente sulle dimensioni delle cassette postali. In un'organizzazione Exchange Server 2013, pianificare lo spazio di archiviazione adeguato per soddisfare i requisiti di conservazione dell'organizzazione.
    
      - La cartella Elementi ripristinabili presenta un proprio limite di archiviazione, quindi gli elementi nella cartella non pesano sul limite di archiviazione della cassetta postale. Come spiegato in precedenza, la conservazione dei dati delle cassette postali per un lungo periodo di tempo causa la crescita della cartella Elementi ripristinabili in una cassetta postale e nell'archivio di un utente. Per rendere possibile questo aumento in Exchange Online, la quota per la cartella Elementi ripristinabili viene automaticamente aumentata da 30 GB a 100 GB quando per una cassetta postale si attiva il blocco per controversia legale.
        
        In Exchange Server 2013, il limite di archiviazione predefinito per la cartella Elementi ripristinabili è di 30 GB. Si consiglia di tenere periodicamente sotto controllo le dimensioni della cartella per verificare di non raggiungere il limite. Per ulteriori informazioni, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

  - Il comando precedente per attivare un blocco in tutte e cassette postali utilizza un filtro destinatario che restituisce tutte le cassette postali utente. È possibile utilizzare altre proprietà dei destinatari per un elenco delle cassette postali specifiche che è quindi possibile restituire al cmdlet **Set-Mailbox** per attivare un blocco per controversia legale in tali cassette postali.
    
    Ecco alcuni esempi sull'utilizzo dei cmdlet **Get-Mailbox** e **Get-Recipient** per restituire un set secondario di cassette postali in base alle proprietà comuni di utenti o cassette postali. Tali esempi presumono che le proprietà della cassetta postale rilevante (ad esempio, *CustomAttributeN* o *Department*) siano state popolate.
    ```powershell
    Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    ```
    
    ```powershell
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```
    
    ```powershell
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    ```powershell
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    
    ```powershell
    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    ```
    

    È possibile utilizzare altre proprietà della cassetta postale utente in un filtro per escludere o includere le cassette postali. Per ulteriori dettagli, vedere [Proprietà filtrabili per il parametro - Filter](https://technet.microsoft.com/it-it/library/bb738155\(v=exchg.150\)).

Torna all'inizio

