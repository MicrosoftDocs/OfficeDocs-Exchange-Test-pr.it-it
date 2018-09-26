---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518124
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**Ultima modifica dell'argomento:** 2018-01-17_

**Sintesi:**  Informazioni sulle cassette postali di arbitrato in Exchange 2013 e su come ricrearle.

Exchange 2013 include cinque cassette postali di sistema chiamate *cassette postali di arbitrato*. Le cassette postali di arbitrato vengono usate per l'archiviazione di diversi tipi di dati di sistema e per la gestione del flusso di lavoro di approvazione dei messaggi. Nel seguente grafico viene elencato ogni tipo di cassetta postale di arbitrato con le rispettive responsabilità.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome della cassetta postale di arbitrato</th>
<th>Nome visualizzato</th>
<th>Capacità persistenti</th>
<th>Funzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Cassetta postale federata di Microsoft Exchange</p></td>
<td><p>{}</p></td>
<td><p>Questa cassetta postale consente di archiviare i dati usati per gestire la federazione tra organizzazioni di Exchange diverse. Include Rights Management Services, probe di monitoraggio e risposte sul flusso di posta cross-premise, notifiche, archivi online, gestione dei record di messaggistica e informazioni sulla disponibilità cross-premise.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Approvazione guidata di Microsoft Exchange</p></td>
<td><p>{}</p></td>
<td><p>Questa cassetta postale viene fornita per l'utilizzo da parte del framework di approvazione di Exchange per la moderazione dei destinatari e le richieste di approvazione per i gruppi automatiche.</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Migrazione di Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>Consente di archiviare i dati per il servizio di migrazione di Exchange da utilizzare durante lo spostamento di cassette postali in batch.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>Cassetta postale del sistema Discovery.</p>
<p>Fornita per l'utilizzo da parte della funzionalità e-Discovery, usata dai responsabili della conformità per individuare i messaggi che corrispondono a specifici criteri selezionati. Questa cassetta postale viene usata, inoltre, da Messaggistica unificata per archiviare i file presenti nella console di Messaggistica unificata e altre informazioni.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>Questa è nota come cassetta postale dell'organizzazione. Viene usata per creare le rubriche offline (OAB). Per il bilanciamento del carico della creazione di OAB nell'organizzazione, compresi i siti di località geografiche separate, è possibile creare ulteriori cassette postali dell'organizzazione.</p></td>
</tr>
</tbody>
</table>


Se è necessario ricreare una o più di queste cassette postali di arbitrato, vedere le istruzioni seguenti.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti per ogni procedura.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Ricreazione di una cassetta postale di arbitrato tramite Exchange Management Shell

Usare le istruzioni seguenti per ricreare un determinato tipo di cassetta postale di arbitrato.


> [!NOTE]
> Tutte le procedure illustrate nelle sezioni seguenti devono essere eseguite dalla stessa directory in cui è stato estratto il supporto di installazione di Exchange.



## Ricreare la cassetta postale federata di Microsoft Exchange

Per ricreare la cassetta postale di arbitrato FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042:

1.  Se non sono presenti delle cassette postali di arbitrato, eseguire il comando seguente:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  In Exchange Management Shell, eseguire le operazioni seguenti:
    
    ```powershell
        Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"
    ```

## Ricreare la cassetta postale Approvazione guidata di Microsoft Exchange

Per ricreare la cassetta postale di arbitrato SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}:

1.  Se non sono presenti delle cassette postali di arbitrato, eseguire il comando seguente:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  In Exchange Management Shell, eseguire le operazioni seguenti:
    ```powershell
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration
    ```

## Ricreare la cassetta postale Migrazione di Microsoft Exchange

Per ricreare la cassetta postale di arbitrato Migration.8f3e7716-2011-43e4-96b1-aba62d229136:

1.  Se non sono presenti delle cassette postali di arbitrato, eseguire il comando seguente:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  In Exchange Management Shell, eseguire le operazioni seguenti:
    
    ```powershell
        Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"
    ```

3.  In Exchange Management Shell, impostare le capacità persistenti (msExchCapabilityIdentifiers) eseguendo il comando seguente:
    
    ```powershell
        Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force
    ```

## Ricreare la cassetta postale del sistema Discovery di Microsoft Exchange

Per ricreare la cassetta postale di arbitrato SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}:

1.  Eseguire il comando seguente:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

## Ricreare la cassetta postale dell'organizzazione di Microsoft Exchange per rubriche offline

Per ricreare la cassetta postale SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}:

1.  Se non sono presenti delle cassette postali di arbitrato, eseguire il comando seguente:
    
    ```powershell
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms
    ```

2.  In Exchange Management Shell, eseguire le operazioni seguenti:
    
    ```powershell
        Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"
    ```

3.  In Exchange Management Shell, impostare le capacità persistenti (msExchCapabilityIdentifiers) eseguendo il comando seguente:
    ```powershell
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force
    ```
Al termine, eseguendo il comando `$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers` si vedrà che 46, 47 e 51 non sono presenti. Eseguire il comando seguente per riaggiungere tutte le funzionalità:
    ```powershell
        Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}
    ```
## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente ricreato la cassetta postale di arbitratoe, utilizzare il cmdlet **Get-Mailbox** con l'opzione *Arbitration* per visualizzare le cassette postali del sistema.

```powershell
Get-Mailbox -Arbitration | Format-Table Name, DisplayName
```

Visualizzare i risultati del comando per verificare che sia stata creata la cassetta postale di sistema appropriata, cercando tramite Nome o Nome visualizzato nella tabella di cui sopra.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


