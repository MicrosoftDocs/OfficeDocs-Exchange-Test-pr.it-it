---
title: 'Regole di protezione del trasporto: Exchange 2013 Help'
TOCTitle: Regole di protezione del trasporto
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 50481273
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Regole di protezione del trasporto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

I messaggi e gli allegati di posta elettronica contengono sempre più importanti informazioni aziendali, quali specifiche di prodotto, documenti sulle strategie aziendali e dati finanziari, o informazioni personali, quali dettagli di contatto, codici fiscali, numeri di carte di credito e record di dipendenti. Esistono una serie di normative locali e specifiche del settore in molte parti del mondo che regolano la raccolta, l'archiviazione e la divulgazione delle informazioni personali.

Per consentire la sicurezza delle informazioni riservate, le organizzazioni creano criteri di messaggistica che forniscono linee guida su come gestire queste informazioni. In MicrosoftExchange Server 2013, è possibile utilizzare le regole di protezione del trasporto per implementare questi criteri di messaggistica esaminando il contenuto dei messaggi, crittografando il contenuto riservato della posta elettronica e utilizzando la gestione dei diritti per controllare l'accesso al contenuto.

Per le attività di gestione relative alla gestione degli elementi IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Regole di protezione del trasporto e AD RMS

Regole di trasporto protezione consentono di utilizzare le regole di trasporto per la protezione IRM messaggi tramite l'applicazione di un modello di criteri [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823) diritti (AD RMS).


> [!NOTE]
> AD&nbsp;RMS è una tecnologia per la sicurezza delle informazioni che interagisce con applicazioni e client abilitati a Rights Management Service (RMS) per proteggere le informazioni riservate online e offline. Per utilizzare la protezione IRM in una distribuzione di Exchange locale, Exchange 2013 richiede una distribuzione locale di AD&nbsp;RMS in esecuzione su Windows Server 2008 o versioni successive.



AD RMS utilizza modelli di criteri basati su XML per consentire alle applicazioni abilitate a IRM compatibili di applicare criteri di sicurezza coerenti. In Windows Server 2008 e versioni successive, il server AD RMS presenta un servizio Web utilizzabile per enumerare e acquisire i modelli. Exchange 2013 viene fornito con il modello Non inoltrare.

Quando il modello Non inoltrare viene applicato a un messaggio, solo i destinatari specificati nel messaggio possono decrittografare il messaggio. I destinatari non possono inoltrare, copiare o stampare il messaggio.

Per soddisfare i requisiti di sicurezza dei diritti per l'organizzazione, è possibile creare ulteriori modelli RMS nella distribuzione locale di AD RMS.


> [!IMPORTANT]
> Se un modello di criteri per i diritti viene rimosso dal server AD&nbsp;RMS, è necessario modificare tutte le regole di protezione del trasporto che utilizzano il modello rimosso. Se una regola di protezione del trasporto continua a utilizzare un modello di criteri per i diritti rimosso, il server AD&nbsp;RMS non concederà la licenza a nessun destinatario e al mittente verrà inviato un rapporto di mancato recapito (NDR).<BR>In Windows Server 2008 e versioni successive, i modelli dei criteri dei diritti possono essere archiviati anziché eliminati. I modelli archiviati possono ancora essere utilizzati per concedere licenze per il contenuto, ma quando si crea o si modifica una regola di protezione del trasporto, i modelli archiviati non vengono compresi nell'elenco dei modelli.



