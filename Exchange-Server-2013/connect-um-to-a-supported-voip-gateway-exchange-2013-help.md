---
title: 'Connettersi alla messaggistica unificata a un gateway VoIP supportato: Exchange 2013 Help'
TOCTitle: Connettersi alla messaggistica unificata a un gateway VoIP supportato
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50555672
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettersi alla messaggistica unificata a un gateway VoIP supportato

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-19_

Quando si installa la messaggistica unificata, è necessario configurare in rete i gateway VoIP (Voice over IP), gli IP PBX, i PBX abilitati a SIP o gli SBC (session border controller) per la comunicazione con i server Accesso client su cui è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali su cui è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange nell'organizzazione Exchange. È inoltre necessario configurare i server Accesso client e Cassette postali per la comunicazione con i gateway VoIP, IB PBX, PBX abilitati a SIP o SBC.


> [!NOTE]
> Dopo aver connesso i server Accesso client e Cassette postali ai gateway VoIP, IP PBX, PBX abilitati a SIP o SBC nella rete dei dati, è necessario creare i componenti di messaggistica unificata richiesti e abilitare gli utenti alla messaggistica unificata in modo che possano utilizzare il sistema di caselle vocali.



## Procedura

Di seguito vengono riportati i passaggi di base per la connessione dei gateway VoIP, IP PBX, PBX abilitati a SIP o SBC ai server Accesso client e Cassette postali:

Passaggio 1: Installare i server Accesso client e Cassette postali dell'organizzazione.

Passaggio 2: Creare e configurare un numero di interno telefonico, un URI SIP o un dial plan di messaggistica unificata E.164.

Passaggio 3: Creare e configurare un gateway IP di messaggistica unificata. È necessario creare e configurare un gateway IP di messaggistica unificata per ciascun gateway VoIP, IP PBX, PBX abilitato a SIP o SBC che accetterà le chiamate in arrivo e invierà le chiamate in uscita.

Passaggio 4: Creare un nuovo gruppo di risposta di messaggistica unificata, se necessario. Se si crea un gateway IP di messaggistica unificata e non si specifica un dial plan di messaggistica unificata, viene creato automaticamente un gruppo di risposta di messaggistica unificata.

Per informazioni su ogni passo, vedere le sezioni seguenti.

## Passaggio 1: Installare i server Accesso client e Cassette postali

Quando si distribuiscono i server Exchange nell'organizzazione, è possibile installare i server Accesso client e Cassette postali nello stesso computer oppure installare il server Accesso client in un computer separato dal server Cassette postali. Per installare il server Accesso client, eseguire Setup.exe. dal supporto di installazione. Il comando utilizzato è lo stesso a prescindere che il server Accesso client venga installato in un computer separato dal server Cassette postali o nello stesso computer. Per ulteriori informazioni, vedere [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Per aggiungere funzioni e funzionalità al server Exchange esistente, è possibile utilizzare **Programmi e funzionalità** o Setup.exe.

## Passaggio 2: Creare e configurare un dial plan di messaggistica unificata

Dopo aver installato i server necessari, occorre innanzitutto creare un dial plan di messaggistica unificata. Un dial plan di messaggistica unificata contiene le impostazioni di configurazione che consentono di connettere la rete di telefonia tramite collegamento a uno o più gateway IP di messaggistica unificata. Un gateway IP di messaggistica unificata e un gruppo di risposta di messaggistica unificata sono collegati direttamente a un dial plan di messaggistica unificata, oltre a essere obbligatori. Per ulteriori informazioni, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

Un dial plan di messaggistica unificata stabilisce un collegamento dal numero di interno del telefono di un utente alla rispettiva cassetta postale abilitata per la messaggistica unificata. Quando si crea un dial plan di messaggistica unificata, è possibile configurare il numero di cifre nei numeri di interni, il tipo di URI e le impostazioni di protezione VoIP per il dial plan.

Sono disponibili tre tipi di dial plan: numero di interno telefonico, URI SIP ed E.164. Quando si crea e configura un dial plan di messaggistica unificata, è necessario determinare il tipo di informazioni inviate da IP PBX, PBX abilitato a SIP o PBX e se le chiamate vengono inviate a un server Accesso client o Cassette postali in un numero di interno o nel formato E.164. Se si sta distribuendo Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, è necessario creare e configurare un dial plan URI SIP.

## Passaggio 3: Creazione e configurazione di un gateway IP di messaggistica unificata

Dopo aver creato un dial plan di messaggistica unificata, è necessario creare un gateway IP di messaggistica unificata che rappresenti un gateway VoIP, un IP PBX o un SBC nella rete. Quando si crea un gateway IP di messaggistica unificata, è possibile configurarlo per l'uso di un indirizzo IP o di un nome di dominio completo. Se si utilizza un FQDN è necessario assicurarsi di aver configurato correttamente un record host DNS per il gateway IP, in modo che il nome host venga risolto in un indirizzo IP.

