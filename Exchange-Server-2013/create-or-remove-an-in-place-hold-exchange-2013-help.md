---
title: "Creare o rimuovere un'archiviazione sul posto: Exchange 2013 Help"
TOCTitle: Creare o rimuovere un'archiviazione sul posto
ms:assetid: 9d5d8d37-a053-4830-9cb1-6e1ede25e963
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979797(v=EXCHG.150)
ms:contentKeyID: 50481300
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare o rimuovere un'archiviazione sul posto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-01-18_


> [!NOTE]
> La scadenza per la creazione di blocchi sul posto in Exchange Online (nei piani autonomi di Office 365 e Exchange Online) è stata rimandata al 1° luglio 2017. Tuttavia, nell'ultima parte di quest'anno oppure all'inizio del prossimo, non sarà possibile creare nuovi blocchi sul posto in Exchange Online. Come alternativa al blocco sul posto, è possibile usare <A href="https://go.microsoft.com/fwlink/?linkid=780738">i casi di eDiscovery</A> oppure <A href="https://go.microsoft.com/fwlink/?linkid=827811">i criteri di conservazione</A> nel Centro sicurezza e conformità di Office 365. Una volta sospesa la creazione di nuovi blocchi sul posto, sarà possibile modificare i blocchi sul posto esistenti e creare nuovi blocchi sul posto nelle distribuzioni ibride di Exchange Server 2013 e Exchange. Inoltre, sarà ancora possibile applicare un blocco per controversia legale alle cassette postali.



An In-Place Hold Consente di mantenere tutto il contenuto delle cassette postali, inclusi gli elementi eliminati e le versioni originali degli elementi modificati. Tutti questi elementi della cassetta postale vengono restituiti in una ricerca [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) . Quando si effettua un'archiviazione sul posto nella cassetta postale dell'utente in, il contenuto nella cassetta postale di archivio corrispondente (se abilitato) è inoltre messa in attesa e restituito in una ricerca eDiscovery.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Archiviazione sul posto" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

  - Per mettere una cassetta postale Exchange Online in archiviazione sul posto, è necessario assegnare una licenza di Exchange Online (piano 2). Se una cassetta postale viene assegnata una licenza di Exchange Online (piano 1), è necessario assegnarlo una licenza separata archiviazione Exchange Online per mettere in attesa.

  - A seconda del Active Directory topologia e latenza della replica, potrebbero richiedere un'ora per an In-Place Hold rendere effettive.

  - Come indicato in precedenza, quando si effettua un'archiviazione sul posto nella cassetta postale dell'utente, contenuto nella cassetta postale di archivio dell'utente anche messa in attesa. Se si effettua un'archiviazione sul posto in una cassetta postale principale locale in una distribuzione ibrida Exchange, cassetta postale di archiviazione basate su cloud (se consentito) inoltre viene messa in attesa.

  - Se un utente viene messa in più archiviazioni sul posto, le query di ricerca da qualsiasi conservazione basata su query vengono combinate (con operatori **OR** ). In questo caso, il numero massimo di parole chiave in tutte le esenzioni basata su query messa in una cassetta postale è 500. Se sono presenti più di 500 parole chiave e quindi tutto il contenuto della cassetta postale viene messa in attesa (non solo che il contenuto che genera una corrispondenza per i criteri di ricerca). Tutto il contenuto viene mantenuto finché non il numero totale di parole chiave è inferiore a 500 o meno.

  - In Exchange Online la quota per la cartella elementi recuperabili viene automaticamente aumentata a 100 GB quando si effettua un'archiviazione sul posto di una cassetta postale. Le dimensioni predefinite della cartella elementi ripristinabili sono 30 GB.

  - Nell' Exchange Online, è possibile effettuare una conservazione In locale nella Office 365 gruppi. Quando si effettua un gruppo di Office 365 in attesa, la cassetta postale di gruppo viene messa in attesa; le cassette postali dei membri del gruppo non sono stato messo in attesa. Per informazioni sui gruppi Office 365, vedere [informazioni sui gruppi di Office 365](https://go.microsoft.com/fwlink/p/?linkid=724066).

## Creare un blocco sul posto

**Utilizzo di EAC per creare un'archiviazione sul posto**

1.  Accedere a **Gestione conformità** \> **eDiscovery e conservazione in locale**.

