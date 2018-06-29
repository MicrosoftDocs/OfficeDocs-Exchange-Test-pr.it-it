---
title: 'Conversione di una cassetta postale: Exchange 2013 Help'
TOCTitle: Conversione di una cassetta postale
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 50481867
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conversione di una cassetta postale

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-04-26_

La procedura di conversione di una cassetta postale in una tipologia differente è molto simile a quella prevista per Exchange 2010. È comunque necessario utilizzare il cmdlet Set-Mailbox in Shell per eseguire la conversione.

È possibile convertire le seguenti cassette postali da una tipologia all'altra:

  - Da cassetta postale utente a cassetta postale delle risorse (attrezzatura o della sala)

  - Da cassetta postale condivisa a cassetta postale utente

  - Da cassetta postale condivisa a cassetta postale per la risorsa

  - Da cassetta postale per la risorsa a cassetta postale utente

  - Da cassetta postale per la risorsa a cassetta postale condivisa

Se l'organizzazione utilizza un ambiente Exchange ibrido, è necessario gestire le cassette postali tramite gli strumenti di gestione di Exchange locali. Per convertire una cassetta postale in un ambiente ibrido, potrebbe essere necessario spostare la cassetta postale di nuovo in Exchange locale, convertire il tipo di cassetta postale e quindi rispostarla in Office 365.


> [!IMPORTANT]
> Se si converte una cassetta postale utente in una cassetta postale condivisa, è necessario rimuovere i dispositivi mobili dalla cassetta postale prima della conversione oppure è necessario bloccare l'accesso mobile alla cassetta postale dopo la conversione. Infatti, una volta che la cassetta postale viene convertita in una cassetta postale condivisa, le funzionalità mobili non funzioneranno correttamente. Per ulteriori informazioni sul blocco dell'accesso, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=847873">Rimuovere un ex dipendente da Office 365</A>.



## Conversione di una cassetta postale tramite Shell

Tempo stimato per il completamento: 5 minuti.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

In questo esempio la cassetta postale condivisa MarketingDept1 viene convertita in una cassetta postale dell'utente.

    Set-Mailbox MarketingDept1 -Type Regular

Per il parametro *Type* è possibile utilizzare i seguenti valori:

  - Regolare

  - Room

  - Equipment

  - Condivisa

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la cassetta postale sia stata convertita correttamente, eseguire il comando della shell riportato di seguito:

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

Il valore di *RecipientTypeDetails* deve essere *UserMailbox*.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


