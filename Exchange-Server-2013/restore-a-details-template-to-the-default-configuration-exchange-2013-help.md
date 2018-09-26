---
title: 'Ripristina modello dettagli config. predefinita: Exchange 2013 Help'
TOCTitle: Ripristinare un modello di dettagli per la configurazione predefinita
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 50481086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ripristinare un modello di dettagli per la configurazione predefinita

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-12_

L'Editor modelli di informazioni non contiene un pulsante **Annulla** e non è possibile utilizzare i tasti di scelta rapida per annullare un'azione. Per annullare un'aggiunta al modello, utilizzare il tasto CANC. Per annullare un'eliminazione, riapplicare l'impostazione. È possibile ripristinare le impostazioni originali anche chiudendo l'Editor modelli di informazioni senza salvare le modifiche. Se si desidera annullare le modifiche dopo aver salvato, ripristinare il modello. Quando si ripristina un modello, tutta la personalizzazione viene persa e viene ripristinata la configurazione originale del modello.

In questo argomento viene descritto come utilizzare la Casella degli strumenti di Exchange 2013 o Exchange Management Shell per ripristinare la configurazione predefinita di un modello di informazioni.

Per ulteriori informazioni sui modelli di informazioni, vedere [Modelli di informazioni](details-templates-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Modelli di informazioni" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare la Casella degli strumenti di Exchange per ripristinare la configurazione predefinita di un modello di informazioni

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange Server 2013** \> **Casella degli strumenti di Exchange**.

2.  In **Casella degli strumenti di Exchange**, fare clic su **Editor modelli di informazioni** e, quindi, fare clic su **Apri strumento** nel riquadro azioni.

3.  Nel riquadro dei dettagli di **Editor modelli di informazioni**, selezionare il modello che si desidera ripristinare, quindi fare clic su **Ripristina** nel riquadro azioni.

4.  Fare clic su **Sì** per confermare la scelta di ripristinare lo stato originale del modello. Tutte le personalizzazioni andranno perse.

## Utilizzare Shell per ripristinare la configurazione predefinita di un modello di informazioni

In questo esempio viene ripristinato il modello di informazioni dei contatti Inglese (Stati Uniti).

```powershell
Restore-DetailsTemplate -Identity "en-US\Contact"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Restore-DetailsTemplate](https://technet.microsoft.com/it-it/library/bb125188\(v=exchg.150\)).