In seguito all'installazione di un gateway VoIP, IP PBX o SBC, è necessario creare un gateway IP di messaggistica unificata che rappresenti il dispositivo hardware fisico. Dopo aver creato il gateway IP di messaggistica unificata, i server Accesso client che lo utilizzano invieranno una richiesta SIP OPTIONS al gateway VoIP, all'IP PBX o all'SBC per verificare che sia attivo. Se il gateway VoIP, l'IP PBX, il PBX abilitato a SIP o l'SBC non risponde alla richiesta, il server Accesso client registrerà un evento con ID 1088 che segnala che la richiesta ha avuto esito negativo. Per risolvere il problema, assicurarsi che il gateway VoIP, l'IP PBX o l'SBC sia disponibile e online e che la configurazione di messaggistica unificata sia corretta.

I server Accesso client e Cassette postali comunicheranno solo con un gateway VoIP, un IP PBX o un SBC elencato come peer SIP attendibile. In alcuni casi, se due gateway VoIP, IP-PBX o SBC sono configurati per l'utilizzo dello stesso indirizzo IP, verrà registrato un evento con ID 1175. Questa eventualità può verificarsi se le zone DNS sono state configurate con nomi di dominio completo (FQDN) per i gateway VoIP in rete. La messaggistica unificata protegge da richieste non autorizzate recuperando l'URL interno della directory virtuale dei servizi Web di messaggistica unificata sul server Cassette postali e utilizza questo URL per compilare l'elenco dei nomi di dominio completi relativo ai peer SIP attendibili. Se due nomi FQDN vengono risolti nello stesso indirizzo IP, viene registrato l'evento descritto in precedenza.

Se un gateway IP di messaggistica unificata viene configurato per utilizzare un nome di dominio completo (FQDN) e se il record DNS del gateway IP di messaggistica unificata viene modificato dopo l'avvio del servizio, è necessario riavviare il servizio Messaggistica unificata di MicrosoftExchange. Se non si riavvia il servizio, il server Cassette postali non sarà in grado di individuare il gateway IP di messaggistica unificata. Ciò avviene perché un server Cassette postali conserva una cache per tutti i gateway IP di messaggistica unificata in memoria e la risoluzione DNS viene eseguita solo quando si riavvia il servizio o quando è stata modificata la configurazione di un gateway VoIP, un IP PBX o SBC.

La messaggistica unificata di Exchange supporta vari fornitori di gateway VoIP e altri fornitori di IP PBX, PBX abilitati a SIP e SBC. Ciascuno di questi gateway VoIP supportati è stato progettato per il collegamento con numerosi sistemi PBX di terze parti.

Per informazioni dettagliate sui gateway VoIP, vedere i seguenti argomenti:

  - [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md)

  - [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

Per ulteriori informazioni, vedere [Connettere il sistema di segreteria telefonica alla rete telefonica](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md).

## Passaggio 4: Creare un nuovo gruppo di risposta di messaggistica unificata, se necessario

L'espressione gruppo di risposta viene utilizzata per descrivere un gruppo di numeri di interni PBX o IP PBX condivisi dagli utenti. I gruppi di risposta vengono utilizzati per distribuire efficacemente le chiamate in entrata o in uscita nell'ambito di una specifica unità aziendale. La creazione e la definizione di un gruppo di risposta riducono al minimo le possibilità che l'utente di una chiamata in arrivo riceva il segnale di occupato quando la chiamata viene ricevuta.

I gruppi di risposta di messaggistica unificata eseguono il mirroring dei gruppi di risposta utilizzati nei sistemi PBX e IP PBX. Quando si configurano i sistemi PBX e IP PBX, è necessario creare e configurare uno o più gruppi di risposta di messaggistica unificata. che possono essere utilizzati come collegamento tra il gateway IP e il dial plan di messaggistica unificata.

A seconda della modalità di creazione del gateway IP di messaggistica unificata, può essere necessario creare uno o più gruppi di risposta di messaggistica unificata nuovi. Se non si collega un gateway IP di messaggistica unificata a un dial plan al momento della creazione del gateway IP di messaggistica unificata, per impostazione predefinita, viene creato un singolo gruppo di risposta di messaggistica unificata. Se si collega un gateway IP di messaggistica unificata a un dial plan di messaggistica unificata quando si crea il gateway IP di messaggistica unificata, tutte le chiamate in arrivo verranno inviate tramite gateway IP di messaggistica unificata e verranno accettate dai server Accesso client e Cassette postali. Se non si collega un gateway IP di messaggistica unificata a un dial plan di messaggistica unificata quando si crea un gateway IP di messaggistica unificata, sarà necessario creare un gruppo di risposta di messaggistica unificata con l'identificatore pilota corretto affinché le chiamate in arrivo vengano inoltrate da un gateway IP di messaggistica unificata a un dial plan.

Se si dispone di più numeri di operatore automatico e Outlook Voice Access e un gateway IP di messaggistica unificata è stato collegato a un dial plan, sarà necessario eliminare il gruppo di risposta di messaggistica unificata creato per impostazione predefinita e creare più gruppi di risposta di messaggistica unificata. Per informazioni dettagliate sulla creazione di un gruppo di risposta di messaggistica unificata, vedere [Creazione di un gruppo di risposta di messaggistica unificata](create-a-um-hunt-group-exchange-2013-help.md).