2.  Fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  **EDiscovery sul posto e conservazione**, nella pagina **nome e descrizione** digitare un nome per la ricerca e una descrizione facoltativa e quindi fare clic su **Avanti**.

4.  Nella pagina **cassette postali e cartelle pubbliche**, scegliere i percorsi contenuti che si desidera mettere in attesa e quindi fare clic su **Avanti**.
    
    ![Scegliere i percorsi dei contenuti da mettere in attesa](images/Dd979797.bbe76c50-a93b-4e5e-acd2-78e0d747ea19(EXCHG.150).png "Scegliere i percorsi dei contenuti da mettere in attesa")  
    
    1.  **Tutte le cassette postali di ricerca**   È possibile selezionare questa opzione per creare an In-Place Hold. È possibile selezionare questa opzione per le ricerche eDiscovery In locale, ma per creare un'archiviazione sul posto, è necessario selezionare le cassette postali specifiche che si desidera mettere in attesa.
    
    2.  **Non cercare tutte le cassette postali**   Selezionare questa opzione se si sta creando an In-Place Hold esclusivamente per le cartelle pubbliche.
    
    3.  **Specificare le cassette postali di ricerca**   Selezionare questa opzione e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per selezionare le cassette postali o gruppi di distribuzione che si desidera mettere in attesa. In Exchange Online, è inoltre possibile selezionare gruppi Office 365 per mettere in attesa.
    
    4.  **Tutte le cartelle pubbliche di ricerca**   In Exchange Online, è possibile selezionare questa casella di controllo di effettuare tutte le cartelle pubbliche nell'organizzazione in attesa. Come indicato in precedenza, per creare un'archiviazione sul posto solo per le cartelle pubbliche, assicurarsi di selezionare l'opzione **non cercare tutte le cassette postali**.

5.  Nella pagina **query di ricerca** compilare i campi seguenti e quindi fare clic su **Avanti**:
    
      - **Includono tutto il contenuto delle cassette postali utente**    Fare clic su questo pulsante per inserire tutto il contenuto nelle cassette postali selezionate in attesa.
    
      - **Filtro in base ai criteri**    Fare clic su questo pulsante per specificare i criteri di ricerca, inclusi parole chiave, le date di inizio e fine, mittente e gli indirizzi dei destinatari e i tipi di messaggio. Quando si crea una query basata su attesa, solo gli elementi che soddisfano la ricerca criteri vengono mantenuti.
        

        > [!TIP]
        > Quando si effettua le cartelle pubbliche su archiviazione sul posto, vengono conservati inoltre messaggi di posta elettronica correlati al processo di sincronizzazione della gerarchia di cartelle pubbliche. In questo caso, migliaia di gerarchia di sincronizzazione relative degli elementi di posta elettronica vengono mantenuti. Questi messaggi possono riempire la quota di archiviazione per la cartella elementi ripristinabili sulle cassette postali di cartelle pubbliche. Per evitare questo problema, è possibile creare una conservazione In locale basata su query e aggiungere la seguente coppia <CODE>property:value</CODE> per le query di ricerca:<BR><CODE>NOT(subject:HierarchySync*)</CODE><BR>Il risultato è che qualsiasi messaggio (associata alla sincronizzazione della gerarchia di cartelle pubbliche) che includono la frase "HierarchySync" nella riga dell'oggetto non viene messa in attesa.



6.  Nella pagina **impostazioni di conservazione In locale**, selezionare la casella di controllo **contenuto locale che corrispondono alla query di ricerca di cassette postali selezionate in attesa** e quindi selezionare una delle opzioni seguenti:
    
      - **Tenere premuto per un tempo indefinito**    Fare clic su questo pulsante per inserire gli elementi restituiti dalla ricerca una conservazione indefinita. Verranno mantenuti gli elementi in attesa finché non rimuovere la cassetta postale dalla ricerca o rimuovere la ricerca.
    
      - **Specificare il numero di giorni di conservazione degli elementi rispetto al loro data di ricezione**    Fare clic su questo pulsante per conservare gli elementi per un determinato periodo. Ad esempio, è possibile utilizzare questa opzione se l'organizzazione richiede che tutti i messaggi di essere conservati per almeno 7 anni. È possibile utilizzare un *basate sul tempo* In-Place Hold insieme a un criterio di conservazione per assicurarsi che gli elementi vengono eliminati in sette anni. Per ulteriori informazioni sulla conservazione criteri, vedere [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md).

