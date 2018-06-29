---
title: 'Configurare un numero Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurare un numero Outlook Voice Access
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50555579
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un numero Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Un numero di Outlook Voice Access consente ad un utente abilitato alla messaggistica unificata e ai messaggi vocali di accedere alla cassetta postale utilizzando Outlook Voice Access. Una volta configurato un numero di accesso del sottoscrittore o di Outlook Voice Access su un dial plan, gli utenti abilitati alla messaggistica unificata potranno chiamare il numero, accedere alla loro cassetta postale, alla posta elettronica, alla casella vocale, al calendario e alle informazioni personali sui contatti.

Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, non viene configurato alcun numero di Outlook Voice Access. Per configurare un numero di Outlook Voice Access, è necessario innanzitutto creare il dial plan, quindi configurare un numero di Outlook Voice Access sotto l'opzione di **Outlook Voice Access** del dial plan. Sebbene non sia obbligatorio immettere un numero di Outlook Voice Access, è necessario configurarne almeno uno per consentire a un utente abilitato alla messaggistica unificata di utilizzare Outlook Voice Access per accedere alla propria cassetta postale. È inoltre possibile configurare più numeri di Outlook Voice Access per un singolo dial plan.

I numeri di Outlook Voice Access possono contenere caratteri alfabetici, numerici e caratteri speciali, separatori e spazi. Esempio:

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

Per ulteriori informazioni sulle opzioni di menu disponibili per gli utenti di Outlook Voice Access, vedere la Guida di riferimento rapido per Outlook Voice Access, disponibile dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=64645).

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione di un numero di Outlook Voice Access tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Outlook Voice Access**, sotto **Numeri di Outlook Voice Access**, utilizzare la casella per immettere il numero che si desidera utilizzare, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Fare clic su **Salva**.

## Configurazione di un numero di Outlook Voice Access tramite Shell

In questo esempio, viene impostato il numero di accesso di Outlook Voice Access su 4255550100 per un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

