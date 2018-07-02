---
title: 'Tenere traccia dei messaggi con i rapporti di recapito: Exchange 2013 Help'
TOCTitle: Tenere traccia dei messaggi con i rapporti di recapito
ms:assetid: a14e4e62-08ca-4a7b-92e1-d39fe3e0a9e5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150554(v=EXCHG.150)
ms:contentKeyID: 50479851
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tenere traccia dei messaggi con i rapporti di recapito

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-13_

I rapporti di recapito sono uno strumento di verifica dei messaggi di Interfaccia di amministrazione di Exchange (EAC) che è possibile utilizzare per conoscere lo stato di recapito dei messaggi di posta elettronica inviati o ricevuti da utenti presenti nella rubrica dell'organizzazione, con un determinato oggetto. È possibile monitorare le informazioni sul recapito dei messaggi inviati o ricevuti da una specifica cassetta postale dell'organizzazione. In un rapporto di recapito non viene restituito il contenuto del corpo del messaggio, ma la riga dell'oggetto viene visualizzata nei risultati. È possibile tener traccia dei messaggi per un massimo di 14 giorni dopo l'invio o la ricezione.


> [!NOTE]
> I rapporti di recapito tengono traccia dei messaggi inviati da persone che utilizzano client di posta elettronica Microsoft Outlook o Outlook Web App. Sono esclusi i messaggi inviati dai client di posta elettronica POP o IMAP, ad esempio Windows Mail, Outlook Express o Mozilla Thunderbird.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: Il tempo di completamento varia in base all'ambito della ricerca.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Tracciabilità messaggi" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Operazione desiderata

Use the EAC to track messages

Use the EAC to review a delivery report

## Utilizzare EAC per tenere traccia dei messaggi

1.  In EAC, accedere a **Flusso di posta** \> **Rapporti di recapito**.

2.  Immettere le informazioni seguenti:
    
      - **\* Cassetta postale di ricerca:**  fare clic su **Sfoglia** per selezionare la cassetta postale dalla rubrica e fare clic su **OK**. È obbligatorio scegliere la cassetta postale per la ricerca.
    
      - Selezionare una delle opzioni seguenti:
        
          - **Cerca i messaggi inviati a**   Utilizzare questa opzione per cercare i messaggi inviati a utenti specifici. Fare clic su **Seleziona utenti**, quindi scegliere gli utenti dalla rubrica selezionando un utente dall'elenco e facendo clic su **Aggiungi**. È possibile selezionare più di un utente. Una volta terminato di selezionare gli utenti, fare clic su **OK** per tornare alla pagina **Rapporti di recapito**. Se si seleziona questa opzione e si desidera individuare i messaggi inviati a qualsiasi utente, lasciare il campo vuoto.
        
          - **Ricerca messaggi ricevuti da**   Utilizzare questa opzione per limitare la ricerca ai messaggi ricevuti da un utente specifico. Ancora una volta, selezionare l'utente desiderato dalla rubrica e fare clic su **OK** per tornare alla pagina **Rapporti di recapito**. Se si seleziona questa opzione, è necessario specificare un mittente.
    
      - **Cerca le seguenti parole nella riga dell'oggetto**   Immettere in questo campo una riga dell'oggetto oppure non specificare alcun dato per non limitare la ricerca.

3.  Al termine, fare clic su **Cerca**. Se si desidera ricominciare da capo, fare clic su **Cancella**.

## Utilizzare EAC per rivedere un rapporto di recapito

Per visualizzare le informazioni sul recapito, selezionare un messaggio nel riquadro **Risultati ricerca** e fare clic su **Dettagli**.

