---
title: "Aggregazione dell'elenco indirizzi attendibili: Exchange 2013 Help"
TOCTitle: Aggregazione dell'elenco indirizzi attendibili
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 50481995
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggregazione dell'elenco indirizzi attendibili

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-09-30_

In Exchange Server 2013, il termine *aggregazione dell'elenco indirizzi attendibili* fa riferimento alla funzionalità di protezione dalla posta indesiderata condivisa da Microsoft Outlook ed Exchange. Questa funzionalità consente di raccogliere i dati dagli elenchi Destinatari attendibili per la protezione da posta indesiderata, elenchi Mittenti attendibili, elenchi Mittenti bloccati e dati di contatto configurati dagli utenti di Outlook, rendendo quindi tali dati disponibili per gli agenti di protezione dalla posta indesiderata di Exchange.

Quando si abilita e configura correttamente l'aggregazione degli elenchi indirizzi attendibili, l'agente filtro contenuto trasmette i messaggi di posta elettronica sicuri alla cassetta postale dell'azienda senza ulteriori elaborazioni. I messaggi di posta elettronica che gli utenti di Outlook ricevono dai contatti aggiunti ai propri elenchi Destinatari attendibili o Mittenti attendibili di Outlook o all'elenco dei contatti attendibili, vengono identificati come sicuri dall'agente filtro contenuto. Un *contatto* Outlook è una persona esterna o interna all'organizzazione dell'utente di cui l'utente può memorizzare vari tipi di informazioni, quali l'indirizzo di posta elettronica, l'indirizzo civico, i numeri di telefono e fax oltre agli URL della pagina Web.

In Exchange 2013, il processo di aggregazione degli elenchi indirizzi attendibili consente inoltre all'agente filtro mittente di bloccare i messaggi in arrivo dall'elenco Mittenti bloccati per singolo destinatario.

L'aggregazione dell'elenco indirizzi attendibili consente di ridurre le istanze di falsi positivi durante l'esecuzione in Exchange del filtro di protezione dalla posta indesiderata. Nell'ambito dei filtri di protezione dalla posta indesiderata, un *falso positivo* esiste quando un filtro di protezione dalla posta indesiderata identifica erroneamente come posta indesiderata un messaggio proveniente da un mittente legittimo.

Nelle organizzazioni in cui vengono filtrati ogni giorno centinaia di migliaia di messaggi da Internet, anche una minima percentuale di falsi positivi comporta per gli utenti la mancata ricezione di molti messaggi identificati erroneamente come posta indesiderata che vengono messi in quarantena o eliminati.

L'aggregazione dell'elenco indirizzi attendibili è probabilmente il modo più efficace per ridurre i falsi positivi. In Outlook 2010 o nelle versioni più recenti, gli utenti possono creare *elenchi di mittenti attendibili*. Gli elenchi di mittenti attendibili consentono di specificare un elenco di nomi di dominio e di indirizzi di posta elettronica da cui l'utente di Outlook desidera ricevere messaggi. Per impostazione predefinita, in questo elenco sono inclusi gli indirizzi di posta elettronica presenti in Contatti di Outlook e nell'elenco indirizzi globale di Exchange. Sempre per impostazione predefinita, tutti i contatti esterni ai quali l'utente invia messaggi vengono aggiunti da Outlook all'elenco Mittenti attendibili.

**Sommario**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## Informazioni archiviate nella raccolta degli elenchi indirizzi attendibili degli utenti di Outlook

Una *raccolta degli elenchi indirizzi attendibili* è costituita dai dati combinati provenienti dall'elenco Mittenti attendibili, dall'elenco Destinatari attendibili, dall'elenco Mittenti bloccati e da contatti esterni. Questi dati sono archiviati in Outlook e nella cassetta postale di Exchange.

