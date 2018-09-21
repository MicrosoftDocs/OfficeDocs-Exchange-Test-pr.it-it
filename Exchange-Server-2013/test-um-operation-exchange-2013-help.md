---
title: 'Eseguire il test della messaggistica unificata operazione: Exchange 2013 Help'
TOCTitle: Eseguire il test della messaggistica unificata operazione
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56269827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire il test della messaggistica unificata operazione

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-06-25_

In questo argomento viene descritto come utilizzare Shell per testare il funzionamento del sistema di caselle vocali. Quando vengono eseguite le procedure riportate di seguito, il server Cassette postali che esegue il servizio Messaggistica unificata di Microsoft Exchange avvia una chiamata SIP (Session Initiation Protocol) diagnostica, quindi restituisce una variabile relativa allo stato di integrità dei servizi di messaggistica unifica.

Questo test diagnostico può essere eseguito solo su un server Cassette postali locale e non è possibile testare il funzionamento di tale server utilizzando l'interfaccia di amministrazione di Exchange.

Per altre attività di gestione relative ai server Accesso client e Cassette postali, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Informazioni preliminari

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere le voci "Server Cassette postali (servizio di messaggistica unificata)" e "Server Accesso client (servizio di routing delle chiamate di messaggistica unificata)" dell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per eseguire le procedure riportate di seguito, è necessario accedere al server Cassette postali utilizzando un account membro del gruppo Administrators locale.

  - Verificare che il server Cassette postali sia installato nello stesso computer del server Accesso client o in un computer diverso.

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o in un computer diverso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per testare il funzionamento dei servizi di messaggistica unificata.

Con questo esempio vengono eseguiti test operativi e di connettività sul server Cassette postali locale e vengono visualizzate le informazioni sulla connettività Voice over IP (VoIP).

```powershell
Test-UMConnectivity
```

In questo esempio viene verificata la capacità del server Accesso client locale riguardo all'ascolto delle richieste SIP in ingresso non crittografate sulla porta TCP port 5060.

```powershell
Test-UMConnectivity -ListenPort 5060
```

In questo esempio viene verificata la capacità del server Accesso client locale riguardo all'ascolto delle richieste SIP in ingresso crittografate sulla porta TCP port 5061.

```powershell
Test-UMConnectivity -ListenPort 5061
```


> [!NOTE]
> Utilizzare la modalità 1 quando non viene specificato il parametro <CODE>-UMIPGateway</CODE>.




> [!NOTE]
> È possibile impostare il parametro <CODE>-Timeout</CODE> con un valore inferiore a 5 secondi. Tuttavia, si consiglia di configurarlo sempre con un valore pari o superiore a 5 secondi.


