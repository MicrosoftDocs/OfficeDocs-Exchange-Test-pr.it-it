---
title: 'Config. errori input prima di discon. Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurare il numero di errori di input prima che gli utenti di Outlook Voice Access vengono disconnessi
ms:assetid: 64c13d17-a26a-4c9b-b495-bd69c716456a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423547(v=EXCHG.150)
ms:contentKeyID: 50480821
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il numero di errori di input prima che gli utenti di Outlook Voice Access vengono disconnessi

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-09_

È possibile specificare per quante volte gli utenti che chiamano un numero di Outlook Voice Access possono immettere dati non corretti prima di venire disconnessi. Questa impostazione vale sia per i chiamanti non autenticati che utilizzano la ricerca per directory che per gli utenti di Outlook Voice Access.

Di seguito sono riportati alcuni esempi dei tipi di dati considerati non corretti:

  - Un chiamante richiede il numero di un interno che non è presente nel sistema.

  - Il sistema non è grado di individuare il numero dell'interno dell'utente per trasferire la chiamata.

  - Un chiamante sceglie un'opzione di menu non valida.

È possibile impostare un qualsiasi valore compreso tra 1 e 20. Nella maggior parte delle organizzazioni, è consigliabile impostarlo su tre tentativi. Se si sceglie un valore troppo basso, i chiamanti potrebbero essere disconnessi troppo presto.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la configurazione degli errori di immissione prima della disconnessione

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Impostazioni**, immettere il numero massimo di tentativi di immissione errati in **Numero di errori di input prima della disconnessione**.

5.  Fare clic su **Salva**.

## Configurazione degli errori di input prima della disconnessione tramite Shell

In questo esempio, il numero di tentativi non riusciti prima della disconnessione viene impostato su 5 per un dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -InputFailuresBeforeDisconnect 5

