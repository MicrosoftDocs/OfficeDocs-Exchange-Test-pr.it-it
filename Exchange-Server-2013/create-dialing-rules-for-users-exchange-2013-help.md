---
title: 'Creare regole di composizione per gli utenti: Exchange 2013 Help'
TOCTitle: Creare regole di composizione per gli utenti
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51407416
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare regole di composizione per gli utenti

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

I gruppi di regole di composizione sono costituiti da voci di regole di composizione Le regole di composizione vengono utilizzate per modificare un numero di telefono prima di inviarlo al PBX (sistema di telefonia) locale o IP PBX per le chiamate in uscita. Le regole di composizione consentono di:

  - Specificare i numeri che è possibile comporre per le chiamate in uscita. Quando si crea una regola di composizione, è possibile specificare i formati dei numeri da comporre. Tutti i numeri che non corrispondono a uno dei formati specificati vengono rifiutati. Se non si imposta alcuna regola di composizione, i chiamanti possono effettuare chiamate all'interno dell'organizzazione ma non possono effettuare chiamate in uscita.

  - Trasformano i numeri composti prima di inviarli al sistema di telefonia locale. Le regole di composizione consentono di rimuovere numeri dal numero composto o di aggiungerne. Consentono, ad esempio, di aggiungere il numero di accesso alla linea esterna per il sistema di telefonia oppure di aggiungere o rimuovere il codice del paese per le chiamate a lunga distanza o per i numeri locali.

Per specificare i tipi di chiamate in uscita da consentire per un dial plan di messaggistica unificata, creare un gruppo di regole di composizione e utilizzarle per autorizzare le chiamate in uscita per gli utenti di Outlok Voice Acceess e i chiamanti che compongono il numero di un operatore automatico di messaggistica unificata. Creare gruppi di regole di composizione separati per le chiamate nazionali e internazionali.


> [!NOTE]
> Se si è interessati a integrare la messaggistica unificata con Microsoft Lync Server, si consiglia di creare almeno un gruppo di regole di composizione e autorizzarlo nei dial plan URI SIP, nei criteri cassette postali di messaggistica unificata e sui risponditori automatici di messaggistica unificata per consentire l'inoltro delle chiamate in uscita a Lync Server.



Per ulteriori attività di gestione per l'esecuzione di chiamate esterne, vedere [Che consente agli utenti di effettuare chiamate procedure](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Esempi di regole di composizione utilizzate più frequentemente


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato numero</strong></p></td>
<td><p><strong>Numero composto</strong></p></td>
<td><p><strong>Casi in cui utilizzare la regola di composizione</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>Consentire tutte le chiamate in uscita.</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>Evitare che gli utenti ottengano un numero di interno o un errore quando dimenticano di comporre il numero di accesso alla linea esterna.</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>Consentire tutti i numeri che iniziano con 1.</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>Aggiungere 1 e l'indicativo di località 425 ai numeri a 7 cifre.</p></td>
</tr>
</tbody>
</table>


## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Se si applicheranno i gruppi di regole di composizione ai criteri cassetta postale di messaggistica unificata, sarà necessario confermare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Se si applicheranno i gruppi di regole di composizione agli operatori automatici di messaggistica unificata, sarà necessario confermare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Creazione di una regola di composizione tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

3.  Nell pagina **Dial plan di messaggistica unificata** \> **Regole di composizione**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") sotto **Regole di composizione nazionali** o **Regole di composizione internazionali**.

4.  Nella pagina **Nuova regola di composizione** immettere le informazioni seguenti:
    
      - **Nome regola composizione**   Immettere il nome della gruppo di regole di composizione nel quale si desidera aggiungere la regola. Per combinarla con altre regole, utilizzare lo stesso nome del gruppo. Per creare un nuovo gruppo di regole di composizione, immettere un nuovo nome univoco.
    
      - **Formato numero da trasformare (maschera numero)**   Immettere il formato di numero da trasformare prima della composizione, ad esempio 91425xxxxxxx. Se un chiamante compone un numero corrispondente, il sistema di messaggistica unificata lo trasforma nel numero composto prima di effettuare la chiamata. Immettere solo numeri e il carattere jolly (x). Il formato del numero viene anche detto *maschera del numero*.
    
      - **Numero composto   **Immettere il numero da comporre. Utilizzare solo numeri e il carattere jolly (x), come nel formato numero 9xxxxxxx. I caratteri jolly (x) vengono sostituiti dalle cifre del numero originale composto dall'utente. Verificare che il numero di caratteri jolly del numero composto corrisponda al numero di caratteri jolly presenti nel formato del numero.
    
      - **Commento   **Immettere un commento o una descrizione per questa regola di composizione. È possibile utilizzare il commento per descrivere l'azione della regola, ad esempio "Aggiungi il numero 9 alle chiamate in uscita".

5.  Fare clic su **OK** per salvare la regola di composizione. È possibile continuare a immettere regole utilizzando lo stesso nome gruppo regole di composizione per le regole che si desidera autorizzare insieme.

