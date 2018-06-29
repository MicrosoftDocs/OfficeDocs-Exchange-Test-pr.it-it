---
title: 'Configurazione di Suggerimenti messaggio personalizzati per i destinatari: Exchange 2013 Help'
TOCTitle: Configurazione di Suggerimenti messaggio personalizzati per i destinatari
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52057340
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione di Suggerimenti messaggio personalizzati per i destinatari

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-06-01_

I *suggerimenti messaggio* sono messaggi informativi visualizzati agli utenti nella barra delle informazioni in Outlook Web App e Microsoft Outlook 2010 o versione successiva quando un utente effettua una delle seguenti operazioni durante la composizione di un messaggio di posta elettronica:

  - Aggiunta di un destinatario

  - Aggiunta di un allegato

  - Risposta al mittente o risposta a tutti

  - Apertura dalla cartella Bozze di un messaggio per cui sono già specificati i destinatari

Oltre ai suggerimenti messaggio incorporati, è possibile creare suggerimenti messaggio personalizzati per tutti i tipi di destinatari. Per ulteriori informazioni sui suggerimenti messaggio incorporati, vedere [MailTips](mailtips-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Suggerimenti messaggio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile configurare il suggerimento messaggio principale nell'interfaccia di amministrazione di Exchange o in Shell. Tuttavia, è possibile configurare ulteriori traduzioni di suggerimenti messaggio solo in Shell.

  - Quando si aggiunge un suggerimento messaggio a un destinatario, accadono due cose:
    
      - Vengono automaticamente aggiunti tag HTML al testo. Se, ad esempio, si immette il testo `This mailbox is not monitored`, il suggerimento messaggio cambia automaticamente in `<html><body>This mailbox is not monitored</body></html>`. Non sono supportati altri tag HTML in Avviso messaggio.
    
      - Il testo viene automaticamente aggiunto alla proprietà *MailTipTranslations* del destinatario come valore predefinito. Se si modifica il testo del suggerimento messaggio, il valore predefinito viene automaticamente aggiornato nella proprietà *MailTipTranslations*.

  - La lunghezza di un suggerimento messaggio non può superare i 175 caratteri visualizzati.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurazione dei suggerimenti messaggio per i destinatari

## Configurazione dei suggerimenti messaggio tramite EAC

1.  In EAC accedere a **Destinatari**.

2.  Selezionare una delle seguenti schede dei destinatari in base al tipo di destinatario:
    
      - **Cassette postali**
    
      - **Gruppi**
    
      - **Risorse**
    
      - **Contatti**
    
      - **Condiviso**

3.  Nella scheda dei destinatari, selezionare il destinatario da modificare e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Nella pagina delle proprietà del destinatario, fare clic su **Suggerimento messaggio**.

5.  Immettere il testo per il suggerimento messaggio. Al termine, fare clic su **Salva**.

## Configurazione dei suggerimenti messaggio tramite Shell

Per configurare un suggerimento messaggio per un destinatario, utilizzare la sintassi seguente.

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* può essere qualsiasi tipo di destinatario. Ad esempio, `Mailbox`, `MailUser`, `MailContact`, `DistributionGroup` o `DynamicDistributionGroup`.

Si supponga, ad esempio, di disporre di una cassetta postale denominata "Help Desk" a cui gli utenti possano inviare richieste di supporto e che il tempo di risposta garantito sia pari a due ore. Per configurare un suggerimento messaggio personalizzato in cui fornire queste informazioni, utilizzare il comando seguente:

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## Configurazione di ulteriori suggerimenti messaggio in lingue diverse tramite Shell

Per configurare ulteriori traduzioni dei suggerimenti messaggio senza modificare il testo esistente o altre traduzioni, utilizzare la sintassi seguente:

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* corrisponde a un codice ISO 639 di due lettere valido associato a una lingua.

Ad esempio, si supponga che per la cassetta postale Notifiche sia disponibile il seguente suggerimento messaggio "Questa cassetta postale non è monitorata". Per aggiungere la traduzione spagnola, utilizzare il seguente comando:

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stato configurato correttamente un suggerimento messaggio per un destinatario, procedere come segue:

1.  In Outlook Web App o Outlook 2010 o versione successiva, comporre un messaggio di posta elettronica indirizzato al destinatario ma non inviarlo.

2.  Verificare che il suggerimento messaggio venga visualizzato nella barra informazioni.

3.  Se sono state configurate ulteriori traduzioni del suggerimento messaggio, comporre il messaggio in Outlook Web App in cui l'impostazione della lingua corrisponde alla traduzione del suggerimento messaggio per verificare i risultati.

