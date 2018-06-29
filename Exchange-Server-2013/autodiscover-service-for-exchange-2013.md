---
title: 'Servizio di individuazione automatica: Exchange 2013 Help'
TOCTitle: Servizio di individuazione automatica
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50555663
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servizio di individuazione automatica

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Informazioni sul servizio Individuazione automatica per Microsoft Exchange 2013. Vengono fornite informazioni sulle funzioni e sul funzionamento del servizio Individuazione automatica di Exchange, nonché sulle opzioni di sviluppo.

MicrosoftExchange 2013 include un servizio denominato servizio di individuazione automatica. In questo argomento viene fornita una panoramica sul servizio e viene illustrato come funziona, come configura i client Outlook, nonché le opzioni disponibili per distribuire il servizio di individuazione automatica nell'ambiente di messaggistica.

Il servizio di individuazione automatica effettua le seguenti operazioni:

  - Configura automaticamente le impostazioni del profilo utente per i client sui quali è in esecuzione MicrosoftOffice Outlook 2007, Outlook 2010 o Outlook 2013, nonché i telefoni cellulari supportati. Sono supportati i telefoni cellulari che eseguono Windows Mobile 6.1 o una versione successiva. Se il telefono cellulare in uso non è un telefono Windows, consultare la documentazione relativa per verificare se è supportato.

  - Fornisce accesso alle funzionalità di Exchange per il client di Outlook 2007, Outlook 2010 o Outlook 2013 connessi all'ambiente di messaggistica di Exchange.

  - Utilizza l'indirizzo di posta elettronica e la password di un utente per fornire impostazioni del profilo ai client di Outlook 2007, Outlook 2010 o Outlook 2013 e ai telefoni cellulari supportati. Se il client di Outlook fa parte di un dominio, viene utilizzato l'account di dominio dell'utente.

**Sommario**

Panoramica sul servizio di individuazione automatica

Come funziona il servizio di individuazione automatica

Opzioni di distribuzione per il servizio di individuazione automatica

Configurazione dell'individuazione automatica per gli spostamenti tra foreste

## Panoramica sul servizio di individuazione automatica

Il servizio di individuazione automatica agevola la configurazione di Outlook 2007, Outlook 2010 o Outlook 2013 e di alcuni cellulari. Non è possibile utilizzare il servizio di individuazione automatica con le versioni di Outlook precedenti a Office Outlook 2007. Nelle versioni precedenti di Microsoft Exchange (Exchange 2003 SP2 o versioni precedenti) e Outlook (Outlook 2003 o versioni precedenti), era necessario configurare manualmente tutti i profili utente per accedere a Exchange. Se l'ambiente di messaggistica cambiava, inoltre, veniva richiesto un ulteriore impegno per gestire i profili. In caso contrario, i client Outlook non funzionavano più correttamente.

Tramite il servizio di individuazione automatica, Outlook individua un nuovo punto di connessione costituito dal GUID della cassetta postale dell'utente + @ + la parte del dominio dell'indirizzo SMTP primario dell'utente. Il servizio di individuazione automatica restituisce le seguenti informazioni al client:

  - Nome visualizzato dell'utente

  - Impostazioni di connessione separate per la connettività interna ed esterna

  - Percorso del server Cassette postali

  - URL per varie funzionalità di Outlook che regolano funzionalità quali le informazioni sulla disponibilità, la messaggistica unificata e la rubrica offline

  - Impostazioni del server Outlook via Internet

Quando viene modificata un'informazione di Exchange di un utente, in Outlook viene riconfigurato automaticamente il profilo dell'utente utilizzando il servizio di individuazione automatica. Ad esempio, se una cassetta postale di un utente viene spostata o se il client non è in grado di connettersi alla cassetta postale dell'utente o a funzionalità di Exchange disponibili, Outlook contatterà il servizio di individuazione automatica e aggiornerà automaticamente il profilo dell'utente per avere le informazioni necessarie per la connessione alla cassetta postale e alle funzionalità di Exchange.

Inizio pagina

## Come funziona il servizio di individuazione automatica

Quando si installa il server Accesso client in Exchange 2013, viene creata una directory virtuale predefinita denominata Individuazione automatica nel sito Web predefinito dei servizi IIS (Internet Information Services). Questa directory virtuale gestisce le richieste del servizio di individuazione automatica provenienti da client di Outlook 2007, Outlook 2010 e Outlook 2013 e da telefoni cellulari supportati nelle circostanze seguenti:

  - Quando viene configurato o aggiornato un account utente

  - Quando un client di Outlook verifica periodicamente le modifiche apportate agli URL dei Servizi Web di Exchange

  - Quando si verificano modifiche nella connessione di rete sottostante nel proprio ambiente di messaggistica di Exchange

Inoltre, viene creato un nuovo oggetto Active Directory denominato punto di connessione del servizio (SCP, Service Connection Point) nel server in cui si installa il server Accesso client.

