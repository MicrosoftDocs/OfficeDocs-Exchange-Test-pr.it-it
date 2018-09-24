---
title: 'Configura filtro contenuto per dati dominio attendibili: Exchange 2013 Help'
TOCTitle: Configurare il filtro del contenuto per usare i dati dei dominio attendibili
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59634572
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurare il filtro del contenuto per usare i dati dei dominio attendibili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-16_

I dati dei domini attendibili sono un intero dominio (ad esempio, @contoso.com) archiviato nell'elenco Mittenti attendibili di un utente. Per impostazione predefinita, l'agente filtro contenuti non usa dati di domini attendibili per identificare i mittenti a cui è consentito ignorare il filtro contenuti.

Questa impostazione predefinita consente di ridurre la quantità di posta indesiderata inviata all'organizzazione. Ad esempio, un utente può aggiungere il dominio di un provider di posta elettronica di grandi dimensioni all'elenco Mittenti attendibili. Se il dominio viene utilizzato di frequente o è soggetto a spoofing da spammer e il filtro contenuti è configurato per l'uso di dati attendibili del dominio per contrassegnare i messaggi come sicuri, i messaggi provenienti da un mittente in quel dominio verranno recapitati ai destinatari dell'organizzazione.

Si consiglia di non modificare l'impostazione predefinita nella maggior parte dei casi. Tuttavia, è possibile configurare i dati dei domini attendibili degli utenti da archiviare in Active Directory e utilizzati dal filtro contenuti per contrassegnare i messaggi come sicuri. A questo scopo, è necessario modificare i file di configurazione dell'applicazione XML MSExchangeMailboxAssistants.exe.config associati al servizio Assistenti cassette postali di Microsoft Exchange come spiegato più avanti in questo argomento. Quando si apporta tale modifica di configurazione, i dati dei domini attendibili con hash e archiviati nell'attributo oggetto utente **msExchSafeSenderHash** dell'utente in Active Directory come parte dell'aggregazione di elenchi di indirizzi attendibili. L'agente filtro contenuti può quindi usare i dati dei domini attendibili per contrassegnare i messaggi dei mittenti di questi domini come sicuri. Per ulteriori informazioni sull'aggregazione degli elenchi indirizzi attendibili, vedere [Aggregazione dell'elenco indirizzi attendibili](safelist-aggregation-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - Le autorizzazioni di Exchange non sono applicabili alle procedure descritte in questo argomento. Queste procedure vengono eseguite nel sistema operativo del server di Exchange.

  - Le modifiche apportate al file MSExchangeMailboxAssistants.exe.config hanno effetto dopo il riavvio del servizio Assistenti cassette postali di Microsoft Exchange.

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare un prompt dei comandi per configurare il filtro contenuti per usare dati dei domini attendibili

1.  In una finestra del prompt dei comandi, aprire il file MSExchangeMailboxAssistants.exe.config in Blocco note utilizzando il seguente comando:
    
    ```powershell
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config
    ```

2.  Posizionare la chiave *\</appsettings\>* alla fine del file e incollare la chiave seguente prima della chiave *\</appsettings\>*:
    
    ```command line
        <add key="IncludeSafeDomains" value="true" />
    ```

3.  Al termine, salvare e chiudere il file MSExchangeMailboxAssistants.exe.config.

4.  Riavviare il servizio Assistenti cassette postali di Microsoft Exchange utilizzando il seguente comando:
    ```powershell
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants
    ```
    
## Come verificare se l'operazione ha avuto esito positivo

Per verificare la configurazione del filtro contenuti per usare dati dei domini attendibili, effettuare le seguenti operazioni:

1.  Verificare che l'aggiunta di un dominio all'elenco Mittenti attendibili dell'utente in Outlook aggiorni l'attributo **msExchSafeSenderHash** dell'utente in Active Directory. A questo scopo, visualizzare l'attributo in ADSIEdit.exe o LDP.exe, aprire la cassetta postale dell'utente in Outlook, aggiungere un dominio all'elenco Mittenti attendibili, eseguire il comando `Update-Safelist <username>` e verificare che i valori originali e correnti di **msExchSafeSenderHash** siano diversi.

2.  Dopo aver verificato che i dati dei domini attendibili sono memorizzati in Active Directory, inviare un messaggio di prova da un mittente esterno al dominio a un utente dell'organizzazione. Verificare che il messaggio sia contrassegnato come sicuro esaminando i campi di intestazione della posta indesiderata nell'intestazione del messaggio.

