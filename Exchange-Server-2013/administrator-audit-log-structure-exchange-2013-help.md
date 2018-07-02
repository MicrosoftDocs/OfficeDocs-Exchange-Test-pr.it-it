---
title: 'Struttura del Registro di controllo amministratore: Exchange 2013 Help'
TOCTitle: Struttura del Registro di controllo amministratore
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50555620
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Struttura del Registro di controllo amministratore

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

I registri di controllo dell'amministratore contengono un record di tutti i cmdlet e parametri eseguiti in Exchange Management Shell e dall'interfaccia di amministrazione di Exchange (EAC). Vengono creati su richiesta quando si esegue il report del registro di controllo dell'amministratore nell'interfaccia di amministrazione di Exchange o quando si esegue il cmdlet **New-AdminAuditLogSearch** nella shell. Per ulteriori informazioni sui registri di controllo, vedere [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md).

I registri di controllo sono file XML e possono contenere più voci. Nella tabella seguente viene descritto ciascun tag XML con gli attributi ad esso associati.

Per informazioni sulle attività di gestione relative ai registri di controllo dell'amministratore? vedere [Amministratore di gestire la registrazione di controllo](manage-administrator-audit-logging-exchange-2013-help.md).

### Tag XML e attributi per il registro di controllo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Attributo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Questo è il tag di dichiarazione del documento XML. È incluso in ciascun registro di controllo e contiene il numero della versione XML e il valore per la codifica dei caratteri.</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Questo tag contiene tutte le voci del registro di controllo nel file XML. Il tag <code>Event</code> è un elemento secondario di questo tag.</p>
<p>È presente un solo tag <code>SearchResults</code> in ogni file XML.</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p><code> </code></p></td>
<td><p>Questo tag contiene la voce del registro di controllo per un singolo cmdlet. Il tag contiene gli attributi <code>Caller</code>,<code>Cmdlet</code>,<code>ObjectModified</code>,<code>RunDate</code>,<code>Succeeded</code>, <code>Error</code> e <code>OriginatingServer</code>. I tag <code>CmdletParameters</code> e <code>ModifiedProperties</code> sono elementi secondari di questo tag.</p>
<p>È presente un tag <code>Event</code> per ogni voce di registro di controllo.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Caller</code></p></td>
<td><p>Questo attributo contiene l'account dell'utente che ha eseguito il cmdlet nell'attributo <code>Cmdlet</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>Questo attributo contiene il nome del cmdlet eseguito dall'utente nell'attributo <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>Questo attributo contiene l'oggetto modificato dal cmdlet specificato nell'attributo <code>Cmdlet</code>. Il tag <code>ModifiedProperties</code> mostra le proprietà che sono state modificate in questo oggetto.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>Questo attributo contiene data e ora di esecuzione del cmdlet nell'attributo <code>Cmdlet</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>Questo attributo specifica se l'esecuzione del cmdlet nell'attributo <code>Cmdlet</code> è stata completata correttamente. Il valore è <code>True</code> o <code>False</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Error</code></p></td>
<td><p>Questo attributo contiene il messaggio di errore generato se l'esecuzione del cmdlet nell'attributo <code>Cmdlet</code> non viene completata correttamente. Se non si è verificato alcun errore, il valore è impostato su <code>None</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>Questo attributo contiene il server su cui è stato eseguito il cmdlet specificato nell'attributo <code>Cmdlet</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Questo tag contiene tutti i parametri specificati per l'esecuzione del cmdlet. Il tag <code>Parameter</code> è un elemento secondario del tag.</p>
<p>C'è un tag <code>CmdletParameters</code> per il tag <code>Event</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p><code> </code></p></td>
<td><p>Questo tag contiene un singolo parametro specificato per l'esecuzione del cmdlet. Questo tag contiene gli attributi <code>Name</code> e <code>Value</code>.</p>
<p>Possono esserci più tag <code>Parameter</code> per il tag <code>CmdletParameters</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>Questo attributo contiene il nome del parametro specificato per il cmdlet eseguito.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Value</code></p></td>
<td><p>Questo attributo contiene il valore fornito per il parametro specificato nell'attributo <code>Name</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Questo tag contiene tutte le proprietà modificate dal cmdlet eseguito. Il tag <code>Property</code> è un elemento secondario di questo tag.</p>
<p>C'è un tag <code>ModifiedProperties</code> per il tag <code>Event</code>.</p>

> [!IMPORTANT]
> Il tag viene popolato solo se il parametro <EM>LogLevel</EM> del cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> è impostato su <CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p><code> </code></p></td>
<td><p>Questo tag contiene una singola proprietà specificata per l'esecuzione del cmdlet. Questo tag contiene gli attributi <code>Name</code>, <code>OldValue</code> e <code>NewValue</code>.</p>
<p>Possono esserci più tag <code>Property</code> per il tag <code>ModifiedProperties</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>Questo attributo contiene il nome della proprietà modificata quando il cmdlet è stato eseguito.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>Questo attributo contiene il vecchio valore della proprietà specificata nell'attributo <code>Name</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>Questo attributo contiene il nuovo valore della proprietà nell'attributo <code>Name</code>.</p></td>
</tr>
</tbody>
</table>


## Esempio di una voce del registro di controllo

Di seguito è riportato un esempio di voce standard del registro di controllo. Dalle informazioni contenute nella voce del registro risulta che:

  - Il 18.10.12 alle 23:59 ora legale Pacifico (UTC-7), l'utente `Administrator` ha eseguito il cmdlet **Set-Mailbox**.

  - Per l'esecuzione del cmdlet **Set-Mailbox**, sono stati forniti i seguenti due parametri:
    
      - *Identity* con valore `david`
    
      - *ProhibitSendReceiveQuota* con valore `10GB`

  - Sono state modificate le due seguenti proprietà dell' oggetto `david`:
    

    > [!NOTE]
    > In questo esempio, le proprietà modificate vengono salvate nel registro di controllo perché il parametro <EM>LogLevel</EM> del cmdlet <CODE>Set-AdminAuditLogConfig</CODE> è stato impostato su <CODE>Verbose</CODE>.

    
      - A *ProhibitSendReceiveQuota* è stato assegnato il nuovo valore `10GB` che sostituisce il precedente (`35GB`)

  - L'operazione è stata completata senza errori.

<!-- end list -->

    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>

