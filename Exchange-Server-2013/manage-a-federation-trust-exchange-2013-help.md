---
title: 'Gestire una relazione di trust federativa: Exchange 2013 Help'
TOCTitle: Gestire una relazione di trust federativa
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50479923
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire una relazione di trust federativa

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-01_

Una relazione di trust federativa stabilisce una relazione di trust tra un'organizzazione di Exchange 2013 Microsoft e il sistema di autenticazione Azure Active Directory e supporta la condivisione federata con altre organizzazioni Exchange federate. In genere, non è necessario gestire o modificare la relazione di trust federativa dopo averlo creato. Tuttavia, può essere situazioni che richiedono l'aggiunta o rimozione dei domini federati o reimpostare il dominio utilizzato per configurare l'identificatore di organizzazione (OrgID) per la relazione di trust federativa.


> [!NOTE]
> La modifica di una relazione di trust federativa esistente, soprattutto il dominio condiviso primario utilizzato per definire l'OrgID, può interrompere la condivisione federata tra organizzazioni di Exchange federate o per le distribuzioni ibride con organizzazioni di Office 365.



Per altre attività di gestione relative alla federazione, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 30 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Autorizzazioni *Federation and certificates* nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Sarà necessario aggiungere un record TXT al proprio DNS pubblico per tutti i nuovi domini federati aggiunti alla relazione di trust federativa. Rivedere i requisiti per l'aggiunta di un record TXT con l'organizzazione che ospita i record DNS pubblici.

  - Ai fini di questo argomento, è stata configurata una relazione di trust federativa con le seguenti impostazioni:
    
      - **Contoso.com** è il dominio condiviso primario per la relazione di trust federativa. (questo dominio non verrà modificato.)
    
      - I domini federati **service.contoso.com** e **sales.contoso.com** sono inclusi nella relazione di trust federativa esistente.
    
      - **Marketing.contoso.com** è un dominio accettato nell'organizzazione di Exchange.

  - In questo argomento, vengono trattate anche altre attività di gestione federative, quali la visualizzazione e la gestione dei certificati utilizzati per la relazione di trust federativa e la visualizzazione delle informazioni sui parametri della relazione di trust federativa in Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Gestione di una relazione di trust federativa tramite Interfaccia di amministrazione di Exchange

1.  Su un server Exchange 2013 nell'organizzazione locale, andare a **Organizzazione** \> **Condivisione**.

2.  Nella sezione **Relazione di trust federativa**, fare clic su **Modifica**.

3.  In **Domini abilitati alla condivisione**, saltare **Passo 1** in quanto il dominio di condivisione primario non viene modificato.

4.  In **Passo 2**, selezionare il dominio **service.contoso.com**, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per rimuovere il dominio dalla relazione di trust federativa.

5.  In **Passo 2**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

6.  In **Seleziona domini accettati**, selezionare **marketing.contoso.com** dall'elenco dei domini accettati, quindi fare clic su **OK** per aggiungere il dominio alla relazione di trust federativa.
    

    > [!IMPORTANT]
    > Verrà creata una stringa di prova del dominio federato per il dominio <STRONG>marketing.contoso.com</STRONG>. È necessario creare un record TXT distinto sul DNS pubblico per questo dominio.



7.  Utilizzando la stringa di prova del dominio federato creata per il dominio **marketing.contoso.com**, creare un record TXT sul server DNS pubblico. A seconda del piano di aggiornamenti dell'host DNS pubblico, la replica delle modifiche DNS può richiedere 15 minuti o più.

8.  Una volta creato e replicato il record TXT, fare clic su **Aggiorna**.

## Gestione di una relazione di trust federativa tramite Shell

1.  In questo esempio, viene rimosso il dominio service.contoso.com dalla relazione di trust federativa.
    
    ```powershell
Remove-FederatedDomain -DomainName service.contoso.com
```

2.  In questo esempio, viene aggiunto il dominio marketing.contoso.com alla relazione di trust federativa esistente.
    
    ```powershell
Add-FederatedDomain -DomainName marketing.contoso.com
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-FederatedDomain](https://technet.microsoft.com/it-it/library/dd298128\(v=exchg.150\)) e [Add-FederatedDomain](https://technet.microsoft.com/it-it/library/dd351208\(v=exchg.150\)).

Eseguire i seguenti comandi Shell per gestire altri aspetti di una relazione di trust federativa.

1.  **Visualizzazione dell'OrgID federato e dei domini federati**
    
    In questo esempio, vengono visualizzati l'OrgID federato di un'organizzazione di Exchange e le relative informazioni, inclusi lo stato e i domini federati.
    
    ```powershell
Get-FederatedOrganizationIdentifier
```

2.  **Visualizzazione dei certificati della relazione di trust federativa**
    
    In questo esempio vengono visualizzati i certificati precedente, corrente e successivo utilizzati dalla relazione di trust federativa "autenticazione Azure AD".
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **Controllo dello stato dei certificati federativi**
    
    In questo esempio, viene visualizzato lo stato dei certificati federativi su tutti i server Cassette postali e Accesso client dell'organizzazione.
    
    ```powershell
Test-FederationTrustCertificate
```

4.  **Configurazione della relazione di trust federativa per utilizzare un certificato come certificato successivo**
    
    In questo esempio viene configurata la relazione di trust federativa "autenticazione Azure AD" per utilizzare il certificato con l'identificazione personale fornita come certificato successivo. Una volta distribuito il certificato in tutti i server di Exchange all'interno dell'organizzazione, è possibile utilizzare l'opzione *PublishCertificate* per configurare la relazione di trust federativa che consente di utilizzare questo certificato come certificato corrente.
    
    ```powershell
Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17
```

5.  **Configurazione della relazione di trust federativa per utilizzare il certificato successivo come certificato corrente**
    
    In questo esempio consente di configurare l'autenticazione di protezione Azure Active Directory federation per utilizzare il certificato successivo come certificato corrente e pubblicarlo nel sistema di autenticazione Azure AD.
    
    ```powershell
Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
```
    

    > [!WARNING]
    > Prima di configurare la relazione di trust federativa per poter utilizzare il certificato successivo come certificato federativo corrente, assicurarsi che il certificato sia distribuito in tutti i server di Exchange dell'organizzazione. Utilizzare il cmdlet <A href="https://technet.microsoft.com/it-it/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</A> per controllare lo stato di distribuzione del certificato.



6.  **Aggiornamento dei metadati di federazione e il certificato dal sistema di autenticazione Azure AD**
    
    Questo esempio vengono aggiornati i metadati di federazione e il certificato del sistema di autenticazione Azure AD per l'autenticazione di Azure Active Directory federation trust.
    
    ```powershell
Set-FederationTrust "Azure AD authentication" -RefreshMetadata
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/it-it/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/it-it/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/it-it/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/it-it/library/dd298034\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo

Il corretto completamento della procedura guidata **Domini abilitati alla condivisione** è il primo segnale del fatto che la relazione di trust federativa è stata configurata come previsto.

Per un ulteriore verifica, effettuare le seguenti operazioni:

1.  Eseguire questo comando Shell per verificare le informazioni di attendibilità del trust federativo.
    
    ```powershell
Get-FederationTrust | format-list
```

2.  Eseguire questo comando Shell per verificare che le informazioni sulla Federazione possano essere recuperate dalla propria organizzazione. Ad esempio, verificare che i domini sales.contoso.com e marketing.contoso.com vengano restituiti nel parametro *DomainNames*.
    
    ```powershell
Get-FederationInformation -DomainName <your primary sharing domain>
```


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


