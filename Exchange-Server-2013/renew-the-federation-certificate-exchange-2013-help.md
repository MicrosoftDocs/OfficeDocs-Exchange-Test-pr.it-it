---
title: 'Rinnovare il certificato di federazione: Exchange 2013 Help'
TOCTitle: Rinnovare il certificato di federazione
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429172
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rinnovare il certificato di federazione

 

_**Ultima modifica dell'argomento:** 2017-02-28_

In questo argomento viene spiegato come aggiornare il certificato di federazione autofirmato utilizzato in un trust federativo:

  - Se il certificato di federazione non è scaduto, seguire i passaggi nella sezione Aggiornare un certificato di federazione funzionante.

  - Se il certificato di federazione è già scaduto, seguire la procedura descritta nella sezione Sostituire un certificato di federazione scaduto.

Per ulteriori informazioni sulle relazioni di trust federativo e sulla federazione, vedere [Federazione](federation-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Federazione e certificati" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Le procedure descritte in questo argomento utilizzano Exchange Management Shell. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per verificare se il certificato di federazione esistente è scaduto, eseguire il comando in Exchange Management Shell:
    ```powershell
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter
    ```
  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Aggiornare un certificato di federazione funzionante

Se il certificato di federazione non è scaduto, è possibile aggiornare la relazione di trust federativa esistente con un nuovo certificato di federazione.

## Passaggio 1: creare un nuovo certificato di federazione

Eseguire il comando seguente in Exchange Management Shell per creare un nuovo certificato di federazione:
```powershell
    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true
```
Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-ExchangeCertificate](https://technet.microsoft.com/it-it/library/aa998327\(v=exchg.150\)).

L'output del comando contiene il valore di identificazione personale del nuovo certificato. Questo valore è necessario nei passaggi rimanenti ed è possibile copiare il valore direttamente dalla finestra Exchange Management Shell:

1.  Fare clic in qualsiasi punto della finestra Exchange Management Shell e selezionare **Contrassegna** nella finestra di dialogo che viene visualizzata.

2.  Selezionare il valore di identificazione personale, quindi premere INVIO.

Per le altre procedure dell'argomento, viene usato il valore di identificazione personale del certificato di federazione: `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`. Il valore di identificazione personale del certificato del certificato sarà differente.

## Passaggio 2: configurare il nuovo certificato come certificato di federazione

Per utilizzare Exchange Management Shell per configurare il nuovo certificato come certificato di federazione, utilizzare la sintassi seguente:
```powershell
    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData
```
In questo esempio, il valore `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73` di identificazione personale del certificato dal passaggio 1.
```powershell
    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-FederationTrust](https://technet.microsoft.com/it-it/library/dd298034\(v=exchg.150\)).

**Nota:**  l'output del comando include un messaggio di avviso in cui viene comunicata la necessità di aggiornare la prova del record TXT relativo alla proprietà del dominio in DNS. Questa operazione viene effettuata nel prossimo passaggio.

## Passaggio 3: aggiornare la prova di federazione del record TXT relativo alla proprietà del dominio in DNS

È possibile eseguire in modo sicuro questo passaggio, dal momento che la prova del record TXT relativa alla proprietà del dominio viene verificata durante l'attivazione (passaggio 5). Tuttavia, dopo aver aggiornato il record TXT e prima di continuare con il passaggio successivo, è necessario dedicare del tempo all'upload del record TXT per propagare (in base alla durata o al valore TTL del record DNS).

1.  Trovare i valori richiesti per ogni record TXT necessario eseguendo il comando seguente in Exchange Management Shell:
    
    ```powershell
    Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
    ```
    
    Ad esempio, se il dominio federato è contoso.com, eseguire il comando seguente:
    
    ```powershell
    Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
    ```
    
    L'output del comando avrà questo aspetto:
    
    `Thumbprint : <new certificate thumbprint>` (ad esempio, `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`)
    
    `Proof      : <new hash text>` (ad esempio, `znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`)
    
    `Thumbprint : <old certificate thumbprint>` (ad esempio, `CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`)
    
    `Proof      : <old hash text>` (ad esempio, `m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`)
    
    Tenere presente che l'output del comando restituisce informazioni per due record di attestazione della proprietà del dominio: uno per il nuovo certificato e uno per il certificato corrente in fase di sostituzione. È possibile distinguerli tramite il valore di identificazione personale e dal valore del testo hash configurato nell'attuale record TXT di attestazione della proprietà del dominio nel DNS esterno (pubblico).

2.  Aggiornare la prova di federazione del record TXT relativo alla proprietà del dominio in DNS. Le istruzioni variano in base al provider DNS, ma è possibile modificare il record TXT corrente al fine di sostituire il valore di testo hash attuale con quello nuovo. Per ulteriori informazioni, vedere la sezione Exchange Online nell'articolo [Record DNS (Domain Name System) esterni per Office 365](https://go.microsoft.com/fwlink/p/?linkid=265522).

## Passaggio 4: verificare la distribuzione del nuovo certificato di federazione su tutti i server di Exchange

Exchange distribuisce automaticamente il nuovo certificato di federazione su tutti i server, ma è necessario verificare la distribuzione prima di procedere.

Per utilizzare Exchange Management Shell al fine di verificare la distribuzione del nuovo certificato di federazione, eseguire il comando seguente:
```powershell
    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject
```
**Nota:**  in Exchange 2010, l'output del cmdlet **Test-FederationCertificate** contiene i nomi dei server. L'output del cmdlet in Exchange 2013 o nelle versione successive non include i nomi dei server.

## Passaggio 5: attivare il nuovo certificato di federazione

Per utilizzare Exchange Management Shell al fine di attivare il nuovo certificato di federazione, eseguire il comando seguente:

```powershell
Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-FederationTrust](https://technet.microsoft.com/it-it/library/dd298034\(v=exchg.150\)).

**Nota:**  l'output del comando include un messaggio di avviso in cui viene comunicata la necessità di aggiornare la prova del record TXT relativo alla proprietà del dominio in DNS (operazione già eseguita al passaggio 3).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la relazione di trust federativa esistente sia stata aggiornata correttamente, utilizzare i passaggi seguenti:

  - In Exchange Management Shell, eseguire il comando riportato di seguito per verificare che venga usato il nuovo certificato:
    ```powershell
        Get-FederationTrust | Format-List *priv*
    ```
      - La proprietà **OrgPrivCertificate** deve includere l'identificazione personale del nuovo certificato di federazione.
    
      - La proprietà **OrgPrevPrivCertificate** deve includere l'identificazione personale del precedente (sostituito) certificato di federazione.

  - In Exchange Management Shell, sostituire *\<user's email address\>* con l'indirizzo e-mail dell'utente della propria organizzazione, quindi eseguire il comando seguente per verificare che la relazione di trust federativa sia funzionante:
    
    ```powershell
    Test-FederationTrust -UserIdentity <user's email address>
    ```

## Sostituire un certificato di federazione scaduto

Se il certificato di federazione è già scaduto, è necessario rimuovere tutti i domini federati dalla relazione di trust federativa, quindi rimuovere e creare di nuovo la relazione di trust federativa.

1.  Se si dispongono più domini federati, è necessario identificare il dominio condiviso principale in modo da rimuoverlo per ultimo. Per utilizzare Exchange Management Shell al fine di identificare il dominio federato principale e tutti i domini federati, eseguire il comando seguente:
    
    ```powershell
        Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
    ```
    
    Il valore della proprietà **AccountNamespace** include il dominio condiviso principale nel formato `FYDIBOHF25SPDLT<primary shared domain>`. Ad esempio, nel valore `FYDIBOHF25SPDLT.contoso.com`, contoso.com è il dominio condiviso principale.

2.  Rimuovere ogni dominio federato che non è nel dominio condiviso principale eseguendo il comando seguente in Exchange Management Shell:
    
    ```powershell
        Remove-FederatedDomain -DomainName <domain> -Force
    ```

3.  Dopo aver rimosso tutti gli altri domini federati, eliminare il dominio condiviso principale eseguendo il comando seguente in Exchange Management Shell:
    
    ```powershell
        Remove-FederatedDomain -DomainName <domain> -Force
    ```

4.  Rimuovere la relazione di trust federativa eseguendo il comando seguente in Exchange Management Shell:
    
    ```powershell
        Remove-FederationTrust "Microsoft Federation Gateway"
    ```

5.  Creare di nuovo la relazione di trust federativa. Per istruzioni, vedere [Creazione di una relazione di trust federativa](https://technet.microsoft.com/it-it/library/dd335198\(v=exchg.150\)).

