---
title: 'Connettere una cassetta postale disabilitata: Exchange 2013 Help'
TOCTitle: Connettere una cassetta postale disabilitata
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50555654
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connettere una cassetta postale disabilitata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-11-13_

È possibile utilizzare EAC o Shell per connettere una cassetta postale disabilitata a un account utente di Active Directory. Una volta disabilitata, la cassetta postale viene conservata da Exchange nel database relativo e viene impostata sullo stato di disabilitato. Anche gli attributi di Exchange vengono rimossi dall'account utente di Active Directory corrispondente, viene invece conservato l'account utente. La cassetta postale viene conservata fino alla scadenza del periodo di conservazione delle cassette postali eliminate, che, per impostazione predefinita, equivale a 30 giorni, quindi viene rimossa permanentemente (o *eliminata definitivamente*) dal database delle cassette postali.

Fino a quando una cassetta postale disabilitata non viene eliminata definitivamente dal database delle cassette postali di Exchange, è possibile utilizzare EAC o Shell per riconnetterla a un account utente di Active Directory originale.

Per ulteriori informazioni sulle cassette postali disconnesse e per eseguire altre attività di gestione correlate, vedere gli argomenti seguenti:

  - [Cassette postali disconnesse](disconnected-mailboxes-exchange-2013-help.md)

  - [Disabilitazione o eliminazione di una cassetta postale](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [La connessione o il ripristino di una cassetta postale eliminata](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Eseguire il cmdlet **Get-User** in Shell per verificare che l'account utente di Active Directory a cui connettere la cassetta postale disabilitata esista e che ad esso non sia già associata a un'altra cassetta postale. Per connettere una cassetta postale disabilitata a un account utente, è necessario che l'account esista e che il valore per la proprietà *RecipientType* sia `User`, che indica che l'account non è ancora abilitato alla cassetta postale.
    
    Per le organizzazioni di Exchange on-premises è inoltre possibile verificare le informazioni in Utenti e computer di Active Directory.

  - Per verificare che la cassetta postale disabilitata che si desidera connettere a un account utente esista nel database delle cassette postali e che non sia una cassetta postale eliminata in maniera reversibile, eseguire il comando seguente.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    Per connettere una cassetta postale disabilitata, è necessario che esista nel database delle cassette postali e che il valore della proprietà *DisconnectReason* sia `Disabled`. Se la cassetta postale è stata eliminata definitivamente dal database, il comando non restituirà alcun risultato.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Connessione di una cassetta postale disabilitata tramite EAC

Nella procedura riportata di seguito viene descritta la modalità di connessione di una cassetta postale utente disabilitata. È inoltre possibile riconnettere cassette postali disabilitate collegate e cassette postali condivise disabilitate all'account utente corrispondente.

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi su **Connessione ad una cassetta postale**.
    
    Verrà visualizzato l'elenco delle cassette postali disconnesse sul server Exchange selezionato nell'organizzazione di Exchange.
    

    > [!NOTE]
    > Nell'elenco sono incluse le cassette postali disabilitate, le cassette postali eliminate e quelle eliminate in maniera reversibile.



3.  Selezionare la cassetta postale disabilitata che si desidera riconnettere, quindi fare clic su **Connetti**.

4.  Nella finestra in cui viene chiesto se si è sicuri di voler riconnettere la cassetta postale, fare clic su **Sì**.
    
    Exchange eseguirà la riconnessione della cassetta postale disabilitata all'account utente corrispondente.

## Connessione di una cassetta postale disabilitata tramite Shell

Utilizzare il cmdlet **Connect-Mailbox** in Shell per connettere un account utente a una cassetta postale disabilitata. È necessario specificare il tipo di cassetta postale che si sta connettendo. Negli esempi seguenti viene illustrata la sintassi per riconnettere cassette postali utente, collegate e condivise.

Con questo esempio viene connessa una cassetta postale utente. Il parametro *Identity* consente di specificare la cassetta postale disconnessa nel database di Exchange. Il parametro *User* consente di specificare l'account utente di Active Directory a cui riconnettere la cassetta postale.

    Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"

In questo esempio viene connessa una cassetta postale collegata. Il parametro *Identity* consente di specificare la cassetta postale disconnessa nel database di Exchange. Il parametro *LinkedMasterAccount* consente di specificare l'account utente di Active Directory nella foresta di account a cui si desidera riconnettere la cassetta postale. Il parametro *Alias* consente di specificare l'alias, ovvero la parte dell'indirizzo di posta elettronica a sinistra del simbolo di chiocciola (@), per la cassetta postale riconnessa.

    Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia

Con questo esempio viene connessa una cassetta postale condivisa.

    Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared


> [!NOTE]
> Se non viene incluso il parametro <EM>Alias</EM> quando si esegue il cmdlet <STRONG>Connect-Mailbox</STRONG>, il valore specificato nel parametro <EM>User</EM> o <EM>LinkedMasterAccount</EM> viene utilizzato per creare l'alias per l'indirizzo di posta elettronica per la cassetta postale riconnessa.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Connect-Mailbox](https://technet.microsoft.com/it-it/library/aa997878\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta connessione della cassetta postale disabilitata a un account utente, effettuare una delle seguenti operazioni:

  - In EAC fare clic su **Destinatari**, accedere alla pagina corretta per il tipo di cassetta postale riconnessa, fare clic su **Aggiorna**![Icona Aggiorna](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icona Aggiorna"), quindi verificare che la cassetta postale sia presente nell'elenco.

  - In Utenti e computer di Active Directory fare clic con il pulsante destro del mouse sull'account utente di cui è stata disabilitata la cassetta postale, quindi scegliere **Proprietà**. Nella scheda **Generali** tenere presente che nella casella **Posta elettronica** sono inseriti i dati dell'indirizzo di posta elettronica per la cassetta postale riconnessa.

  - In Shell, utilizzare il seguente comando.
    
        Get-User <identity>
    
    Il valore **UserMailbox** per la proprietà *RecipientType* indica che l'account utente e la cassetta postale sono connessi. È inoltre possibile eseguire il comando **Get-Mailbox** per verificare che la cassetta postale esista.

