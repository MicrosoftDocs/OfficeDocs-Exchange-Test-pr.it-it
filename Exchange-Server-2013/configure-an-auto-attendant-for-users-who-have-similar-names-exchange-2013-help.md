---
title: 'Configurare un operatore automatico per gli utenti con nomi simili: Exchange 2013 Help'
TOCTitle: Configurare un operatore automatico per gli utenti con nomi simili
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52057225
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un operatore automatico per gli utenti con nomi simili

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-16_

È possibile configurare il metodo di utilizzo per utenti con nomi simili nelle opzioni dell'operatore automatico **Accesso operatore e rubrica** oppure è possibile mantenere le impostazioni predefinite dell'operatore automatico e configurare questa impostazione nel dial plan associato. Per impostazione predefinita, l'operatore automatico non è in grado di distinguere tra due o più utenti che hanno lo stesso nome perché l'impostazione predefinita per l'operatore automatico è **Eredita dal dial plan**.


> [!NOTE]
> Per un corretto utilizzo delle informazioni relative a utenti con nomi simili, è necessario fornire la posizione professionale, il reparto e la posizione dei destinatari nell'organizzazione Microsoft Exchange.



Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la configurazione di un operatore automatico di Messaggistica unificata per utenti con nomi simili

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera configurare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatori automatici di messaggistica unificata**, fare clic su **Accesso operatore e rubrica** e in **Informazioni da includere per utenti con lo stesso nome**, selezionarne uno dei seguenti:
    
      - **Titolo**   L'operatore automatico include la posizione professionale di ciascun utente in caso di corrispondenza.
    
      - **Reparto**   L'operatore automatico include il reparto di ciascun utente in caso di corrispondenza.
    
      - **Posizione**   L'operatore automatico include la posizione di ciascun utente in caso di corrispondenza.
    
      - **Nessuno**   L'operatore automatico non include ulteriori informazioni in caso di corrispondenza.
    
      - **Prompt per l'alias**   L'operatore automatico richiede al chiamante l'alias dell'utente.
    
      - **Ereditato da dial plan**   L'operatore automatico utilizza le impostazioni predefinite del dial plan associato all'operatore automatico.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per la configurazione di un operatore automatico di messaggistica unificata per utenti con nomi simili

In questo esempio vengono impostate le informazioni da includere insieme a utenti con nomi simili al Prompt per l'alias di un operatore automatico di messaggistica unificata chiamato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

In questo esempio vengono impostate le informazioni da includere insieme a utenti con nomi simili alla posizione professionale, vengono abilitate le ricerche di nomi e viene consentito ai chiamanti che utilizzano l'operatore automatico di premere \* per essere presentati con una formula di benvenuto in Outlook Voice Access ad un operatore automatico di messaggistica unificata chiamato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

