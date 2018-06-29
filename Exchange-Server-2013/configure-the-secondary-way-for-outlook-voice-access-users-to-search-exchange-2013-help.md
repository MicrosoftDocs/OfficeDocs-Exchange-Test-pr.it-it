---
title: 'Configurare la modalità secondaria per Outlook Voice Access la ricerca: Exchange 2013 Help'
TOCTitle: Configurare la modalità secondaria per Outlook Voice Access la ricerca
ms:assetid: 5cd4e0a0-d023-45a1-aa3c-b8dea6ec6d72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998311(v=EXCHG.150)
ms:contentKeyID: 52057260
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la modalità secondaria per Outlook Voice Access la ricerca

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

Quando viene creato un dial plan, è possibile configurare i metodi o le modalità principali e secondari *di composizione per nome* con cui i chiamanti eseguono la ricerca per nomi. Questi metodi di composizione per nome vengono utilizzati dai chiamanti per la ricerca dei nomi quando intendono individuare e contattare un utente durante la chiamata a un numero di Outlook Voice Access oppure durante la chiamata a un operatore automatico di messaggistica unificata associato al dial plan. I chiamanti possono utilizzare gli input a toni per individuare gli utenti abilitati per messaggistica unificata.


> [!NOTE]
> Se si seleziona <STRONG>Nessuno</STRONG> in modalità secondaria per la ricerca per nomi, sarà disponibile solo la modalità primaria di ricerca per i chiamanti che intendono individuare gli utenti. Se si configurano le modalità primaria e secondaria di ricerca per nome, ai chiamanti viene richiesto di utilizzare entrambe.



Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Modifica del metodo secondario di composizione per nome tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

4.  Selezionando **Impostazioni**, in **Modalità secondaria per la ricerca dei nomi**, utilizzare l'opzione desiderata nell'elenco a discesa:
    
      - **Cognome Nome** (impostazione predefinita)
    
      - **Nome Cognome**
    
      - **Indirizzo SMTP**
    
      - **Nessuno**

5.  Fare clic su **Salva**.

## Modifica del metodo secondario di composizione per nome tramite Shell

In questo esempio, il metodo secondario di composizione per nome viene impostato su `FirstLast`. In questo modo, i chiamanti che utilizzano il numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata in base prima al nome e poi al cognome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary FirstLast

In questo esempio, il metodo secondario di composizione per nome viene impostato su `LastFirst`. In questo modo, i chiamanti che utilizzano il numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata in base prima al cognome e poi al nome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary LastFirst 

In questo esempio, il metodo secondario di composizione per nome viene impostato su `SMTP address`. In questo modo, i chiamanti che utilizzano il numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata in base all'indirizzo SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary SMTPAddress 

In questo esempio viene impostato il metodo secondario di composizione per nome su `None` e il metodo principale su `SMTP address`. In questo modo, i chiamanti che si collegano al numero di Outlook Voice Access o a un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata esclusivamente in base all'indirizzo SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress -DialByNameSecondary None

