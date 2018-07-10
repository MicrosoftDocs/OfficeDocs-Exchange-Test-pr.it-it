---
title: 'Configurare il mezzo principale per Outlook Voice Access la ricerca: Exchange 2013 Help'
TOCTitle: Configurare il mezzo principale per Outlook Voice Access la ricerca
ms:assetid: 3d93a037-5820-41d3-9206-69f534414daf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997563(v=EXCHG.150)
ms:contentKeyID: 50480417
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il mezzo principale per Outlook Voice Access la ricerca

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

Quando si crea un dial plan di messaggistica unificata, è possibile configurare i canali primari e secondari in cui i chiamanti possono effettuare una ricerca per nome per individuare un utente quando chiamano un numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan. Per individuare un utente abilitato alla messaggistica unificata i chiamanti possono utilizzare gli input a toni.


> [!NOTE]
> <STRONG>Nessuno</STRONG> non è disponibile per il metodo principale di ricerca per nome. Quando <STRONG>Nessuno</STRONG> è selezionato per il metodo secondario di ricerca per nome, per i chiamanti sarà disponibile solo il metodo principale. Se si configurano entrambi i metodi principale e secondario di ricerca per nome, i chiamanti saranno invitati a utilizzare entrambe le modalità.



Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la modifica del metodo principale di composizione per nome

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, fare clic su **Configura**.

4.  In **Impostazioni**, selezionare l'opzione desiderata nel menu a discesa **Modalità principale per la ricerca dei nomi**:
    
      - **Cognome Nome** (impostazione predefinita)
    
      - **Nome Cognome**
    
      - **Indirizzo SMTP**

5.  Fare clic su **Salva**.

## Utilizzare Shell per modificare il metodo principale di composizione per nome

In questo esempio, il metodo principale di composizione per nome viene impostato su `FirstLast`. In questo modo, i chiamanti che utilizzano il numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata in base prima al nome e poi al cognome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary FirstLast

In questo esempio, il metodo principale di composizione per nome viene impostato su `LastFirst`. In questo modo, i chiamanti che utilizzano il numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata in base prima al cognome e poi al nome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary LastFirst 

In questo esempio, il metodo principale di composizione per nome viene impostato su `SMTP address`. In questo modo, i chiamanti che utilizzano il numero di Outlook Voice Access o un operatore automatico di messaggistica unificata associato al dial plan, possono cercare un utente abilitato alla messaggistica unificata in base all'indirizzo SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress

