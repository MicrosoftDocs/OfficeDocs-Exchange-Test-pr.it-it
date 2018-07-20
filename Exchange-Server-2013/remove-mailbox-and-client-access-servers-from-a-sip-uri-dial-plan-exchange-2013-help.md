---
title: 'Rimuovere i server cassette postali e accesso Client da un dial plan URI SIP: Exchange 2013 Help'
TOCTitle: Rimuovere i server cassette postali e accesso Client da un dial plan URI SIP
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54652863
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere i server cassette postali e accesso Client da un dial plan URI SIP

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-16_

È possibile rimuovere i server Accesso client e Cassette postali dai dial plan URI SIP. Affinché le chiamate in uscita vengano abilitate correttamente durante la distribuzione di Microsoft Lync Server, è necessario aggiungere manualmente tutti i server Accesso client e Cassette postali ai dial plan URI SIP creati con Lync Server. Tuttavia, se si sta eseguendo la manutenzione o disconnettendo il server, è necessario rimuovere il server Accesso client o Cassette postali dalla distribuzione Lync.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan URI SIP prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Rimozione del server Cassette postali dal dial plan URI SIP tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Cassette postali che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Server Exchange** scegliere **Messaggistica unificata**.

4.  In **Impostazioni del servizio di messaggistica unificata** \> **Dial plan associati**, individuare il dial plan URI SIP da rimuovere, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"), quindi su **Salva**. Se si desidera rimuovere più di un dial plan URI SIP, tenere premuto il tasto CTRL, selezionare il dial plan da rimuovere e scegliere **Salva**.

## Rimozione del server Cassette postali dal dial plan URI SIP tramite Shell

Con questo esempio viene rimosso il server Cassette postali `MyMailboxServer` dal dial plan URI SIP `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

In questo esempio, sono presenti tre dial plan URI SIP: SipDP1, SipDP2 e SipDP3. Con questo esempio viene rimosso il server Cassette postali `MyMailboxServer` dal dial plan SipDP3.

    Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2

In questo esempio, sono presenti due dial plan URI SIP: SipDP1 e SipDP2. Con questo esempio viene rimosso il server Cassette postali `MyMailboxServer` dal dial plan SipDP2.

    Set-UMService -id MyMailboxServer -DialPlans SipDP1

Con questo esempio viene rimosso il server Cassette postali `MyMailboxServer` da tutti i dial plan SIP.

    Set-UMService -id MyUMServer -DialPlans $null

## Rimozione del server Accesso client dal dial plan URI SIP tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Accesso client che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Server Exchange** scegliere **Messaggistica unificata**.

4.  In **Impostazioni routing di chiamate di messaggistica unificata** \> **Dial plan associati**, individuare il dial plan URI SIP da rimuovere, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"), quindi su **Salva**. Se si desidera rimuovere più di un dial plan URI SIP, tenere premuto il tasto CTRL, selezionare il dial plan da rimuovere e scegliere **Salva**.

## Rimozione del server Accesso client dal dial plan URI SIP tramite Shell

Con questo esempio viene rimosso il server Accesso client `MyClientAccessServer` dal dial plan URI SIP `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

In questo esempio, sono presenti tre dial plan URI SIP: SipDP1, SipDP2 e SipDP3. Con questo esempio viene rimosso il server Accesso client `MyClientAccessServer` dal dial plan SipDP3.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2

In questo esempio, sono presenti due dial plan URI SIP: SipDP1 e SipDP2. Con questo esempio viene rimosso il server Accesso client `MyClientAccessServer` dal dial plan SipDP2.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1

Con questo esempio viene rimosso il server Accesso client `MyClientAccessServer` da tutti i dial plan SIP.

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null

