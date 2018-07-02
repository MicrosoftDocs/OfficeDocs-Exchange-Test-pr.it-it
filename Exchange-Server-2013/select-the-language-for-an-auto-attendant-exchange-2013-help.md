---
title: 'Selezionare la lingua per un operatore automatico: Exchange 2013 Help'
TOCTitle: Selezionare la lingua per un operatore automatico
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50555570
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Selezionare la lingua per un operatore automatico

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile configurare le impostazioni della lingua predefinita dell'operatore automatico di messaggistica unificata. L'impostazione della lingua disponibile per un operatore automatico di messaggistica unificata consentono di configurare la lingua predefinita dell'operatore automatico. Quando si utilizzano le istruzioni vocali predefinite di sistema per l'operatore automatico, questo utilizzerà la lingua configurata per rispondere alle chiamate in arrivo. Questa impostazione della lingua riguarda solo le istruzioni predefinite del sistema fornite dopo che sarà stato installato il server Cassette postali su cui viene eseguito il servizio di messaggistica unificata di Microsoft Exchange. Questa impostazione non influisce sulle istruzioni personalizzate che vengono configurate per un operatore automatico. Le lingue disponibili dipendono dai Language Pack di messaggistica unificata installati sul server Cassette postali.

Ogni operatore automatico che si crea inizialmente utilizzerà inglese (en-US) come lingua predefinita. Il language pack in inglese (en-US) viene installato per impostazione predefinita in tutte le versioni di Microsoft Exchange 2013 e non possono essere rimosse. Se si desidera selezionare un'altra lingua, ad esempio in tedesco (de-DE), è necessario scaricare il tedesco UM language pack file .exe da [Exchange 2013 UM Language Pack Server](https://go.microsoft.com/fwlink/?linkid=266542) e installare il language pack di messaggistica UNIFICATA sul server cassette postali utilizzando il file di installazione de.exe UMLanguagePack.de. Dopo aver installato il language pack di messaggistica UNIFICATA, è possibile impostare la lingua predefinita per una lingua diversa da quella inglese (en-US) in operatori automatici di messaggistica UNIFICATA.

Per ulteriori attività relative alle lingue di messaggistica unificata, vedere [Procedure di lingue, istruzioni e messaggi di saluto di messaggistica unificata](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per configurare l'impostazione predefinita della lingua

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Nella pagina **Generale**, in **Lingua per interfaccia vocale automatica**, selezionare la lingua richiesta dall'elenco a discesa.

5.  Fare clic su **Salva** per accettare le modifiche.

## Utilizzo di Shell per configurare l'impostazione della lingua predefinita

In questo esempio la lingua predefinita per l'operatore automatico di messaggistica unificata `MyUMAutoAttendant` viene impostata sull'inglese (Gran Bretagna).

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

In questo esempio la lingua predefinita per l'operatore automatico di messaggistica unificata `MyUMAutoAttendant` viene impostata sull'inglese (Gran Bretagna).

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

