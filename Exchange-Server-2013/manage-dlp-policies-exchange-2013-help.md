---
title: 'Gestire i criteri DLP: Exchange 2013 Help'
TOCTitle: Gestire i criteri DLP
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 50481511
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i criteri DLP

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-14_

È possibile visualizzare, modificare o rimuovere criteri (DLP) prevenzione della perdita di dati esistenti in Microsoft Exchange, utilizzando l'interfaccia di amministrazione di Exchange (EAC) oppure Exchange Management Shell.

Per altre attività di gestione relative a DLP, vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013 ) o [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\)) (Exchange Online ).

Per ulteriori informazioni su Exchange Management Shell, vedere [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 15-60 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Prevenzione della perdita di dati (DLP)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per i criteri DLP, è possibile selezionare uno dei seguenti tre modi:
    
      -    **Imponi**   Le regole all'interno del criterio vengono valutate per tutti i messaggi e tipi di file supportati. Il flusso di posta può essere interrotto se vengono rilevati dati che soddisfano le condizioni del criterio. Vengono eseguite tutte le azioni descritte all'interno del criterio.
    
      -    **Testa criterio DLP con suggerimenti sul criterio**   Le regole all'interno del criterio vengono valutate per tutti i messaggi e tipi di file supportati. Il flusso di posta non verrà interrotto se vengono rilevati dati che soddisfano le condizioni del criterio. Vale a dire, i messaggi non sono bloccati. Se sono stati configurati suggerimenti sul criterio, vengono mostrati agli utenti.
    
      -    **Testa criterio DLP senza suggerimenti sul criterio**   Le regole all'interno del criterio vengono valutate per tutti i messaggi e tipi di file supportati. Il flusso di posta non verrà interrotto se vengono rilevati dati che soddisfano le condizioni del criterio. Vale a dire, i messaggi non sono bloccati. Se sono stati configurati suggerimenti sul criterio, non vengono mostrati agli utenti.

  - Una singola regola all'interno di un criterio DLP può avere le proprie impostazioni modalità. Quando la modalità di un criterio è diversa rispetto alla modalità di una regola all'interno del criterio, l'impostazione della regola con priorità e viene valutato secondo le modalità.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzare i dettagli di un criterio DLP esistente

Potrebbe essere necessario visualizzare le regole e le azioni di un criterio DLP esistente che già stata definita per l'organizzazione. Può essere utile se si verificano problemi di flusso di posta elettronica imprevisto o se l'organizzazione viene modificato il modo in cui devono essere monitorati informazioni riservate.

## Utilizzare EAC per visualizzare i dettagli di un criterio DLP esistente

1.  In EAC, individuare **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare doppio clic su uno dei criteri visualizzati nell'elenco dei criteri o evidenziare un elemento e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **criteri DLP modifica** fare clic su **regole**.


> [!TIP]
> È possibile creare un criterio DLP e lasciare in modalità non attivato o disattivata. In questa modalità, non viene applicato un criterio ed è possibile modificare qualsiasi predicati, azioni o valori associati alle regole prima di test o si intenda procedere.



## Utilizzo della Shell per visualizzare i dettagli di un criterio DLP esistente

Questo esempio vengono restituite informazioni sul criterio DLP fittizia denominato Employee Numbers. Il comando viene inviata tramite pipe al cmdlet **Format-List** per visualizzare informazioni dettagliate sulla configurazione dei criteri DLP specificato.

```powershell
Get-DlpPolicy "Employee Numbers" | Format-List
```

Per informazioni di sintassi e sui parametri, vedere [Get-DlpPolicy](https://technet.microsoft.com/it-it/library/jj215752\(v=exchg.150\)).

## Modificare un criterio DLP

È possibile modificare un criterio DLP esistente modificando il nome del criterio o le regole che gestiscono gli effetti del criterio. Modifica una regola esempio potrebbe includere aggiungere dichiarazione di non responsabilità personalizzato a un corpo del messaggio e la protezione RMS per i messaggi inviati all'interno di un dominio specifico e che vengono rilevate disporre di informazioni riservate. Se si utilizzano i modelli di criteri DLP, tenere presente che queste sono solo una delle funzionalità di Exchange 2013 che consentono di creare e applicare un sistema di criteri e conformità affidabile per l'ambiente di messaggistica.

## Utilizzare EAC per modificare un criterio DLP esistente

1.  In EAC, individuare **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare doppio clic su uno dei criteri basati su modelli visualizzati nell'elenco dei criteri o evidenziare un elemento e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **criteri DLP modifica** fare clic su **regole**.

4.  Per modificare una regola esistente, evidenziare la regola e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

5.  Per aggiungere una nuova regola vuota completamente personalizzabile, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

6.  Per aggiungere una regola su notifica mittente, blocco dei messaggi o alla possibilità di sostituzioni, fare clic sulla freccia accanto all'icona![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")**New**.

7.  Per rimuovere una regola, evidenziare la regola e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

8.  Fare clic su **Salva** per completare la modifica il criterio e salvare le modifiche.

## Utilizzo della Shell per modificare un criterio DLP esistente

È possibile specificare il livello di azione e le notifiche di un criterio utilizzando Exchange Management Shell. In questo esempio viene impostata la modalità di un criterio DLP fittizia denominato Employee Numbers in modo che non vengono applicate le azioni e non vengono visualizzati messaggi di notifica.

```powershell
Set-DlpPolicy "Employee Numbers" -Mode Audit
```

Per informazioni di sintassi e sui parametri, vedere [Set-DlpPolicy](https://technet.microsoft.com/it-it/library/jj215778\(v=exchg.150\)).

## Eliminare un criterio DLP

È possibile rimuovere definitivamente un criterio DLP utilizzando l'interfaccia di amministrazione di Exchange. Dopo aver eliminato un criterio, non vengono più applicata e nessuna delle regole e le azioni verranno salvata.

In alternativa, è possibile impostare lo stato operativo o la modalità di un criterio al **criterio DLP Test senza suggerimenti sui criteri**. Interrompe impedita messaggio nell'ambiente in uso, ma mantiene le impostazioni di configurazione dettagliate del criterio stesso. Può essere utile se vi è la possibilità che è necessario applicare il criterio in futuro.

## Utilizzare EAC per eliminare un criterio DLP esistente

1.  In EAC, individuare **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Selezionare il criterio che si desidera rimuovere dall'elenco dei criteri e quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Utilizzo della Shell per eliminare un criterio DLP esistente

In questo esempio viene rimosso il criterio DLP fittizio denominato Employee Numbers.

```powershell
Remove-DlpPolicy "Employee Numbers"
```

Per informazioni di sintassi e sui parametri, vedere [Remove-DlpPolicy](https://technet.microsoft.com/it-it/library/jj215677\(v=exchg.150\)).

## Ulteriori informazioni

[Prevenzione della perdita di dati](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Suggerimenti per i criteri](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/policy-tips)

