---
title: 'Consenti o meno trasfer. chiamate da operat. automatico: Exchange 2013 Help'
TOCTitle: Consentire o impedire il trasferimento di chiamate da un operatore automatico
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52057333
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire o impedire il trasferimento di chiamate da un operatore automatico

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile consentire o impedire ai chiamanti di trasferire le chiamate agli utenti tramite un operatore automatico. Per impostazione predefinita questa opzione è abilitata e i chiamati possono trasferire le chiamate a utenti abilitati alla messaggistica unificata nel dial plan di messaggistica unificata associato all'operatore automatico di messaggistica unificata.

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

## Abilitazione o disabilitazione dei trasferimenti delle chiamate agli utenti tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera impostare il trasferimento di chiamata e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Accesso operatore e rubrica**, sotto **Opzioni per contattare gli utenti**, selezionare la casella di controllo accanto a **Consenti ai chiamanti il trasferimento agli utenti** per consentire il trasferimento delle chiamate. Per impedire i trasferimenti delle chiamate, deselezionare la casella di controllo.

4.  Fare clic su **Salva**.


> [!NOTE]
> Se si deseleziona questa casella di controllo e anche l'opzione <STRONG>Consenti ai chiamanti di lasciare messaggi vocali per gli utenti</STRONG>, vengono disabilitate le <STRONG>Opzioni per la ricerca nella rubrica</STRONG>.



## Abilitazione o disabilitazione dei trasferimenti delle chiamate agli utenti tramite Shell

In questo esempio si impedisce il trasferimento delle chiamate in un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

In questo esempio si consente il trasferimento delle chiamata in un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

