---
title: 'Configura modalità di avvio in un server Accesso Client: Exchange 2013 Help'
TOCTitle: Configurare la modalità di avvio in un server Accesso Client
ms:assetid: 71cc9061-9e3c-4b4a-8dbe-f590ca5bcee8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673533(v=EXCHG.150)
ms:contentKeyID: 50555616
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la modalità di avvio in un server Accesso Client

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-15_

È possibile specificare la modalità di avvio per il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange su un server Accesso client. Per impostazione predefinita, il server Accesso client si avvierà in modalità TCP, ma se si sta utilizzando Transport Layer Security (TLS) per crittografare il traffico VoIP è necessario configurare il server Accesso client per la modalità TLS o Dual. È preferibile configurare i server Accesso client per l'utilizzo di Dual in modalità di avvio. Questa situazione si verifica perché i server Accesso client e Cassette postali rispondono alle chiamate in arrivo per tutti i dial plan di messaggistica unificata, ma tali dial plan possono avere impostazioni di protezione diverse. Se si modifica la modalità di avvio, è necessario riavviare il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange per rendere effettive le modifiche.


> [!IMPORTANT]
> Per impostazione predefinita, i server Accesso Client sono disponibili per rispondere alle chiamate in arrivo. Non è necessario aggiungere un server Accesso client a un dial plan di messaggistica unificata per elaborare le chiamate di messaggistica unificata, a meno che non si stia integrando la messaggistica unificata con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server.



Per ulteriori attività di gestione relative ai server Messaggistica unificata e Accesso client, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Accesso client (servizio di routing delle chiamate di messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o in un computer diverso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Configurazione della modalità di avvio su un server Accesso client tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** scegliere il pulsante **Messaggistica unificata**.

4.  In **Impostazioni router di chiamata messaggistica unificata** \> **Modalità di avvio messaggistica unificata**, selezionare una delle seguenti opzioni dall'elenco a discesa:
    
      - **TCP**   Utilizzare quest'opzione se non si utilizza mTLS e si utilizzano solo dial plan non protetti.
    
      - **TLS**   Utilizzare quest'opzione se si utilizza mTLS e si utilizzano solo SIP con protezione o dial plan protetti.
    
      - **DUAL**   Utilizzare quest'opzione se si utilizza mTLS e si utilizzano SIP con protezione, senza protezione o dial plan protetti.

5.  Dopo aver selezionato la modalità di avvio Messaggistica unificata, fare clic su **Salva**.

## Configurazione della modalità di avvio su un server Accesso client tramite Shell

In questo esempio viene imposta la modalità di avvio per il server Accesso client `UMCallRouter1` in modalità Dual.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode Dual

In questo esempio viene imposta la modalità di avvio per il server Accesso client `UMCallRouter1` in modalità TLS.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode TLS

