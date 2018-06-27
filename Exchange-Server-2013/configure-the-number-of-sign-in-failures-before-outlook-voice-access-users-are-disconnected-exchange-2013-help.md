---
title: 'Configurare il numero di errori di accesso prima che gli utenti di Outlook Voice Access vengono disconnessi: Exchange 2013 Help'
TOCTitle: Configurare il numero di errori di accesso prima che gli utenti di Outlook Voice Access vengono disconnessi
ms:assetid: 02f93888-168c-44bb-8cf6-17f5fcc3d733
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423537(v=EXCHG.150)
ms:contentKeyID: 50479914
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il numero di errori di accesso prima che gli utenti di Outlook Voice Access vengono disconnessi

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-09_

È possibile specificare il numero consentito di tentativi di accesso non riusciti consecutivi prima della disconnessione di un chiamante. Il valore di questa impostazione può essere compreso tra 1 e 20. L'impostazione di un valore troppo basso può causare alcune difficoltà agli utenti. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore deve essere di tre tentativi.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzo dell'interfaccia di amministrazione di Exchange per la configurazione del numero massimo di tentativi di accesso errati prima della disconnessione

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Impostazioni**, immettere il numero massimo di tentativi di accesso errati in **Numero di errori di accesso prima della disconnessione**.

5.  Fare clic su **Salva**.

## Configurazione del numero di errori di accesso prima della disconnessione degli utenti tramite Shell

In questo esempio viene impostato il numero di errori di accesso prima della disconnessione degli utenti su 5 per un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -LogonFailuresBeforeDisconnect 5

