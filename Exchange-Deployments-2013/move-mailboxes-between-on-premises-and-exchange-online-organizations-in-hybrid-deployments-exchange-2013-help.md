---
title: 'Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride: Exchange 2013 Help'
TOCTitle: Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/it-it/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51406950
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-10-02_

Con la distribuzione ibrida basata su Exchange, è possibile scegliere di spostare le cassette postali locali di Exchange nell'organizzazione di Exchange Online oppure di spostare le cassette postali di Exchange Online nell'organizzazione Exchange. Quando si spostano cassette postali tra le organizzazioni locali e di Exchange Online, per eseguire la richiesta di spostamento remoto delle cassette postali vengono utilizzati i batch di migrazione. Questo approccio consente di spostare le cassette postali esistenti anziché creare nuove cassette postali utente e di importare i dati utente. Si tratta di un approccio diverso rispetto alla migrazione delle cassette postali utente da un'organizzazione di Exchange locale a Exchange Online nell'ambito di una migrazione completa di Exchange nel cloud. Le cassette postali discusse in questo argomento fanno parte della gestione amministrativa di Exchange, in una relazione di coesistenza a lungo termine tra organizzazioni Exchange locali e di Exchange Online.

Per ulteriori informazioni sulla migrazione delle organizzazioni Exchange locali a Exchange Online, vedere [Modi per eseguire la migrazione di più account di posta elettronica a Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).


