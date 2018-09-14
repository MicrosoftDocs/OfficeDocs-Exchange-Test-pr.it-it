---
title: 'Agg. cassette postali/accesso Client a dial plan URI SIP:Exchange 2013 Help'
TOCTitle: Aggiungere server cassette postali e accesso Client a un dial plan URI SIP
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52063046
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere server cassette postali e accesso Client a un dial plan URI SIP

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-16_

È possibile aggiungere i server Accesso client e Cassette postali ai dial plan SIP. I server Accesso client e Cassette postali non possono essere associati con dial plan Telephone Extension o E.164, ma i server risponderanno alle chiamate in arrivo.

Se si sta distribuendo Microsoft Lync Server, per abilitare il corretto funzionamento delle chiamate in uscita, è necessario aggiungere manualmente tutti i server Accesso client e Cassette postali ai dial plan URI SIP creati per Lync Server.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan SIP URI prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzare l'interfaccia di amministrazione di Exchange per aggiungere un server Cassette postali a un dial plan URI SIP

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Cassette postali che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** fare clic su **Messaggistica unificata**.

4.  In **Impostazioni del servizio di messaggistica unificata** \> **Dial plan associati**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Nella finestra **Seleziona un dial plan di messaggistica unificata**, selezionare il dial plan URI SIP, fare clic su **Aggiungi**, selezionare **OK**, quindi fare clic su **Salva**.

## Utilizzare l'interfaccia di amministrazione di Shell per aggiungere un server Cassette postali a un dial plan URI SIP

In questo esempio viene aggiunto il server Cassette postali denominato `MyMailboxServer` a un dial plan URI SIP denominato `MySIPDialPlan` e gli impedisce di accettare nuove chiamate. Inoltre, la modalità di avvio viene impostata su Dual per consentire al server Cassette postali di accettare le richieste TCP e TLS.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual

In questo esempio viene aggiunto il server Cassette postali denominato `MyMailboxServer` a due dial plan SIP, denominati `MySIPDialPlan` and `MySIPDialPlan2`, e configura le seguenti opzioni:

  - Consente gli indirizzi IPv4 e IPv6.

  - Il numero massimo di chiamate in arrivo viene impostato su 50.

  - Configura il servizio di accesso SIP per Lync Server.

<!-- end list -->

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com

## Utilizzare l'interfaccia di amministrazione di Exchange per aggiungere un server Accesso client a un dial plan URI SIP

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Accesso client che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** fare clic su **Messaggistica unificata**.

4.  In **Impostazioni router di chiamata di messaggistica unificata** \> **Dial plan associati**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Nella finestra **Seleziona un dial plan di messaggistica unificata**, selezionare il dial plan URI SIP, fare clic su **Aggiungi**, selezionare **OK**, quindi fare clic su **Salva**.

## Utilizzare Shell per aggiungere un server Accesso client a un dial plan URI SIP

In questo esempio viene aggiunto il server Accesso client denominato `MyClientAccessServer` a un dial plan URI SIP denominato `MySIPDialPlan`. Inoltre, la modalità di avvio viene impostata su Dual per consentire al server Accesso client di accettare le richieste TCP e TLS.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual

In questo esempio viene aggiunto il server Accesso client denominato `MyClientAccessServer` a due dial plan SIP, denominati `MySIPDialPlan` e `MySIPDialPlan2` e viene consentito al server di utilizzare sia indirizzi IPv4 che IPv6.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer

