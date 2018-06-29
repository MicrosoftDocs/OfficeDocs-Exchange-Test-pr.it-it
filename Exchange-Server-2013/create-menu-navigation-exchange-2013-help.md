---
title: 'Creare lo spostamento tra menu: Exchange 2013 Help'
TOCTitle: Creare lo spostamento tra menu
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 50480394
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# Creare lo spostamento tra menu

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-05_

È possibile utilizzare la pagina **nuova voce di menu struttura di spostamento** per creare singolo o più mapping dei tasti per le aziende o menu principale orario non di ufficio viene richiesto di operatori automatici. È possibile definire l'azione che verrà eseguita quando si preme un tasto sulla tastiera del telefono è, ad esempio, trasferire la chiamata a un numero interno o operatore automatico di un'altra.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per configurare i menu di spostamento operatore automatico di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial Plan**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera creare navigazione nei menu. Sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina di **Operatore automatico di messaggistica unificata**, fare clic su **navigazione nei Menu**, selezionare **Attiva navigazione nei menu in orario di ufficio** o **abilitare navigazione nei menu in orario non di ufficio** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella pagina **nuova voce di menu struttura di spostamento**, configurare quanto segue:
    
      - **Prompt** Utilizzare questa casella per digitare il nome del nuovo menu di navigazione. Il nome del menu di navigazione viene utilizzato solo per la visualizzazione. Questo campo è obbligatorio.
        
        Dal momento che si può scegliere di specificare più menu di navigazione, si consiglia di utilizzare nomi significativi per i mapping dei tasti. La lunghezza massima del nome di un'associazione di tasti è di 64 caratteri e sono ammessi gli spazi, Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Quando si preme questo tasto**   Utilizzare questo elenco per abilitare il mapping dei tasti. L'associazione di tasti è il tasto numerico che il chiamante preme affinché l'operatore automatico esegua un'operazione specifica, ad esempio, l'inoltro della chiamata a un altro operatore automatico o a un operatore. Per impostazione predefinita, non viene definita nessuna voce.
        
        Utilizzare l'elenco a discesa selezionare il codice numerico (da 1 a 9) che occorre premere il chiamante. Zero (0) è riservato per l'operatore di operatore automatico.
        
        Se si seleziona **Timeout** dall'elenco a discesa, si abilita il trasferimento della chiamata a un interno o a un altro operatore automatico nel caso in cui il chiamante non prema nessun tasto sul tastierino del telefono. (ad esempio, "Resti in linea. La sua chiamata verrà trasferita al primo operatore disponibile.") L'impostazione predefinita è 5 secondi. Se si abilita questa opzione, viene creata un'associazione di tasti vuota.
    
      - **Riproduci il seguente file audio**    Utilizzare questa opzione per selezionare un file audio registrato in precedenza per i chiamanti. Fare clic su **Modifica** e quindi fare clic su **Sfoglia** per individuare il file audio.
    
      - **Esegui questa ulteriore azione**   Selezionare una delle seguenti opzioni per definire l'azione che si desidera che l'operatore automatico esegua per il chiamante:
        
          - **Nessuno**    Se non si desidera all'operatore automatico di trasferire la chiamata a un'estensione o a un altro operatore automatico o lasciare un messaggio per un utente, utilizzare questa opzione.
        
          - **Trasferisci a questo numero di interno**   Selezionare questa opzione per abilitare le chiamate da trasferire a un numero di interno. Se si abilita questa opzione, utilizzare la casella per digitare il numero di interno a cui trasferire la chiamata. In questo campo è possibile inserire solo caratteri numerici. Non sono ammessi i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Trasferisci a questo operatore automatico di messaggistica unificata**   Selezionare questa opzione per trasferire la chiamata a un operatore automatico. Fare clic su **Sfoglia** per individuare l'operatore automatico che si desidera utilizzare. Prima di abilitare questa opzione, è necessario creare e configurare l'operatore automatico. Questa opzione viene utilizzata quando si crea una struttura padre/figlio di operatori automatici di messaggistica unificata.
        
          - **Lascia un messaggio vocale per questo utente**   Selezionare questa opzione per abilitare un chiamante a lasciare un messaggio vocale per un utente sullo stesso dial plan dell'operatore automatico di messaggistica unificata che si sta configurando. Quando un chiamante sceglie questa opzione dal menu di un operatore automatico, gli verrà richiesto di lasciare un messaggio vocale per l'utente selezionato. Fare clic su **Sfoglia** per individuare l'utente abilitato alla messaggistica unificata.
        
          - **Notifica sede aziendale**   Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sulla sede aziendale che è configurata sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima inserire la sede aziendale nella casella **Sede aziendale** nella pagina **Generale** dell'operatore automatico di messaggistica unificata.
        
          - **Notifica orario di ufficio**  Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sull'orario di ufficio dell'azienda configurato sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima configurare l'orario di ufficio nella pagina **Orario di ufficio** dell'operatore automatico di messaggistica unificata.

5.  Fare clic su **OK** per creare il nuovo menu di navigazione.

6.  Nella pagina **Operatore automatico di messaggistica unificata**, fare clic su **Salva** per salvare le modifiche.

## Utilizzo della Shell per configurare mapping dei tasti operatore automatico messaggistica unificata

Questo esempio vengono attivati i mapping dei tasti orari d'ufficio in modo che:

  - Quando i chiamanti premere 1, essi verranno inoltrate a un altro operatore automatico di messaggistica unificata denominato `SalesAutoAttendant`.

  - Quando si preme 2, essi verranno inoltrate al numero di interno 12345 per il supporto.

  - Quando si preme 3, essi verranno inviati a un altro operatore automatico che riprodurrà un file audio.

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

In questo esempio imposta i mapping dei tasti definito in un file con valori delimitati da virgole (con estensione csv). Creare innanzitutto il file CSV con le seguenti intestazioni e la voce della correzione: \< chiave \> \< descrizione \> \[\< estensione \>\] \[\< nome autoattendant \>\], \[\< promptfilenamepath \>\] \[\< asrphrase1; asrphrase2 \>\], \[\< leavevoicemailfor \>\] \[\< transfertomailbox \>\]. I valori tra parentesi quadre sono facoltativi. Dopo aver creato il file CSV, importare il file CSV utilizzando il cmdlet **Import-csv** .

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

In questo esempio Esporta mapping dei tasti da un operatore automatico di messaggistica unificata esistente in un file CSV e quindi Importa il mapping dei tasti stesso in un altro operatore automatico di messaggistica unificata. Si potrebbe inoltre di esportare il mapping dei tasti in un file CSV, modificare o modificare il mapping dei tasti nel file CSV e quindi importare i mapping dei tasti in un altro operatore automatico di messaggistica unificata.

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

