---
title: 'Server Cassette postali: Exchange 2013 Help'
TOCTitle: Server Cassette postali
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 50480101
ms.date: 01/13/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Server Cassette postali

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-02-19_

In Microsoft Exchange Server 2010, il ruolo Cassette postali ospitava i database delle cassette postali e delle cartelle pubbliche e fungeva anche da archivio per i messaggi di posta elettronica. Ora, in Exchange Server 2013, il ruolo Cassette postali include anche i protocolli Accesso client e i componenti del servizio di trasporto, dei database delle cassette postali e della messaggistica unificata.

In Exchange 2013, il ruolo Cassette postali interagisce direttamente con Active Directory, il server Accesso client e i client Microsoft Outlook nel seguente processo:

  - Il server Cassette postali utilizza LDAP per accedere alle informazioni di configurazione dei destinatari, dei server e delle organizzazioni ricavate da Active Directory.

  - Il server Accesso client invia le richieste dai client al server Cassette postali e restituisce i dati dal server Cassette postali ai client. Il server Accesso client consente inoltre l'accesso ai file della Rubrica online nel server Cassette postali mediante la condivisione file NetBIOS. Il server Accesso client invia i messaggi, i dati sulla disponibilità, le impostazioni dei profili client e i dati della Rubrica online tra il client e il server Cassette postali.

  - I client Outlook all'interno del firewall accedono al server Accesso client per inviare e recuperare i messaggi. I client Outlook esterni al firewall possono accedere al server Accesso client utilizzando Outlook Anywhere (che utilizza il componente proxy RPC su HTTP).

  - Le cassette postali delle cartelle pubbliche sono accessibili tramite RPC su HTTP, indipendentemente dal fatto che il client si trovi all'interno o all'esterno del firewall.

  - Il computer dell'amministratore recupera le informazioni sulla topologia di Active Directory dal servizio di topologia di Active Directory di Microsoft Exchange. Recupera inoltre le informazioni sui criteri dell'indirizzo di posta elettronica e le informazioni sull'elenco indirizzi.

  - Il server Accesso client utilizza LDAP o l'interfaccia NSPI (Name Service Provider Interface) per contattare il server Active Directory e recuperare le informazioni di Active Directory sugli utenti.

**Architettura e interazione tra i server Accesso client e Cassette postali**

![Interazione tra server Accesso client e Cassette postali](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "Interazione tra server Accesso client e Cassette postali")

Per ulteriori dettagli, vedere la sezione “Architettura di Exchange 2013” in [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

## Nuove funzionalità del server Cassette postali

Di seguito sono elencate e descritte brevemente alcune funzionalità nuove o migliorate nel ruolo Cassette postali di Exchange 2013:

  - Evoluzione del gruppo di disponibilità del database di Exchange 2010:
    
      - Il codice del registro delle transazioni è stato sottoposto a refactoring per un failover più veloce con il punto di arresto in profondità sulle copie passive del database.
    
      - Per supportare la resilienza del sito avanzata, i server possono essere in luoghi diversi.

  - Exchange 2013 ora ospita alcuni componenti di Accesso client, i componenti di Trasporto e di Messaggistica unificata.

  - L'archivio di Exchange è stato riscritto in codice gestito per migliorare le prestazioni grazie a una maggiore affidabilità e una riduzione delle operazioni I/O.

  - Ciacun database di Exchange 2013 viene ora eseguito separatamente.

  - La funzionalità di ricerca avanzata ha sostituito l'infrastruttura di ricerca in più cassette postali di Exchange 2010.

## Sicurezza dei server Cassette postali

Per impostazione predefinita, le comunicazioni HTTP, Microsoft Exchange ActiveSync, POP3 e IMAP4 tra i server Cassette postali e altri ruoli server di Exchange, controller di dominio e server del catalogo globale vengono crittografate. Assicurarsi inoltre che i server Cassette postali non siano accessibili da Internet.

## Ulteriori informazioni

[\[ONP\] di messaggistica unificata](unified-messaging-exchange-2013-help.md)

[Flusso di posta](mail-flow-exchange-2013-help.md)

[Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md)

[Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md)

[Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Gestire il database delle cassette postali in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md)

[Destinatari](recipients-exchange-2013-help.md)

[Collaborazione](collaboration-exchange-2013-help.md)

