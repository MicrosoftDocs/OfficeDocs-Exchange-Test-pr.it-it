---
title: 'Quarantena posta indesiderata: Exchange 2013 Help'
TOCTitle: Quarantena posta indesiderata
ms:assetid: 4535496f-de6a-43df-8e53-c9a97f65cccc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997692(v=EXCHG.150)
ms:contentKeyID: 50480492
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quarantena posta indesiderata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-12_

Numerose organizzazioni sono obbligate da requisiti legali o normativi a mantenere o fornire tutti i messaggi di posta elettronica legittimi. In Microsoft Exchange Server 2013, la quarantena della posta indesiderata è una funzione dell'agente Filtro contenuti che riduce il rischio di perdita di messaggi legittimi. Tale funzionalità fornisce una posizione di archiviazione temporanea per i messaggi identificati come posta indesiderata che non devono essere consegnati alla cassetta postale di un utente all'interno dell'organizzazione.

I messaggi identificati come posta indesiderata dall'agente Filtro contenuti vengono inseriti in un rapporto di mancato recapito (NDR, Non-Delivery Report) e vengono recapitati alla cassetta postale per la quarantena della posta indesiderata all'interno dell'organizzazione. Successivamente è possibile gestire i messaggi recapitati in tale cassetta postale eseguendo le azioni appropriate, ad esempio eliminando i messaggi o instradando ai destinatari i messaggi contrassegnati come falsi positivi nel filtro della posta indesiderata. Inoltre, è possibile configurare la cassetta per la quarantena della posta indesiderata in modo che i messaggi vengano eliminati automaticamente dopo un determinato periodo di tempo.

**Sommario**

Spam confidence level

Spam quarantine

## Livello di probabilità di posta indesiderata

Quando un utente esterno invia messaggi di posta elettronica a un server di Exchange che esegue funzioni di protezione dalla posta indesiderata, tali funzioni valutano in maniera cumulativa le caratteristiche dei messaggi e agiscono nel modo indicato di seguito.

  - I messaggi sospetti di essere posta indesiderata vengono filtrati.

  - Viene assegnato un livello ai messaggi in base alla probabilità che rappresentino posta indesiderata. Questo livello viene memorizzato come una proprietà del messaggio nota come livello di probabilità di posta indesiderata.

La quarantena della posta indesiderata utilizza il livello di probabilità di posta indesiderata per determinare se un messaggio rientra molto probabilmente nella categoria della posta indesiderata. Il livello di probabilità di posta indesiderata è un valore compreso tra 0 e 9, dove 0 rappresenta il numero minore di probabilità che il messaggio sia posta indesiderata e 9 il numero maggiore di probabilità che lo sia.

È possibile stabilire che la posta con un determinato livello di probabilità di posta indesiderata venga eliminata, rifiutata o messa in quarantena. Il livello che attiva una di queste azioni viene denominato *soglia del livello di probabilità di posta indesiderata per la quarantena*. Nell'ambito del filtro del contenuto è possibile configurare l'agente Filtro contenuti in modo che le azioni vengono svolte sulla base della soglia del livello di probabilità di posta indesiderata per la quarantena. Ad esempio, è possibile impostare le condizioni seguenti:

  - La soglia del livello di probabilità di posta indesiderata per l'eliminazione viene impostata su 8.

  - La soglia del livello di probabilità di posta indesiderata per il rifiuto viene impostata su 7.

  - La soglia del livello di probabilità di posta indesiderata per la quarantena viene impostata su 6.

  - La soglia della cartella Posta indesiderata relativa al livello di probabilità di posta indesiderata viene impostata su 5.

In base alle soglie del livello di probabilità di posta indesiderata precedenti, tutta la posta elettronica con un livello di probabilità di posta indesiderata pari a 6 verrà recapitata alla cassetta postale per la quarantena della posta indesiderata.

Per ulteriori informazioni, vedere [Gestire il filtro contenuto](manage-content-filtering-exchange-2013-help.md).

Inizio pagina

## Quarantena posta indesiderata

Quando si ricevono messaggi dal server di Exchange che utilizza tutti gli agenti di posta indesiderata predefiniti, il filtro contenuti viene applicato come indicato di seguito:

  - Se il del livello di probabilità di posta indesiderata è maggiore o uguale alla soglia del livello di probabilità di posta indesiderata per la quarantena ma inferiore alla soglia del livello di probabilità di posta indesiderata per l'eliminazione o il rifiuto, il messaggio viene inviato alla cassetta di quarantena per la posta indesiderata.

  - Se il livello di probabilità di posta indesiderata è inferiore al limite di quarantena per la posta indesiderata, il messaggio viene recapitato nella Posta in arrivo del destinatario.

L'amministratore dei messaggi utilizza Microsoft Outlook per monitorare i falsi positivi nella cassetta postale per la quarantena della posta indesiderata. Se viene trovato un falso positivo, l'amministratore può inviare il messaggio alla cassetta postale del destinatario.

L'amministratore dei messaggi può esaminare gli indicatori di protezione dalla posta indesiderata se una delle seguenti condizioni è vera:

  - Troppi falsi positivi vengono filtrati nella cassetta della quarantena per la posta indesiderata.

  - Una quantità insufficiente di posta indesiderata viene rifiutata o eliminata.

Per ulteriori informazioni, vedere [Contrassegni filtro posta indesiderata](anti-spam-stamps-exchange-2013-help.md).

È quindi possibile modificare le impostazioni del livello di probabilità di posta indesiderata in modo da filtrare più accuratamente la posta indesiderata che entra nell'organizzazione. Per ulteriori informazioni, vedere [Soglia del livello di probabilità di posta indesiderata](spam-confidence-level-threshold-exchange-2013-help.md).

Per utilizzare la quarantena della posta indesiderata, procedere come segue:

1.  Verificare che sia abilitato il filtro contenuti.

2.  Creare una cassetta postale dedicata per la quarantena della posta indesiderata.

3.  Specificare la cassetta postale della quarantena per la posta indesiderata.

4.  Configurare la soglia del livello di probabilità di posta indesiderata per la quarantena.

5.  Gestire la cassetta postale della quarantena per la posta indesiderata.

6.  Impostare la soglia del livello di probabilità di posta indesiderata per la quarantena.

Per istruzioni dettagliate, vedere [Configurare una cassetta postale di quarantena della posta indesiderata](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

Inizio pagina

