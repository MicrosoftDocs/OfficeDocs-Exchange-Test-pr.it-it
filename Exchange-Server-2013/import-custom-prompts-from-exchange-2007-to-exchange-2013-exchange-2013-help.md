---
title: 'Importare i prompt personalizzati da Exchange 2007 a Exchange 2013: Exchange 2013 Help'
TOCTitle: Importare i prompt personalizzati da Exchange 2007 a Exchange 2013
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54652873
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importare i prompt personalizzati da Exchange 2007 a Exchange 2013

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile importare i file audio file che contengono messaggi di saluto personalizzati, annunci, menu e menu vocali da Messaggistica unificata di Exchange 2007 nella Messaggistica unificata di Exchange 2013. Tramite uno script Shell, i menu vocali vengono importati nella cassetta postale del sistema Exchange denominata {e0dc1c29-89c3-4034-b678-e6c29d823ed9}, che viene creata durante l'installazione di Microsoft Exchange 2013. La cassetta postale del sistema viene utilizzata nella Messaggistica unificata per memorizzare annunci, menu, menu vocali, rapporti di Messaggistica unificata e messaggi di saluto personalizzati di dial plan e operatori automatici.

I file audio, in formato .wav o .wma, vengono utilizzati come segue:

  - Su dial plan di Messaggistica unificata, i file audio vengono utilizzati per saluti di benvenuto personalizzati e per messaggi informativi. Vengono riprodotti durante le chiamate degli utenti di Outlook Voice Access a un numero Outlook Voice Access.

  - Sugli operatori automatici di Messaggistica unificata, i file audio vengono utilizzati per i messaggi di saluto personalizzati per orario di ufficio e non, messaggi informativi, istruzioni vocali e menu di navigazione. Vengono riprodotti durante le chiamate a un operatore automatico di Messaggistica unificata.

Si utilizza lo script MigrateUMCustomPrompts.ps1 per eseguire la migrazione di una copia di tutti i gli annunci, i menu vocali e i messaggi di saluto personalizzati della Messaggistica unificata di Exchange Server 2007 alla Messaggistica unificata di Exchange 2013 per tutti i dial plan e gli operatori automatici di Messaggistica unificata di Exchange 2007.

Per impostazione predefinita, lo script MigrateUMCustomPrompts.ps1 è nella cartella \<Programmi\>\\Microsoft\\Exchange Server\\V15\\Scripts su un server Exchange 2013.


> [!NOTE]
> Lo script MigrateUMCustomPrompts.ps1 è incluso con Exchange 2013. Deve essere eseguito su un server Cassette postali di Exchange 2013 nella stessa organizzazione con i server di Messaggistica unificata di Exchange&nbsp;2007.



Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" e "operatori automatici di messaggistica unificata? voci nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md) .

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo dello script MigrateUMCustomPrompts.ps1 per migrare una copia di tutti i prompt personalizzati per i dial plan e operatore automatico di messaggistica unificata

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange Server 2013** \> **Exchange Management Shell**.

2.  In Shell, al prompt, digitare il percorso dello script. Ad esempio, digitare **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"** e quindi premere Invio.

3.  Al prompt dei comandi della shell, digitare **".\\MigrateUMCustomPrompt"**, quindi premere Invio.

