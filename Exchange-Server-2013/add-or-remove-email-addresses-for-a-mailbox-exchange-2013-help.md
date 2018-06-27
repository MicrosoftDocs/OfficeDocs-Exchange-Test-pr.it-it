---
title: 'Aggiunta o rimozione di indirizzi di posta elettronica per una cassetta postale: Exchange 2013 Help'
TOCTitle: Aggiunta o rimozione di indirizzi di posta elettronica per una cassetta postale
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50555635
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Aggiunta o rimozione di indirizzi di posta elettronica per una cassetta postale

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile configurare più indirizzi di posta elettronica per la stessa cassetta postale. Gli indirizzi aggiuntivi sono denominati *indirizzi proxy*. Un indirizzo proxy consente all'utente di ricevere un messaggio di posta elettronica inviato a un indirizzo diverso. Ogni messaggio di posta elettronica inviato all'indirizzo proxy dell'utente viene recapitato all'indirizzo di posta elettronica principale, noto anche come *indirizzo SMTP primario* o *indirizzo di risposta predefinito*.


> [!IMPORTANT]
> Se si utilizza Office 365 per le aziende, è necessario aggiungere o rimuovere gli indirizzi di posta elettronica per le cassette postali utente nell'<A href="https://go.microsoft.com/fwlink/p/?linkid=8347775">interfaccia di amministrazione di Office 365: Aggiungere ulteriori alias di posta elettronica a un utente in Office 365</A>



Per le attività di gestione aggiuntive relative alla gestione dei destinatari, vedere la tabella "Documentazione per i destinatari" in [Destinatari](recipients-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Le procedure descritte in questo argomento mostrano come aggiungere o rimuovere indirizzi di posta elettronica per la cassetta postale di un utente. È possibile utilizzare procedure analoghe per aggiungere o rimuovere indirizzi di posta elettronica per altri tipi di destinatari.

## Operazione desiderata?

## Aggiunta di un indirizzo di posta elettronica alla cassetta postale di un utente

## Aggiunta di un indirizzo di posta elettronica tramite l'interfaccia di amministrazione di Exchange

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale a cui si desidera aggiungere un indirizzo di posta elettronica, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà della cassetta postale, fare clic su **Indirizzo di posta elettronica**.
    

    > [!NOTE]
    > Nella pagina <STRONG>Indirizzo di posta elettronica</STRONG>, l'indirizzo SMTP primario viene visualizzato con il testo in grassetto nell'elenco degli indirizzi, con il valore <STRONG>SMTP</STRONG> in maiuscolo nella colonna <STRONG>Tipo</STRONG>.



4.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi su **SMTP** per aggiungere un indirizzo di posta elettronica SMTP alla cassetta postale.
    

    > [!NOTE]
    > SMTP è il tipo di indirizzo predefinito. È possibile aggiungere anche indirizzi di messaggistica unificata di Exchange (EUM) o indirizzi personalizzati a una cassetta postale. Per ulteriori informazioni, vedere "Modifica delle proprietà della cassetta postale utente" nell'argomento <A href="manage-user-mailboxes-exchange-2013-help.md">Gestire le cassette postali degli utenti</A>.



5.  Digitare il nuovo indirizzo SMTP nella casella **Indirizzo di posta elettronica**, quindi fare clic su **OK**.
    
    Il nuovo indirizzo viene visualizzato nell'elenco degli indirizzi di posta elettronica per la cassetta postale selezionata.

6.  Fare clic su **Salva** per salvare la modifica.

## Aggiunta di un indirizzo di posta elettronica tramite Shell

Gli indirizzi di posta elettronica associati a una cassetta postale sono contenuti nella proprietà *EmailAddresses* della cassetta postale. Poiché è in grado di contenere più indirizzi di posta elettronica, la proprietà *EmailAddresses* è nota come proprietà *multivalore*. Negli esempi seguenti vengono illustrati i diversi metodi per modificare una proprietà multivalore.

In questo esempio viene mostrato come aggiungere un indirizzo SMTP alla cassetta postale di Dan Jump.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

In questo esempio viene mostrato come aggiungere più indirizzi SMTP a una cassetta postale.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

Per ulteriori informazioni sull'utilizzo del metodo di aggiunta e rimozione per proprietà multivalore, vedere [Modifica delle proprietà multivalore](modifying-multivalued-properties-exchange-2013-help.md).

In questo esempio viene descritto un altro metodo per aggiungere indirizzi di posta elettronica a una cassetta postale specificando tutti gli indirizzi ad essa associati. In questo esempio, danj@tailspintoys.com è il nuovo indirizzo di posta elettronica da aggiungere. Gli altri due sono gli indirizzi di posta elettronica già esistenti. L'indirizzo con il qualificatore con distinzione tra maiuscole e minuscole `SMTP` è l'indirizzo SMTP primario. Quando si utilizza questa sintassi dei comandi, è necessario includere tutti gli indirizzi di posta elettronica. In caso contrario, gli indirizzi specificati nel comando sovrascriveranno gli indirizzi esistenti.

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta aggiunta di un indirizzo di posta elettronica a una cassetta postale, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**, fare clic sulla cassetta postale, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

  - Nella pagina delle proprietà della cassetta postale, fare clic su **Indirizzo di posta elettronica**.

  - Nell'elenco degli indirizzi di posta elettronica della cassetta postale, verificare che sia incluso il nuovo indirizzo di posta elettronica.

Oppure

  - Eseguire il seguente comando in Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verificare che il nuovo indirizzo di posta elettronica sia incluso nei risultati.

## Rimozione di un indirizzo di posta elettronica dalla cassetta postale di un utente

## Rimozione di un indirizzo di posta elettronica tramite l'interfaccia di amministrazione di Exchange

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale da cui si desidera rimuovere un indirizzo di posta elettronica, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà della cassetta postale, fare clic su **Indirizzo di posta elettronica**.

4.  Nell'elenco degli indirizzi di posta elettronica, selezionare l'indirizzo che si desidera rimuovere, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

5.  Fare clic su **Salva** per salvare la modifica.

## Rimozione di un indirizzo di posta elettronica tramite Shell

In questo esempio viene mostrato come rimuovere un indirizzo di posta elettronica dalla cassetta postale di Janet Schorr.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

In questo esempio viene mostrato come rimuovere più indirizzi da una cassetta postale.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

Per ulteriori informazioni sull'utilizzo del metodo di aggiunta e rimozione per proprietà multivalore, vedere [Modifica delle proprietà multivalore](modifying-multivalued-properties-exchange-2013-help.md).

È possibile, inoltre, rimuovere un indirizzo di posta elettronica omettendolo dal comando per l'impostazione degli indirizzi di posta elettronica di una cassetta postale. Ad esempio, supponiamo che la cassetta postale di Janet Schorr disponga di tre indirizzi di posta elettronica: Janets@contoso.com (l'indirizzo SMTP primario), janets@corp.contoso.com e janets@tailspintoys.com. Per rimuovere l'indirizzo janets@corp.contoso.com, si dovrebbe eseguire il comando riportato di seguito.

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

