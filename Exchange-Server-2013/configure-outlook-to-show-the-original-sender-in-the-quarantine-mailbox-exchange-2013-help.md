---
title: 'Configurare Outlook per visualizzare il mittente originale nella cassetta postale di quarantena: Exchange 2013 Help'
TOCTitle: Configurare Outlook per visualizzare il mittente originale nella cassetta postale di quarantena
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50481209
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare Outlook per visualizzare il mittente originale nella cassetta postale di quarantena

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Quarantena della posta indesiderata è una funzionalità dell'agente Filtro contenuti che riduce il rischio di perdita di messaggi legittimi. Tale funzionalità fornisce una posizione di archiviazione temporanea per i messaggi identificati come posta indesiderata che non devono essere consegnati alla cassetta postale di un utente all'interno dell'organizzazione.

Se un messaggio raggiunge la soglia di quarantena della posta indesiderata, viene racchiuso in un rapporto di mancato recapito (NDR) e recapitato alla cassetta postale di quarantena della posta indesiderata. Poiché i messaggi messi in quarantena vengono archiviati come rapporti di mancato recapito nella cassetta postale per la quarantena, l'indirizzo del postmaster dell'organizzazione verrà elencato come Da: indirizzo per tutti i messaggi. Tuttavia, se si dispone dell'indirizzo originale del mittente, dell'indirizzo originale del destinatario e del livello di probabilità di posta indesiderata originale (SCL) nell'elenco dei campi, sarà più facile individuare il messaggio che si desidera recuperare.

Per impostazione predefinita, non è possibile selezionare questi campi in Microsoft Outlook. Prima di poter aggiungere questi campi nella visualizzazione del messaggio, è necessario creare un modulo Outlook che aggiunga il mittente originale, il destinatario originale e il livello di probabilità di posta indesiderata originale come campi facoltativi selezionabili. Dopo aver creato questo modulo personalizzato, è possibile configurare Outlook per visualizzare questi campi nella visualizzazione del messaggio.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa procedura: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Accesso alle cassette postali" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Questa procedura richiede la configurazione della cassetta postale della quarantena antispam. Per ulteriori informazioni, vedere [Configurare una cassetta postale di quarantena della posta indesiderata](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Per accedere alla cassetta postale di quarantena, è necessario configurare un profilo di Outlook per tale cassetta postale e quindi aprire la cassetta postale utilizzando Outlook. Per ulteriori informazioni sulla configurazione e utilizzo di più profili di Outlook, vedere [Panoramica di Outlook profili di posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=178975).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Passaggio 1: Utilizzare Blocco note per creare un modulo Outlook personalizzato

1.  Aprire Blocco note e copiare il codice riportato di seguito nel documento.
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  Salvare il file nella cartella Forms di Office utilizzando i seguenti valori:
    
      - **Percorso**   *\<Percorso di installazione di Office\>*\\\<*VersioneOffice\>*\\Forms\\*\<LCID\>*
        
          - *\<Percorso di installazione di Office\>*   Per le versioni a 32 bit di Office su versioni a 32 bit di Microsoft Windows o per le versioni a 64 bit di Office su versioni a 64 bit di Windows, il percorso predefinito è `C:\Program Files\Microsoft Office`. Per le versioni a 32 bit di Office su versioni a 64 bit di Windows, il percorso predefinito è `C:\Program Files (x86)\Microsoft Office`.
        
          - *\<VersioneOffice\>*   Per Outlook 2007, il valore è `Office12`. Per Outlook 2010 il valore è `Office14`. Per Outlook 2013 il valore è `Office15`.
        
          - *\<LCID\>*   È il valore dell'ID impostazioni locali (LCID). Ad esempio, il valore LCID per Inglese (Stati Uniti) è 1033. Per ulteriori informazioni, vedere [KB221435: Elenco degli identificatori delle impostazioni locali supportate in Word](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=221435).
    
      - **Nome**   Nel resto della procedura si presumerà che il file sia denominato `QTNE.cfg`. Il nome del file non è importante, ma occorre assicurarsi di racchiudere il valore tra virgolette in modo che il file venga salvato come QTNE.cfg e non come QTNE.cfg.txt.
    
    Ad esempio, per la versione Inglese (Stati Uniti) a a 32 bit di Outlook 2013 installata su una versione a 64 bit di Windows, il file deve essere salvato come:
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    

    > [!NOTE]
    > Se Windows controllo accesso (utente) impedisce il salvataggio del file nella posizione corretta, salvarla prima in un percorso temporaneo e quindi copiarlo.



## Passaggio 2: Configurare Outlook per utilizzare il modulo Outlook personalizzato

Utilizzare una delle seguenti procedure in base alla versione di Outlook installata sul computer.

## Configurare Outlook 2010 o Outlook 2013

1.  In Outlook 2010 o Outlook 2013, fare clic su **File** \> **Opzioni** \> **Avanzate**.

2.  Nella sezione **Sviluppatori**, fare clic su **Moduli personalizzati**.

3.  Nella finestra di dialogo **Opzioni**, fare clic su **Gestione moduli**.

