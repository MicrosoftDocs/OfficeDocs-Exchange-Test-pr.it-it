---
title: 'Regole di protezione di Outlook: Exchange 2013 Help'
TOCTitle: Regole di protezione di Outlook
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 50481579
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Regole di protezione di Outlook

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Ogni giorno, information worker scambiano di informazioni riservate tramite posta elettronica, inclusi i report finanziari e dati, clienti e informazioni sui dipendenti, informazioni sul prodotto confidential e specifiche. In Microsoft Exchange Server 2013, Microsoft Outlook e Microsoft OfficeOutlook Web App, gli utenti possono applicare protezione Information Rights Management (IRM) per i messaggi tramite l'applicazione di un modello di criteri per i diritti di Active Directory Rights Management Services (AD RMS). Questo richiede la distribuzione di AD RMS nell'organizzazione. Per ulteriori informazioni su AD RMS, vedere [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823).

Se la decisione viene lasciata agli utenti, i messaggi possono essere inviati come testo non crittografato senza la protezione IRM. Nelle organizzazioni che utilizzano la posta elettronica come servizio ospitato, esiste il pericolo di fuga delle informazioni nel momento in cui un messaggio lascia il client e viene instradato e archiviato all'esterno dei limiti di un'organizzazione. Nonostante le società di hosting della posta elettronica dispongano di procedure e controlli ben definiti per prevenire il pericolo di fuga delle informazioni, l'organizzazione perde il controllo delle informazioni nel momento in cui un messaggio lascia i suoi confini. Le regole di protezione di Outlook facilitano la protezione contro questo tipo di fuga delle informazioni.

Per le attività di gestione relative alla gestione degli elementi IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Protezione IRM automatica in Outlook

In Exchange 2013, le regole di protezione di Outlook aiutano l'organizzazione a proteggersi dal pericolo di fuga delle informazioni mediante l'applicazione automatica della protezione IRM ai messaggi in Exchange 2013. I messaggi vengono protetti da IRM prima di lasciare il client Outlook. Questa protezione viene applicata anche agli allegati che utilizzano formati di file supportati.

Quando si creano regole di protezione di Outlook su un server Exchange 2013, le regole vengono automaticamente distribuite ad Outlook 2010 per mezzo di Servizi Web Exchange. Affinché Outlook 2010 possa applicare la regola, il modello di criteri per i diritti di utilizzo di AD RMS specificato deve essere disponibile sui computer degli utenti.


> [!IMPORTANT]
> Se un modello di criteri per i diritti viene rimosso dal server AD RMS, è necessario modificare le regole di protezione Outlook che utilizzano il modello rimosso. Se una regola di protezione Outlook continua a utilizzare un modello di criteri di diritti che è stata rimossa e la decrittografia di trasporto è attivata nell'organizzazione, agente di decrittografia avrà esito negativo decrittografare il messaggio protetto con il modello che non è più disponibile. Se la decrittografia di trasporto è configurata come obbligatorio, il servizio di trasporto verrà Rifiuta il messaggio e inviare un rapporto di mancato recapito (NDR) al mittente. Per ulteriori informazioni sulla decrittografia di trasporto, vedere <A href="transport-decryption-exchange-2013-help.md">Decrittografia di trasporto</A>. Per ulteriori informazioni sui modelli di criteri per i diritti AD RMS, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=179455">Considerazioni sulla modello dei criteri di AD RMS</A>.<BR>In Windows Server 2008 e versioni successive, i modelli dei criteri dei diritti possono essere archiviati anziché eliminati. I modelli archiviati sono tuttora utilizzabili per concedere in licenza il contenuto, ma non sono inclusi nell'elenco dei modelli durante la creazione o la modifica di una regola di protezione di Outlook.



