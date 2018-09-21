---
title: 'Modifica delle proprietà multivalore: Exchange 2013 Help'
TOCTitle: Modifica delle proprietà multivalore
ms:assetid: dc2c1062-ad79-404b-8da3-5b5798dbb73b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb684908(v=EXCHG.150)
ms:contentKeyID: 50481847
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifica delle proprietà multivalore

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Una proprietà multivalore è una proprietà che può contenere più valori. Ad esempio, la proprietà **BlockedRecipients** dell'oggetto **RecipientFilterConfig** può accettare più indirizzi di destinatari come nei seguenti esempi:

  - john@contoso.com

  - kim@northwindtraders.com

  - david@adatum.com

Dato che la proprietà **BlockedRecipients** può accettare più valori, viene definita proprietà multivalore. In questo argomento viene descritto come utilizzare Exchange Management Shell per aggiungere e rimuovere valori da una proprietà multivalore di un oggetto.

Per ulteriori informazioni sugli oggetti, vedere [Dati strutturati](https://technet.microsoft.com/it-it/library/aa996386\(v=exchg.150\)). Per ulteriori informazioni sulla shell, vedere [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)).

## Confronto tra la modifica di una proprietà multivalore e la modifica di una proprietà che accetta un valore singolo

Il metodo utilizzato per la modifica di una proprietà multivalore è leggermente diverso da quello che consente di modificare una proprietà che accetta un unico valore. Quando si modifica una proprietà che accetta un unico valore, è possibile assegnare un valore direttamente alla proprietà, come nel comando riportato di seguito.

```powershell
Set-TransportConfig -MaxSendSize 12MB
```

Quando si utilizza questo comando per fornire un nuovo valore alla proprietà **MaxSendSize**, il valore archiviato viene sovrascritto. Ciò non costituisce un problema con le proprietà che accettano un unico valore. Tuttavia, la situazione diventa problematica nel caso di proprietà multivalore. Si supponga ad esempio che la proprietà **BlockedRecipients** dell'oggetto **RecipientFilterConfig** sia configurata in modo da assumere i tre valori indicati nella sezione precedente. Quando si esegue il comando `Get-RecipientFilterConfig | Format-List BlockedRecipients`, vengono visualizzate le seguenti informazioni.

```powershell
BlockedRecipients : {david@adatum.com, kim@northwindtraders.com, john@contoso.com}
```

Si supponga ora di aver ricevuto una richiesta per aggiungere un nuovo indirizzo SMTP all'elenco dei destinatari bloccati. Per aggiungere il nuovo indirizzo SMTP, viene eseguito il comando riportato di seguito.

```powershell
Set-RecipientFilterConfig -BlockedRecipients chris@contoso.com
```

Quando si esegue nuovamente il comando `Get-RecipientFilterConfig | Format-List BlockedRecipients`, vengono visualizzate le seguenti informazioni.

```powershell
BlockedRecipients : {chris@contoso.com}
```

Pertanto, non si ottengono i risultati previsti. Si desiderava aggiungere il nuovo indirizzo SMTP all'elenco di destinatari bloccati esistente, mentre invece tale elenco è stato sovrascritto dal nuovo indirizzo SMTP. Questo risultato imprevisto dimostra che la modifica di una proprietà multivalore è diversa dalla modifica di una proprietà che accetta un singolo valore. Quando si modifica una proprietà multivalore, è necessario accertarsi di aggiungere o rimuovere valori anziché sovrascrivere l'intero elenco di valori esistente. Nelle seguenti sezioni viene descritto come ottenere i risultati desiderati.

## Modifica delle proprietà multivalore

La modifica delle proprietà multivalore è simile alla modifica delle proprietà a valore singolo. È sufficiente aggiungere alcune informazioni per indicare che si desidera aggiungere o rimuovere valori nella proprietà multivalore, anziché sostituire l'intero contenuto della proprietà. Tale sintassi viene inclusa, insieme ai valori da aggiungere o rimuovere nella proprietà, sotto forma di valore di un parametro quando si esegue un cmdlet. La sintassi da aggiungere a un parametro di un cmdlet per modificare una proprietà multivalore è riportata nella tabella seguente.

### Sintassi per le proprietà multivalore

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Sintassi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aggiungere uno o più valori a una proprietà multivalore</p></td>
<td><pre><code>@{Add=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Rimuovere uno o più valori da una proprietà multivalore</p></td>
<td><pre><code>@{Remove=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
</tbody>
</table>


La sintassi scelta nella tabella Sintassi per le proprietà multivalore è specificata come valore di un parametro per un cmdlet. Il comando che segue, ad esempio, aggiunge più valori a una proprietà multivalore:

```powershell
Set-ExampleCmdlet -Parameter @{Add="Red", "Blue", "Green"}
```

Quando si utilizzata tale sintassi, i valori specificati vengono aggiunti o rimossi nell'elenco dei valori già presenti nella proprietà. Nel caso del precedente esempio relativo a **BlockedRecipients**, è possibile aggiungere il valore chris@contoso.com senza sovrascrivere gli altri valori della proprietà, utilizzando il comando seguente:

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"}
```

Se si desidera rimuovere david@adatum.com dall'elenco dei valori, è necessario utilizzare il comando seguente:

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Remove="david@adatum.com"}
```

È possibile utilizzare combinazioni più complesse, ad esempio per aggiungere e rimuovere contemporaneamente valori da una determinata proprietà. A tale scopo, inserire un punto e virgola (`;`) tra le azioni `Add` e `Remove`. Esempio:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="carter@contoso.com", "sam@northwindtraders.com", "brian@adatum.com"; Remove="john@contoso.com"}

Se si utilizza di nuovo il comando `Get-RecipientFilterConfig | Format-List BlockedRecipients`, è possibile notare che gli indirizzi di posta elettronica per Carter, Sam e Brian sono stati aggiunti, mentre quello per John è stato rimosso.

    BlockedRecipients : {brian@adatum.com, sam@northwindtraders.com, carter@contoso.com, chris@contoso.com, kim@northwindtraders.com}