L'oggetto SCP contiene l'elenco autorevole degli URL del servizio di individuazione automatica per la foresta. È possibile utilizzare il cmdlet **Set-ClientAccessServer** per aggiornare l'oggetto SCP. Per ulteriori informazioni, vedere [Set-ClientAccessServer](https://technet.microsoft.com/it-it/library/bb125157\(v=exchg.150\)).


> [!IMPORTANT]
> Prima di eseguire il cmdlet <STRONG>Set-ClientAccessServer</STRONG>, assicurarsi che l'account Authenticated Users nel server Accesso client abbia l'autorizzazione in lettura per l'oggetto SCP. Se gli utenti non dispongono delle autorizzazioni corrette, non saranno in grado di eseguire ricerche e di leggere gli elementi.



Per ulteriori informazioni sugli oggetti SCP, vedere [Publishing with Service Connection Points](https://go.microsoft.com/fwlink/p/?linkid=72744).

Per l'accesso esterno o mediante DNS, il client rileva il servizio di individuazione automatica su Internet utilizzando l'indirizzo di dominio SMTP primario dall'indirizzo di posta elettronica dell'utente.


> [!NOTE]
> È necessario fornire un record di risorsa per il servizio host (SRV) in DNS per consentire ai client di Outlook di rilevare il servizio di individuazione automatica mediante DNS. Per ulteriori informazioni, vedere la documentazione di Windows per la configurazione di DNS <A href="https://go.microsoft.com/fwlink/p/?linkid=85214">White Paper: Servizio di individuazione automatica di Exchange 2007</A>.



A seconda che si sia scelto o meno di configurare il servizio di individuazione automatica su un sito separato, il relativo URL sarà https://\<*smtp-indirizzo-dominio*\>/autodiscover/autodiscover.xml o https://autodiscover.\<*smtp-indirizzo-dominio*\>/autodiscover/autodiscover.xml, dove ://\<*smtp-indirizzo-dominio*\> è l'indirizzo del dominio SMTP primario. Se ad esempio l'indirizzo di posta elettronica dell'utente è tony@contoso.com, l'indirizzo del dominio SMTP primario è contoso.com. Quando il client si connette a Active Directory, il client esegue la ricerca dell'oggetto SCP creato durante l'installazione. In distribuzioni che comprendono più server Accesso client, viene creato un oggetto SCP per ciascun server Accesso client. L'oggetto SCP contiene l'attributo *ServiceBindingInfo* il cui nome di dominio completo del server Accesso client è in formato https://CAS01/autodiscover/autodiscover.xml, dove CAS01 è il nome di dominio completo del server Accesso client. Utilizzando le credenziali dell'utente, il client di Outlook 2007, Outlook 2010 o Outlook 2013 esegue l'autenticazione su Active Directory e ricerca gli oggetti SCP di individuazione automatica. Dopo che ha ottenuto ed elencato le istanze del servizio di individuazione automatica, il client si connette al primo server Accesso client dell'elenco enumerato e ottiene le informazioni del profilo sotto forma di dati XML necessari per connettersi alla cassetta postale dell'utente e alle funzionalità di Exchange disponibili.

Inizio pagina

## Opzioni di distribuzione per il servizio di individuazione automatica

Il servizio di individuazione automatica deve essere distribuito e configurato correttamente affinché i client di Outlook 2007, Outlook 2010 e Outlook 2013 possano connettersi automaticamente alle funzionalità di Exchange quali la rubrica offline, il servizio di disponibilità e la messaggistica unificata. La distribuzione del servizio di individuazione automatica rappresenta solo il primo passaggio per verificare che i servizi di Exchange, come il servizio di disponibilità, siano accessibili ai client di Outlook 2007, Outlook 2010 o Outlook 2013.

## Configurazione dell'individuazione automatica per gli spostamenti tra foreste

Il servizio di individuazione automatica può fornire informazioni sul profilo utente per la connessione ai client di Outlook per le cassette postali che sono state spostate da una foresta di Exchange a un'altra. A questo scopo, è necessario configurare un utente abilitato alla posta sia nella foresta originale in cui si trovava la cassetta postale dell'utente che nella foresta di destinazione tramite il cmdlet **New-MailUser**. Nella foresta di origine utilizzare il parametro *ExternalEmailAddress* nel cmdlet per specificare il nuovo indirizzo di posta elettronica della cassetta postale nella foresta di destinazione. Per ulteriori informazioni, vedere [New-MailUser](https://technet.microsoft.com/it-it/library/aa996335\(v=exchg.150\)).

Quando si configura un utente abilitato alla posta elettronica, il servizio di individuazione automatica nella foresta originale reindirizzerà l'utente in fase di autenticazione al nuovo indirizzo di posta elettronica nella foresta di destinazione. Il client di Outlook che si connette sarà quindi reindirizzato al server Accesso client nella foresta di destinazione in cui la cassetta postale è stata spostata.

Inizio pagina

