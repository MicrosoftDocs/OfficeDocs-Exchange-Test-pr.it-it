---
title: 'Decrittografia dei rapporti del journal: Exchange 2013 Help'
TOCTitle: Decrittografia dei rapporti del journal
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 50481592
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Decrittografia dei rapporti del journal

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-16_

In Microsoft Exchange Server 2013, IRM (Information Rights Management) consente agli utenti di Microsoft Outlook 2010 e versione successiva e Microsoft Office Outlook Web App di proteggere i loro messaggi. È possibile creare regole di protezione di Outlook per applicare automaticamente la protezione IRM ai messaggi prima che vengano inviati da un client Outlook 2010. È inoltre possibile creare regole di protezione di trasporto per applicare la protezione IRM ai messaggi in transito che soddisfano le condizioni della regola.

Per ulteriori informazioni sulle regole di protezione di Outlook, vedere [Regole di protezione di Outlook](outlook-protection-rules-exchange-2013-help.md).

## Limiti delle soluzioni di crittografia standard

Se l'organizzazione applica la crittografia ai messaggi utilizzando soluzioni tradizionali come S/MIME, i gestori dei record non saranno in grado di esaminare o ricercare il contenuto crittografato. L'archiviazione di messaggi crittografati, il cui contenuto è inaccessibile e non ricercabile, potrebbe non rispettare i requisiti aziendali, normativi o di conformità. A fronte di una richiesta di individuazione elettronica (eDiscovery), l'impossibilità di decrittografare, ricercare e presentare il contenuto dei messaggi crittografati potrebbe rivelarsi un problema tale da esporre l'organizzazione a rischi legali e finanziari.

Inoltre, i criteri di messaggistica dell'organizzazione potrebbero richiedere la decrittografia dei messaggi inseriti nel journal affinché il contenuto sia accessibile agli strumenti eDiscovery, ai processi automatizzati o ai gestori dei record che accedono a una cassetta postale di inserimento nel journal. La decrittografia dei rapporti del journal in Exchange 2010 consente di soddisfare questi requisiti.

Per ulteriori informazioni sull'inserimento dei dati nel journal, vedere [Inserimento nel journal](journaling-exchange-2013-help.md).

## Decrittografia dei report del journal

La decrittografia dei rapporti del journal consente di salvare nei rapporti del journal una copia in chiaro dei messaggi protetti da IRM, insieme al messaggio originale protetto da IRM. Se il messaggio protetto da IRM contiene allegati supportati protetti dal cluster Active Directory Rights Management Services (AD RMS) nell'organizzazione, vengono decrittografati anche gli allegati.


> [!IMPORTANT]
> Per utilizzare la decrittografia dei rapporti del journal è necessario disporre di una licenza CAL Exchange di Exchange Enterprise. La decrittografia dei rapporti del journal supporta solo l'inserimento nel journal avanzato.



La decrittografia viene eseguita dall'agente di decrittografia dei rapporti del journal, un agente di trasporto mirato alle questioni di conformità. L'agente di decrittografia dei rapporti del journal viene attivato a seguito dell'evento **OnCategorizedMessage**. I messaggi protetti nella fase di transito per mezzo delle regole di protezione del trasporto sono già stati crittografati dall'agente di crittografia, che viene attivato dall'evento **OnRoutedMessage**, prima di raggiungere l'agente di decrittografia dei rapporti del journal. L'agente di decrittografia dei rapporti del journal consente di decrittografare questi messaggi.


> [!NOTE]
> In Exchange 2013, l'agente di decrittografia dei rapporti del journal è un agente incorporato. Gli agenti incorporati non sono inclusi nell'elenco di agenti restituiti dal cmdlet <STRONG>Get-TransportAgent</STRONG>. Per ulteriori informazioni, vedere <A href="transport-agents-exchange-2013-help.md">Agenti di trasporto</A>.



L'agente decrittografa i seguenti tipi di messaggi protetti da IRM:

  - Messaggi che sono stati protetti da IRM dall'utente in Outlook Web App.

  - Messaggi che sono stati protetti da IRM dall'utente in Outlook 2010.

  - Messaggi che sono stati protetti da IRM automaticamente in Outlook 2010 utilizzando le regole di protezione di Outlook.

  - Messaggi che sono stati protetti da IRM automaticamente in fase di transito, utilizzando le regole di protezione del trasporto.


> [!IMPORTANT]
> Solo i messaggi protetti da IRM attraverso il server AD&nbsp;RMS nell'organizzazione vengono decrittografati dall'agente di decrittografia dei rapporti del journal. L'agente non decrittografa un allegato se non è stato protetto contemporaneamente al messaggio (e pertanto non dispone della stessa di licenza di utilizzo) o se un file protetto da IRM è stato allegato a un messaggio non protetto.



## Configurazione della decrittografia dei rapporti del journal

La decrittografia dei rapporti del journal viene configurata utilizzando il cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)) in Exchange Management Shell. Tuttavia, prima di configurare la decrittografia dei rapporti del journal, è necessario assegnare ai server Exchange 2013 le autorizzazioni per decrittografare il contenuto protetto da IRM dal server AD RMS. A tal fine, è necessario aggiungere la cassetta postale federata al gruppo di utenti con privilegi avanzati configurato nel cluster AD RMS dell'organizzazione. Per ulteriori informazioni, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).


> [!IMPORTANT]
> Nelle distribuzioni di AD&nbsp;RMS tra foreste, in cui in ogni foresta è stato distribuito un cluster AD&nbsp;RMS, è necessario aggiungere la cassetta postale federata al gruppo di utenti con privilegi avanzati sul cluster AD&nbsp;RMS in ogni foresta per consentire al servizio di trasporto di Exchange 2013 di decrittografare i messaggi protetti su ogni cluster AD&nbsp;RMS.



Per ulteriori informazioni sulla configurazione della decrittografia dei rapporti del journal, vedere [Attivare o disattivare la decrittografia dei rapporti del Journal](enable-or-disable-journal-report-decryption-exchange-2013-help.md).

Dopo aver abilitato la decrittografia dei rapporti del journal, la cassetta del journaling può contenere rapporti del journal con informazioni riservate in una forma non crittografata. Secondo la procedura ottimale è consigliabile controllare attentamente l'accesso alla cassetta del journaling e limitarlo solo agli utenti autorizzati. Questa procedura è consigliata anche se non si utilizza la protezione IRM per la posta elettronica.

