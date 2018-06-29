---
title: 'Pianificazione del server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Pianificazione del server Trasporto Edge
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61543916
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pianificazione del server Trasporto Edge

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Il ruolo server Trasporto Edge Transport è stato reintrodotto in Exchange Service Pack 1. Trasporto Edge fornisce protezione da posta indesiderata migliorata per l'organizzazione Exchange. Il server Trasporto Edge, inoltre, applica criteri ai messaggi in transito tra le organizzazioni. Questo ruolo del server viene distribuito nella rete perimetrale e all'esterno della foresta di Active Directory. I server Trasporto Edge non dispongono dell'accesso diretto a Active Directory per informazioni sulla configurazione e sui destinatari come invece accade per i server Accesso client o Cassette postali. Il server Trasporto Edge usa Active Directory Lightweight Directory Service (AD LDS) per archiviare localmente le informazioni relativi alla configurazione e ai destinatari.

È possibile aggiungere una server Trasporto Edge a un'organizzazione Exchange 2013 esistente. L'installazione del server Trasporto Edge non richiede alcuna procedura di preparazione aggiuntiva per Active Directory.


> [!NOTE]
> Se si sta aggiungendo Trasporto Edge a un' esistente Exchange&nbsp;2010 o Exchange&nbsp;2007 organizzazione, è necessario installare aggiornamenti cumulativi specifici nei server legacy prima di installare Exchange 2013 Trasporto Edge. Per ulteriori informazioni, vedere <A href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</A>.



Quando si pianifica la distribuzione dei server Trasporto Edge, è necessario considerare le seguenti questioni:

  - **Capacità del server**   La pianificazione della capacità del server include la pianificazione del monitoraggio delle prestazioni del server Trasporto Edge. Il monitoraggio delle prestazioni consentirà di comprendere la portata dell'attività del server. Queste informazioni determineranno la capacità della configurazione hardware corrente.

  - **Funzionalità di trasporto**   Il server Trasporto Edge è in grado di fornire la protezione dalla posta indesiderata fino ai limiti della rete. Nell'ambito del processo di pianificazione, è necessario determinare le funzionalità di protezione dalla posta indesiderata da abilitare nel server Trasporto Edge e le relative modalità di configurazione.

  - **Sicurezza**   Il ruolo del server Trasporto Edge è progettato per ridurre al minimo la superficie di attacco. Pertanto, è importante proteggere e gestire in modo corretto sia l'accesso fisico che l'accesso di rete al server. La pianificazione della protezione consentirà di assicurarsi che le connessioni IP siano abilitate solo da server e da utenti autorizzati. Per ulteriori informazioni, vedere [Checklist della distribuzione di protezione](deployment-security-checklist-exchange-2013-help.md).
    
    La procedura consigliata consiste nell'inserire il server Trasporto Edge in una rete perimetrale. Per assicurarsi che il server sia in grado di inviare e ricevere messaggi di posta elettronica e di ricevere gli aggiornamenti dei dati di configurazione dal servizio Microsoft Exchange EdgeSync, è necessario consentire la comunicazione tramite le porte elencate nella seguente tabella.
    
    ### Impostazioni delle porte di comunicazione per i server Trasporto Edge
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Interfaccia di rete</th>
    <th>Porta aperta</th>
    <th>Protocollo</th>
    <th>Nota</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>In ingresso e in uscita da e verso Internet</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Questa porta è necessaria per il flusso di posta da e verso Internet.</p></td>
    </tr>
    <tr class="even">
    <td><p>In ingresso e in uscita verso la rete interna</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Questa porta è necessaria per il flusso di posta da e verso l'organizzazione Exchange.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Solo locale</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>Questa porta viene utilizzata per effettuare una connessione locale verso AD LDS.</p></td>
    </tr>
    <tr class="even">
    <td><p>In ingresso dalla rete interna</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>LDAP protetto</p></td>
    <td><p>Questa porta è necessaria per la sincronizzazione EdgeSync.</p></td>
    </tr>
    <tr class="odd">
    <td><p>In ingresso dalla rete interna</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>L'apertura della porta è facoltativa. Offre maggiore flessibilità nella gestione dei server Trasporto Edge dalla rete interna consentendo l'utilizzo di una connessione Desktop remoto per la gestione del server Trasporto Edge.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > Il ruolo del server Trasporto Edge utilizza porte LDAP non standard. Le porte specificate in questo argomento sono le porte di comunicazione LDAP configurate quando è installato il ruolo del server Trasporto Edge.



  - **EdgeSync**   Il processo di distribuzione consigliato consiste nella creazione di una sottoscrizione Edge per sottoscrivere il server Trasporto Edge nell'organizzazione di Exchange. Quando si crea una sottoscrizione Edge, i dati relativi alla configurazione e ai destinatari vengono replicati da Active Directory ad AD LDS. Il server Trasporto Edge viene sottoscritto in un sito di Active Directory. Il servizio EdgeSync di MicrosoftExchange in esecuzione sui server Cassette postali in quel sito aggiorna periodicamente AD LDS sincronizzando i dati da Active Directory. Il processo di sottoscrizione Edge predisporrà automaticamente i connettori di invio necessari per abilitare il flusso di posta dall'organizzazione di Exchange a Internet tramite un server Trasporto Edge. Se si utilizzano le funzionalità di ricerca dei destinatari o di aggregazione degli elenchi indirizzi attendibili nel server Trasporto Edge, è necessario sottoscrivere il server Trasporto Edge nell'organizzazione.

