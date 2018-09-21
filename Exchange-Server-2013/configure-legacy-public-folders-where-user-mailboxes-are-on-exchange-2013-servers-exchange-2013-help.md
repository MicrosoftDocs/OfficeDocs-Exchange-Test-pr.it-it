---
title: 'Config. cart. pub. legacy-cass. post. utenti-Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurazione delle cartelle pubbliche legacy in cui si trovano le cassette postali degli utenti su server Exchange 2013
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281120
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione delle cartelle pubbliche legacy in cui si trovano le cassette postali degli utenti su server Exchange 2013

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2017-03-27_

Come consentire agli utenti di Exchange 2013 oppure Exchange 2016 di accesso Exchange 2010 o cartelle pubbliche precedenti (noto anche come delle cartelle pubbliche legacy).

## Che cosa è necessario sapere prima di iniziare

Gli utenti le cui cassette postali si trovano in Exchange Server 2013 o Exchange Server 2016 non saranno in grado di accedere alle cartelle pubbliche legacy da Outlook Web App, Outlook sul web o Outlook per Mac. I passaggi descritti in questo articolo funzionano sia per 2016 Exchange per Exchange 2013.


> [!NOTE]
> 2016 Outlook per Mac possono accedere alle cartelle pubbliche legacy dopo aver eseguito i passaggi descritti in questo articolo. Se i client nell'organizzazione utilizzano 2016 Outlook per Mac, assicurarsi di che aver installato l'aggiornamento di aprile 2016. In caso contrario, gli utenti non potranno accedere alle cartelle pubbliche in un coesistenza o di una topologia ibrida. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac">Accesso alle cartelle pubbliche con Outlook 2016 per Mac</A>.



## Passaggio 1: Rendere individuabili le cartelle pubbliche di Exchange 2010

1.  Se le cartelle pubbliche in Exchange 2010 server o versioni successive, è necessario installare il ruolo Server accesso Client su tutti i server cassette postali con un database delle cartelle pubbliche. In questo modo il servizio Microsoft Exchange RpcClientAccess sia in esecuzione, che consente di tutti i client di accedere alle cartelle pubbliche. Il ruolo accesso client non è obbligatorio per i server di cartelle pubbliche di Exchange 2007 e questo passaggio non è necessario. Per ulteriori informazioni, vedere [installazione di Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    

    > [!NOTE]
    > Il server non deve essere parte del bilanciamento del carico di Accesso client. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/ff625247(v=exchg.141).aspx">Understanding Load Balancing in Exchange 2010</A>.



2.  Creare un database delle cassette postali vuoto su ogni server di cartelle pubbliche.
    
    Per Exchange 2010, utilizzare il seguente comando. Questo comando esclude il database delle cassette postali dal sistema di bilanciamento del carico di provisioning delle cassette postali. In tal modo si impedisce l'aggiunta automatica di nuove cassette postali a questo database.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    
    Per Exchange 2007, utilizzare il seguente comando:
    
    ```powershell
New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
```
    

    > [!NOTE]
    > L'unica cassetta postale aggiunta a questo database deve essere la cassetta postale proxy creata al passaggio 3. Nessun'altra cassetta postale deve essere creata in questo database delle cassette postali.



3.  Creare una cassetta postale proxy nel nuovo database delle cassette postali e nascondere la cassetta postale dalla rubrica. L'SMTP di questa cassetta postale sarà restituito da Individuazione automatica come SMTP di *DefaultPublicFolderMailbox*, cosicché risolvendo questo SMTP il client può raggiungere il server Exchange legacy per l'accesso alle cartelle pubbliche.
    ```
    New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    ```
    ```
```powershell
Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true
```
    ```

4.  Per Exchange 2010, abilitare Individuazione automatica per la restituzione delle cassette postali delle cartelle pubbliche proxy. Questo passaggio non è necessario per Exchange 2007.
    
    ```powershell
Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>
```

5.  Ripetere la procedura precedente per ogni server di cartelle pubbliche dell'organizzazione.

## Passaggio 2: Configurare le cassette postali degli utenti per l'accesso alle cartelle pubbliche legacy

Il passaggio finale di questa procedura prevede la configurazione delle cassette postali degli utenti per consentire l'accesso alle cartelle pubbliche locali legacy.

Consentire agli utenti locali di Exchange Server 2013 di accedere alle cartelle pubbliche legacy. Puntare a tutte le cassette postali delle cartelle pubbliche proxy create in [Step 2: Make remote public folders discoverable](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders). Lanciare il seguente comando da un server Exchange 2013 con aggiornamento CU5 o successivo.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3


> [!NOTE]
> Per visualizzare le modifiche è necessario attendere che la sincronizzazione di ActiveDirectory sia completa. Questo processo potrebbe richiedere diverse ore.



## Come verificare se l'operazione ha avuto esito positivo?

Accedere ad Outlook per un utente la cui cassetta postale di trova in un server Exchange Server 2013 CU5 o versione successiva ed effettuare le seguenti prove sulle cartelle pubbliche:

1.  Verificare che il client Outlook sia in esecuzione.

2.  Tenere premuto il tasto CTRL, quindi tenere premuto il pulsante destro del mouse sull'icona di Outlook nell'area di notifica sulla destra della barra delle applicazioni di Windows.

3.  Selezionare **Test E-Mail Auto Configuration…**

4.  Accertarsi che lo strumento Text E-mail Auto Configuration restituisca le seguenti informazioni nella scheda XML:
    
      - \<PublicFolderInformation\>
    
      - \<IndirizzoSmtp\>\<Indirizzo SMTP per la cassetta postale delle cartelle pubbliche\</IndirizzoSmtp\>
    
      - \</PublicFolderInformation\>

5.  Nel client Outlook, effettuare le seguenti attività:
    
      - Visualizzare la gerarchia delle cartelle pubbliche
    
      - Controllare le autorizzazioni.
    
      - Creare ed eliminare cartelle pubbliche.
    
      - Pubblicare il contenuto ed eliminare il contenuto da una cartella pubblica.

