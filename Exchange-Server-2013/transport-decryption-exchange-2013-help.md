---
title: 'Decrittografia di trasporto: Exchange 2013 Help'
TOCTitle: Decrittografia di trasporto
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 50480496
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Decrittografia di trasporto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

In Microsoft Exchange Server 2013, Microsoft Outlook 2010 e versioni successive e Microsoft OfficeOutlook Web App, gli utenti possono utilizzare Information Rights Management (IRM) per proteggere i messaggi. È possibile creare le regole di protezione di Outlook per applicare automaticamente la protezione IRM ai messaggi prima che vengano inviati da un client Outlook 2010. È inoltre possibile creare regole di protezione di trasporto per applicare la protezione IRM ai messaggi in transito che soddisfano le condizioni della regola. La decrittografia di trasporto consente di accedere al contenuto dei messaggi protetti da IRM per applicare i criteri di messaggistica.

Per le attività di gestione relative alla gestione degli elementi IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Limitazioni di altre soluzioni di crittografia

Se è importante che l'organizzazione protegga le informazioni riservate, comprese le informazioni aziendali e quelle personali, è opportuno crittografare i messaggi di posta elettronica e gli allegati. Le soluzioni di crittografia dei messaggi di posta elettronica, ad esempio S/MIME, sono state disponibili per molto tempo. Tali soluzioni sono state utilizzate da diversi tipi di organizzazioni in diversi campi. Tuttavia, presentano le seguenti problematiche:

  - **Impossibilità di applicare i criteri di messaggistica**   Le organizzazioni devono soddisfare i requisiti di conformità che richiedono di controllare il contenuto dei messaggi per fare in modo che sia conforme ai criteri di messaggistica. Tuttavia, i messaggi crittografati con la maggior parte delle soluzioni di crittografia basate su client, compreso S/MIME, impediscono il controllo del contenuto sul server. Se il controllo non viene eseguito, l'organizzazione non è in grado di confermare che tutti i messaggi inviati o ricevuti dagli utenti sono conformi ai criteri di messaggistica. Ad esempio, per essere conformi ad una normativa legale, è stata configurata una regola di trasporto per rilevare PII, come un numero di previdenza sociale ed è stato applicata una dichiarazione di non responsabilità al messaggio. Se il messaggio è crittografato, l'agente delle regole di trasporto nel servizio Trasporto non è in grado di accedere al contenuto del messaggio e di conseguenza non verrà applicata la dichiarazione di non responsabilità. Questo determina una violazione del criterio.

  - **Sicurezza diminuita**   Il software antivirus non è in grado di eseguire la scansione dei messaggi crittografati. L'organizzazione sarà maggiormente esposta al rischio di ricevere contenuti dannosi, come virus o worm. Di solito i messaggi crittografati vengono considerati affidabili dalla maggior parte degli utenti. Di conseguenza, aumenta la probabilità di diffusione di virus nell'organizzazione. Ad esempio, è stata configurata una regola di protezione di Outlook per applicare automaticamente la protezione IRM a tutti i messaggi inviati all'elenco di distribuzione Tutti i dipendenti con il modello RMS (Rights Management Service) riservato dell'azienda. La workstation dell'utente viene infettata da un virus che si diffonde utilizzando automaticamente Rispondi a tutti per rispondere ai messaggi. Se il messaggio contenente il virus è crittografato, lo scanner antivirus non è in grado di eseguire la scansione del messaggio.

  - **Impatto sugli agenti di trasporto personalizzati**   Molte organizzazioni sviluppano agenti di trasporto personalizzati per scopi diversi, ad esempio soddisfare i requisiti di elaborazione per la conformità, sicurezza o routing dei messaggi personalizzati. Gli agenti di trasporto personalizzati sviluppati da un'organizzazione per controllare o modificare i messaggi non sono in grado di elaborare i messaggi crittografati. Se gli agenti di trasporto personalizzati sviluppati dall'organizzazione non sono in grado di accedere al contenuto dei messaggi, è possibile che la crittografia dei messaggi impedisca all'organizzazione di raggiungere gli obiettivi per i quali sono stati sviluppati gli agenti di trasporto.

