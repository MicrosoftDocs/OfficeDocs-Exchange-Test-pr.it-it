---
title: 'Configurazione della condivisione federata tra organizzazioni di Exchange: Exchange 2013 Help'
TOCTitle: Configurazione della condivisione federata tra organizzazioni di Exchange
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 50481220
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione della condivisione federata tra organizzazioni di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Con la condivisione federata, gli utenti dell'organizzazione di Exchange locale possono condividere le informazioni sulla disponibilità del calendario con i destinatari in altre organizzazioni di Exchange configurate per la condivisione federata. La condivisione delle informazioni sulla disponibilità può essere abilitata tra due organizzazioni di Exchange 2013 e tra organizzazioni con una distribuzione di Exchange mista. Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

Questo argomento contiene un riepilogo dei requisiti e delle procedure di configurazione necessarie per abilitare la condivisione delle informazioni sulla disponibilità tra due diversi tipi delle seguenti distribuzioni comuni di Exchange:

  - Due organizzazioni di Exchange 2013.

  - Un'organizzazione di Exchange 2013 e un'organizzazione di Exchange 2010 SP2.

  - Un'organizzazione di Exchange 2007 (o un'organizzazione mista con Exchange 2007 ed Exchange 2010 SP2) e un'organizzazione di Exchange 2013.

  - Un'organizzazione di Exchange 2003 (o un'organizzazione mista con Exchange 2003 ed Exchange 2010 SP2) e un'organizzazione di Exchange 2013.