**Utilizzo della Shell per creare un'archiviazione sul posto**

In questo esempio crea an In-Place Hold denominato CaseId012 esenzione e aggiunge la cassetta postale joe@contoso.com all'esenzione.


> [!IMPORTANT]
> Se non viene specificato parametri di ricerca aggiuntivi per an In-Place Hold, tutti gli elementi di origine specificata cassette postali si trovano in attesa. Se non si specifica il parametro <EM>ItemHoldPeriod</EM> , gli elementi sono messa in attesa o indefinito finché la cassetta postale viene rimosso dall'esenzione o esenzione viene eliminato.



    New-MailboxSearch "Hold-CaseId012"-SourceMailboxes "joe@contoso.com" -InPlaceHoldEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxSearch](https://technet.microsoft.com/it-it/library/dd298064\(v=exchg.150\)).

**Come verificare se l'operazione ha avuto esito positivo?**

Per verificare di aver creato correttamente l'archiviazione sul posto, effettuare una delle operazioni seguenti:

  - Utilizzare EAC per verificare che l'archiviazione sul posto è elencato nella visualizzazione elenco della scheda **esenzione ed eDiscovery In locale**.

  - Utilizzare il cmdlet **Get-MailboxSearch** per recuperare la cassetta postale di ricerca e controllare i parametri di ricerca. Per un esempio di come recuperare una cassetta postale di ricerca, vedere gli esempi in [Get-MailboxSearch](https://technet.microsoft.com/it-it/library/dd351021\(v=exchg.150\)).

Torna all'inizio

## Rimuovere un'archiviazione sul posto


> [!IMPORTANT]
> Nell' Exchange 2013 ricerche nelle cassette postali è utilizzabile per un'archiviazione sul posto e In-Place eDiscovery. Non è possibile rimuovere una ricerca cassetta postale viene utilizzata per la conservazione In locale. È necessario prima disabilitare l'archiviazione sul posto, deselezionare la casella di controllo <STRONG>contenuto locale che corrispondono alla query di ricerca di cassette postali selezionate in attesa</STRONG> nella pagina <STRONG>impostazioni di archiviazione sul posto</STRONG> o impostando il parametro <EM>InPlaceHoldEnabled</EM> su <CODE>$false</CODE> in Shell. È inoltre possibile rimuovere una cassetta postale utilizzando il parametro <EM>SourceMailboxes</EM> specificato nella ricerca.



**Utilizzare EAC per rimuovere un'archiviazione sul posto**

1.  Accedere a **Gestione conformità** \> **eDiscovery sul posto e conservazione**.

2.  Nella visualizzazione elenco selezionare i In-Place Hold si desidera rimuovere e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Proprietà **In-Place eDiscovery e archiviazione**, nella pagina **Conservazione In locale** di cancellare il **contenuto locale che corrispondono alla query di ricerca di cassette postali selezionate in attesa** e quindi fare clic su **Salva**.

4.  Selezionare In-Place Hold nuovamente dalla visualizzazione elenco e quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

5.  Nell'avviso, fare clic su **Sì** per rimuovere la ricerca.

**Utilizzo della Shell per rimuovere un'archiviazione sul posto**

In questo esempio disabilita l'archiviazione sul posto denominata CaseId012 esenzione e quindi rimuove la cassetta postale di ricerca.

    Set-MailboxSearch "Hold-CaseId012"  -InPlaceHoldEnabled $false
    Remove-MailboxSearch "Hold-CaseId012"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-MailboxSearch](https://technet.microsoft.com/it-it/library/dd335145\(v=exchg.150\)).

**Come verificare se l'operazione ha avuto esito positivo?**

Per verificare che sia stata rimossa correttamente an In-Place Hold, effettuare una delle operazioni seguenti:

  - Utilizzare EAC per verificare che l'archiviazione sul posto non viene visualizzata nella visualizzazione elenco della scheda **esenzione ed eDiscovery In locale**.

  - Utilizzare il cmdlet **Get-MailboxSearch** per recuperare tutte le ricerche nelle cassette postali e verificare che la ricerca che è stato rimosso non è più elencata. Per un esempio di come recuperare una cassetta postale di ricerca, vedere gli esempi in [Get-MailboxSearch](https://technet.microsoft.com/it-it/library/dd351021\(v=exchg.150\)).

Torna all'inizio

