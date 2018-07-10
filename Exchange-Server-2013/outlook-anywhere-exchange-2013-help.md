---
title: 'Outlook via Internet: Exchange 2013 Help'
TOCTitle: Outlook via Internet
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 50481196
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook via Internet

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In Microsoft Exchange Server 2013, la funzionalità Outlook via Internet, conosciuta come RPC su HTTP, consente ai client che usano MicrosoftOutlook 2013, Outlook 2010 o Outlook 2007 di connettersi ai server Exchange dall'esterno della rete aziendale o su Internet utilizzando il componente di rete Windows RPC su HTTP. In questo argomento viene illustrata la caratteristica Outlook via Internet e i vantaggi dell'utilizzo di Outlook via Internet.

**Sommario**

Outlook via Internet ed Exchange 2013

Vantaggi dell'utilizzo di Outlook via Internet

Distribuzione di Outlook via Internet

Gestione di Outlook via Internet

Coesistenza di Outlook via Internet

Verifica della connettività di Outlook via Internet

## Outlook via Internet ed Exchange 2013

Il componente proxy Windows RPC su HTTP, che i client di Outlook via Internet utilizzano per connettersi, integra le chiamate di procedura remote (RPC) in un livello HTTP, consentendo al traffico di superare i firewall di rete senza richiedere l'apertura di porte RPC. In Exchange 2013, questa funzionalità è abilitata per impostazione predefinita, poiché Exchange 2013 non consente la connettività RPC diretta.

## Vantaggi dell'utilizzo di Outlook via Internet

Outlook via Internet offre i seguenti vantaggi ai client che utilizzano Outlook 2013, Outlook 2010 o Outlook 2007 per accedere all'infrastruttura di messaggistica di Exchange:

  - Gli utenti possono accedere in remoto ai server Exchange da Internet.

  - È possibile utilizzare lo stesso URL e spazio dei nomi utilizzati per Outlook Web App e MicrosoftExchange ActiveSync.

  - È possibile utilizzare lo stesso certificato del server SSL utilizzato per Outlook Web App e Exchange ActiveSync.

  - Le richieste non autenticate da Outlook non possono accedere ai server Exchange.

  - Non è necessario utilizzare un rete privata virtuale (VPN) per accedere ai server Exchange su Internet.

  - Se si utilizza già Outlook Web App con SSL o Exchange ActiveSync con SSL, non è necessario aprire porte aggiuntive da Internet.

  - È possibile verificare la connettività client end-to-end per Outlook via Internet e le connessioni basate su TCP utilizzando il cmdlet **Test-OutlookConnectivity**.

## Distribuzione di Outlook via Internet

In Exchange 2013, Outlook via Internet è abilitato per impostazione predefinita, perché tutta la connettività di Outlook avviene attraverso Outlook via Internet. L'unica attività successiva alla distribuzione da eseguire per utilizzare correttamente Outlook via Internet è l'installazione di un certificato SSL valido sul server Accesso client. I server Cassette postali nell'organizzazione richiedono solamente il certificato SSL autofirmato predefinito.

## Gestione di Outlook via Internet

È possibile gestire Outlook via Internet utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell.

## Coesistenza di Outlook via Internet

Se si pianifica di installare Exchange 2013 in uno scenario di coesistenza con versioni precedenti di Exchange Server, potrebbe essere possibile avere ancora client Outlook 2003 nell'organizzazione. Outlook 2003 non è una soluzione consigliata per Exchange 2013.

Prima di spostare lo spazio dei nomi in Exchange 2013, è necessario assicurarsi che tutti i client Outlook siano stati aggiornati alle versioni minime. Outlook 2007 o versione successiva è necessario per una connessione Outlook via Internet a Exchange 2013, anche se la cassetta postale di destinazione è ancora su Exchange 2007 o Exchange 2010.

Se al momento si utilizza Outlook via Internet negli ambienti Exchange 2007 o 2010, per consentire al server Accesso client di Exchange 2013 di inoltrare le connessioni ai server Exchange 2007/2010, è necessario abilitare e configurare Outlook via Internet su tutti i server Exchange 2007/2010 dell'organizzazione. Tuttavia, se al momento non si utilizza Outlook via Internet nell'ambiente Exchange 2007/2010 e non si desidera iniziare a utilizzarlo, non è necessario abilitare Outlook via Internet nell'ambiente legacy. Per istruzioni su come abilitare Outlook via Internet per i server Accesso client eseguiti in Exchange Server 2007, vedere [Come abilitare Outlook via Internet](https://go.microsoft.com/fwlink/p/?linkid=510497). Per istruzioni su come abilitare Outlook via Internet per i server Accesso client eseguiti in Exchange Server 2010, vedere [Come abilitare Outlook via Internet](https://go.microsoft.com/fwlink/p/?linkid=510502).

Quando si abilita Outlook via Internet nel server Accesso client, assicurarsi di scegliere NTLM per l'autenticazione IIS.

Infine, configurare il nome dell'host esterno di Outlook via Internet per scegliere il nome host di Outlook via Internet di Exchange 2013. Per istruzioni per Exchange Server 2007, vedere [Configurazione di un nome host esterno per Outlook via Internet](https://go.microsoft.com/fwlink/p/?linkid=510530). Per istruzioni per Exchange Server 2010, vedere [Configurazione di un nome host esterno per Outlook via Internet](https://go.microsoft.com/fwlink/p/?linkid=510531).

## Verifica della connettività di Outlook via Internet

È possibile verificare la connettività del client end-to-end di Outlook effettuando una delle seguenti operazioni:

  - Eseguendo il cmdlet **Test-OutlookConnectivity**. Il cmdlet verifica la connettività di Outlook via Internet (RPC su HTTP). Se la verifica del cmdlet restituisce un errore, l'output segnalerà il passaggio come non riuscito. Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Test-OutlookConnectivity](https://technet.microsoft.com/it-it/library/dd638082\(v=exchg.150\)).

  - Eseguendo la verifica della connettività di Outlook via Internet utilizzando l'Analizzatore connettività remota (ExRCA) di Exchange. Quando si esegue la verifica, verrà restituito un riepilogo dettagliato che mostra il punto in cui la verifica ha restituito l'errore e le procedure per correggerlo. Per altre informazioni, vedere [Analizzatore connettività remota di Exchange](exchange-remote-connectivity-analyzer-exchange-2013-help.md).

Entrambi i test provano ad accedere mediante Outlook via Internet dopo aver ottenuto le impostazioni del server dal servizio di individuazione automatica. La verifica end-to-end comprende quanto segue:

  - Verifica della connettività del servizio di individuazione automatica

  - Convalida del DNS

  - Convalida dei certificati (se il nome del certificato corrisponde al sito Web, se il certificato è scaduto e se è attendibile)

  - Verifica della corretta configurazione del firewall (ExRCA controlla la configurazione generale del firewall. Il cmdlet verifica la configurazione del firewall Windows).

  - Conferma della connettività client mediante accesso alla cassetta postale dell'utente

