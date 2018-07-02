---
title: 'Configurare la modalità di avvio in un server cassette postali: Exchange 2013 Help'
TOCTitle: Configurare la modalità di avvio in un server cassette postali
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50555578
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la modalità di avvio in un server cassette postali

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-15_

È possibile specificare la modalità di avvio per il il servizio Messaggistica unificata di Microsoft Exchange su un server Cassette postali. Per impostazione predefinita, il server Cassette postali si avvierà in modalità TCP, ma se si sta utilizzando Transport Layer Security (TLS) per crittografare il traffico VoIP, è necessario configurare il server Cassette postali per la modalità TLS o Doppio. È consigliabile configurare i server Cassette postali per l'utilizzo della modalità Doppio all'avvio. Infatti, tutti i server Accesso client e Cassette postali possono rispondere alle chiamate in ingresso per tutti i dial plan di messaggistica unificata e questi dial plan possono utilizzare diverse impostazioni di sicurezza (Non sicuro, SIP con protezione o Protetto). Se si modifica la modalità di avvio, è necessario riavviare il servizio messaggistica unificata di Microsoft Exchange affinchè le modifiche abbiano effetto.


> [!IMPORTANT]
> Per impostazione predefinita, i server Cassette postali sono disponibili per rispondere alle chiamate in ingresso. Non è necessario aggiungere un server Cassette postali a un dial plan di messaggistica unificata per elaborare le chiamate di messaggistica unificata, a meno che non si stia integrando la messaggistica unificata e Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server.



Per informazioni sulle altre attività di gestione relative ai server Cassette postali e Messaggistica unificata, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Cassette postali (servizio Messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server Cassette postali sia installato nello stesso computer del server Accesso client o in un altro computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione della modalità di avvio su un server Cassette postali tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Server Exchange** scegliere **Messaggistica unificata**.

4.  In **Impostazioni servizio di Messaggistica unificata** \> **Modalità di avvio per la messaggistica unificata**, selezionare una delle seguenti opzioni dall'elenco a discesa:
    
      - **TCP**   Utilizzare questa opzione se non si utilizza MTLS e se si utilizzano solo dial plan non protetti.
    
      - **TLS**   Utilizzare questa opzione se si utilizza MTLS e solo se si utilizza SIP protetta o dial plan protetti.
    
      - **DUAL**   Utilizzare questa opzione se si utilizza MTLS, SIP protetta, non protetta e dial plan protetti.

5.  Dopo aver selezionato la modalità di avvio per la messaggistica unificata, fare clic su **Salva**.

## Configurazione della modalità di avvio su un server Cassette postali tramite Shell

In questo esempio viene imposta la modalità di avvio per un server Cassette postali denominato `MyUMServer1` per la modalità dual.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual

In questo esempio viene imposta la modalità di avvio per un server Cassette postali denominato `MyUMServer1` per la modalità TLS.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS

