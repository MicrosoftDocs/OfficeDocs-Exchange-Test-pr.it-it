---
title: 'Test e risoluzione dei problemi con il cmdlet Test-UMConnectivity: Exchange 2013 Help'
TOCTitle: Test e risoluzione dei problemi con il cmdlet Test-UMConnectivity
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56269828
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Test e risoluzione dei problemi con il cmdlet Test-UMConnectivity

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-06-25_

Dopo avere installato i server Cassette postali e Accesso client e configurato la messaggistica unificata, è possibile utilizzare diversi test diagnostici e un'applicazione telefonica basata su software per testare la connettività telefonica e il funzionamento dei servizi di messaggistica unificata.

## Test-UMConnectivity

Il cmdlet **Test-UMConnectivity** consente di verificare la connettività dei server Cassette postali e Accesso client in diversi modi, a seconda dei parametri utilizzati. Per la verifica della funzionalità Messaggistica unificata sono disponibili tre test:

  - **Locale**   Il cmdlet **Test-UMConnectivity** verifica la comunicazione VoIP (Voice over IP) con i server Cassette postali in esecuzione sullo stesso computer locale.

  - **Locale con accesso all'interfaccia telefonica**   Il cmdlet **Test-UMConnectivity** tenta di stabilire la comunicazione VoIP con il server Cassette postali in esecuzione sullo stesso computer. Se la connessione ha esito positivo, il cmdlet tenta di accedere a una o più cassette postali abilitate alla messaggistica unificata inviando il numero di interno e il PIN della cassetta postale. Se viene specificato il parametro *–TUILogon*, è necessario specificare anche i valori dei seguenti parametri con le informazioni corrette per la cassetta postale di prova:
    
      - *–Phone*   Questo parametro deve contenere il numero di interno della cassetta postale di prova.
    
      - *–PIN*   Questo parametro deve contenere il PIN della cassetta postale abilitata alla messaggistica unificata.
    
      - *–UMDialPlan   *Questo parametro deve contenere il dial plan associato alla cassetta postale di prova.

  - **Remoto**   Il cmdlet **Test-UMConnectivity** tenta di connettersi a un server Accesso client remoto effettuando una chiamata mediante un gateway VoIP. Una volta stabilita la connessione, eseguirà controlli della connettività sul server Accesso client remoto e sui percorsi dei supporti.
    

    > [!NOTE]
    > Se si riceve il seguente messaggio, è necessario riavviare il servizio di messaggistica unificata di MicrosoftExchange perché evidentemente è stato arrestato o non risponde: "L'attività Test-UMConnectivity ha rilevato un errore durante il tentativo di eseguire una chiamata. Dettagli: Impossibile stabilire una connessione".