Le regole di protezione di Outlook sono simili alle regole di protezione del trasporto. Entrambe vengono applicate in base alle condizioni del messaggio ed entrambe proteggono i messaggi applicando un modello di protezione per i diritti di utilizzo di AD RMS. Le regole di protezione del trasporto vengono tuttavia applicate al servizio Trasporto sul server Cassette postali dall'agente Regole di trasporto. Le regole di protezione di Outlook vengono applicate in Outlook 2010 prima che il messaggio lasci il computer dell'utente. I messaggi protetti da una regola di protezione di Outlook entrano nella pipeline di trasporto con la protezione IRM già applicata. Inoltre, i messaggi protetti da una regola di protezione di Outlook vengono salvati in formato crittografato nella cartella Posta inviata della cassetta postale del mittente.


> [!NOTE]
> Se nell'organizzazione di Exchange è attivata la decrittografia del trasporto, i messaggi protetti da IRM attraverso una regola di protezione di Outlook per mezzo del server AD&nbsp;RMS nell'organizzazione possono essere decrittografati dall'agente di decrittografia sul servizio Trasporto. Il contenuto del messaggio può essere ispezionato dall'agente Regole di trasporto e da altri agenti di trasporto installati nel servizio Trasporto. Per ulteriori informazioni sulla decrittografia del trasporto, vedere <A href="transport-decryption-exchange-2013-help.md">Decrittografia di trasporto</A>.



Durante l'uso delle regole di protezione del trasporto, gli utenti non ottengono alcuna indicazione relativa alla protezione automatica di un messaggio nel servizio Trasporto. Quando una regola di protezione di Outlook viene applicata a un messaggio in Outlook 2010, invece, gli utenti sono a conoscenza della protezione IRM del messaggio. Se necessario, gli utenti possono inoltre selezionare un modello di criteri per i diritti di utilizzo differente.

## Creazione di regole di protezione di Outlook

Per creare le regole di protezione di Outlook, è necessario utilizzare il cmdlet [New-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd298182\(v=exchg.150\)) in Exchange Management Shell. Per istruzioni dettagliate, vedere [Creare una regola di protezione di Outlook](create-an-outlook-protection-rule-exchange-2013-help.md).

Durante la creazione di una regola, è possibile specificare se l'utente può sostituirla sia rimuovendo la protezione IRM sia applicando un modello di criteri per i diritti di utilizzo di AD RMS diverso rispetto a quello specificato nella regola. Se un utente sostituisce la protezione IRM applicata da una regola di protezione di Outlook, Outlook 2010 inserisce l'intestazione `X-MS-Outlook-Client-Rule-Overridden` nel messaggio per consentire di determinare che la regola è stata sostituita dall'utente.

## Predicati nelle regole di protezione di Outlook

Le regole di protezione di Outlook consentono di utilizzare tre predicati per applicare automaticamente la protezione IRM in Outlook 2010:

  - **FromDepartment**   Il predicato *FromDepartment* consente di ricercare l'attributo di reparto del mittente in Active Directory e di proteggere automaticamente con IRM il messaggio se il reparto del mittente corrisponde al reparto specificato nella regola. Ad esempio, è possibile creare una regola di protezione di Outlook per proteggere automaticamente tutti i messaggi inviati dal reparto Ricerca.

  - **SentTo**   È possibile che l'organizzazione debba proteggere i messaggi inviati a determinati destinatari sensibili, ad esempio i gruppi di distribuzione Tutta la società o Finanze. Utilizzando il predicato *SentTo* è possibile creare una regola di protezione di Outlook per proteggere automaticamente con IRM i messaggi inviati a destinatari specificati.

  - **SentToScope**   Il predicato *SentToScope* consente di creare una regola di protezione di Outlook per proteggere automaticamente con IRM i messaggi inviati all'interno o all'esterno dell'organizzazione. Ad esempio, è possibile utilizzare il predicato *SentToScope* con il predicato *FromDepartment* per proteggere con IRM i messaggi inviati da un particolare reparto agli utenti interni.

