---
title: 'Elenchi indirizzi: Exchange 2013 Help'
TOCTitle: Elenchi indirizzi
ms:assetid: 8ee2672a-3a45-4897-8cc0-fa23c374dbf9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232119(v=EXCHG.150)
ms:contentKeyID: 50481161
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenchi indirizzi

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-02_

Un *elenco indirizzi* indica una raccolta di oggetti destinatario e altri oggetti Active Directory. ‎Ogni elenco indirizzi può contenere uno o più tipi di oggetti (ad esempio utenti, contatti, gruppi, cartelle pubbliche, risorse di sala e attrezzature). È possibile utilizzare gli elenchi di indirizzi per organizzare destinatari e risorse, facilitando l'individuazione dei destinatari e delle risorse desiderate. Gli elenchi di indirizzi vengono aggiornati dinamicamente. Pertanto, quando si aggiungono all'organizzazione, i nuovi destinatari vengono aggiunti automaticamente anche agli elenchi indirizzi appropriati.

Come mostrato nella figura seguente, nelle applicazioni client, come Microsoft Outlook, vengono visualizzati gli elenchi indirizzi disponibili forniti da Exchange.

**Elenco indirizzi globale visualizzato in Microsoft Office Outlook 2007**

![Elenchi di indirizzi visualizzati in Outlook 2007](images/Bb232119.54d7729c-2e28-4863-8944-b0c37dabbbb3(EXCHG.150).gif "Elenchi di indirizzi visualizzati in Outlook 2007")

Gli elenchi indirizzi si trovano in Active Directory. Pertanto, gli utenti di dispositivi mobili disconnessi dalla rete sono anche disconnessi dagli elenchi di indirizzi sul lato server. Tuttavia, è possibile creare Rubriche fuori rete per gli utenti non connessi alla rete. Queste rubriche offline possono essere scaricate sul disco rigido di un utente. Le Rubriche fuori rete sono sottoinsiemi di informazioni contenute negli elenchi di indirizzi effettivi che si trovano nei server e in genere vengono utilizzate per risparmiare le risorse del computer. Per ulteriori informazioni, vedere [Rubriche offline](offline-address-books-exchange-2013-help.md).

**Sommario**

Default address lists

Custom address lists

Best practices for creating address lists

## Elenchi indirizzi predefiniti

Quando gli utenti desiderano utilizzare l'applicazione client per individuare le informazioni sui destinatari, possono scegliere fra gli elenchi di indirizzi disponibili. Diversi elenchi indirizzi, come l'elenco indirizzi globale (GAL), vengono creati per impostazione predefinita. Exchange contiene i seguenti elenchi indirizzi predefiniti, in cui vengono compilati automaticamente con nuovi utenti, contatti, gruppi o sale una volta aggiunti all'organizzazione:

  - **Tutti i contatti**   Questo elenco di indirizzi contiene tutti i contatti abilitati alla posta nell'organizzazione. I contatti abilitati alla posta sono i destinatari con indirizzo di posta elettronica esterno. Per rendere disponibili a tutti gli utenti dell'organizzazione le informazioni sui contatti abilitati alla posta, è necessario includere il contatto nell'elenco indirizzi globale. Per ulteriori informazioni sui contatti di posta, vedere [Destinatari](recipients-exchange-2013-help.md).

  - **Tutte le liste di distribuzione**   Questo elenco indirizzi contiene gruppi abilitati alla posta, come i gruppi di sicurezza abilitati alla posta, gruppi di distribuzione e gruppi di distribuzione dinamici nell'organizzazione. I gruppi abilitati alla posta sono elenchi di destinatari creati per accelerare l'invio di massa dei messaggi di posta elettronica e di altre informazioni. Quando si invia un messaggio di posta elettronica a un gruppo abilitato alla posta, tutti i membri dell'elenco ricevono una copia del messaggio. Per ulteriori informazioni sui gruppi abilitati alla posta, vedere [Destinatari](recipients-exchange-2013-help.md).

  - **Tutte le sale**   Questo elenco di indirizzi contiene tutte le risorse designate come sala nell'organizzazione. Le sale sono risorse dell'organizzazione che possono essere pianificate inviando una convocazione di riunione da un'applicazione client. L'account utente associato a una sala è disabilitato. Per ulteriori informazioni sulle cassette postali per le risorse, vedere [Destinatari](recipients-exchange-2013-help.md).

  - **Tutti gli utenti**   Questo elenco di indirizzi contiene tutti gli utenti abilitati alla posta nell'organizzazione. Un utente abilitato alla posta rappresenta un utente esterno all'organizzazione Exchange. Ciascun utente abilitato alla posta dispone di un indirizzo di posta elettronica esterno. Tutti i messaggi inviati agli utenti abilitati alla posta vengono instradati a questo indirizzo di posta elettronica esterno. L'utente abilitato alla posta è simile al contatto di posta ma, diversamente da quest'ultimo, dispone di credenziali di accesso ad Active Directory ed è in grado di accedere alle risorse. Per ulteriori informazioni sugli utenti abilitati alla posta, vedere [Destinatari](recipients-exchange-2013-help.md).

  - **Elenco indirizzi globale predefinito**   Questo elenco di indirizzi contiene tutti gli utenti, contatti, gruppi o sale nell'organizzazione abilitati alla posta. Durante l'installazione, Exchange consente di creare diversi elenchi indirizzi predefiniti. L'elenco indirizzi più noto è l'elenco indirizzi globale che, per impostazione predefinita, contiene tutti i destinatari di un'organizzazione Exchange: in altre parole, nell'elenco indirizzi globale viene elencato qualsiasi oggetto abilitato alla cassetta postale o alla posta in una foresta di Active Directory in cui è installato Exchange. Per facilitarne l'utilizzo, l'elenco indirizzi globale è organizzato per nome e non per indirizzo di posta elettronica. Per ulteriori informazioni, vedere [Creare un elenco indirizzi globale](create-a-global-address-list-exchange-2013-help.md).

  - **Cartelle pubbliche**   Questo elenco di indirizzi contiene tutte le cartelle pubbliche dell'organizzazione. Le autorizzazioni di accesso determinano gli utenti autorizzati a visualizzare e utilizzare le cartelle. Le cartelle pubbliche vengono archiviate nei computer che eseguono Exchange. Per ulteriori informazioni sulle cartelle pubbliche in Exchange 2013, vedere [Cartelle pubbliche](public-folders-exchange-2013-help.md). Per ulteriori informazioni sulle cartelle pubbliche in Exchange Online, vedere [Cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj200758\(v=exchg.150\)).