I seguenti tipi di informazioni sono archiviati in una raccolta degli elenchi indirizzi attendibili di un utente di Outlook:

  - **Mittenti e destinatari sicuri**   L'intestazione Da del messaggio indica un mittente. Il campo A del messaggio di posta elettronica indica il destinatario. Sia i mittenti che i destinatari attendibili sono rappresentati da indirizzi completi SMTP, ad esempio masato@contoso.com. Gli utenti di Outlook possono aggiungere mittenti e destinatari ai relativi elenchi di indirizzi attendibili.

  - **Mittenti bloccati**   Come per i mittenti attendibili, gli utenti possono bloccare i mittenti indesiderati aggiungendoli agli elenchi di mittenti bloccati.

  - **Dominio sicuro**   Il dominio è la parte di un indirizzo SMTP che segue il simbolo @. Ad esempio, contoso.com è il dominio dell'indirizzo masato@contoso.com. Gli utenti di Outlook possono aggiungere domini di mittenti nei relativi elenchi di indirizzi attendibili.
    

    > [!IMPORTANT]
    > Per impostazione predefinita, Exchange non include i domini durante l'aggregazione dell'elenco indirizzi attendibili. Tuttavia, è possibile configurare l'aggregazione dell'elenco indirizzi attendibili affinché includa dati di dominio sicuri per agenti di protezione dalla posta indesiderata. Per ulteriori informazioni, vedere <A href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">Configurare il filtro del contenuto per usare i dati dei dominio attendibili</A>.



  - **Contatti esterni**   Nell'aggregazione dell'elenco indirizzi attendibili possono essere inclusi due tipi di contatti esterni. Il primo tipo comprende i contatti a cui gli utenti di Outlook hanno inviato messaggi di posta elettronica. Questa classe di contatti viene aggiunta all'elenco Mittenti attendibili solo se un utente di Outlook seleziona l'opzione corrispondente dalle impostazioni relative alla posta indesiderata di Outlook 2007.
    
    Il secondo tipo di contati esterni comprende i contatti degli utenti di Outlook. Gli utenti possono aggiungere o importare questi contatti in Outlook. Questa classe di contatti viene aggiunta all'elenco Mittenti attendibili solo se un utente di Outlook seleziona l'opzione corrispondente nelle impostazioni del filtro per la posta indesiderata di Outlook 2010 o Outlook 2007.

Inizio pagina

## Utilizzo della raccolta degli elenchi indirizzi attendibili da parte di Exchange

La raccolta degli elenchi indirizzi attendibili è archiviata sul server di cassette postali dell'utente. Un utente può disporre di un massimo di 1024 voci univoche in una raccolta degli elenchi indirizzi attendibili. Exchange 2013 dispone di un assistente per le cassette postali, chiamato Assistente opzioni di posta indesiderata, che controlla i cambiamenti apportati alla raccolta degli elenchi indirizzi attendibili per le cassette postali dell'utente. L'assistente replica tali modifiche in Active Directory, dove la raccolta degli elenchi indirizzi attendibili è archiviata in ciascun oggetto utente. Quando la raccolta degli elenchi indirizzi attendibili è archiviata nell'oggetto utente in Active Directory, viene aggregata con la funzionalità di protezione dalla posta indesiderata di Exchange 2013 ed è ottimizzata per l'archiviazione e la replica. Exchange utilizza i dati della raccolta degli elenchi indirizzi attendibili durante il filtraggio dei contenuti. Se nella rete perimetrale è presente un server Trasporto Edge sottoscritto, il servizio Microsoft Exchange EdgeSync replica la raccolta degli elenchi indirizzi attendibili nell'istanza Lightweight Directory Services (AD LDS) di Active Directory sul server Trasporto Edge.


> [!IMPORTANT]
> Anche se i dati dei destinatari attendibili vengono archiviati in Outlook e possono essere aggregati alla raccolta degli elenchi indirizzi attendibili, la funzionalità filtro contenuto non agisce sui dati dei destinatari attendibili.



Inizio pagina

## Hashing delle voci della raccolta degli elenchi indirizzi attendibili

