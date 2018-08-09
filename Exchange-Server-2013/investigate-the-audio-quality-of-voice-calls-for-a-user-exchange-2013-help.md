---
title: 'Esamina qualità audio chiamate vocali: Exchange 2013 Help'
TOCTitle: Esaminare la qualità dell'audio delle chiamate vocali per un utente
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50555537
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esaminare la qualità dell'audio delle chiamate vocali per un utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

Se un utente segnala problemi relativi alla qualità audio delle chiamate di messaggistica unificata (UM), utilizzare il rapporto Registri chiamate utente per individuare la causa di tali problemi.


> [!NOTE]
> La qualità audio di una chiamata può subire gli effetti di fattori che non vengono considerati nei rapporti. Ad esempio, se nei server Exchange è presente un carico di memoria o CPU eccessivo, la qualità delle chiamate può risultare scarsa, anche se nei rapporti viene segnalata una qualità audio eccellente.



Per le attività aggiuntive relative a rapporti di messaggistica unificata, vedere [Procedure di rapporti di messaggistica unificata](um-reports-procedures-exchange-2013-help.md)

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cmdlet per i rapporti sui dati della chiamata e di riepilogo di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare EAC per ottenere le registrazioni delle chiamate per un utente abilitato alla Messaggistica Unificata

1.  In EAC, accedere a **Messaggistica unificata** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **Registri chiamate utente**.

2.  Fare clic su **Seleziona utente**, quindi selezionare l'utente per il quale si desidera visualizzare i dati.

3.  Per ottenere maggiori informazioni sulla qualità audio per una riga del rapporto, selezionare la riga e fare clic su **Dettagli qualità audio**. Sono disponibili le seguente informazioni:
    
      - **DATA E ORA**   La data e l'ora della chiamata, nel fuso orario impostato dall'utente selezionato in Outlook Web App.
    
      - **UTENTE**   L'utente selezionato.
    
      - **DIAL PLAN DI MESSAGGISTICA UNIFICATA**   Il dial plan per la chiamata.
    
      - **GATEWAY IP DI MESSAGGISTICA UNIFICATA**   Il gateway utilizzato per la chiamata.
    
      - **CODEC AUDIO**   Il codec audio utilizzato durante la chiamata.
    
      - **NMOS**   Punteggio NMOS (Network Mean Opinion Score) per la chiamata. Il punteggio NMOS indica la qualità audio della chiamata con un numero su una scala da 1 a 5, dove 5 rappresenta l'eccellenza.
        

        > [!NOTE]
        > Il massimo punteggio NMOS per una chiamata dipende dal codec audio utilizzato. Il punteggio NMOS potrebbe non essere disponibile per chiamate molto brevi, che durano meno di 10 secondi.

    
      - **DEGRADAZIONE NMOS**   La degradazione audio del punteggio NMOS dal valore massimo possibile per il codec audio in uso. Ad esempio, se il valore di degradazione NMOS per una chiamata fosse 1,2 e il punteggio NMOS indicato per la chiamata fosse 3,3, il punteggio NMOS massimo per questa chiamata particolare sarebbe pari a 4,5 (1,2 + 3,3).
    
      - **INSTABILITÀ**   La variazione media nell'arrivo dei pacchetti di dati per la chiamata.
    
      - **PERDITA PACCHETTI**   La percentuale media di perdita dei pacchetti di dati per la chiamata selezionata. La perdita di pacchetti è un'indicazione dell'affidabilità della connessione.
    
      - **ANDATA E RITORNO**   La media del percorso di andata e ritorno, in millisecondi, per l'audio della chiamata selezionata. Il punteggio del percorso di andata e ritorno consente di misurare la latenza della connessione.
    
      - **DURATA PERDITA BURST**   La durata media della perdita di pacchetti durante i burst di perdite per la chiamata selezionata.

