---
title: 'Distribuzione messaggistica unificata Exchange 2013: Exchange 2013 Help'
TOCTitle: Distribuzione della messaggistica unificata di Exchange 2013
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 50481749
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione della messaggistica unificata di Exchange 2013

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

La messaggistica unificata richiede l'integrazione della distribuzione di Exchange Server nel sistema di telefonia esistente dell'organizzazione. Una distribuzione corretta richiede un'attenta analisi dell'infrastruttura telefonica esistente e l'esecuzione della procedura di pianificazione corretta per distribuire e gestire la posta vocale in Messaggistica unificata.

**Sommario**

Before you deploy

Deploying Unified Messaging

Post-deployment tasks for Unified Messaging

## Prima della distribuzione

Prima di distribuire la messaggistica unificata, si consiglia di acquisire familiarità con i concetti dei seguenti argomenti:

  - [Dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-dial-plans)

  - [Gateway IP di messaggistica unificata](um-ip-gateways-exchange-2013-help.md)

  - [Servizi di messaggistica unificata](um-services-exchange-2013-help.md)

  - [Gruppi di risposta di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups)

  - [Rispondere automaticamente e il routing delle chiamate in arrivo](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)

  - [Criteri cassetta postale di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies)

  - [Segreteria telefonica per gli utenti](voice-mail-for-users-exchange-2013-help.md)

## Distribuzione della messaggistica unificata

Indipendentemente dalla modalità di distribuzione della messaggistica unificata, ovvero tramite IP PBX, gateway VoIP o Microsoft Lync Server, tutte le opzioni di distribuzione hanno diversi passaggi in comune. Questi passi sono necessari per creare un sistema scalabile e ad elevata disponibilità che supporti un gran numero di utenti di messaggistica unificata. Questi passaggi sono i seguenti:

1.  Distribuire e configurare i componenti di telefonia per la messaggistica unificata.

2.  Verificare l'installazione corretta del server Accesso client su cui è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e il server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange.

3.  Creare e configurare i componenti necessari per la messaggistica unificata.

4.  Eseguire le attività successive alla distribuzione per la messaggistica unificata.

## Distribuzione e configurazione dei componenti di telefonia

Per distribuire correttamente la messaggistica unificata in un'organizzazione Exchange, l'amministratore di Exchange deve avere familiarità con i concetti relativi alle reti di dati e con la terminologia relativa alla telefonia nonché essere in grado di configurare correttamente i componenti di telefonia necessari per la messaggistica unificata. Per eseguire una nuova distribuzione o l'aggiornamento di un sistema di caselle vocali legacy, è necessario conoscere in maniera approfondita le reti di telefonia e la messaggistica unificata.

In genere, per configurare correttamente i componenti di telefonia richiesti dalla messaggistica unificata è necessario completare tre attività:

1.  **Provisioning delle linee PBX**   Il primo passo per la distribuzione di una soluzione scalabile di messaggistica unificata è il provisioning delle linee PBX.

2.  **Organizzazione dei canali**   Una volta eseguito il provisioning dei canali vocali basati su PBX, è possibile organizzare i canali in gruppi di risposta.

3.  **Distribuzione dei gateway VoIP**   Dopo aver organizzato i canali vocali come gruppi di risposta, è necessario terminare i canali nei gateway VoIP. I gateway VoIP vengono utilizzati con un sistema PBX legacy per convertire i protocolli a commutazione di circuito che si trovano in una rete di telefonia in protocolli a commutazione di pacchetto basati su IP.

