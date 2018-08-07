---
title: 'Gestire/risolvere problemi di approvazione del messaggio: Exchange 2013 Help'
TOCTitle: Gestire e risolvere i problemi di approvazione del messaggio
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52063119
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire e risolvere i problemi di approvazione del messaggio

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando si tenta di rimuovere una cassetta postale di arbitraggio, si verifichi l'errore seguente:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Impossibile rimuovere la cassetta postale di arbitraggio &lt;<em>mailbox</em>&gt; perché è in uso per il flusso di lavoro di approvazione per i destinatari esistenti con restrizioni o moderazione abilitato. È consigliabile disattivare le caratteristiche di approvazione nei destinatari o specificare una cassetta postale di arbitraggio diverso per i destinatari dopo la rimozione di questa cassetta postale di arbitraggio.</p></td>
</tr>
</tbody>
</table>


Cassetta postale di arbitraggio consente di gestire il flusso di lavoro di approvazione per i destinatari con moderatore e le approvazioni l'appartenenza al gruppo di distribuzione. Utilizzare PowerShell per trovare tutti i destinatari sono configurati per utilizzare la cassetta postale di arbitraggio. Dopo aver identificato i destinatari, è possibile configurare in modo da utilizzare una cassetta postale di arbitraggio diverso oppure è possibile disabilitare la moderazione del.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Aribtration" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) .

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Passaggio 1: Utilizzare Shell per trovare tutti i destinatari che utilizzano si sta cercando di eliminare la cassetta postale di arbitraggio

Eseguire i comandi seguenti:

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

Ad esempio, per trovare tutti i destinatari che utilizzano la cassetta postale di arbitraggio denominata arbitraggio Mailbox01, eseguire i comandi seguenti:

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}


> [!NOTE]
> Cassetta postale di arbitraggio viene specificata utilizzando il nome distinto (DN). Se si conosce il nome distinto della cassetta postale di arbitraggio, è possibile eseguire il comando singolo: <CODE>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</CODE>.



## Passaggio 2: Utilizzare Shell per specificare una cassetta postale di arbitraggio diversi o disabilitare la moderazione per i destinatari

Per interrompere l'utilizzo cassetta postale di arbitraggio che si sta cercando di eliminare i destinatari con moderatore, è possibile specificare una cassetta postale di arbitraggio diverso oppure è possibile disabilitare la moderazione per i destinatari.

Se si sceglie di specificare una cassetta postale di arbitraggio diverso per i destinatari, eseguire il comando seguente:

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

Ad esempio, per riconfigurare il gruppo di distribuzione denominato tutti i dipendenti di utilizzare la cassetta postale di arbitraggio denominata Mailbox02 arbitraggio per approvazione dell'appartenenza, eseguire il comando seguente:

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

Se si sceglie di disabilitare la moderazione per i destinatari, eseguire il comando seguente:

    Set-<RecipientType> <Identity> -ModerationEanbled $false

Per disabilitare la moderazione per la cassetta postale denominata risorse umane, ad esempio, eseguire il comando seguente:

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## Come verificare se l'operazione ha avuto esito positivo

La procedura sia stata eseguita correttamente se è possibile eliminare la cassetta postale di arbitraggio senza ricevere l'errore viene utilizzato.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

