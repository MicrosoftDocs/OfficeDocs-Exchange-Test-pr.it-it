---
title: "Abilitare o disabilitare l'invio di messaggi vocali per gli utenti: Exchange 2013 Help"
TOCTitle: Abilitare o disabilitare l'invio di messaggi vocali per gli utenti
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52057360
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare l'invio di messaggi vocali per gli utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-13_

È possibile abilitare o disabilitare i chiamanti all'invio di messaggi vocali agli utenti da un operatore automatico di messaggistica unificata. Per impostazione predefinita, questa opzione è abilitata e consente ai chiamanti di inviare messaggi vocali agli utenti nel dial plan di messaggistica unificata associato all'operatore automatico di messaggistica unificata. Se questa opzione viene disabilitata, l'operatore automatico non inviterà i chiamanti a inviare un messaggio vocale durante un prompt di sistema.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per consentire o impedire ai chiamanti di inviare messaggi vocali

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Accesso operatore e rubrica**, sotto **Opzioni per contattare gli utenti**, selezionare la casella di controllo accanto a **Consenti a chiamanti di lasciare messaggi vocali per gli utenti** per consentire ai chiamati di lasciare messaggi vocali. Per impedire ai chiamati di lasciare messaggi vocali, deselezionare la casella di controllo.

4.  Fare clic su **Salva**.


> [!NOTE]
> Se vengono disabilitate questa opzione e l'opzione <STRONG>Consenti ai chiamanti di chiamare gli utenti</STRONG>, vengono disabilitate anche le opzioni sotto <STRONG>Opzioni per la ricerca nella rubrica</STRONG>.



## Utilizzo di Shell per consentire o impedire ai chiamanti di inviare messaggi vocali

Con questo esempio si impedisce ai chiamanti che contattano l'operatore automatico di messaggistica unificata `MyUMAutoAttendant` di inviare messaggi vocali.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

Con questo esempio si consente ai chiamanti che contattano l'operatore automatico di messaggistica unificata `MyUMAutoAttendant` di inviare messaggi vocali.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