Per informazioni sulle altre attività di gestione relative alla condivisione federata, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 2 ore.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Prima di eseguire le procedure in questo argomento, assicurarsi di aver compreso le limitazioni associate alla condivisione delle informazioni sulla disponibilità nelle organizzazioni di Exchange. Per ulteriori informazioni, vedere [Limitations of free/busy sharing](sharing-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Per saperne di più

## Configurare la condivisione delle informazioni sulla disponibilità tra organizzazioni di Exchange 2013

Completare la procedura in [Configurare la condivisione federata](configure-federated-sharing-exchange-2013-help.md) per entrambe le organizzazioni.

## Configurare la condivisione delle informazioni sulla disponibilità tra organizzazioni di Exchange 2013 ed Exchange 2010 SP2

  - Configurare la condivisione federata per l'organizzazione di Exchange 2013. Completare i passaggi in [Configurare la condivisione federata](configure-federated-sharing-exchange-2013-help.md).

  - Configurare la delega federata (nome precedente per la condivisione federata) per l'organizzazione di Exchange 2010 SP2. Completare la procedura descritta in [Configure federated delega](https://go.microsoft.com/fwlink/p/?linkid=268410).

## Configurare la condivisione delle informazioni sulla disponibilità tra organizzazioni di Exchange 2013 ed Exchange 2007

  - Configurare la condivisione federata per l'organizzazione di Exchange 2013. Completare i passaggi in [Configurare la condivisione federata](configure-federated-sharing-exchange-2013-help.md).

  - Completare i seguenti passaggi nell'organizzazione di Exchange 2007:
    
    1.  **Aggiungere un server di Exchange 2010 SP2**
        
        Installare un server di Exchange 2010 SP2 con il ruolo del server Accesso Client nell'organizzazione di Exchange 2007. Se si dispone di server di Exchange 2010 esistenti, si dovrebbe aggiornati a Exchange 2010 SP2. Per informazioni sull'installazione di Exchange 2010 in un'organizzazione di Exchange 2007, vedere [Exchange 2007 - Roadmap di pianificazione per l'aggiornamento e la coesistenza](https://go.microsoft.com/fwlink/p/?linkid=268411).
    
    2.  **Configurare la delega federata**
        
        Configurare la delega federata per l'organizzazione di Exchange 2007. In un server di Exchange 2010 SP2 nell'organizzazione di Exchange 2007, completare i passaggi descritti in [Configure federated delega](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurare la sincronizzazione con Active Directory**
        
        La sincronizzazione di Active Directory deve essere configurata per tutti gli utenti che devono condividere informazioni sulla disponibilità tra le organizzazioni. La sincronizzazione di Active Directory può essere configurata manualmente o utilizzando un servizio di sincronizzazione automatica di Active Directory. Per configurare la sincronizzazione di Active Directory, vedere la procedura seguente:
        
          - **Prerequisiti**   Verificare che l'organizzazione soddisfi i requisiti per l'installazione del servizio di sincronizzazione di Active Directory.
            
            Per ulteriori informazioni, vedere Preparazione per la sincronizzazione di Active Directory[](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Pianificazione**   Informazioni sullo strumento di sincronizzazione delle directory di Microsoft Online e roadmap di installazione.
            
            Per saperne di più, vedere [Sincronizzazione di Active Directory: roadmap](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Installazione e configurazione**   Configurare la sincronizzazione di Active Directory tra l'organizzazione locale e l'organizzazione tenant del servizio Office 365.
            
            Per ulteriori informazioni, vedere [installare ed eseguire l'aggiornamento dello strumento di sincronizzazione di Directory di Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Creare uno spazio degli indirizzi di disponibilità**
        
        Creare uno spazio degli indirizzi di disponibilità per l'organizzazione di Exchange 2013 remota, che indirizzi le richieste di disponibilità degli utenti delle cassette postali di Exchange 2007 al server Accesso client di Exchange 2010 SP2 nell'organizzazione di Exchange 2007. Questa impostazione consente di abilitare il proxy delle richieste di disponibilità degli utenti di Exchange 2007 per gli utenti dell'organizzazione di Exchange 2013 remota tramite il server Accesso client di Exchange 20120 nell'organizzazione di Exchange 2007. Il server Accesso client di Exchange 20120 nell'organizzazione di Exchange 2007 utilizza la relazione di trust federativa e la relazione dell'organizzazione per inviare le richieste di disponibilità all'endpoint di disponibilità della foresta dell'organizzazione di Exchange 2013 remota.
        
        Per configurare lo spazio degli indirizzi di disponibilità, eseguire il comando seguente in Exchange Management Shell sul server Accesso client di Exchange 2010 nell'organizzazione di Exchange 2007:
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        Per informazioni dettagliate sulla sintassi e sui parametri, vedere Add-AvailabilityAddressSpace[](https://go.microsoft.com/fwlink/p/?linkid=268413)

## Configurare la condivisione delle informazioni sulla disponibilità tra organizzazioni di Exchange 2013 ed Exchange 2003

  - Configurare la condivisione federata per l'organizzazione di Exchange 2013. Completare i passaggi in [Configurare la condivisione federata](configure-federated-sharing-exchange-2013-help.md).

  - Completare i seguenti passaggi nell'organizzazione di Exchange 2003:
    
    1.  **Aggiungere un server di Exchange 2010 SP2**.
        
        Installare un server di Exchange 2010 SP2 con il ruolo del server Accesso Client nell'organizzazione di Exchange 2003. Se si dispone di server di Exchange 2010 esistenti, si dovrebbe aggiornati a Exchange 2010 SP2. Per informazioni sull'installazione di Exchange 2010 in un'organizzazione di Exchange 2003, vedere [Exchange 2003 - Roadmap di pianificazione per l'aggiornamento e la coesistenza](https://go.microsoft.com/fwlink/?linkid=268414).
        

        > [!WARNING]
        > Affinché le informazioni sulla disponibilità funzionino correttamente tra le organizzazioni di Exchange 2013 ed Exchange 2003, nella gerarchia delle cartelle pubbliche deve esistere la cartella pubblica <STRONG>OU=EXTERNAL (FYDIBOHF25SPDLT)</STRONG>. Questa cartella viene creata automaticamente nel server Cassette postali di Exchange 2010 nell'organizzazione di Exchange 2003 solo se si seleziona l'opzione per creare le cartelle pubbliche come parte della configurazione delle impostazioni client per il supporto di Outlook 2003 durante l'installazione di Exchange 2010. Inoltre, questa opzione viene presentata durante il processo di installazione solo se il server Cassette postali di Exchange 20120 è il primo server Cassette postali installato nell'organizzazione. Se la cartella pubblica <STRONG>OU=EXTERNAL (FYDIBOHF25SPDLT)</STRONG> non è stata creata durante l'installazione, sarà necessario crearla manualmente. Per ulteriori informazioni sulla creazione della cartella pubblica, vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2555008">Come risolvere i problemi di disponibilità quando si utilizza la federazione di Exchange in Microsoft Office 365 per l'ambiente aziendale</A>.

    
    2.  **Configurare la delega federata**.
        
        Configurare la delega federata per l'organizzazione di Exchange 2003. In un server di Exchange 2010 SP2 nell'organizzazione di Exchange 2003, completare i passaggi descritti in [Configure federated delega](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurare la sincronizzazione con Active Directory**.
        
        Sincronizzazione di Active Directory deve essere configurata per tutti gli utenti che devono condividere le informazioni sulla disponibilità tra le organizzazioni. È possibile configurare manualmente la sincronizzazione di Active Directory o un servizio di sincronizzazione di Active Directory automatizzato. Per ulteriori informazioni sulla sincronizzazione di Active Directory, vedere [Forefront Identity Management](https://go.microsoft.com/fwlink/?linkid=294645).
        
          - **Prerequisiti**   Verificare che l'organizzazione soddisfi i requisiti per l'installazione del servizio di sincronizzazione di Active Directory.
            
            Per ulteriori informazioni, vedere Preparazione per la sincronizzazione di Active Directory[](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Pianificazione**   Informazioni sullo strumento di sincronizzazione delle directory di Microsoft Online e roadmap di installazione.
            
            Per saperne di più, vedere [Sincronizzazione di Active Directory: roadmap](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Installazione e configurazione**   Configurare la sincronizzazione di Active Directory tra l'organizzazione locale e l'organizzazione tenant del servizio Office 365.
            
            Per ulteriori informazioni, vedere [installare ed eseguire l'aggiornamento dello strumento di sincronizzazione di Directory di Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Configurare le cartelle pubbliche per la condivisione delle informazioni sulla disponibilità nell'organizzazione di Exchange 2003.**
        
        Completare i seguenti passaggi su un server di Exchange 2003:
        
          - In Gestore di sistema di Exchange, nell'albero della console, accedere a **Gruppi amministrativi** \> **Primo gruppo amministrativo** \> **Server**.
        
          - Selezionare il server Exchange 2003 e accedere a **Primo gruppo di archiviazione** \> **Archivio cartella pubblica** \> **Cartelle pubbliche** \> **Schedule+ FREE BUSY**.
        
          - Nel riquadro azioni, selezionare la cartella **OU=EXTERNAL (FYDIBOHF25SPDLT)** per **Primo gruppo di archiviazione**.
        
          - Fare clic con il pulsante destro del mouse sulla cartella **OU=EXTERNAL (FYDIBOHF25SPDLT)**, quindi fare clic su **Proprietà**.
        
          - In **Proprietà - OU=EXTERNAL (FYDIBOHF25SPDLT)**, selezionare la scheda **Replica**.
        
          - Per replicare la cartella **OU=EXTERNAL (FYDIBOHF25SPDLT)** nel server Accesso client/Cassette postali di Exchange 2010, fare clic su **Aggiungi**.
        
          - In **Selezionare un archivio delle cartelle pubbliche** selezionare il database delle cartelle pubbliche per il server Accesso client/Cassette postali di Exchange 2010, quindi fare clic su **OK**.
            

            > [!NOTE]
            > Per impostazione predefinita, Exchange utilizza la pianificazione della replica impostata sul database delle cartelle pubbliche.

        
          - Fare clic su **OK** per chiudere **Proprietà - OU=EXTERNAL (FYDIBOHF25SPDLT)** e salvare le modifiche.
        
          - Completare gli stessi passaggi per la cartella **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)**.
            

            > [!WARNING]
            > A seconda delle dimensioni delle cartelle pubbliche, la replica potrebbe richiedere diverse ore.

        
          - Dopo aver replicato le cartelle pubbliche **OU=EXTERNAL (FYDIBOHF25SPDLT)** e **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** nel server Accesso client/Cassette postali di Exchange 2010, è necessario rimuovere le repliche di queste cartelle pubbliche dal server di Exchange 2003.
    
    5.  **Modificare il parametro LegacyExchangeDN**
        
        Modificare il parametro *LegacyExchangeDN* per tutti gli oggetti abilitati alla posta elettronica nell'organizzazione di Exchange 2003 che fanno riferimento all'organizzazione di Exchange 2013 remota. Impostare su **External (FYDIBOHF25SPDLT)** il valore dell'unità organizzativa esistente per l'oggetto abilitato alla posta elettronica. Ad esempio: **LegacyExchangeDN=/o=First Organization/ou=External (FYDIBOHF25SPDLT)/cn=Recipients/cn=User Name**.
        
        Per modificare gli oggetti abilitati alla posta elettronica nell'organizzazione di Exchange 2003, è possibile utilizzare la [strumento Active Directory Service Interfaces Editor (ADSI Edit)](https://go.microsoft.com/fwlink/?linkid=294644) o [LegacyDN utilità di Microsoft Exchange Server](http://go.microsoft.com/fwlink/?linkid=294643).

