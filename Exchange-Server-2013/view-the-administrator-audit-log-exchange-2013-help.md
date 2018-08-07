---
title: 'Visualizza registro controllo amministratore: Exchange Online Protection Help'
TOCTitle: Visualizzare il registro di controllo dell'amministratore
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56269542
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare il registro di controllo dell'amministratore

 

_**Si applica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-05-03_

In Microsoft Exchange Online Protection (EOP), Microsoft Exchange Online e Microsoft Exchange 2013, è possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) per ricercare e visualizzare le voci nel *registro di controllo dell'amministratore*. Il registro di controllo dell'amministratore registra operazioni specifiche, basate sul cmdlet di Exchange Management Shell, eseguite dagli amministratori e dagli utenti a cui sono stati assegnati privilegi amministrativi. Le voci nel registro di controllo dell'amministratore forniscono informazioni sul cmdlet eseguito, sui parametri utilizzati, sull'utente che ha eseguito il cmdlet e sugli oggetti coinvolti.


> [!NOTE]
> <UL>
> <LI>
> <P>Per impostazione predefinita, è abilitata la registrazione di controllo di amministratore.</P>
> <LI>
> <P>Il registro di controllo dell'amministratore non registra le operazioni basate sul cmdlet di Exchange Management Shell che iniziano con i verbi <STRONG>Get</STRONG>, <STRONG>Search</STRONG> o <STRONG>Test</STRONG>.</P>
> <LI>
> <P>Le voci del registro di controllo vengono conservate per 90&nbsp;giorni. Dopo 90 giorni, le voci vengono eliminate.</P></LI></UL>



## Informazioni preliminari

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Visualizzazione di report" nell'argomento [Autorizzazioni di funzionalità in EOP](https://technet.microsoft.com/it-it/library/jj723125\(v=exchg.150\)).

  - Come descritto in precedenza, la registrazione di controllo di amministratore è attivata per impostazione predefinita. Per verificare che sia stata abilitata, è possibile eseguire il comando seguente.
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    In Exchange 2013, è possibile abilitare la registrazione di controllo di amministratore se è disattivata eseguendo il comando seguente.
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    In Exchange Online Protection e Exchange Online, la registrazione di controllo di amministratore è sempre attivata. Non può essere disabilitata.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Visualizzazione del log di controllo dell'amministratore tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange andare a **Gestione della conformità** \> **Controllo**, quindi selezionare **Esegui rapporto del log di controllo dell'amministratore**.

2.  Scegliere una **Data di inizio** e una **Data di fine**, quindi scegliere **Ricerca**. Vengono visualizzate tutte le modifiche alla configurazione effettuate durante il periodo di tempo specificato. Tali modifiche possono essere ordinate utilizzando le seguenti informazioni:
    
      - **Data** La data e l'ora in cui è stata effettuata la modifica alla configurazione. La data e l'ora vengono memorizzati in formato UTC (Coordinated Universal Time).
    
      - **Cmdlet** Il nome del cmdlet utilizzato per modificare la configurazione.
    
      - **Utente** Il nome dell'account utente di chi ha effettuato le modifiche alla configurazione.
    
    Saranno visualizzate fino a 5000 voci su più pagine. Se si desidera limitare i risultati, specificare un intervallo di date più piccolo. Se è stato selezionato un risultato di ricerca individuale, le seguenti informazioni aggiuntive vengono visualizzate nel riquadro dei dettagli:
    
      - **Oggetto modificato** L'oggetto è stato modificato dal cmdlet.
    
      - **Parametri (Parameter:Value)** I parametri cmdlet utilizzati e qualunque valore specificato con il parametro.

3.  Se si desidera stampare una voce specifica del registro di controllo, selezionare il pulsante **Stampa** nel riquadro dei dettagli.

## Verifica dell'esito positivo dell'operazione

Se è stato correttamente eseguito un report del registro di controllo dell'amministratore, le modifiche alla configurazione effettuate nell'intervallo di date specificate, vengono visualizzate nel riquadro dei risultati di ricerca. Se non sono presenti risultati, modificare l'intervallo di date, quindi eseguire di nuovo il report.


> [!NOTE]
> Quando viene effettuata una modifica nell'organizzazione, questa può richiedere fino a 15 minuti per essere visualizzata nei risultati di ricerca del registro di controllo. Se una modifica non viene visualizzata nel registro di controllo dell'amministratore, attendere qualche minuto ed eseguire nuovamente la ricerca.


