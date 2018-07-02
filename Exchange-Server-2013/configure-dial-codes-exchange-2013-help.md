---
title: 'Configurare i codici di chiamata: Exchange 2013 Help'
TOCTitle: Configurare i codici di chiamata
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51407437
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare i codici di chiamata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile configurare codici di chiamata, prefissi numerici e formati dei numeri utilizzati dalla messaggistica unificata per comporre chiamate in ingresso e in uscita per gli utenti abilitati alla messaggistica unificata. Nella maggioranza dei casi si configurerà un dial plan con codici di chiamata, prefissi e formati dei numeri sulla rete telefonica.

I codici di chiamata e i prefissi dei numeri vengono utilizzati per determinare il numero corretto da comporre per una chiamata in uscita effettuata da un utente abilitato alla messaggistica unificata. *Composizione di chiamata esterna* è l'espressione utilizzata per descrivere il processo tramite cui un utente del dial plan di messaggistica unificata inizia una chiamata in uscita. I formati dei numeri vengono utilizzati per le chiamate in ingresso in un paese, le chiamate internazionali o le chiamate effettuate in un dial plan. È possibile configurare un dial plan per la corrispondenza al formato numerico della chiamata in ingresso sia per i numeri nazionali che per quelli internazionali. Quando si configurano i formati dei numeri nazionali e internazionali, è possibile limitare le chiamate in ingresso per gli utenti collegati a un dial plan.

Per altre attività di gestione relative alla composizione di chiamate esterne, vedere [Che consente agli utenti di effettuare chiamate procedure](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione di codici di chiamata, prefissi e formati dei numeri tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Selezionare il dial plan di messaggistica unificata da gestire fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

4.  Nella pagina **Dial plan di messaggistica unificata** \> **Codici di chiamata**, configurare le seguenti opzioni:
    
      - **Codici di accesso per linee esterne**
    
      - **Codice di accesso internazionale**
    
      - **Prefisso nazionale**
    
      - **Codice paese**

5.  In **Formati dei numeri per la composizione tra dial plan**, configurare le seguenti opzioni:
    
      - **Formato numero nazionale**
    
      - **Formato numeri internazionali**
    
      - **Formati dei numeri delle chiamate in ingresso nello stesso dial plan**   Per aggiungere un formato di numero, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

6.  Fare clic su **Salva** per salvare le modifiche.

## Configurazione di codici di chiamata, prefissi e formati numerici tramite Shell

Con questo esempio viene configurato il dial plan di messaggistica unificata `MyUMDialPlan` con un formato di numero nazionale, un formato di numero internazionale e i seguenti codici di chiamata:

  - 9 come codice di accesso alla linea esterna

  - 011 come codice di accesso internazionale

  - 1 come prefisso per i numeri nazionali

  - 1 come codice di paese

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