## Elenchi di indirizzi personalizzati

Un'organizzazione Exchange può contenere migliaia di destinatari. Se si inseriscono tutti i destinatari negli elenchi di indirizzi predefiniti, le dimensioni degli elenchi aumentano in modo considerevole. Per evitare un eccessivo aumento delle dimensioni, è possibile creare elenchi di indirizzi personalizzati per consentire agli utenti dell'organizzazione di individuare più facilmente l'oggetto della ricerca.

Si consideri, ad esempio, un'azienda che dispone di due grandi divisioni e di un'organizzazione Exchange. Una divisione denominata Fourth Coffee importa e vende caffè. L'altra divisione Contoso, Ltd sottoscrive polizze assicurative. Per la maggior parte delle attività quotidiane, i dipendenti di Fourth Coffee non comunicano con i dipendenti di Contoso, Ltd. Pertanto, per facilitare ai dipendenti la ricerca dei destinatari presenti solo nella loro divisione, è possibile creare due nuovi elenchi indirizzi personalizzati, uno per Fourth Coffee e uno per Contoso, Ltd. Durante la ricerca dei destinatari della loro divisione, questi elenchi indirizzi personalizzati consentono ai dipendenti di selezionare solo l'elenco indirizzi specifico della loro divisione. Tuttavia, se un dipendente non è sicuro della divisione in cui si trova il destinatario, può cercare all'interno dell'elenco indirizzi globale che contiene tutti i destinatari di entrambe le divisioni.

È possibile, inoltre, creare sottocategorie di elenchi di indirizzi denominate elenchi di indirizzi gerarchici. Ad esempio, è possibile creare un elenco indirizzi contenente tutti i destinatari di Manchester e un altro contenente tutti i destinatari di Stoccarda.

## Procedure consigliate per la creazione degli elenchi di indirizzi

Gli elenchi di indirizzi sono strumenti utili per gli utenti, tuttavia se non sono adeguatamente programmati, possono rivelarsi controproducenti. Per fare in modo che gli elenchi di indirizzi siano funzionali per gli utenti, è consigliabile osservare le seguenti istruzioni:

  - Evitare di creare un numero eccessivo di elenchi indirizzi per non confondere gli utenti sull'elenco da consultare per cercare i destinatari.

  - Gli elenchi indirizzi dovrebbero semplificare l'individuazione degli indirizzi nell'elenco indirizzi globale.

  - Assegnare agli elenchi di indirizzi un nome descrittivo che consenta agli utenti di riconoscere immediatamente i tipi di destinatari contenuti nell'elenco. Se si ha difficoltà ad assegnare nomi agli elenchi di indirizzi, creare un numero minore di elenchi e ricordare agli utenti che è possibile individuare chiunque appartenga all'organizzazione utilizzando l'elenco indirizzi globale.
    

    > [!NOTE]
    > Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento <A href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</A>.



Per istruzioni dettagliate sulla creazione di un elenco indirizzi in Exchange 2013, vedere [Creazione di un elenco di indirizzi](create-an-address-list-exchange-2013-help.md). Per istruzioni dettagliate sulla creazione di un elenco indirizzi in Exchange Online, vedere [Gestire elenchi di indirizzi in Exchange Online](https://technet.microsoft.com/it-it/library/jj983798\(v=exchg.150\)).

