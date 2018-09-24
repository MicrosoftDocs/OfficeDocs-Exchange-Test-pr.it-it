---
title: 'Gestire i messaggi DSN: Exchange 2013 Help'
TOCTitle: Gestire i messaggi DSN
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 50480242
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i messaggi DSN

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-20_

Microsoft Exchange Server 2013 utilizza le notifiche dello stato del recapito per fornire ai mittenti dei rapporti di mancato recapito e altri messaggi di stato. È possibile utilizzare le notifiche predefinite dello stato del recapito oppure crearne di personalizzate per soddisfare le esigenze della propria organizzazione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "DSN" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Non è possibile rimuovere una notifica predefinito dello stato del recapito che è inclusa con Exchange. Per modificare una notifica predefinita dello stato del recapito, è necessario creare un nuovo messaggio personalizzato per il codice di notifica che si intende personalizzare. Quando si rimuove una notifica personalizzata dello stato del recapito, il codice di notifica associato al messaggio ripristina il messaggio predefinito per la notifica incluso con Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per visualizzare i messaggi predefiniti e personalizzati per la notifica dello stato del recapito

Per visualizzare un elenco riepilogativo di tutti i messaggi predefiniti per la notifica dello stato del recapito inclusi con Exchange 2013, utilizzare il seguente comando:

```powershell
Get-SystemMessage -Original
```

Per visualizzare un elenco riepilogativo di tutti i messaggi personalizzati per la notifica dello stato del recapito presenti nell'organizzazione, utilizzare il seguente comando:

```powershell
Get-SystemMessage
```

Per visualizzare informazioni dettagliate sul messaggio per la notifica dello stato del recapito per il codice 5.1.2 inviato ai mittenti interni in inglese, utilizzare il seguente comando:

```powershell
Get-SystemMessage En\Internal\5.1.2 | Format-List
```

## Utilizzo di Shell per creare un messaggio personalizzato per la notifica dello stato del recapito

Eseguire il comando indicato di seguito:
```powershell
    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"
```
In questo esempio viene creato un messaggio personalizzato per la notifica dello stato del recapito in formato testo normale per il codice 5.1.2; questo messaggio viene inviato ai mittenti interni in inglese.
```powershell
    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."
```
In questo esempio viene creato un messaggio personalizzato per la notifica dello stato del recapito in formato testo normale per il codice 5.1.2; questo messaggio viene inviato ai mittenti esterni in inglese.
```powershell
    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."
```
In questo esempio viene creato un messaggio personalizzato per la notifica dello stato del recapito in formato HTML per il codice 5.1.2; questo messaggio viene inviato ai mittenti interni in inglese.
```powershell
    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'
```
## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il messaggio personalizzato per la notifica dello stato del recapito sia stato creato correttamente, fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
    Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language
    ```

2.  Verificare che i valori visualizzati siano quelli configurati.

3.  Inviare un messaggio di prova che genererà il messaggio personalizzato per la notifica dello stato del recapito così come è stato configurato.

## Modifica del testo di un messaggio DSN personalizzato tramite Shell

Per modificare il testo di un messaggio personalizzato per la notifica dello stato del recapito, utilizzare il seguente comando:
```powershell
    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"
```
In questo esempio viene modificato il testo assegnato al messaggio personalizzato per la notifica dello stato del recapito per il codice 5.1.2; questo messaggio viene inviato ai mittenti interni in inglese.
```powershell
    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."
```
## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il testo del messaggio personalizzato per la notifica dello stato del recapito sia stato modificato correttamente, fare quanto segue:

1.  Eseguire il comando indicato di seguito: `Get-SystemMessage`.
    
    ```powershell
    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text
    ```

2.  Verificare che il valore visualizzato sia quello configurato.

## Utilizzo di Shell per rimuovere un messaggio personalizzato per la notifica dello stato del recapito

Eseguire il comando indicato di seguito:

```powershell
Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>
```

In questo esempio viene rimosso il messaggio personalizzato per la notifica dello stato del recapito per il codice 5.1.2; questo messaggio viene inviato ai mittenti interni in inglese.

```powershell
Remove-SystemMessage En\Internal\5.1.2
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il messaggio personalizzato per la notifica dello stato del recapito sia stato rimosso correttamente, fare quanto segue:

1.  Eseguire il comando: `Get-SystemMessage`.

2.  Verificare che nell'elenco non sia presente una notifica dello stato del recapito con impostazioni locali, destinatari interni o esterni e codice uguali a quelli della notifica eliminata.

## Inoltro delle copie dei messaggi per la notifica dello stato del recapito alla cassetta postale del destinatario di Exchange

È possibile specificare un elenco di codici per le notifiche dello stato del recapito da monitorare copiando i messaggi per la notifica nella cassetta postale del destinatario di Exchange. Tuttavia, per impostazione predefinita, al destinatario di Exchange non è assegnata alcuna cassetta postale e di conseguenza i messaggi inviati al destinatario di Exchange vengono ignorati. Per inviare le copie dei messaggi per la notifica dello stato del recapito alla cassetta postale del destinatario di Exchange, è necessario assegnare al destinatario di Exchange una cassetta postale e quindi specificare i codici per le notifiche che si desidera monitorare. Per impostazione predefinita, vengono monitorati i seguenti codici DSN: `5.4.8`, `5.4.6`, `5.4.4`, `5.2.4`, `5.2.0` e `5.1.4`.

## Passaggio 1: Utilizzare Shell per assegnare una cassetta postale al destinatario di Exchange

Per assegnare una cassetta postale al destinatario di Exchange, fare quanto segue:

1.  A causa del volume potenzialmente elevato di messaggi di posta elettronica, può essere opportuno creare un account utente di Active Directory e una cassetta postale dedicati per il destinatario di Exchange. Per ulteriori informazioni, vedere [Creazione di cassette postali utente](create-user-mailboxes-exchange-2013-help.md). Altrimenti, identificare la cassetta postale esistente da associare al destinatario di Exchange.

2.  Eseguire il comando indicato di seguito:
    
    ```powershell
    Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    ```
    
    Ad esempio, per assegnare al destinatario di Exchange la cassetta postale esistente denominata "Contoso System Mailbox", utilizzare il seguente comando:
    
    ```powershell
    Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"
    ```

## Passaggio 2: Specificare i codici per le notifiche dello stato del recapito che si desidera monitorare

## Utilizzo dell'interfaccia di amministrazione di Exchange per specificare i codici per le notifiche dello stato del recapito

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Connettori di ricezione** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **Impostazioni di trasporto nell'organizzazione** \> **Recapito**.

2.  Nella sezione **Codici per le notifiche dello stato del recapito**, digitare il codice che si desidera monitorare utilizzando il formato *\<x.y.z\>*, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Selezionare una voce esistente e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per modificarla oppure fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per rimuoverla. Al termine, fare clic su **Save**.

## Utilizzo di Shell per la scelta dei codici per la notifica dello stato del recapito

Per sostituire i valori esistenti, eseguire questo comando:

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...
```

In questo esempio, l'organizzazione Exchange viene configurata per l'inoltro all'account di posta elettronica postmaster di tutti i messaggi per la notifica dello stato del recapito con codice 5.7.1, 5.7.2 e 5.7.3.

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3
```

Per aggiungere o rimuovere le voci senza modificare i valori esistenti, eseguire questo comando:
```powershell
    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}
```
In questo esempio, il codice 5.7.5 viene aggiunto e il codice 5.7.1 viene rimosso dall'elenco esistente di messaggi per la notifica dello stato del recapito inoltrati al destinatario Exchange.

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato correttamente l'invio dei messaggi per la notifica dello stato del recapito alla cassetta postale del destinatario di Exchange, monitorare la cassetta postale associata al destinatario di Exchange e verificare che i messaggi per la notifica dello stato del recapito contengano i codici specificati.

