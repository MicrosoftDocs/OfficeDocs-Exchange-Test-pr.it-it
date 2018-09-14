---
title: 'Mettere in attesa tutte le cassette postali: Exchange 2013 Help'
TOCTitle: Mettere in attesa tutte le cassette postali
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486285
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mettere in attesa tutte le cassette postali

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-01-18_


> [!NOTE]
> La scadenza per la creazione di blocchi sul posto in Exchange Online (nei piani autonomi di Office 365 e Exchange Online) è stata rimandata al 1° luglio 2017. Tuttavia, nell'ultima parte di quest'anno oppure all'inizio del prossimo, non sarà possibile creare nuovi blocchi sul posto in Exchange Online. Come alternativa al blocco sul posto, è possibile usare <A href="https://go.microsoft.com/fwlink/?linkid=780738">i casi di eDiscovery</A> oppure <A href="https://go.microsoft.com/fwlink/?linkid=827811">i criteri di conservazione</A> nel Centro sicurezza e conformità di Office 365. Una volta sospesa la creazione di nuovi blocchi sul posto, sarà possibile modificare i blocchi sul posto esistenti e creare nuovi blocchi sul posto nelle distribuzioni ibride di Exchange Server 2013 e Exchange. Inoltre, sarà ancora possibile applicare un blocco per controversia legale alle cassette postali.



L'organizzazione può richiedere dati della cassetta postale deve essere conservato per un determinato periodo. È possibile utilizzare conservazione per controversia legale o archiviazione sul posto per soddisfare questo requisito. Dopo che si effettua una cassetta postale di conservazione per controversia legale o archiviazione sul posto, gli elementi delle cassette postali che sono stati modificati o eliminati definitivamente vengono mantenuti nella cartella elementi ripristinabili. Per ulteriori informazioni, vedere [Archiviazione sul posto e conservazione per controversia legale](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-and-litigation-holds).