4.  Nella finestra di dialogo **Gestione moduli**, fare clic su **Installa**. Passare al percorso del file `QTNE.cfg` , selezionarlo e fare clic su **Apri**. Nella finestra di dialogo **Proprietà modulo** esaminare le informazioni e quindi fare clic su **OK** per installare il modulo estensione quarantena nella libreria moduli personali.

5.  Nella finestra di dialogo **Gestione moduli**, fare clic su **Chiudi**. Fare clic due volte su **OK** per chiudere le altre finestre di dialogo e ritornare all'interfaccia principale di Outlook.

6.  Sulla scheda della **Home** nella visualizzazione della **Posta elettronica** di Posta in arrivo, fare clic con il tasto destro del mouse sulla riga dell'intestazione della colonna (potrebbe essere necessario espandere l'ampiezza dell'elenco dei messaggi per vedere le colonne) e quindi selezionare **Visualizza impostazioni**.

7.  Nella finestra di dialogo **Impostazioni visualizzazione avanzate**, fare clic su **Colonne**.

8.  Nella finestra di dialogo **Mostra colonne**, scorrere l'elenco a discesa **Seleziona colonne disponibili da** e selezionare **Moduli**.

9.  Nella finestra di dialogo **Seleziona moduli per la colonna**, nel campo **Moduli selezionati**, selezionare **Messaggio** e fare clic su **Rimuovi**. Nel campo **Moduli personali**, selezionare **Modulo estensione quarantena** e fare clic su **Aggiungi**. Al termine, fare clic su **Chiudi**.

10. Nella finestra di dialogo **Mostra colonne**, nella sezione **Colonne disponibili**, selezionare uno o più campi e fare clic su **Aggiungi** dopo ogni campo selezionato.
    
      - **ReceivedRepresentingEmailAddress** mittente originale
    
      - **DisplayTo**   Destinatario originale (si noti che appare come **a** dopo aver aggiunto)
    
      - **OriginalScl** Livello di probabilità di posta indesiderata originale
    
    Utilizzare i pulsanti **Sposta su** o **Sposta giù** per posizionare le colonne nella visualizzazione. Per risultati ottimali, posizionare tre nuovi campi dopo il campo **allegato** e prima del campo **da**. Al termine, fare clic su **OK** due volte per tornare all'interfaccia principale Outlook.

## Configurare Outlook 2007

1.  In Outlook 2007, scegliere **Strumenti** \> **Opzioni**.

2.  Nella finestra di dialogo **Opzioni** fare clic sulla scheda **Altro**, quindi scegliere **Generale**, **Opzioni avanzate**.

3.  Nella finestra di dialogo **Opzioni avanzate** fare clic su **Moduli personalizzati**, quindi dalla finestra di dialogo **Moduli personalizzati** scegliere **Gestisci moduli**.

4.  Nella finestra di dialogo **Gestione moduli**, fare clic su **Installa**. Passare al percorso del file `QTNE.cfg` , selezionarlo e fare clic su **Apri**. Nella finestra di dialogo **Proprietà modulo** esaminare le informazioni e quindi fare clic su **OK** per installare il modulo estensione quarantena nella libreria moduli personali.

5.  Chiudere la finestra di dialogo **Gestione moduli** e quindi fare clic su **OK** tre volte per chiudere le altre finestre di dialogo e tornare all'interfaccia principale Outlook 2007.

6.  Nella visualizzazione **Stampa** della posta in arrivo, fare clic sulla riga di intestazione della colonna (potrebbe essere necessario espandere la larghezza dell'elenco dei messaggi per visualizzare le colonne) e quindi selezionare **Personalizza visualizzazione corrente**.

7.  Nella **Personalizza visualizzazione: i messaggi** finestra di dialogo fare clic su **Mostra campi**.

8.  Nell'elenco a discesa **selezionare campi disponibili dalla** finestra di dialogo **Mostra campi** scorrere fino alla fine dell'elenco e selezionare **moduli**.

9.  Nella finestra di dialogo **Seleziona moduli per la colonna**, nel campo **Moduli selezionati**, selezionare **Messaggio** e fare clic su **Rimuovi**. Nel campo **Moduli personali**, selezionare **Modulo estensione quarantena** e fare clic su **Aggiungi**. Al termine, fare clic su **Chiudi**.

10. Nella finestra di dialogo **Mostra campi**, nella sezione **Campi disponibili** selezionare uno o più campi e fare clic su **Aggiungi** dopo ogni campo selezionato.
    
      - **ReceivedRepresentingEmailAddress** mittente originale
    
      - **DisplayTo**   Destinatario originale (si noti che appare come **a** dopo aver aggiunto)
    
      - **OriginalScl** Livello di probabilità di posta indesiderata originale
    
    Utilizzare i pulsanti **Sposta su** o **Sposta giù** per posizionare le colonne nella visualizzazione. Per risultati ottimali, posizionare tre nuovi campi dopo il campo **allegato** e prima del campo **da**. Al termine, fare clic su **OK** due volte per tornare all'interfaccia principale Outlook 2007.

## Come verificare se l'operazione ha avuto esito positivo

Questa procedura ha avuto esito positivo se è possibile vedere i valori originali di mittente, destinatario e livello di probabilità di posta indesiderata per i messaggi in quarantena nella cassetta postale di quarantena della posta indesiderata utilizzando Outlook.