> [!IMPORTANT]
> È necessario configurare una distribuzione ibrida tra le organizzazioni locali e quelle di Exchange Online per completare le procedure di spostamento delle cassette postali in questo argomento. Per ulteriori informazioni sulle distribuzioni ibride, vedere <A href="exchange-server-hybrid-deployments-exchange-2013-help.md">Distribuzioni ibride di Exchange Server</A>.<BR><BR>Prima di spostare le cassette postali abilitate alla messaggistica unificata su Exchange Online, è necessario accertare che le versioni locali di Skype for Business 2015, Skype for Business Online ed Exchange Online soddisfino i requisiti specificati in <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Prerequisiti per la distribuzione ibrida</A>. Per informazioni su come eseguire il mapping dei criteri relativi alla messaggistica unificata in locale con i criteri di Exchange Online, vedere <A href="https://technet.microsoft.com/it-it/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti per configurare il batch di migrazione, ma il tempo totale per completare la migrazione dipende dal numero di cassette postali incluse in ogni batch di migrazione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di migrazione e spostamento delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](https://technet.microsoft.com/it-it/library/dd638132\(v=exchg.150\)).

  - La distribuzione ibrida è configurata tra le organizzazioni locali e quelle di Exchange Online.

  - Se si esegue Exchange 2013, accertarsi che il servizio proxy di replica della cassetta postale (MRSProxy) sia abilitato nei server Accesso client locali di Exchange 2013.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](https://technet.microsoft.com/it-it/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Passaggio 1: creare un endpoint di migrazione

Prima di eseguire la migrazione remota on-boarding e off-boarding in una distribuzione ibrida di Exchange, è consigliabile creare degli endpoint di migrazione remota di Exchange. L'endpoint di migrazione contiene le impostazioni di connessione per un server Exchange locale che esegue il servizio proxy MRS, necessario per completare le migrazioni remote da e verso Exchange Online.

Per le procedure dettagliate, vedere [Creare gli endpoint di migrazione](https://technet.microsoft.com/it-it/library/jj874458\(v=exchg.150\)).

## Passaggio 2: attivare il servizio MRSProxy

Se il servizio MRSProxy non è già abilitato per i server Accesso client di Exchange 2013 locali, attenersi alla seguente procedura nell'interfaccia di amministrazione di Exchange:

1.  Aprire l'interfaccia di amministrazione di Exchange, quindi andare a **Server** \> **Directory virtuali**.

2.  Selezionare il server Accesso client, quindi selezionare la directory virtuale **EWS**, e fare clic su **Modifica** ![Icona Modifica](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Selezionare la casella di controllo **Proxy MRS abilitato**, quindi fare clic su **Salva**.

## Passaggio 3: usare l'interfaccia di amministrazione di Exchange per spostare le cassette postali

È possibile utilizzare la procedura guidata per la migrazione degli spostamenti remoti nella scheda **Office 365** nell'interfaccia di amministrazione di Exchange in un server Exchange per spostare le cassette postali utente esistenti dall'organizzazione locale all'organizzazione di Exchange Online o per spostare le cassette postali di Exchange Online nell'organizzazione locale. Scegliere una delle procedure seguenti:

## Spostare cassette postali locali in Exchange Online

È possibile utilizzare la procedura guidata per la migrazione remota nella scheda **Office 365** nell'interfaccia di amministrazione di Exchange in un server Exchange per spostare le cassette postali utente esistenti dall'organizzazione locale all'organizzazione di Exchange Online. Attenersi alla seguente procedura:

1.  Aprire l'interfaccia di amministrazione di Exchange, quindi andare a **Office 365** \> **Destinatari** \> **Migrazione**.

2.  Fare clic su **Aggiungi**![Icona Aggiungi](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare **Migra a Exchange Online**.

3.  Nella pagina **Seleziona un tipo di migrazione**, selezionare **Migrazione remota** e fare clic su **Avanti**.

4.  Nella pagina **Seleziona gli utenti**, fare clic su **Aggiungi**![Icona Aggiungi](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare gli utenti locali da spostare in Office 365, quindi fare clic su **Aggiungi** e poi su **OK**. Fare clic su **Avanti**.

5.  Nella pagina **Immetti le credenziali dell'account utente Windows**, immettere il nome dell'account dell'amministratore locale nel campo di testo **Nome amministratore locale** e la password ad esso associata nel campo di testo **Password amministratore locale**. Ad esempio, "corp\\administrator" e una password. Fare clic su **Avanti**.
    

    > [!NOTE]
    > Se è già stato creato un endpoint di migrazione, si riceverà una richiesta di conferma dell'endpoint per questo passaggio. Se sono stati creati due o più endpoint di migrazione, è necessario scegliere un endpoint dal menu a discesa degli endpoint migrazione.



6.  Nella pagina **Conferma l'endpoint di migrazione**, verificare che il nome di dominio completo del server Exchange locale sia visualizzato quando la procedura guidata conferma l'endpoint di migrazione. Ad esempio, "mail.contoso.com". Fare clic su **Avanti**.
    

    > [!NOTE]
    > Il servizio MRSProxy nei server Exchange applica automaticamente le richieste di migrazione delle cassette postali quando si selezionano più cassette postali da spostare in Exchange Online. Il tempo totale richiesto per completare lo spostamento delle cassette postali dipende dal numero di cassette postali selezionate, dalla dimensione delle cassette postali e dalla configurazione di MRSProxy. Per ulteriori informazioni sulla personalizzazione di MRSProxy, vedere <A href="https://technet.microsoft.com/it-it/library/bb232205(v=exchg.150)">Limitazione per il messaggio</A>.



7.  Nella pagina **Configurazione spostamento**, immettere un nome per il batch di migrazione nel campo di testo **Nome del nuovo batch di migrazione**. Usare la freccia giù ![Icona Freccia in giù](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icona Freccia in giù") per selezionare il **dominio di recapito di destinazione per le cassette postali di cui si esegue la migrazione a Office 365**. Nella maggior parte delle distribuzioni ibride, si tratta del dominio SMTP principale utilizzato per le cassette postali dell'organizzazione di Exchange Online. Ad esempio, contoso.mail.onmicrosoft.com. Verificare che l'opzione **Sposta la cassetta postale primaria insieme alla cassetta di archiviazione** sia selezionata, quindi fare clic su **Avanti**.

8.  Nella pagina **Avvia il batch**, selezionare almeno un destinatario che riceverà il rapporto di completamento del batch. Verificare che sia selezionata l'opzione **Avvia automaticamente il batch**, quindi selezionare la casella di controllo **Completa automaticamente il batch di migrazione**. Fare clic su **Nuova regola**.

## Spostamento delle cassette postali dall'organizzazione Exchange Online all'organizzazione locale

È possibile utilizzare la procedura guidata per la migrazione remota nella scheda **Office 365** nell'interfaccia di amministrazione di Exchange in un server Exchange per spostare le cassette postali utente esistenti dall'organizzazione locale all'organizzazione di Exchange Online:

1.  Aprire l'interfaccia di amministrazione di Exchange, quindi andare a **Office 365** \> **Destinatari** \> **Migrazione**.

2.  Fare clic su **Aggiungi**![Icona Aggiungi](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare **Migra a Exchange Online**.

3.  Nella pagina **Seleziona gli utenti**, selezionare **Seleziona gli utenti da spostare** , quindi fare clic su **Avanti**.

4.  Nella pagina **Seleziona gli utenti**, fare clic su **Aggiungi**![Icona Aggiungi](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare gli utenti di Exchange Online da spostare nell'organizzazione locale, quindi fare clic su **Aggiungi** e su **OK**. Fare clic su **Avanti**.

5.  Nella pagina **Conferma l'endpoint di migrazione**, verificare che il nome di dominio completo del server Exchange locale sia visualizzato quando la procedura guidata conferma l'endpoint di migrazione. Ad esempio, "mail.contoso.com". Fare clic su **Avanti**.
    

    > [!NOTE]
    > Il servizio MRSProxy nei server Exchange applica automaticamente le richieste di migrazione delle cassette postali quando si selezionano più cassette postali da spostare in Exchange Online. Il tempo totale richiesto per completare lo spostamento delle cassette postali dipende dal numero di cassette postali selezionate, dalla dimensione delle cassette postali e dalla configurazione di MRSProxy. Per ulteriori informazioni sulla personalizzazione di MRSProxy, vedere <A href="https://technet.microsoft.com/it-it/library/bb232205(v=exchg.150)">Limitazione per il messaggio</A>.



6.  Nella pagina **Configurazione spostamento**, immettere un nome per il batch di migrazione nel campo **Nome del nuovo batch di migrazione**. Immettere quindi il dominio di recapito di destinazione nel campo **Dominio di recapito di destinazione per le cassette postali da migrare a Office 365**. Nella maggior parte delle distribuzioni ibride, si tratta del dominio SMTP primario utilizzato sia per le cassette postali dell'organizzazione locale, sia per quelle di Exchange Online. Ad esempio, contoso.com.

7.  Scegliere se si desidera spostare anche la cassetta postale di archiviazione per l'utente selezionato e immettere il nome del database in cui spostare questa cassetta postale nel campo di testo **Database di destinazione**. Ad esempio, Database delle cassette postali 123456789. Fare clic su **Avanti**.

8.  Nella pagina **Avvia il batch**, selezionare almeno un destinatario che riceverà il rapporto di completamento del batch. Verificare che sia selezionata l'opzione **Avvia automaticamente il batch**, quindi selezionare la casella di controllo **Completa automaticamente il batch di migrazione**. Fare clic su **Nuova regola**.

## Passaggio 4: rimuovere i batch di migrazione completati

Dopo aver completato gli spostamenti delle cassette postali, è consigliabile rimuovere i batch di migrazione completati per ridurre al minimo la probabilità di errori se gli stessi utenti vengono spostati nuovamente.

Per rimuovere un batch di migrazione completato:

1.  Aprire l'interfaccia di amministrazione di Exchange, quindi andare a **Office 365** \> **Destinatari** \> **Migrazione**.

2.  Fare clic su un batch di migrazione completato, quindi fare clic su **Elimina** ![Icona Elimina](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Nella finestra di conferma di avviso di eliminazione, fare clic su **Sì**.

## Passaggio 5: abilitare nuovamente l'accesso offline per Outlook sul Web

L'accesso offline in Outlook sul Web (in precedenza denominato Outlook Web App) consente agli utenti di accedere alla cassetta postale quando non sono collegati a una rete. Se vengono migrate le cassette postali di Exchange in Exchange Online, è necessario che gli utenti ripristinino l'impostazione di accesso offline nel browser, in modo da utilizzare Outlook sul Web offline. Per ulteriori informazioni sull'accesso offline in Outlook sul Web, sui browser che lo supportano e su come attivarlo, vedere [Utilizzare Outlook Web App offline](https://go.microsoft.com/fwlink/p/?linkid=286942).

## Come verificare se l'operazione ha avuto esito positivo

Quando si spostano le cassette postali utente esistenti tra le organizzazioni locali e di Exchange Online, il corretto completamento della procedura guidata per la migrazione remota costituisce una prima indicazione del fatto che lo spostamento della cassetta postale è avvenuto come previsto.

Dal momento che il completamento del processo di spostamento delle cassette postali richiede diversi minuti, è possibile verificare che l'operazione stia procedendo correttamente aprendo l'interfaccia di amministrazione di Exchange e selezionando **Office 365** \> **Destinatari** \> **Migrazione** per visualizzare lo stato di avanzamento dello spostamento per le cassette postali selezionate nella procedura guidata. Il valore di **Stato** è **Sincronizzazione** durante lo spostamento delle cassette postali e **Completato** dopo che la cassetta postale è stata correttamente spostata nell'organizzazione locale o di Exchange Online.

Al termine dello spostamento della cassetta postale, è possibile verificare il corretto spostamento della cassetta postale remota nell'organizzazione locale o di Exchange Online verificando le proprietà della cassetta postale. A tal fine, accedere a **Destinatari** \> **Cassette postali** nell'interfaccia di amministrazione di Exchange dell'organizzazione locale o di Exchange Online. La cassetta postale utente dovrebbe mostrare **Tipo di cassetta postale** di **Office 365** per le cassette postali di Exchange Online e **Utente** per le cassette postali locali.

È anche possibile eseguire il seguente cmdlet in Exchange Management Shell per verificare lo stato del batch di migrazione.

    Get-MigrationBatch -Identity <batch name>

In caso di problemi, è possibile chiedere aiuto nei forum di Office 365. Per accedere ai forum, è necessario un account che disponga dell'accesso come amministratore al servizio basato sul cloud. I forum sono disponibili all'indirizzo: [forum di Office 365](https://go.microsoft.com/fwlink/p/?linkid=201915)

## Nuovo utente di Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Piccola icona per LinkedIn Learning" alt="Piccola icona per LinkedIn Learning" /> <strong>Nuovo utente di Office 365?</strong><br />
Sono disponibili esercitazioni video gratuite per <a href="https://support.office.com/it-it/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> grazie a LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