Per ulteriori informazioni sulla creazione di modelli di AD RMS, vedere [Guida dettagliata AD RMS diritti di criteri di modelli di distribuzione](https://go.microsoft.com/fwlink/p/?linkid=136593).

## Protezione automatica tramite le regole di protezione del trasporto

I messaggi contenenti importanti informazioni aziendali o informazioni personali possono essere identificati utilizzando una combinazione di condizioni delle regole di trasporto, comprese le espressioni regolari per identificare i modelli di testo, come i codici fiscali. Le organizzazioni richiedono diversi livelli di sicurezza per le informazioni riservate. Alcune informazioni possono essere limitate a dipendenti, fornitori o partner; mentre altre informazioni possono essere limitate solo ai dipendenti a tempo pieno. Il livello di sicurezza desiderato può essere applicato ai messaggi adottando un modello di criteri per i diritti adeguato. Ad esempio, gli utenti possono contrassegnare i messaggi o gli allegati di posta elettronica come Materiale aziendale riservato. Come illustrato nella figura seguente, è possibile creare una regola di protezione del trasporto per esaminare il contenuto del messaggio con le parole "Materiale aziendale riservato" e proteggere automaticamente con IRM il messaggio.

Per ulteriori informazioni sulla creazione del regole di trasporto per applicare la sicurezza dei diritti, vedere [Creare una regola di protezione del trasporto](create-a-transport-protection-rule-exchange-2013-help.md).

## Protezione permanente degli allegati di posta elettronica

Gli utenti inviano informazioni aziendali importanti e informazioni personali negli allegati di posta elettronica utilizzando comuni formati di file di Microsoft Office, quali Microsoft Office Word, Excel e PowerPoint. Tutti questi formati di file supportano la sicurezza permanente tramite IRM ed è possibile assicurare la sicurezza adeguata delle informazioni aziendali importanti e delle informazioni personali contenute in questi documenti. Le regole di protezione del trasporto consentono di applicare lo stesso livello di protezione ai messaggi e agli allegati di posta elettronica nei formati di file supportati.

## Agente Regole di trasporto e agente di crittografia

Quando si utilizzano le regole di protezione del trasporto per proteggere con IRM i messaggi in base alle condizioni delle regole, i messaggi vengono esaminati dall'agente Regole di trasporto nel servizio Trasporto. Se soddisfano tutte le condizioni e nessuna eccezione, il messaggio viene contrassegnato per la protezione IRM. L'agente di crittografia, un agente di trasporto incorporato che si attiva in concomitanza dell'evento **OnRoutedMessage**, rende effettiva la protezione IRM del messaggio. L'agente di crittografia agisce sui messaggi solo se IRM è abilitato per i messaggi interni. Per ulteriori informazioni sull'abilitazione di IRM, vedere [Abilitazione o disabilitazione di IRM per i messaggi interni](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

Quando il servizio di trasporto viene riavviato ed elabora il primo messaggio richiedente la crittografia IRM, l'agente di crittografia deve essere in grado di raggiungere un server AD RMS dell'organizzazione. Per i messaggi successivi, l'agente non deve contattare il server AD RMS. Se la crittografia del messaggio non riesce per condizioni temporanee, Exchange tenta di rieseguire l'operazione per tre volte a intervalli di 10 minuti. Dopo tre tentativi, se non può essere crittografato, il messaggio non viene recapitato ai destinatari. Al mittente viene inviato un rapporto di mancato recapito. Si consiglia di pianificare la distribuzione di AD RMS a elevata disponibilità per assicurarsi di non interferire con il flusso dei messaggi.

Durante la pianificazione dell'utilizzo delle regole di protezione del trasporto, è necessario considerare il tipo di informazioni da proteggere e pianificare la creazione delle relative regole. In Exchange 2013, le regole di trasporto dispongono di un gran numero di predicati che consentono di esaminare il contenuto dei messaggi, compresi gli allegati supportati, le intestazioni dei messaggi, gli indirizzi del mittente e dei destinatari e gli attributi di Active Directory quali reparto, appartenenza ai gruppi di distribuzione e relazioni di gestione del mittente con i destinatari. Per informazioni dettagliate sui predicati delle regole di trasporto disponibili in Exchange 2013, vedere [Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Inoltre, è necessario considerare il traffico di messaggistica dell'organizzazione e il numero di messaggi da proteggere utilizzando le regole di protezione del trasporto. L'applicazione della protezione IRM a un gran numero di messaggi richiede maggiori risorse sul server Cassette postali. Inoltre, la protezione di un gran numero di messaggi o di tutti i messaggi interferisce anche con le prestazioni client, in particolare per gli utenti di Microsoft Outlook.