Nel rapporto di recapito vengono visualizzati lo stato del recapito e informazioni dettagliate sul recapito del messaggio selezionato nel riquadro **Risultati ricerca**. All'inizio del rapporto saranno visualizzati i seguenti campi:

  - **Oggetto**   La riga dell'oggetto del messaggio viene visualizzata come intestazione del rapporto.

  - **Da**   L'alias, il nome visualizzato o l'indirizzo di posta elettronica del mittente del messaggio.

  - **A**   L'alias, il nome visualizzato o l'indirizzo di posta elettronica di ogni destinatario del messaggio.

  - **Inviato**  La data e l'ora in cui il messaggio è stato inviato.

## Sezione Riepilogo fino alla data

Questa sezione viene visualizzata nel rapporto di recapito se un messaggio è stato inviato a più di una persona o destinatario. All'inizio della sezione viene riportato il numero complessivo di destinatari del messaggio e fornite brevi informazioni sul recapito per ognuno di essi.

  - **Riepilogo fino alla data**   Visualizza il numero complessivo di destinatari e se sono presenti messaggi con stato In sospeso, Recapitato o Non riuscito. Fare clic sui collegamenti ipertestuali per ordinare i messaggi in base allo stato.

  - **Casella di ricerca**   La casella di ricerca è utile se il messaggio è stato inviato a un gruppo di oltre 30 destinatari. Nella casella di ricerca digitare l'indirizzo di posta elettronica di cui si desidera visualizzare le informazioni sul recapito e fare clic sulla lente di ingrandimento.

  - **A**   Mostra l'indirizzo di posta elettronica del destinatario.

  - **Stato**   In questa colonna viene visualizzato lo stato del messaggio per ciascun destinatario.

## Informazioni dettagliate sul rapporto

Questa sezione contiene informazioni dettagliate sul recapito di un messaggio inviato al destinatario selezionato nella sezione Riepilogo fino alla data.

  - **Rapporto di recapito per**   In questo campo è mostrato l'indirizzo di posta elettronica del destinatario selezionato.

  - **Inviato**   La data e l'ora in cui il messaggio è stato inviato dal sistema per il recapito.

A seconda dello stato del messaggio è possibile visualizzare diversi stati, tra cui:

  - **Recapitato**   Indica un'operazione di recapito riuscita.

  - **Rinviato**   Indica che il recapito di un messaggio è ritardato.

  - **In sospeso**   Se il recapito è in sospeso perché il messaggio soddisfa i criteri relativi a una regola o a un criterio a livello di organizzazione o perché è soggetto ad approvazione, nel messaggio di stato sarà indicata l'azione eseguita dalla regola oppure che il messaggio deve essere approvato da un moderatore prima del recapito.

  - **Moderatore**   Lo stato indica se il messaggio è stato approvato o rifiutato dal moderatore.

  - **Gruppi espansi**   Se un messaggio è stato inviato a un gruppo, i singoli utenti vengono mostrati nella sezione **Riepilogo fino alla data** per consentire di conoscere lo stato di recapito per ciascuno destinatario. Se è necessario rimuovere o aggiungere un utente a un gruppo durante l'esame del rapporto sul recapito, è possibile modificare il gruppo facendo clic su **Modifica gruppi**.

  - **Non riuscito**   Mostra la data, l'ora e il motivo di un recapito non riuscito. È possibile, ad esempio, che una regola a livello di organizzazione stia bloccando il recapito del messaggi o che non sia stato possibile recapitare il messaggio.

Una volta completato l'esame del rapporto, fare clic su **Chiudi**. I rapporti sul recapito non vengono salvati, ma possono essere rieseguiti in qualsiasi momento. Tenere presente che esiste una finestra di ricerca di due settimane.

## Come verificare se l'operazione ha avuto esito positivo

Se la ricerca è riuscita, i messaggi corrispondenti ai criteri di ricerca vengono elencati nel riquadro **Risultati ricerca**. Per visualizzare le informazioni sul recapito di un messaggio specificato, selezionarlo e fare clic su **Dettagli**. Se non vengono visualizzati messaggi nel riquadro **Risultati ricerca**, cambiare i criteri di ricerca e rieseguire la ricerca.

