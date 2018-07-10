---
title: 'Configurare il numero di chiamate in arrivo in un server cassette postali: Exchange 2013 Help'
TOCTitle: Configurare il numero di chiamate in arrivo in un server cassette postali
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50555573
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il numero di chiamate in arrivo in un server cassette postali

 

_**Si applica a:** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile configurare il numero di connessioni contemporanee in ingresso che un server Cassette postali con il servizio di messaggistica unificata di Microsoft Exchange può accettare. Questo comprende chiamate in ingresso di Outlook Voice Access, ricezione chiamate, operatore automatico e chiamate fax. Se sul server Cassette postali viene aumentato il numero di connessioni contemporanee, saranno necessarie più risorse di sistema. Ridurre il numero di connessioni contemporanee è particolarmente importante nei computer più lenti su cui sono installati i servizi di messaggistica unificata. L'intervallo del numero di chiamate vocali contemporanee va da 0 e 200. L'impostazione predefinita è 100.

Per informazioni sulle altre attività relative ai server Cassette postali e Messaggistica unificata, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Cassette postali (servizio Messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare di aver installato correttamente i server Accesso client e Cassette postali.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione del numero di chiamate in ingresso su un server Cassette postali tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server di Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Server Exchange** scegliere **Messaggistica unificata**.

4.  In **Impostazioni Messaggistica unificata**, **Numero massimo di chiamate consentite**, inserire un numero compreso tra 0 e 200, quindi fare clic su **Salva**.

## Configurazione del numero di chiamate in ingresso su un server Cassette postali tramite Shell

In questo esempio, viene impostato su 50 il numero di chiamate vocali, Outlook Voice Access e fax in ingresso che il server Cassette postali `MyMailboxServer1` può accettare.

    Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50

