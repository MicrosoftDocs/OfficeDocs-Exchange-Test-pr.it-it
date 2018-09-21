---
title: 'Configura messagg. unificata con Lync Server: Exchange 2013 Help'
TOCTitle: Configurare la messaggistica unificata per l'utilizzo con Lync Server
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52063053
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la messaggistica unificata per l'utilizzo con Lync Server

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-06-11_

Quando si effettua l'integrazione di Microsoft Lync Server con il servizio Messaggistica unificata di Exchange, è necessario eseguire lo script ExchUcUtil.ps1 script in Shell. Lo script ExchUcUtil.ps1 esegue quanto indicato di seguito:

  - Crea un gateway IP di messaggistica unificata per ogni pool di Lync Server.
    

    > [!IMPORTANT]
    > Lo script ExchUcUtil.ps1 crea uno o più gateway IP di messaggistica unificata. È necessario disabilitare le chiamate in uscita su tutti i gateway IP di messaggistica unificata, ad eccezione di quello creato dallo script. Questo comprende la disabilitazione delle chiamate in uscita sui gateway IP di messaggistica unificata creati prima dell'esecuzione dello script. Per disabilitare le chiamate in uscita su un gateway IP di messaggistica unificata, vedere <A href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-outgoing-calls-on-um-ip-gateways">Disabilitare le chiamate in uscita sui gateway IP di messaggistica unificata</A>.



  - Crea un gruppo di risposta di messaggistica unificata per ciascun gateway IP di messaggistica unificata. L'identificatore pilota di ciascun gruppo di risposta di messaggistica unificata specifica il dial plan URI SIP di messaggistica unificata utilizzato dal pool Lync Server Front End o dal server Standard Edition associato al gateway IP di messaggistica unificata.

  - Concede le autorizzazioni Lync Server per la lettura di oggetti contenitore di messaggistica unificata di Active Directory, ad esempio dial plan di messaggistica unificata, operatori automatici, gateway IP di messaggistica unificata e gruppi di risposta di messaggistica unificata.


> [!IMPORTANT]
> Ciascuna foresta di messaggistica unificata deve essere configurata in modo da considerare attendibile la foresta in cui è distribuito Lync Server 2013 e la foresta in cui è distribuito Lync Server 2013 deve essere configurata in modo da considerare attendibile ciascuna foresta di messaggistica unificata. Se Messaggistica unificata di Exchange è installata in più foreste, i passaggi per l'integrazione di Exchange Server devono essere eseguiti per ciascuna foresta di messaggistica unificata. In caso contrario, è necessario specificare il dominio Lync Server. Ad esempio, <EM>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</EM>.



Per ulteriori attività di gestione correlate all'integrazione di Lync Server e Messaggistica unificata, vedere [Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

## Informazioni preliminari

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cmdlet per le autorizzazioni" nell'argomento [Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per l'esecuzione dello script ExchUcUtil.ps1

Eseguire lo script ExchUcUtil.ps1 su qualsiasi server di Exchange dell'organizzazione che si trovi nella stessa topologia di Microsoft Lync Server. È possibile eseguire lo script da un server Cassette postali utilizzando Shell oppure utilizzando Windows PowerShell remoto su un server Accesso client. Se si esegue lo script su un server Accesso client dell'organizzazione, tale server inoltrerà la sessione di Windows PowerShell remoto a un server Cassette postali dell'organizzazione.


> [!IMPORTANT]
> Lo script ExchUcUtil.ps1 crea uno o più gateway IP di messaggistica unificata. È necessario disabilitare le chiamate in uscita su tutti i gateway IP di messaggistica unificata, ad eccezione di quello creato dallo script. Questo comprende la disabilitazione delle chiamate in uscita sui gateway IP di messaggistica unificata creati prima dell'esecuzione dello script. Per disabilitare le chiamate in uscita su un gateway IP di messaggistica unificata, vedere <A href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-outgoing-calls-on-um-ip-gateways">Disabilitare le chiamate in uscita sui gateway IP di messaggistica unificata</A>.




> [!IMPORTANT]
> Per eseguire lo script, è necessario disporre delle autorizzazioni del ruolo Exchange Organization Management o essere membri del gruppo di sicurezza Exchange Organization Administrators.



1.  Aprire Exchange Management Shell.

2.  Al prompt di `C:\Windows\System32`, digitare **cd \&quot;\<lettera unità\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1\&quot;**, quindi premere Invio.

## Verifica dell'esito positivo dell'operazione

Per verificare che lo script ExchUcUtul.ps1 sia stato eseguito correttamente, procedere come segue:

  - Utilizzare il cmdlet **Get-UMIPGateway** o l'interfaccia di amministrazione di Exchange per visualizzare il nuovo gateway IP di messaggistica unificata o i gateway che sono stati creati.

  - Utilizzare il cmdlet **Get-UMHuntGroup** o l'interfaccia di amministrazione di Exchange per visualizzare il nuovo gruppo di risposta di messaggistica unificata o i gruppi che sono stati creati.