## Configurazione delle impostazioni DNS per il ruolo del server Trasporto Edge

Il server Trasporto Edge viene distribuito come server autonomo nella rete perimetrale o come membro del dominio di Active Directory della rete perimetrale all'esterno dell'organizzazione di Exchange. È necessario configurare manualmente il suffisso DNS corretto per il ruolo del server Trasporto Edge prima di installare Exchange 2013. Se non viene configurato un suffisso DNS, non è possibile completare l'installazione.

Poiché il server Trasporto Edge viene distribuito nella rete perimetrale, dispone di interfacce di rete collegate a più segmenti di rete, ciascuno dei quali presenta una configurazione IP univoca. È necessario configurare l'interfaccia di rete collegata al segmento di rete esterno, o pubblico, per l'utilizzo di un server DNS pubblico per la risoluzione dei nomi. In tal modo si consente al server di risolvere i nomi di dominio SMPT per i record di risorsa MX e di instradare la posta a Internet.

È necessario configurare l'interfaccia di rete collegata al segmento di rete interno, o privato, per l'utilizzo di un server DNS in grado di risolvere i nomi dei server Cassette postali nell'organizzazione, o predisporre la disponibilità di un file Hosts per tale interfaccia di rete. I server Trasporto Edge e i server Cassette postali devono supportare la risoluzione host DNS per potersi riconoscere.

Per abilitare la risoluzione dei nomi dei server Cassette postali dai server Trasporto Edge, adottare uno dei seguenti metodi:

  - Creare manualmente i record delle risorse per i server Cassette postali in una zona di ricerca diretta sul server DNS configurato nella scheda di rete interna del server Trasporto Edge.

  - Modificare il file Hosts sul server Trasporto Edge per includere i record host dei server Cassette postali. Il file Hosts è un file di testo locale nello stesso formato del file 4.3 Berkeley Software Distribution (BSD) UNIX /etc/hosts. Il file associa nomi host a indirizzi IP ed è archiviato nella cartella \\%Systemroot%\\System32\\Drivers\\Etc.

Per abilitare la risoluzione dei nomi dei server Cassette postali dai server Trasporto Edge, adottare uno dei seguenti metodi:

  - Creare manualmente i record delle risorse per i server Trasporto Edge in una zona di ricerca diretta nel server DNS configurato sul server Cassette postali.

  - Per includere i record host per i server Trasporto Edge, modificare il file Hosts nei server Cassette postali ubicati nel sito Active Directory registrato.

Seguire questa procedura per configurare le impostazioni DNS per il server Trasporto Edge:

1.  Verificare che le impostazioni del server DNS per ciascuna interfaccia di rete siano corrette per il segmento di rete.

2.  Configurare il suffisso DNS per il nome del server Trasporto Edge utilizzando la seguente procedura:
    
    1.  Aprire il Pannello di controllo e quindi selezionare **Proprietà sistema**.
    
    2.  Scegliere la scheda **Nome computer**.
    
    3.  Scegliere **Cambia**.
    
    4.  Nella pagina **Cambiamenti nome computer**, fare clic su **Altro**.
    
    5.  Nel campo **Suffisso DNS primario del computer**, immettere un nome di dominio DNS e un suffisso per il server Trasporto Edge.
    
    Non è possibile modificare questo nome una volta installato il ruolo del server Trasporto Edge.

## Sostituzione delle impostazioni DNS

Potrebbe essere necessario sostituire le impostazioni DNS predefinite sul server Exchange in modo che la posta possa essere instradata e recapitata correttamente. A tale scopo, modificare le impostazioni **Ricerche DNS interne** e **Ricerche DNS esterne** delle proprietà del server di trasporto. Queste impostazioni sostituiscono quelle presenti nella scheda di rete per l'instradamento de messaggi di posta elettronica.