## Utilizzo della decrittografia di trasporto per il contenuto crittografato

In Exchange 2013, le funzionalità IRM risolvono questi problemi. Se i messaggi sono protetti da IRM la decrittografia di trasporto consente di decrittografarli mentre sono in transito. I messaggi protetti da IRM vengono decrittografati dall'agente di decrittografia, un agente di trasporto che ha come principale obiettivo la verifica della conformità.


> [!NOTE]
> In Exchange 2013, l'agente di decrittografia è incorporato. Gli agenti incorporati non sono inclusi nell'elenco degli agenti restituiti dal cmdlet <STRONG>Get-TransportAgent</STRONG>. Per ulteriori informazioni, vedere <A href="transport-agents-exchange-2013-help.md">Agenti di trasporto</A>.



L'agente di decrittografia consente di decrittografare i seguenti tipi di messaggi protetti con IRM:

  - Messaggi protetti con IRM dall'utente in Outlook Web App.

  - Messaggi protetti con IRM dall'utente in Outlook 2010.

  - Messaggi automaticamente protetti con IRM dalle regole di protezione di Outlook in Exchange 2013 e Outlook 2010.


> [!IMPORTANT]
> Solo i messaggi protetti con IRM dal server AD&nbsp;RMS nell'organizzazione vengono decrittografati dall'agente di decrittografia.




> [!NOTE]
> I messaggi protetti durante il trasferimento mediante le regole di protezione di trasporto non necessitano di essere decrittografati dall'agente di decrittografia. L'agente di decrittografia si attiva in concomitanza degli eventi di trasporto <STRONG>OnEndOfData</STRONG> e <STRONG>OnSubmit</STRONG>. Le regole di protezione di trasporto vengono applicate dall'agente delle regole di trasporto, che si attiva in concomitanza dell'evento <STRONG>OnRoutedMessage</STRONG> e la protezione con IRM viene applicata dall'agente di crittografia in concomitanza dell'evento <STRONG>OnRoutedMessage</STRONG>. Per ulteriori informazioni sugli agenti di trasporto e per un elenco di eventi SMTP in cui possono essere registrati, vedere <A href="transport-agents-exchange-2013-help.md">Agenti di trasporto</A>.



La decrittografia di trasporto viene eseguita sul primo servizio Trasporto di Exchange 2013 che gestisce un messaggio nella foresta di Active Directory. Se il messaggio viene trasferito su un servizio Trasporto in un'altra foresta di Active Directory, verrà nuovamente decrittografato. Dopo la decrittografia, il contenuto non crittografato sarà disponibile sugli altri agenti di trasporto in quel server. Ad esempio, l'agente delle regole di trasporto su un servizio Trasporto può controllare il contenuto del messaggio e applicare le regole di trasporto. Qualsiasi azione specificata nella regola, ad esempio l'applicazione di una dichiarazione di non responsabilità o la modifica del messaggio, può essere eseguita nel messaggio non crittografato. Gli agenti di trasporto di terze parti, ad esempio gli scanner antivirus, possono eseguire la scansione del messaggio per verificare la presenza di virus o altro malware. Dopo che altri agenti di trasporto hanno controllato il messaggio e apportato delle modifiche, il messaggio verrà nuovamente crittografato con gli stessi diritti utente che aveva prima di essere decrittografato dall'agente di decrittografia. Lo stesso messaggio non viene di nuovo decrittografato da un altro servizio Trasporto su altri server Cassette postali dell'organizzazione.

