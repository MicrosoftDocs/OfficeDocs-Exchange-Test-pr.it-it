---
title: 'Aggiungere un numero e. 164: Exchange 2013 Help'
TOCTitle: Aggiungere un numero e. 164
ms:assetid: fab86207-be03-40ef-9fea-045a50f3d122
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ662762(v=EXCHG.150)
ms:contentKeyID: 50555713
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere un numero e. 164

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-14_

Quando si abilita un utente alla messaggistica unificata e lo si collega a un dial plan E.164, vengono creati due indirizzi proxy di messaggistica unificata di Exchange. Uno contiene il numero di interno dell'utente e l'altro il numero E.164 dell'utente. Il numero di interno viene utilizzato quando l'utente chiama un numero di Outlook Voice Access.

Il numero E.164 primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata verrà elencato come indirizzo proxy di messaggistica unificata di Exchange primario. Se il numero E.164 primario è stato rimosso, il primo indirizzo proxy di messaggistica unificata di Exchange aggiunto che contiene il numero E.164 dell'utente verrà elencato come indirizzo proxy di messaggistica unificata di Exchange primario. Ulteriori numeri E.164 aggiunti verranno elencati come indirizzi proxy di messaggistica unificata di Exchange secondari. Quando vengono aggiunti altri numeri E.164, i chiamanti possono lasciare messaggi vocali per l'utente a tutti i numeri E.164 che sono stati impostati. Tutti i messaggi vocali saranno consegnati alla cassetta postale dello stesso utente.

È possibile utilizzare EAC o Shell per aggiungere un numero E.164 primario o secondario per l'utente. È possibile utilizzare la pagina **Indirizzo di posta elettronica** nella cassetta postale dell'utente in EAC per aggiungere un numero E.164 primario o secondario. Non è possibile utilizzare la pagina **Cassetta postale di messaggistica unificata** in EAC per aggiungere un numero E.164 primario o secondario.

È possibile visualizzare i numeri E.164 primario e secondario per un utente utilizzando il cmdlet **Get-UMMailbox** o **Get-Mailbox** in Shell.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire queste procedure, è necessario confermare la creazione di un dial plan di messaggistica unificata E.164. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata e collegata a un dial plan E.164. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che il numero E.164 che sarà assegnato all'utente sia valido e formattato correttamente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Aggiunta di un numero E.164 primario o secondario tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale per cui si desidera aggiungere un numero E.164, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina **Cassetta postale utente**, sotto **Indirizzo di posta elettronica**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Dalla pagina **Nuovo indirizzo di posta elettronica** selezionare **Indirizzo di messaggistica unificata di Exchange** e immettere il nuovo numero E.164 per l'utente nella casella **Indirizzo/estensione**.

5.  Dalla pagina **Nuovo indirizzo di posta elettronica**, sotto **Dial plan**, fare clic su **Sfoglia** per selezionare il dial plan E.164, quindi fare clic su **OK**.

6.  Fare clic su **Salva**.

## Aggiunta di un numero E.164 tramite Shell

Con questo esempio viene aggiunto un numero E.164 per Tony Smith, un utente abilitato alla messaggistica unificata.


> [!NOTE]
> Prima di aggiungere un numero E.164 tramite Shell, è necessario stabilire la posizione dell'indirizzo proxy di messaggistica unificata di Exchange che si desidera aggiungere. Per stabilire la posizione, utilizzare il comando <STRONG>$mbx.EmailAddresses</STRONG>. Il primo indirizzo proxy nell'elenco sarà 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(2)="eum:+14255550123;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

