---
title: 'Impostare la lingua predefinita per un dial plan: Exchange 2013 Help'
TOCTitle: Impostare la lingua predefinita per un dial plan
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50555625
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la lingua predefinita per un dial plan

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile impostare la lingua predefinita per un dial plan di messaggistica unificata (UM). Ogni dial plan creato utilizzerà l'inglese (en-US) come lingua predefinita. Il Language Pack per l'inglese (en-US) è installato in tutte le versioni di Microsoft Exchange Server 2013 e non può essere rimosso.

Se si desidera selezionare un'altra lingua come lingua predefinita, ad esempio in tedesco (de-DE), è necessario scaricare il tedesco UM language pack file .exe da [Exchange 2013 UM Language Pack Server](https://go.microsoft.com/fwlink/p/?linkid=266542) e installare il language pack nel server cassette postali utilizzando il file di installazione de.exe UMLanguagePack.de. Dopo aver installato il language pack, è possibile impostare la lingua predefinita per una lingua diversa da quella inglese (en-US) nel dial plan di messaggistica UNIFICATA.

Per ulteriori attività relative alle lingue di messaggistica unificata, vedere [Procedure di lingue, istruzioni e messaggi di saluto di messaggistica unificata](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Impostazione della lingua predefinita per un dial plan di messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  Nella pagina **Impostazioni** di **Lingua per l'audio**, selezionare nell'elenco a discesa la lingua che si desidera impostare.

5.  Fare clic su **Salva** per accettare le modifiche.

## Impostazione della lingua predefinita per un dial plan di messaggistica unificata tramite Shell

In questo esempio viene impostata la lingua predefinita su un dial plan di messaggistica unificata denominato `MyUMDialPlan` su Tedesco.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

In questo esempio viene impostata la lingua predefinita su un dial plan di messaggistica unificata denominato `MyUMDialPlan` su Giapponese.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

In questo esempio viene impostata la lingua predefinita su un dial plan di messaggistica unificata denominato `MyUMDialPlan` su Inglese australiano.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