I messaggi decrittografati dall'agente di decrittografia non lasciano il servizio Trasporto senza essere stati prima nuovamente crittografati. Se viene restituito un errore temporaneo durante la decrittografia o la crittografia del messaggio, il servizio Trasporto tenta di eseguire l'operazione due volte. Al terzo tentativo non riuscito, l'errore viene considerato un errore permanente. Se si verificano errori permanenti, compresi gli errori temporanei considerati errori permanenti, il servizio Trasporto li considera nel modo seguente:

  - Se l'errore permanente si verifica durante la decrittografia, il rapporto di mancato recapito viene inviato solo se la decrittografia di trasporto è impostata su `Mandatory` e il messaggio crittografato viene inviato con il rapporto di mancato recapito. Per ulteriori informazioni sulle opzioni di configurazione disponibili per la decrittografia di trasporto, vedere la sezione Configuring Transport Decryption descritta in seguito in questo argomento.

  - Se l'errore permanente si verifica durante la nuova crittografia, il rapporto di mancato recapito viene sempre inviato senza il messaggio decrittografato.


> [!IMPORTANT]
> Qualsiasi agente personalizzato o di terze parti installato su un servizio Trasporto ha accesso al messaggio decrittografato. È necessario prendere in considerazione il comportamento di tali agenti di trasporto. Si consiglia di controllarli attentamente prima di distribuirli in un ambiente di produzione.<BR>Dopo che il messaggio è stato decrittografato dall'agente di decrittografia, se un agente di trasporto crea un nuovo messaggio e allega il messaggio originale a quello nuovo, verrà protetto solo il nuovo messaggio. Il messaggio originale, che diventa allegato nel nuovo messaggio, non verrà nuovamente crittografato. L'utente che riceve tale tipo di messaggio può aprire il messaggio allegato, rispondere al messaggio o inoltrarlo, ignorando in tal modo l'applicazione dei diritti.



## Configurazione della decrittografia di trasporto

La decrittografia di trasporto viene configurata utilizzando il cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)) in Exchange Management Shell. Tuttavia, prima di configurare la decrittografia di trasporto, è necessario fornire ai server Exchange 2013 il diritto di decrittografare il contenuto protetto dal server AD RMS. È possibile eseguire l'operazione aggiungendo la cassetta postale di recapito federativo al gruppo di utenti con privilegi avanzati configurati nel cluster AD RMS dell'organizzazione.


> [!IMPORTANT]
> Più foreste AD RMS nelle distribuzioni in cui si trova un cluster AD RMS distribuito in ogni foresta, è necessario aggiungere la cassetta postale di federazione al gruppo utenti con privilegi avanzati nel cluster AD RMS in ogni foresta per consentire al servizio di trasporto in un server cassette postali Exchange 2013 o un server Trasporto Hub Exchange&nbsp;2010 per decrittografare i messaggi protetti da ogni cluster AD RMS.



Per i dettagli, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

In Exchange 2013 esistono due impostazioni diverse quando si abilita la decrittografia di trasporto:

  - **Obbligatorio**   Quando la decrittografia di trasporto è impostata su `Mandatory`, l'agente di decrittografia rifiuta il messaggio e restituisce un rapporto di mancato recapito al mittente se viene restituito un errore permanente durante la decrittografia del messaggio. Se l'organizzazione non desidera che il messaggio (non correttamente decrittografato) venga recapitato e se viene eseguita la scansione antivirus e vengono applicate le regole di trasporto, è necessario scegliere questa impostazione.

  - **Facoltativo**   Quando la decrittografia di trasporto è impostata su Facoltativo, l'agente di decrittografia utilizza una tecnica migliore. Vengono decrittografati i messaggi in cui è possibile eseguire questa operazione. Tuttavia, vengono recapitati anche i messaggi in cui si è verificato un errore permanente durante la decrittografia. Se l'organizzazione stabilisce che il recapito dei messaggi ha la priorità sui criteri di messaggistica, è necessario utilizzare questa impostazione.

Per ulteriori informazioni sulla configurazione della decrittografia di trasporto, vedere [Abilitare o disabilitare la decrittografia di trasporto](enable-or-disable-transport-decryption-exchange-2013-help.md).