Prima di mettere tutte le cassette postali di un'organizzazione su Conservazione per controversia legale o Archiviazione sul posto, tenere presente che:

  - Quando si effettua le cassette postali in attesa, contenuto nella cassetta postale di archivio dell'utente (se abilitato) inoltre viene messa in attesa.

  - Effettuare tutte le cassette postali in un'organizzazione di attesa può ridurre notevolmente le dimensioni delle cassette postali. In una distribuzione Exchange Server 2013 pianificare archiviazione adeguato soddisfare i requisiti di conservazione dell'organizzazione. Exchange Online[limiti di archiviazione delle cassette postali](https://go.microsoft.com/fwlink/?linkid=403645) per gli utenti si basano su licenza di sottoscrizione dell'utente.

  - Conservazione dei dati delle cassette postali per un periodo di tempo produce crescita della cartella elementi ripristinabili nella cassetta postale principale dell'utente e cassetta postale di archivio. La cartella elementi ripristinabili è il limite di archiviazione, in modo che non conteggio degli elementi nella cartella per raggiungere il limite di archiviazione delle cassette postali. In Exchange Server 2013 e Exchange Online, il limite di archiviazione predefinita per la cartella elementi ripristinabili è 30 GB.
    
      - In Exchange Online, la quota per la cartella elementi recuperabili viene automaticamente aumentata a 100 GB quando si effettua una cassetta postale in attesa.
    
      - In Exchange Server 2013, è consigliabile monitorare periodicamente le dimensioni della cartella per assicurarsi che non raggiunge il limite previsto. Per ulteriori informazioni, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

## Scelta tra archiviazione sul posto e conservazione per controversia legale

Ecco alcuni fattori da considerare quando si decide la funzionalità di archiviazione da utilizzare per tutte le cassette postali nell'organizzazione di mettere in attesa.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si desidera...</th>
<th>Utilizzare Conservazione per controversia legale</th>
<th>Utilizzare Archiviazione sul posto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilizzare l'interfaccia di amministrazione di Exchange</p></td>
<td><p>Sì</p>
<p>Per l'impostazione di conservazione per controversia legale, EAC è adatto per veloce azioni singoli in alcune cassette postali. È consigliabile utilizzare la Shell per l'impostazione di conservazione per controversia legale per tutti gli utenti nell'organizzazione.</p></td>
<td><p>Sì</p>
<p>Tuttavia, non è possibile selezionare più di 500 cassette postali di origine in EAC.</p></td>
</tr>
<tr class="even">
<td><p>Utilizzare Shell</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Archiviare più di 10.000 cassette postali</p></td>
<td><p>Sì</p>
<p>Conservazione per controversia legale è una proprietà della cassetta postale. Utilizzare il cmdlet <strong>Set-Mailbox</strong> , è possibile effettuare tutte le cassette postali in un'organizzazione in attesa.</p></td>
<td><p>Sì. utilizzare più archiviazioni sul posto</p>
<p>È possibile utilizzare i gruppi di distribuzione per specificare un massimo di 10.000 cassette postali in un singolo In-Place Hold. Per archiviare aggiuntivi cassette postali, è necessario creare ulteriori archiviazioni sul posto. Il risultato è sovraccarico di gestione. Utilizzo di conservazione per controversia legale posizionamento un numero elevato di cassette postali in attesa è più semplice.</p></td>
</tr>
<tr class="even">
<td><p>Archiviare molte cassette postali diverse per diversi periodi.</p></td>
<td><p>Sì</p>
<p>Conservazione per controversia legale è una proprietà della cassetta postale. È possibile archiviare ogni cassetta postale (o set di cassette postali) per una diversa durata.</p>
<p>Vedere la sezione informazioni per alcuni esempi dell'utilizzo di proprietà dei destinatari in un filtro in modo che è possibile effettuare una conservazione per controversia legale in un sottoinsieme delle cassette postali.</p></td>
<td><p>Sì</p>
<p>Se si desidera archiviare singole cassette postali su migliaia di cassette postali, è consigliabile utilizzare Conservazione per controversia legale. Se si stanno creando archivi per eventi specifici che coinvolgono più utenti, utilizzare una sola archiviazione sul posto per il gruppo di utenti.</p>
<p>Non è consigliabile per creare archiviazione sul posto separate per ciascuna cassetta postale come numero di query In-Place Hold che sarà più difficili da gestire di conservazione per controversia contiene verrà creato. Un numero elevato di oggetti In-Place Hold potrebbero inoltre prestazioni lente in EAC durante l'aggiornamento, creazione o modifica di oggetti attesa.</p></td>
</tr>
<tr class="odd">
<td><p>Archiviare automaticamente le nuove cassette postali</p></td>
<td><p>No</p>
<p>È necessario inserire una nuova cassetta postale conservazione per controversia legale dopo averlo creato. È possibile pianificare il comando o lo script deve essere eseguito frequentemente in base alle esigenze per ottenere lo stesso effetto.</p></td>
<td><p>No</p>
<p>È necessario aggiungere una nuova cassetta postale a an In-Place Hold, anche se è stato specificato un gruppo di distribuzione quando è stato creato In-Place Hold. È inoltre possibile pianificare il comando o lo script deve essere eseguito frequentemente in base alle esigenze per ottenere lo stesso effetto. È consigliabile che il controllo dello script se una conservazione In locale esistente ha già raggiunto il limite di 10.000 cassette postali e creare una nuova archiviazione sul posto se necessario.</p></td>
</tr>
<tr class="even">
<td><p>Tutte le cartelle pubbliche di mettere in attesa</p></td>
<td><p>No</p>
<p>In Exchange Online il posizionamento di conservazione per controversia legale in cassette postali delle cartelle pubbliche non è supportato. È necessario utilizzare conservazione In locale.</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


## Archiviare tutte le cassette postali mediante Conservazione per controversia legale

È possibile modo semplice e rapido effettuare tutte le cassette postali in attesa tempo indeterminato o per un periodo specificato utilizzando la Shell. Questo comando effettua tutte le cassette postali per 2555 giorni (circa 7 anni).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

Nell'esempio viene utilizzato il cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) e un filtro destinatario per recuperare tutte le cassette postali nell'organizzazione e quindi l'elenco delle cassette postali al cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) per abilitare la conservazione per controversia legale e specificare un intervallo di tempo di attesa. Per ulteriori informazioni, vedere [Conservazione in caso di dispute di una cassetta postale](place-a-mailbox-on-litigation-hold-exchange-2013-help.md).

## Archiviare tutte le cassette postali con Archiviazione sul posto

È possibile utilizzare EAC per selezionare fino a 500 cassette postali e archiviarle. Per ulteriori informazioni, vedere [Creare o rimuovere un'archiviazione sul posto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/create-or-remove-in-place-holds).


> [!TIP]
> Per archiviare più di 500 utenti conservazione In locale, utilizzare Shell. Vedere <A href="https://technet.microsoft.com/it-it/library/dd298064(v=exchg.150)">New-MailboxSearch</A>.



## Ulteriori informazioni

  - Quando si effettua tutte le cassette postali nell'organizzazione in attesa, solo le cassette postali presenti in fase di che esecuzione del comando sono messi in attesa. Se si creano nuove cassette postali in seguito, eseguire nuovamente il comando per posizionarli in attesa. Se si creano spesso nuove cassette postali, è possibile eseguire il comando come attività pianificata con una frequenza in base alle esigenze.

  - Posizionare le cassette postali in attesa conserva i dati di evitare l'eliminazione prima del periodo specificato, quindi salvare la versione originale di un messaggio prima che venga modificato. I messaggi non verranno automaticamente eliminati dopo il periodo specificato. Combinare conservazione per controversia legale o archiviazione sul posto con un criterio di conservazione, che può eliminare automaticamente i messaggi al termine del periodo specificato, per soddisfare requisiti di conservazione di posta elettronica dell'organizzazione. [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md) per ulteriori informazioni, vedere.

  - Il comando PowerShell utilizzato in questo argomento per posizionare una conservazione per controversia legale in tutte le cassette postali viene utilizzato un filtro destinatari che restituisce tutte le cassette postali degli utenti. È possibile utilizzare altre proprietà del destinatario per restituire un elenco di cassette postali specifiche che è possibile quindi inviata tramite pipe al cmdlet **Set-Mailbox** per mettere una conservazione per controversia legale per le cassette postali.
    
    Di seguito sono riportati alcuni esempi di utilizzo dei cmdlet **Get-Mailbox** e **Get-Recipient** per restituire un sottoinsieme delle cassette postali basato su utente comuni o proprietà della cassetta postale. In questi esempi si presuppongono che sono state popolate proprietà delle cassette postali rilevanti (ad esempio *CustomAttributeN* o *Department*).
    
    ```
    Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    ```
    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    ```
    
    È possibile utilizzare altre proprietà delle cassette postali utente in un filtro per includere o escludere le cassette postali. Per ulteriori informazioni, vedere [Proprietà filtrabili per il parametro - Filter](https://technet.microsoft.com/it-it/library/bb738155\(v=exchg.150\)).