Quando si integrano le reti di telefonia e dei dati dell'organizzazione durante la distribuzione della messaggistica unificata, è necessario configurare correttamente i componenti delle reti di telefonia e dei dati. È necessario, inoltre, configurare i seguenti componenti o interfacce per distribuire correttamente la messaggistica unificata:

  - **Configurare la connessione dai sistemi PBX dell'organizzazione per comunicare con i gateway VoIP.**   Per i dettagli, vedere [Connettere un gateway VoIP per comunicare con un PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configurare la connessione tra l'interfaccia del gateway VoIP e il sistema PBX.**   Per ulteriori informazioni sulla configurazione del sistema PBX per la comunicazione con il gateway VoIP supportato, vedere la documentazione del prodotto specifica del PBX o [Connettere un gateway VoIP per comunicare con un PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configurare la connessione tra l'interfaccia gateway VoIP e i server Accesso client e Cassette postali.**   Per informazioni dettagliate, vedete [Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md).

  - **Configurare la connessione tra i server Accesso client e Cassette postali e l'interfaccia gateway VoIP.**   Per informazioni dettagliate, vedere [Connettersi alla messaggistica unificata a un gateway VoIP supportato](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md).

Inizio pagina

## Installazione dei server Cassette postali e Accesso Client

Sono disponibili diversi percorsi di distribuzione per le organizzazioni che intendono distribuire la messaggistica unificata di Exchange. Sebbene il risultato finale sia sempre lo stesso, vale a dire la corretta distribuzione della messaggistica unificata, i vari percorsi presentano lievi differenze, in quanto ogni cliente ha esigenze e punti di partenza diversi. In genere, comunque, esistono dei punti di partenza e dei percorsi comuni che interessano tutti gli scenari di distribuzione supportati, tra cui nuove installazioni e aggiornamenti. Per distribuire i server Accesso client e Cassette postali, attenersi alle procedure seguenti:

1.  Verificare che l'infrastruttura esistente soddisfi determinati prerequisiti. Per ulteriori informazioni, vedere [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Distribuire la nuova organizzazione di Exchange 2013. Per ulteriori informazioni, vedere [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    

    > [!WARNING]
    > È necessario distribuire un server Cassette postali di Exchange 2013 nell'organizzazione prima di configurare i gateway VoIP e gli IP PBX per inviare il traffico SIP messaggistica unificata e RTP ai server Accesso client di Exchange 2013.



3.  Verificare di aver installato correttamente i server Accesso client e Cassette postali. Dopo aver installato i server, si consiglia di verificare l'installazione e di controllare i registri del programma di installazione dei server. Per ulteriori informazioni, vedere [Verificare un'installazione di Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

## Aggiungere i Language Pack di messaggistica unificata necessari

I Language Pack di messaggistica unificata consentono ai chiamanti e agli utenti di Outlook Voice Access di interagire con il sistema di caselle vocali in più lingue. Dopo avere installato un Language Pack supplementare in un server Cassette postali, i chiamanti e gli utenti di Outlook Voice Access potranno ascoltare i messaggi di posta elettronica e interagire con il sistema di caselle vocali nella lingua specificata.

Alla prima installazione di Exchange, la lingua predefinita, nonché l'unica disponibile per il dial plan, è Inglese (Stati Uniti). Una volta installato un Language Pack di messaggistica unificata su un server Cassette postali, anche la lingua associata al Language Pack verrà elencata come opzione disponibile durante la configurazione della lingua predefinita per il dial plan. Per impostazione predefinita, gli operatori automatici di messaggistica unificata sono associati a un dial plan di messaggistica unificata al momento della creazione e utilizzano quindi l'impostazione della lingua predefinita del dial plan di messaggistica unificata associato. Tuttavia, è possibile modificare questa impostazione dopo avere creato l'operatore automatico di messaggistica unificata.

È possibile aggiungere i language pack di messaggistica UNIFICATA utilizzando il comando Setup.exe oppure eseguendo il programma di installazione .exe *\<UMLanguagePack\>*dopo aver scaricato il language pack di messaggistica UNIFICATA di [Exchange Server 2013 messaggistica UNIFICATA di Language Pack](https://go.microsoft.com/fwlink/p/?linkid=266542). Tuttavia, è necessario utilizzare il comando Setup.exe per rimuovere un language pack di messaggistica UNIFICATA. Non esiste alcun cmdlet Management Shell Exchange che è possibile utilizzare per aggiungere o rimuovere lingue da un server cassette postali. Per ulteriori informazioni su come installare un language pack di messaggistica UNIFICATA, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md).


> [!NOTE]
> Per impostazione predefinita, quando si installa un server Cassette postali, viene installata la lingua inglese americano (en-US). Non è possibile rimuoverle, a meno che non si rimuova il server Cassette postali dal computer.



Inizio pagina

## Creazione e configurazione dei componenti di messaggistica unificata

Diversi componenti di messaggistica unificata sono necessari per la distribuzione e l'utilizzo della messaggistica unificata. I componenti di messaggistica unificata consentono di collegare l'infrastruttura di telefonia all'ambiente di messaggistica unificata. Dopo aver installato correttamente i server Accesso client e Cassette postali, attenersi ai passaggi seguenti.

## Passaggio 1: creare e configurare i dial plan di messaggistica unificata

I dial plan sono una parte importante della messaggistica unificata e sono necessari per la corretta distribuzione della messaggistica unificata sulla rete. Dopo aver installato correttamente i server Accesso client e Cassette postali, un dial plan di messaggistica unificata sarà il primo componente che verrà creato.

Per impostazione predefinita, i dial plan di messaggistica unificata e i server Accesso client e Cassette postali associati al dial plan inviano e ricevono i dati senza utilizzare la crittografia. In modalità non protetta, il traffico VoIP e SIP non verrà crittografato. Quando si crea o dopo aver creato il dial plan, è possibile configurarlo per crittografare il traffico VoIP e SIP utilizzando Mutual Transport Layer Security (Mutual TLS). Se si intende utilizzare TLS, è necessario impostare il dial plan su SIP con protezione o Protetto, impostare la modalità di avvio della messaggistica unificata su TLS o Doppio e creare e distribuire un certificato attendibile sui server Exchange e sui gateway VoIP, i PBX IP o SBC (Session Border Controller). Dopo aver configurato l'impostazione della protezione VoIP, sarà quindi necessario configurare la modalità di avvio per i server Accesso client e Cassette postali. Per i dettagli, vedere [Configurare la modalità di avvio in un server cassette postali](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) o [Configurare la modalità di avvio in un server Accesso Client](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

Eseguire la procedura seguente per creare un nuovo dial plan di messaggistica unificata.

## Creazione di un dial plan di messaggistica unificata

1.  In Interfaccia di amministrazione di Exchange (EAC) accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata**, completare le seguenti caselle:
    
      - **Nome** Digitare il nome del dial plan. Il nome del dial plan di messaggistica unificata è obbligatorio e deve essere univoco. Il nome digitato viene utilizzato solo per la visualizzazione in EAC e Shell. La lunghezza massima per il nome di un dial plan di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
        

        > [!IMPORTANT]
        > Anche se la casella per il nome del dial plan può contenere fino a 64 caratteri, il nome del dial plan non può superare i 49 caratteri. Infatti, quando si crea un dial plan, viene creato anche un criterio cassetta postale di messaggistica unificata predefinito con il nome Criterio predefinito <EM>&lt;NomeDialPlan&gt;</EM>. Il parametro <EM>name</EM> per il dial plan e il criterio cassetta postale di messaggistica unificata può contenere 64 caratteri.

    
      - **Lunghezza numero di interno (cifre)** Immettere il numero di cifre per i numeri di interni nel dial plan. Il numero di cifre dei numeri di interno è basato sul dial plan di telefonia creato su un sistema PBX. Ad esempio, se un utente associato a un dial plan di telefonia compone un numero di interno di quattro cifre per chiamare un altro utente nello stesso dial plan, occorre selezionare 4 come numero di cifre dell'interno.
        
        È una casella obbligatoria il cui intervallo di valori è compreso tra 1 e 20. La lunghezza tipica dell'interno è compresa tra 3 e 7 numeri. Se l'ambiente di telefonia esistente contiene numeri di interni, è necessario specificare un numero di cifre che corrisponda al numero di cifre di quegli interni.
        
        Quando si crea un dial plan per gli interni telefonici, è necessario immettere un numero di interno per l'utente quando è collegato al dial plan dell'interno. Anche con i dial plan SIP o E.164 è necessario un numero di interno quando un utente abilitato alla messaggistica unificata è collegato a un dial plan URI SIP o E.164. Questo numero di interno viene utilizzato dagli utenti di Outlook Voice Access per accedere alla cassetta postale di Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo di UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Sicurezza UI\_VoIP)
    
      - **Codice paese**   Utilizzare questa casella per digitare il numero del codice paese utilizzato per le chiamate in uscita. Questo numero verrà anteposto automaticamente al numero di telefono composto. La casella consente di immettere da 1 a 4 cifre. Ad esempio, negli Stati Uniti il codice paese è 1, nel Regno Unito è 44.

3.  Fare clic su **Salva**.
    

    > [!IMPORTANT]
    > Nelle versioni precedenti di Exchange, era necessario aggiungere il server Messaggistica unificata a un dial plan di messaggistica unificata. In Exchange 2013 i server Accesso client e Cassette postali non possono essere associati a un interno telefonico o a un dial plan E.164. I server Accesso client e Cassette postali risponderanno alle chiamate in arrivo per tutti i tipi di dial plan. Se si sta tuttavia integrando la messaggistica unificata con Microsoft Lync Server, è necessario aggiungere tutti i server Accesso client e Cassette postali a tutti i dial plan URI SIP per consentire il corretto funzionamento del routing delle chiamate con Lync Server.



Inizio pagina

## Passaggio 2: creare e configurare i gateway IP di messaggistica unificata

Un gateway IP di messaggistica unificata rappresenta un dispositivo hardware di gateway VoIP o IP PBX. La combinazione di gateway IP di messaggistica unificata e gruppo di risposta di messaggistica unificata stabilisce un collegamento tra gateway VoIP o IP PBX e un dial plan di messaggistica unificata.

Se è stata creata o abilitata la protezione VoIP per un dial plan, il gateway IP di messaggistica unificata, che verrà creato utilizzando una delle procedure descritte in questa sezione, verrà associato a un dial plan di messaggistica unificata che utilizza la protezione VoIP. In tal caso, per creare il gateway IP di messaggistica unificata, è necessario utilizzare un nome di dominio completo (FQDN) e non un indirizzo IP. È necessario configurare anche il gateway IP di messaggistica unificata per l'ascolto sulla porta TCP 5061. Per effettuare questa operazione, eseguire il seguente comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`. È inoltre necessario verificare che ogni gateway VoIP o IP PBX sia stato configurato per l'ascolto sulla porta 5061 per Mutual TLS.

Utilizzare la procedura seguente per creare un nuovo gateway IP di messaggistica unificata.

## Creare un gateway IP di messaggistica unificata

1.  
    
    In EAC accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo gateway IP di messaggistica unificata** immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per specificare un nome univoco per il gateway IP di messaggistica unificata. Si tratta del nome che verrà visualizzato in EAC. Qualora fosse necessario modificare il nome visualizzato del gateway IP di messaggistica unificata dopo la sua creazione, occorre innanzitutto eliminare il gateway IP di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Benché il nome del gateway IP di messaggistica unificata sia obbligatorio viene utilizzato solo ai fini della visualizzazione. Dal momento che l'organizzazione può utilizzare più gateway IP di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un gateway IP di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Indirizzo**   È possibile configurare un gateway IP di messaggistica unificata con un indirizzo IP o un nome di dominio completo (FQDN). Utilizzare questa casella per specificare l'indirizzo IP configurato nel gateway VoIP, nel PBX abilitato per SIP, nel PBX IP o in SBC, oppure specificare un FQDN. Questa casella accetta solo FQDN validi immessi nel formato corretto.
        
        In questa casella è possibile immettere caratteri alfabetici e numerici. Sono supportati indirizzi IPv4, indirizzi IPv6 e nomi di dominio completi (FQDN). Se si desidera utilizzare TLS tra un gateway IP di messaggistica unificata e un dial plan in funzione in modalità protetta o protetta con SIP, è necessario configurare il gateway IP di messaggistica unificata con un nome di dominio completo. È necessario configurarlo anche per rimanere in ascolto sulla porta 5061 e verificare che un gateway VoIP o un PBX IP sia stato configurato per l'ascolto delle richieste MTLS sulla porta 5061. Per configurare un gateway IP di messaggistica unificata, eseguire questo comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Se si utilizza un FQDN, è inoltre necessario verificare che sia stato correttamente configurato un record host DNS per il gateway VoIP, affinché il nome host venga risolto in un indirizzo IP. Inoltre, se si utilizza un nome di dominio completo anziché un indirizzo IP, e la configurazione DNS per il gateway IP di messaggistica unificata è stata modificata, è necessario disabilitare e quindi abilitare di nuovo il gateway IP di messaggistica unificata per avere la certezza che le informazioni di configurazione del gateway IP di messaggistica unificata vengano aggiornate correttamente
    
      - **Dial plan di messaggistica unificata**   Fare clic su **Sfoglia** per selezionare il dial plan di messaggistica unificata che si desidera associare al gateway IP di messaggistica unificata. Selezionando un dial plan di messaggistica unificata da associare a un gateway IP di messaggistica unificata, viene inoltre creato un gruppo di risposta di messaggistica unificata predefinito associato al dial plan di messaggistica unificata selezionato. Se non si seleziona alcun dial plan di messaggistica unificata, sarà necessario creare manualmente un gruppo di risposta di messaggistica unificata e successivamente associarlo al gateway IP di messaggistica unificata creato.

3.  
    
    Fare clic su **Salva**.

## Passaggio 3: creare e configurare i gruppi di risposta di messaggistica unificata (facoltativo)

*Gruppo di risposta* è un termine utilizzato per descrivere un gruppo di risorse PBX o IP PBX o i numeri di interni condivisi dagli utenti. I gruppi di risposta vengono utilizzati per distribuire efficacemente le chiamate in entrata o in uscita di una determinata unità aziendale.

Se è stato creato un gateway IP di messaggistica unificata associato a un dial plan, viene creato un gruppo di risposta predefinito. È possibile associare un altro gruppo di risposta di messaggistica unificata allo stesso o a un altro gateway IP, a seconda del numero di gateway IP creati.

Quando si crea un gruppo di risposta di messaggistica unificata, si abilitano tutti i server Cassette postali specificati all'interno del dial plan di messaggistica unificata per la comunicazione con un gateway VoIP. Per ulteriori informazioni, vedere [Gruppi di risposta di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups).

## Creazione di un gruppo di risposta di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Gruppi di risposta di messaggistica unificata** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo gruppo di risposta di messaggistica unificata**, completare le caselle seguenti:
    
      - **Gateway IP di messaggistica unificata associato**   In questa casella di sola lettura viene visualizzato il nome del gateway IP che verrà associato al gruppo di risposta di messaggistica unificata.
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per il gruppo di risposta di messaggistica unificata. Il nome di un gruppo di risposta di messaggistica unificata è obbligatorio e deve essere univoco, ma viene utilizzato solo per la visualizzazione in EAC e Shell. Se si desidera modificare il nome visualizzato del gruppo di risposta dopo la creazione, è necessario eliminare il gruppo di risposta esistente e crearne uno con il nome desiderato.
        
        Se l'organizzazione utilizza più gruppi di risposta, si consiglia di utilizzare un nome univoco per ciascun gruppo di risposta. La lunghezza massima per il nome di un gruppo di risposta di messaggistica unificata è di 64 caratteri e può contenere spazi, Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Dial plan**   Fare clic sul pulsante **Sfoglia** per selezionare il dial plan da associare al gruppo di risposta di messaggistica unificata. L'associazione di un gruppo di risposta a un dial plan è obbligatoria. Un gruppo di risposta di messaggistica unificata può essere associato a un solo gateway IP e a un solo dial plan.
    
      - **Identificatore pilota**   Utilizzare questa casella di testo per specificare una stringa che identifichi in modo univoco l'identificatore pilota o l'ID pilota configurato per il sistema PBX o IP PBX.
        
        Questa casella può essere compilata con un numero di interno o con un URI (Uniform Resource Identifier) SIP (Session Initiated Protocol). La casella accetta caratteri alfanumerici. Per PBX legacy, si utilizza un valore numerico come identificatore pilota. Tuttavia, alcuni IP PBX possono utilizzare URI SIP.

4.  Fare clic su **Salva**.

Inizio pagina

## Passaggio 4: creare e configurare un criterio cassetta postale di messaggistica unificata

I criteri cassetta postale di messaggistica unificata sono necessari quando si abilitano utenti per la messaggistica unificata. La cassetta postale di ogni utente abilitato alla messaggistica unificata deve essere collegata a un singolo criterio cassetta postale di messaggistica unificata. Una volta creato un criterio cassetta postale di messaggistica unificata, è possibile associare una o più cassette postali abilitate alla messaggistica unificata al criterio. Questo consente di controllare le impostazioni di sicurezza PIN, quali il numero minimo di cifre in un PIN o il numero massimo di tentativi di accesso non riusciti per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata.

Ogni volta che si crea un dial plan, viene creato anche un criterio cassetta postale di messaggistica unificata. Il criterio cassetta postale di messaggistica unificata sarà chiamato Criteri predefiniti \<*nomeDialPlan*\>. Tuttavia, se si desidera creare un nuovo criterio cassetta postale di messaggistica unificata, attenersi alla seguente procedura.

## Creazione di un criterio cassetta postale di messaggistica unificata

1.  
    
    Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale messaggistica unificata** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo criterio cassetta postale di messaggistica unificata**, nella casella di testo **Nome** immettere il nome del nuovo criterio cassetta postale di messaggistica unificata.
    
    Questa casella consente di specificare un nome univoco per il criterio cassetta postale di messaggistica unificata. Si tratta del nome che verrà visualizzato in EAC. Se si desidera modificare il nome visualizzato del criterio cassetta postale di messaggistica unificata dopo la creazione, è necessario eliminare il criterio esistente e crearne un altro con il nome desiderato. Non è possibile eliminare un criterio cassetta postale di messaggistica unificata se ad esso sono associati utenti abilitati alla messaggistica unificata.
    
    Benché il nome del criterio cassetta postale di messaggistica unificata sia obbligatorio, viene utilizzato solo ai fini della visualizzazione. Dal momento che l'organizzazione può utilizzare più criteri cassette postali di messaggistica unificata, si consiglia di utilizzare un nome univoco per ciascun criterio. La lunghezza massima per il nome di un criterio cassetta postale di messaggistica unificata è di 64 caratteri e può contenere spazi, Non può tuttavia contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Fare clic su **Salva** per salvare il nuovo criterio cassetta postale di messaggistica unificata. Quando viene salvato il criterio cassetta postale di messaggistica unificata, vengono abilitate tutte le impostazioni predefinite inclusi i criteri PIN, le funzionalità della posta vocale e le impostazioni del sistema di caselle vocali protette. Per personalizzare o modificare le impostazioni predefinite, utilizzare il cmdlet **Set-UMMailbox** che consente di modificare le impostazioni del criterio cassetta postale di messaggistica unificata appena creato.

## Passaggio 5: creare e configurare gli operatori automatici di messaggistica unificata (facoltativo)

La messaggistica unificata consente di creare uno o più operatori automatici di messaggistica unificata, in base alle esigenze dell'organizzazione. Quando si crea un operatore automatico di messaggistica unificata, viene creato un sistema dei menu vocali per l'organizzazione. I chiamanti esterni o interni all'organizzazione possono quindi spostarsi nel sistema dei menu per individuare ed effettuare o trasferire le chiamate agli utenti o ai reparti dell'organizzazione.

I chiamanti possono spostarsi all'interno del sistema dei menu utilizzando gli input del segnale multifrequenza (DTMF), noti anche come input a toni, o gli input vocali. Per abilitare il riconoscimento vocale automatico (ASR) in modo che gli utenti possano utilizzare gli input vocali, è necessario abilitare l'operatore automatico di messaggistica unificata al servizio di sintesi vocale.

La creazione e l'utilizzo degli operatori automatici sono operazioni facoltative nella messaggistica unificata. Tuttavia, se si desidera creare un nuovo operatore automatico di messaggistica unificata, attenersi alla seguente procedura.

## Creazione di un operatore automatico di messaggistica unificata

1.  
    
    In EAC accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**, selezionare il dial plan di messaggistica unificata per cui si desidera aggiungere un operatore automatico e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") .

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo operatore automatico di messaggistica unificata** completare le seguenti caselle:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per l'operatore automatico di messaggistica unificata. Il nome di un operatore automatico di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, viene utilizzato solo per la visualizzazione in EAC e Shell.
        
        Qualora fosse necessario modificare il nome visualizzato dell'operatore automatico dopo che è stato creato, eliminare in primo luogo l'operatore automatico di messaggistica unificata esistente, quindi creare un altro operatore automatico con il nome desiderato. Se nell'organizzazione vengono utilizzati più operatori automatici di messaggistica unificata, si consiglia di utilizzare nomi significativi per gli operatori automatici di messaggistica unificata. La lunghezza massima del nome di un operatore automatico di messaggistica unificata è di 64 caratteri e può contenere spazi.
        
        Anche se a un nuovo operatore automatico di messaggistica unificata è possibile assegnare un nome contenente spazi, è necessario evitare l'uso degli spazi se la messaggistica unificata viene integrata con Office Communications Server 2007 R2 o Microsoft Lync Server. Di conseguenza, se è stato creato un operatore automatico con spazi nel nome visualizzato e la messaggistica unificata viene integrata con Office Communications Server 2007 R2 o Lync Server, è necessario innanzitutto eliminare l'operatore automatico e poi crearne un altro il cui nome visualizzato non contenga spazi.
    
      - **Crea l'operatore automatico come abilitato**   Selezionare questa casella di controllo per consentire all'operatore automatico di rispondere alle chiamate in arrivo al termine della creazione dell'operatore automatico di messaggistica unificata. Per impostazione predefinita, un nuovo operatore automatico viene creato come disabilitato.
        
        Se si decide di creare l'operatore automatico di messaggistica unificata come disabilitato, è possibile utilizzare EAC o Shell per abilitare l'operatore automatico una volta che è stato creato.
    
      - **Imposta operatore automatico per rispondere ai comandi vocali**   Selezionare questa casella di controllo per abilitare l'operatore automatico di messaggistica unificata al servizio di sintesi vocale. In questo modo, i chiamanti possono rispondere mediante toni o input vocali ai prompt di sistema o ai prompt personalizzati utilizzati dall'operatore automatico di messaggistica unificata. Per impostazione predefinita, l'operatore automatico non è abilitato al servizio di sintesi vocale quando viene creato.
        
        Affinché i chiamanti utilizzino un operatore automatico abilitato alla sintesi vocale in una lingua diversa dall'inglese americano (en-US), è necessario installare il Language Pack di messaggistica unificata appropriato e configurare le proprietà dell'operatore automatico per utilizzare questa lingua. Il Language Pack di messaggistica unificata per l'inglese americano viene installato per impostazione predefinita quando si installa il server Cassette postali.
    
      - **Numeri di accesso**   Utilizzare questa casella per immettere il numero di interno o i numeri di telefono che i chiamanti utilizzeranno per raggiungere l'operatore automatico. Digitare un numero di telefono o un numero interno nella casella, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere il numero all'elenco. Il numero di cifre per il numero di telefono o il numero interno immesso non deve corrispondere quello di un interno configurato per il dial plan di messaggistica unificata associato. in quanto le chiamate dirette agli operatori automatici di messaggistica unificata sono consentite.
        
        Il numero dei numeri di interni o degli identificatori pilota immessi è illimitato. Tuttavia, è possibile creare il nuovo operatore automatico senza elencare un numero di interno o di telefono. Non è necessario specificare un numero di telefono o un numero interno.
        
        È possibile modificare o rimuovere un numero di interno o un identificatore pilota esistente. Per modificare un numero di telefono o un numero interno esistente, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Per rimuovere dall'elenco un numero di telefono o un numero interno esistente, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

4.  Fare clic su **Salva**.

Inizio pagina

## Attività successive alla distribuzione della messaggistica unificata

Dopo aver completato l'installazione dei server Accesso client e Cassette postali e aver distribuito correttamente la messaggistica unificata, è necessario completare le attività successive alla distribuzione. Le attività successive alla distribuzione consentiranno di abilitare gli utenti alla messaggistica unificata, di proteggere la distribuzione e di abilitare la ricezione fax per gli utenti abilitati alla messaggistica unificata.

## Abilitazione degli utenti alla posta vocale.

Dopo aver distribuito i gateway VoIP o IP PBX, aver installato i server Accesso client e Cassette postali e aver creato i componenti necessari per la messaggistica unificata, è necessario abilitare gli utenti alla messaggistica unificata. Per ulteriori informazioni, vedere [Consentire a un utente per la segreteria telefonica](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

## Sistema di caselle vocali protette

Per proteggere i messaggi vocali per un'organizzazione, è possibile configurare la messaggistica unificata per l'utilizzo di Rights Management Services di Active Directory (AD RMS). Questa funzionalità è nota come Sistema di caselle vocali protette. Quando un messaggio vocale è protetto, non solo al destinatario non è consentito inoltrare il messaggio, ma la messaggistica unificata garantisce che solo i destinatari previsti del messaggio saranno in grado di accedere al contenuto. È possibile accedere al Sistema di caselle vocali protette utilizzando Microsoft Outlook 2010 o versione successiva, Outlook Web App o Outlook Voice Access. Per ulteriori informazioni, vedere [Sistema di caselle vocali protette](protect-voice-mail-exchange-2013-help.md).

## Mutual TLS per la messaggistica unificata

Per utilizzare TLS e crittografare il traffico SIP e RTP (Realtime Transport Protocol) inviato e ricevuto dai server Accesso client e Cassette postali, effettuare le seguenti operazioni:

  - Eseguire la Gestione guidata certificati di Exchange. Per ulteriori informazioni, vedere [Distribuzione dei certificati per la messaggistica unificata](deploying-certificates-for-um-exchange-2013-help.md).

  - Importare il certificato sui server Accesso client e Cassette postali.

  - Importare i certificati richiesti per i gateway VoIP e IP PBX e per i server Accesso client e Cassette postali dell'organizzazione.

  - Configurare la protezione VoIP per i dial plan di messaggistica unificata. Per ulteriori informazioni, vedere [Configurare le impostazioni di protezione VoIP](configure-the-voip-security-setting-exchange-2013-help.md).

  - Configurare la modalità di avvio sul server Accesso client e Cassette postali. Per ulteriori informazioni, vedere [Configurare la modalità di avvio in un server cassette postali](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) e [Configurare la modalità di avvio in un server Accesso Client](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

  - Configurare i gateway IP di messaggistica unificata per l'ascolto sulla porta 5061. Per informazioni dettagliate, vedere [Configurare la porta di attesa](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-listening-port).

## Criteri PIN per gli utenti abilitati alla messaggistica unificata

Nella messaggistica unificata, i criteri del PIN vengono definiti e configurati su un criterio cassetta postale di messaggistica unificata. Quando viene abilitato alla messaggistica unificata, l'utente viene associato a un criterio cassetta postale di messaggistica unificata esistente. I criteri del PIN di messaggistica unificata configurati sul criterio di messaggistica unificata devono essere basati sui requisiti di protezione dell'organizzazione. Per ulteriori informazioni sulla configurazione delle impostazioni PIN per gli utenti abilitati alla messaggistica unificata, vedere [Configurare la protezione di Outlook Voice Access PIN](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-outlook-voice-access-pin-security/set-outlook-voice-access-pin-security).

## Installazione delle funzionalità di posta vocale del client

Una volta distribuiti i server e i componenti di messaggistica unificata richiesti, è possibile configurare diverse funzionalità opzionali correlate alla posta vocale. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Configurazione di Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md)

  - [Consentire agli utenti di posta elettronica di inoltrare le chiamate vocali](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-voice-mail-users-to-forward-calls)

  - [Consentire agli utenti di visualizzare una trascrizione di posta vocale](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)

  - [Consentire agli utenti di posta vocale di ricevere fax](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)


> [!IMPORTANT]
> Se si integra l'ambiente di messaggistica unificata con Microsoft Lync Server, è necessario tenere presenti altre considerazioni di pianificazione. Per ulteriori informazioni, vedere <A href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server</A>.



Inizio pagina