Le voci della raccolta degli elenchi indirizzi attendibili vengono sottoposte a hashing (SHA-256) unidirezionale prima di essere archiviate come set di array in tre attributi dell'oggetto utente, **msExchSafeSenderHash**, **msExchSafeRecipientHash** e **msExchBlockedSendersHash**, come oggetto binario di grandi dimensioni. Quando i dati vengono sottoposti a hashing, viene generato un output con lunghezza fissa, molto probabilmente univoco. Per l'hashing delle voci della raccolta degli elenchi indirizzi attendibili, viene generato un hash a 4 byte. Quando un messaggio viene ricevuto da Internet, Exchange sottopone a hashing l'indirizzo del mittente e lo confronta con gli hash archiviati per conto dell'utente di Outlook a cui è stato inviato il messaggio. Se il mittente corrisponde a un hash dei mittenti attendibili, il messaggio supera il filtro contenuto. Se il mittente corrisponde a un hash dei mittenti bloccati, il messaggio viene bloccato.

L'hashing unidirezionale delle voci della raccolta degli elenchi indirizzi attendibili consente di portare a termine le seguenti importanti funzioni:

  - **Ridurre al minimo lo spazio di archiviazione e di replica**   Quasi sempre, l'hashing riduce la dimensione dei dati sottoposti a hashing. Quindi, il salvataggio e la trasmissione di una versione sottoposta a hashing di una voce della raccolta degli elenchi indirizzi attendibili consente di ottimizzare lo spazio di archiviazione e i tempi di replica. Ad esempio, un utente che dispone di 200 voci nella propria raccolta degli elenchi indirizzi attendibili creerà circa 800 byte di dati sottoposti a hashing archiviati e replicati in Active Directory.

  - **Non consentire l'utilizzo delle raccolte degli elenchi indirizzi attendibili agli utenti malintenzionati**   Poiché è impossibile decompilare i valori hash nell'indirizzo o nel dominio SMTP originale, le raccolte degli elenchi indirizzi attendibili non producono indirizzi di posta elettronica utilizzabili dagli utenti malintenzionati che potrebbero compromettere un server Exchange.

Inizio pagina

## Abilitazione dell'aggregazione degli elenchi indirizzi attendibili

L'aggregazione dell'elenco indirizzi attendibili è abilitata per impostazione predefinita in Exchange 2013. A differenza di Exchange Server 2007, non è necessario eseguire manualmente il cmdlet **Update-SafeList** per eseguire l'hashing e scrivere i dati della raccolta degli elenchi indirizzi attendibili in Active Directory. In Exchange 2013, i dati della raccolta elenchi indirizzi attendibili vengono scritti in Active Directory dall'assistente cassette postali Opzioni posta indesiderata.

Per rendere i dati dell'aggregazione dell'elenco indirizzi attendibili in Active Directory disponibili per i server Trasporto Edge della rete perimetrale, è necessario installare e configurare il servizio EdgeSync di Microsoft Exchange in modo che i dati dell'aggregazione dell'elenco indirizzi attendibili siano replicati in AD LDS.

È tuttora possibile eseguire manualmente l'aggregazione dell'elenco indirizzi attendibili utilizzando il cmdlet **UpdateSafelist**. È opportuno tuttavia prestare attenzione al traffico di rete e di replica che potrebbe essere generato durante l'esecuzione del comando. Se il comando **Update-Safelist** viene eseguito su più cassette postali in cui gli elenchi indirizzi attendibili vengono utilizzati in modo intensivo, è possibile che venga generata una quantità significativa di traffico. Se si esegue il comando su più cassette postali, è consigliabile effettuare l'operazione negli orari di scarso traffico e non di ufficio.

Il cmdlet **Update-SafeList** consente di leggere la raccolta degli elenchi indirizzi attendibili dalla cassetta postale dell'utente, di sottoporre a hashing tutte le voci, di ordinarle per agevolare la ricerca e quindi di convertire il valore hash in un attributo binario. Infine, il cmdlet **Update-SafeList** consente di confrontare l'attributo binario creato con qualsiasi valore memorizzato nell'attributo. Se i due valori sono identici, il cmdlet **Update-SafeList** non consente di aggiornare il valore dell'attributo dell'utente con i dati di aggregazione dell'elenco indirizzi attendibili. Se i valori dei due attributi sono diversi, il cmdlet **Update-SafeList** consente di aggiornare il valore dell'aggregazione dell'elenco indirizzi attendibili.

Inizio pagina