Poiché janets@corp.contoso.com è stato omesso nel comando precedente, risulta rimosso dalla cassetta postale.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta rimozione di un indirizzo di posta elettronica da una cassetta postale, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**, fare clic sulla cassetta postale, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

  - Nella pagina delle proprietà della cassetta postale, fare clic su **Indirizzo di posta elettronica**.

  - Nell'elenco degli indirizzi di posta elettronica della cassetta postale, verificare che il nuovo indirizzo di posta elettronica non sia incluso.

Oppure

  - Eseguire il seguente comando in Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verificare che l'indirizzo di posta elettronica non sia incluso nei risultati.

## Aggiunta di indirizzi di posta elettronica a più cassette postali tramite Shell

È possibile aggiungere un nuovo indirizzo di posta elettronica a più cassette postali contemporaneamente utilizzando la shell e un file con valori delimitati da virgole (CSV).

In questo esempio, i dati vengono importati da C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv, che ha il seguente formato.

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

Eseguire il comando riportato di seguito per utilizzare i dati del file CSV per aggiungere l'indirizzo di posta elettronica a ogni cassetta postale specificata nel file.

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}


> [!NOTE]
> I nomi di colonna nella prima riga di questo file CSV (<CODE>Mailbox,NewEmailAddress</CODE>) sono arbitrari. I nomi di colonna utilizzati, qualunque essi siano, devono tuttavia corrispondere a quelli nel comando della shell.



## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta aggiunta di un indirizzo di posta elettronica a più cassette postali, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**, fare clic sulla cassetta postale a cui è stato aggiunto l'indirizzo, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

  - Nella pagina delle proprietà della cassetta postale, fare clic su **Indirizzo di posta elettronica**.

  - Nell'elenco degli indirizzi di posta elettronica della cassetta postale, verificare che sia incluso il nuovo indirizzo di posta elettronica.

Oppure

  - Eseguire nella shell il comando riportato di seguito utilizzando lo stesso file CSV utilizzato per aggiungere il nuovo indirizzo di posta elettronica.
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - Verificare che il nuovo indirizzo di posta elettronica sia incluso nei risultati per ogni cassetta postale.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..


