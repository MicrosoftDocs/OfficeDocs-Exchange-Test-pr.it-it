---
title: 'Ascolta al telefono: Exchange 2013 Help'
TOCTitle: Ascolta al telefono
ms:assetid: 511e4950-340a-48cc-a020-35d11e76b993
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn205136(v=EXCHG.150)
ms:contentKeyID: 54652842
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ascolta al telefono

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-25_

Quando viene ricevuto un messaggio vocale, gli utenti possono scegliere di ascoltarlo tramite gli altoparlanti o le cuffie del computer oppure di utilizzare la funzionalità Ascolta al telefono. Microsoft Outlook e Outlook Web App includono la funzionalità Ascolta al telefono e le relative impostazioni sono disponibili nella sezione **Ascolta al telefono** nelle opzioni **Casella vocale**. In questo argomento viene descritto in che modo un utente abilitato alla messaggistica unificata può utilizzare la funzionalità Ascolta al telefono.

## Informazioni su Ascolta al telefono

La funzionalità Ascolta al telefono consente agli utenti abilitati alla messaggistica unificata di ascoltare i messaggi vocali al telefono. Se un utente abilitato alla messaggistica unificata si trova nel cubicolo di un ufficio, sta utilizzando un computer pubblico o un computer non multimediale o sta ascoltando un messaggio vocale privato, potrebbe non desiderare o non essere in grado di ascoltare il messaggio con gli altoparlanti del computer. In alternativa, può riprodurre il messaggio vocale utilizzando un qualsiasi telefono: di casa, dell'ufficio o cellulare. Per rivedere le impostazioni di Ascolta al telefono in Outlook, andare su **File** \> **Info** \> **Gestisci casella vocale**. Facendo clic sul pulsante **Gestisci casella vocale** si effettuerà automaticamente l'accesso ad Outlook Web App; inoltre, è possibile accedervi utilizzando un browser Web. In Outlook Web App, andare nella sezione **Opzioni** \> **Telefono** \> **Casella vocale** \> **Ascolta al telefono** nella pagina **Casella vocale**.

Quando l'utente fa clic sull'opzione Ascolta al telefono nella barra degli strumenti nel modulo del sistema di casella vocale, viene visualizzata la finestra di dialogo **Ascolta al telefono**. La finestra di dialogo **Ascolta la telefono** fornisce i controlli per selezionare o immettere il numero di telefono da utilizzare per ascoltare il messaggio vocale, per iniziare e terminare la chiamata e il messaggio di stato per monitorare la chiamata. Se l'utente è collegato al dial plan URI SIP, l'indirizzo SIP verrà visualizzato nella casella **Dial**. Se è collegato al dial plan E.164, il numero E.164 completo verrà visualizzato nella casella **Dial**.


> [!NOTE]
> È possibile ascoltare solo un messaggio alla volta. Se l'utente tenta di iniziare una seconda chiamata con Ascolta al telefono mentre è ancora in corso l'altra, verrà visualizzato un messaggio di errore.



## Elenco dei numeri di telefono utilizzati di recente

Nella casella **Dial** gli utenti possono visualizzare un elenco dei numeri di telefono utilizzati più di recente. Il numero di telefono specificato nella sezione **Ascolta al telefono** è sempre visualizzato per primo ed è automaticamente selezionato come numero principale. Gli utenti possono utilizzare il menu a discesa per scegliere numeri di telefono da comporre diversi da quello configurato come principale.


> [!NOTE]
> Per abilitare gli utenti che utilizzano la funzionalità Ascolta al telefono alla composizione di un numero di telefono esterno senza codice di accesso alla linea esterna, ad esempio 425-555-1234 anziché 9-425-555-1234, configurare regole di composizione nazionali in un dial plan di messaggistica unificata che includano la seguente riga: group1, 9xxxxxxxxxx, 91xxxxxxxxxx. Dopo aver configurato l'elenco delle regole di composizione nazionali, aggiungerlo ai criteri cassetta postale di messaggistica unificata.



## Pulsanti Ascolta al telefono

Nella finestra di dialogo **Ascolta al telefono** sono presenti le opzioni **Componi** e **Disconnetti**. Quando la finestra di dialogo **Ascolta al telefono** viene aperta per la prima volta, il pulsante **Componi** è abilitato mentre **Disconnetti** è disabilitato. Durante l'esecuzione della chiamata, il pulsante **Componi** viene disabilitato fino al termine della chiamata. La chiamata può essere terminata sia facendo clic sul pulsante **Disconnetti** o riagganciando la cornetta del telefono. Se si chiude la finestra di dialogo **Ascolta al telefono** utilizzando il pulsante **Chiudi** la chiamata, se in corso, viene terminata. In Outlook, l'opzione **Ascolta al telefono** e altre opzioni sono disponibili nell'anteprima del **Riquadro di lettura**. Se si apre il messaggio della casella vocale da un'altra finestra, il pulsante **Ascolta al telefono** si trova sulla barra degli strumenti.

## Sezione Stato, Inviato e Oggetto

Nella sezione in basso della finestra di dialogo **Ascolta al telefono** sono visualizzati l'oggetto del messaggio vocale, la data e l'orario di invio e un messaggio con lo stato corrente della chiamata. Gli eventuali errori rilevati durante le operazioni con Ascolta al telefono vengono visualizzati in questa sezione della finestra di dialogo **Ascolta al telefono**.

## Convalida dei numeri di telefono

Ascolta al telefono consente di eseguire solo semplici convalide per gli input nella finestra di dialogo **Ascolta al telefono**. Non consente di convalidare i numeri di telefono. Se un numero di telefono non è valido, il servizio Messaggistica unificata restituirà all'utente un codice di errore significativo.

