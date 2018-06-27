---
title: 'Configurare le ore lavorative: Exchange 2013 Help'
TOCTitle: Configurare le ore lavorative
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 50481246
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le ore lavorative

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-19_

Quando si configura l'orario di ufficio per un operatore automatico di messaggistica unificata, vengono definite le ore del giorno in cui l'organizzazione è aperta e le istruzioni vocali per il menu e i messaggi di saluto relativi all'orario di ufficio che i chiamanti ascolteranno quando chiamano un numero di interno configurato sull'operatore automatico. Se un chiamante si mette in contatto con l'operatore automatico durante le ore non definite come orario di ufficio, ascolterà le istruzioni vocali e i messaggi di saluto relativi all'orario non di ufficio.

Sono disponibili diverse opzioni di pianificazione predefinita in EAC. Molte aziende, ad esempio, sono aperte dal lunedì al venerdì, dalle 8.00 alle 17.00. Talvolta, può capitare che le opzioni predefinite non soddisfino specifiche esigenze e sia necessario personalizzare la pianificazione. Se l'orario di ufficio è diverso dalle pianificazioni predefinite disponibili nel sistema, è possibile definire una pianificazione personalizzata per l'operatore automatico.

Per impostazione predefinita, l'operatore automatico di messaggistica unificata riprodurrà le istruzioni vocali e i messaggi di saluto relativi all'orario di ufficio indipendentemente dall'ora del giorno in cui l'operatore automatico riceve la chiamata.


> [!NOTE]
> Quando si imposta la pianificazione per l'orario di ufficio e non di ufficio su un operatore automatico di messaggistica unificata, verificare che il fuso orario sia configurato correttamente.



Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per specificare l'orario di ufficio per un operatore automatico di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera impostare l'orario di ufficio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Orario di ufficio**, sotto **Orario di ufficio**, fare clic su **Configura orario di ufficio**.

4.  Nella pagina **Configura orario di ufficio**, selezionare le ore che si desidera utilizzare come orario di ufficio per ogni giorno della settimana.

5.  Fare clic su **OK**, quindi fare clic su **Salva**.

## Definizione dell'orario di ufficio per un operatore automatico di messaggistica unificata tramite Shell

In questo esempio, viene impostato l'orario di ufficio per un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

