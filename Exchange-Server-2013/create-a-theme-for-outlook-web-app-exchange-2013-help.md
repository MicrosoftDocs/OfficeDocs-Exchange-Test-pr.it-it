---
title: 'Creare un tema per Outlook Web App: Exchange 2013 Help'
TOCTitle: Creare un tema per Outlook Web App
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54652875
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un tema per Outlook Web App

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Un *tema* definisce il colore di sfondo, tipi di carattere, colori di evidenziazione, le icone e intestazione utilizzati da MicrosoftOutlook Web App. Ogni tema è un insieme di file multimediali e file (con estensione CSS) fogli di stile CSS che vengono archiviati nel serverExchangeMicrosoft nella directory di installazione in \\Client Access\\OWA\\prem\\*version*\\resources\\themes. Ogni tema viene archiviato in una sottodirectory della \\THEMES..

Vedere \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base il tema predefinito. Ogni cartella tema contiene tutti i file necessari per definire un tema. Questi file includono file CSS, grafica e un file XML che definisce il nome del tema. Temi aggiuntivi vengono creati copiando tutti i file da un tema in una nuova cartella e modificare i file in base alle esigenze.

Per impostazione predefinita, più temi vengono installati durante l'installazione di Exchange Server 2013, come segue:

  - I file con estensione css definiscono colori, sfumature e tipi di carattere.

  - I file di immagine (.png) forniscono le icone e altri elementi grafici. Se si modifica una qualsiasi delle icone, non modificarne la dimensione. Se si modifica la dimensione di altri elementi grafici, verificare le modifiche per assicurarsi che gli elementi continuino a rientrare tutti insieme negli appositi spazi.

Questi file vengono archiviati nel server Accesso Client nella directory di installazione in \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes. Ogni tema viene archiviato in una sottodirectory dei temi. È possibile creare ulteriori temi copiando un tema esistente e modificare la copia.

Dopo aver creato un tema, è anche possibile procedere con la[Personalizzare le pagine di accesso, di selezione della lingua e di errore di Outlook Web App](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md).


> [!NOTE]
> La versione light di Outlook Web App non supporta i temi.




> [!WARNING]
> In caso di più server che supportano Outlook Web App, copiare il tema personalizzato su ogni server. È inoltre necessario creare una copia di backup del tema personalizzato. Se Exchange viene reinstallato o aggiornato, tutti i file presenti nelle cartelle dei temi verranno sovrascritti. Una volta completata la reinstallazione o l'aggiornamento, sarà necessario ricopiare il tema personalizzato nella cartella appropriata.<BR>Eseguire copie di backup di tutti i file che verranno modificati prima di iniziare a creare il tema personalizzato.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 60 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Directory virtuali di Outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - È necessario disporre dell'accesso di amministratore del server locale per eseguire queste procedure.

  - È necessario un editor di testo per cambiare i colori predefiniti e un editor di grafica per modificare le immagini. Se deve corrispondere a un colore specifico e non è possibile trovare una corrispondenza nella [Tabella dei colori](https://go.microsoft.com/fwlink/p/?linkid=280679), è possibile utilizzare un'immagine dello strumento di modifica per campionare un colore e determinare il relativo valore RGB HTML.

  - Si consiglia di utilizzare le linee guida seguenti ogni volta che si modifica o si crea un tema di Outlook Web App:
    
      - Se si decide di modificare un tema esistente, assicurarsi di eseguire copie di backup dei file originali prima di iniziare a modificarli.
    
      - Non elimina i \\resources\\themes\\base*version*\\Client Access\\OWA\\prem\\ cartella o uno dei file in essa contenuti.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Come eseguire l'operazione?

## Passaggio 1: Creazione di un nuovo tema di Outlook Web App

Per iniziare, creare una cartella per il nuovo tema, quindi copiare nella nuova cartella i file dal tema esistente.

1.  Connettersi al server Exchange che ospita la directory virtuale di Outlook Web App utilizzando un account che disponga della delega di appartenenza al gruppo Administrators locale.

2.  Aprire Esplora risorse di Windows, quindi individuare la directory di installazione del server Exchange.

3.  In \\Client Access\\OWA\\prem\\*version*\\resources\\themes, creare una nuova cartella e denominarla, ad esempio, Fourth Coffee.

4.  Copiare da un altro tema tutti i file nella nuova cartella.

## Passaggio 2: Attribuzione del nome al nuovo tema

Per impostare il nome di visualizzazione del nuovo tema, procedere come segue:

1.  Aprire la copia del file themeinfo.xml che si trova nella cartella del tema personalizzato appena creata.

2.  Trovare il valore `displayname` del tema e modificarlo a seconda del nome che si desidera utilizzare. Ad esempio: `displayname = "Fourth Coffee Theme"`.

3.  Salvare e chiudere il file themeinfo.xml

## Passaggio 3: Modificare l'ordinamento del nuovo tema (opzione facoltativa)

Se si desidera è possibile modificare l'ordinamento del nuovo tema, modificando il file themeinfo.xml. L'ordinamento determina la posizione del tema nel riquadro **Cambia tema** del menu Impostazioni.

Per modificare l'ordinamento del nuovo tema utilizzando il file themeinfo.xml, procedere come segue:

1.  Aprire la copia del file themeinfo.xml che si trova nella cartella del tema personalizzato.

2.  Trovare il valore `sortorder` del tema e modificarlo affinché rispecchi la posizione in elenco in cui si desidera visualizzare il nuovo tema. I temi verranno ordinati per valore numerico in ordine crescente. Per impostazione predefinita, il tema di base è il primo e il relativo valore `sortorder` "0". Ad esempio: `sortorder="<number>"`.

3.  Salvare e chiudere il file themeinfo.xml

## Passaggio 4: Modifica del nuovo tema

Dopo aver copiato i file e denominato il tema, è possibile personalizzarlo. I seguenti elementi possono essere personalizzati in un tema di Outlook Web App:

  - File immagine, che definiscono l'area intestazione e le icone.

  - File CSS, che definiscono caratteri e colori.

## File immagine

Le immagini del tema vengono memorizzate in due cartelle in \\themes*\\\<theme name\>*\\images\\. La cartella \\images\\0 contiene immagini che verranno utilizzate nelle lingue da sinistra a destra (ad esempio la lingua inglese) mentre le lingue da destra a sinistra utilizzeranno le immagini nella cartella \\images\\rtl.


> [!NOTE]
> Alcune delle immagini nella cartella \images\rtl sono le stesse della cartella \images\0, ma sono speculari.



Per la personalizzazione del tema, è possibile utilizzare uno strumento di modifica dell'immagine per aprire e modificare le immagini seguenti:

  - Headerbgmain.png
    
      - Questa è l'immagine intestazione principale. Si consiglia di verificare che l'immagine non superi l'altezza testata di 30 pixel. Il tema predefinito non utilizza un'immagine di sfondo, quindi l'immagine è trasparente. Per un esempio di un tema con un'immagine di sfondo personalizzata, vedere l'immagine nella cartella del tema **Progetto**.

  - Headerbgright.png
    
      - Viene utilizzata come immagine di affiancamento dietro l'intestazione. Il tema predefinito non utilizza un'immagine di sfondo di affiancamento, quindi l'immagine è trasparente. Per un esempio di un tema con un'immagine di sfondo di affiancamento personalizzata, vedere l'immagine nella cartella del tema **Progetto**.

  - sprite1.mouse.png
    
      - Contiene la maggior parte delle immagini utilizzate in un tema. È possibile modificare il colore delle immagini affinché corrisponda al tema e modificare anche il logo di testo Outlook Web App predefinito.
    
      - Per evitare problemi, non modificare la dimensione delle icone individuali in sprite e assicurarsi di aver eseguito il salvataggio come file .png trasparente.

  - themepreview.png
    
      - L'immagine verrà utilizzata per rappresentare il tema nel pannello **Cambia tema** del menu Impostazioni in Outlook Web App.

## Colori e caratteri

I file CSS definiscono i colori e i caratteri utilizzati in un tema e vengono memorizzati in cartelle multiple in \\themes\\*\<nome tema\>*. La cartella \\*\<nome tema\>*\\0 contiene i file .css che verranno utilizzati nelle lingue da sinistra a destra (ad esempio l'inglese), mentre le lingue da destra a sinistra utilizzeranno i file .css nella cartella \\*\<nome tema\>*\\rtl. Esistono anche cartelle specifiche per lingua, (ad esempio, \\ja, \\ko, \\zhs e \\zht) che contengono file .css da utilizzare con tali lingue.

Avviare modificando il \\*\<theme name\>*\\images\\0 cartella. Esistono quattro colori utilizzati in ogni tema che può essere personalizzata.

  - BrandColor: \#0072C6

  - NavBarHoverColor: \#4C9CD7

  - UnreadColor: \#2A8DD4

  - FocusColor: \#DFEDFA

È possibile utilizzare un editor di testo come Blocco note per ricercare e sostituire tutte le istanze di questi valori con i colori del tema nei due file seguenti: owa2styles.mouseCSS and owa2styles2.mouseCSS. È necessario eseguire l'operazione in tutti i i file del nuovo tema che contengono questi file .css.

## Passaggio 5: Impostazione del tema predefinito di Outlook Web App

L'impostazione di un nuovo tema predefinito influirà solo sugli utenti che non hanno modificato il tema nel menu Impostazioni di Outlook Web App.

Per impostare il tema predefinito per tutti gli utenti, è necessario disattivare la selezione del tema oltre a impostare un tema predefinito.

## Impostazione del tema predefinito per Outlook Web App tramite Shell

In questo esempio viene impostato il tema predefinito di Outlook Web App, dove il nome del server è `fourthcoffee`, il nome della directory virtuale è `owa`, l nome del sito Web è `default web site` e il tema si trova nella cartella denominata `Custom`.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\)).

## Disabilitazione della selezione del tema per Outlook Web App tramite Shell

In questo esempio viene disabilitata la selezione del tema in Outlook Web App, dove il nome del server è `fourthcoffee`, il nome della directory virtuale è `owa` e il nome del sito Web è `default web site`.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 

Inoltre è possibile eseguire entrambi i comandi contemporaneamente mediante il seguente comando:

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\)).

## Passaggio 6: Esecuzione di iisreset/noforce per salvare le modifiche

Se si aggiunge o si modifica un tema, se si modifica il nome di un tema o il suo ordinamento, è necessario arrestare e avviare IIS (Internet Information Services) affinché la modifica abbia effetto. A tal fine, aprire una finestra del prompt dei comandi sul server dove è stato creato il nuovo tema ed eseguire il comando **iisresest /nforce**.

## Come verificare se l'operazione ha avuto esito positivo?

1.  Accedere a Outlook Web App tramite la directory virtuale sul server dove è stato creato il nuovo tema. Se si stanno verificando le modifiche al sito Web predefinito sul server Exchange che ospita la directory virtuale Outlook Web App, è possibile effettuare la verifica aprendo Internet Explorer e inserendo l'URL https://localhost/owa.

2.  Passare al tema personalizzato selezionando il menu Impostazioni \> **Cambia tema** e selezionando il tema personalizzato.

## Nonostante l'esecuzione di iisreset/noforce le modifiche più recenti non vengono visualizzate

1.  Dalla barra degli strumenti Internet Explorer, selezionare il menu Impostazioni \> **Opzioni Internet**.

2.  Dalla scheda **Generale**, in **Cronologia esplorazioni**, selezionare **Elimina**, quindi verificare che **File temporanei Internet e file sito Web** sia selezionato. Quindi selezionare **Elimina** per rimuovere i file.

3.  Selezionare **OK** per chiudere **Opzioni Internet**.

4.  Selezionare **Aggiorna** per visualizzare le modifiche.

Ogni volta che si apporta una modifica ai file del tema, ripetere questi passaggi per visualizzare le modifiche. Se si apportano diverse modifiche, è possibile lasciare Outlook Web App aperto e ripetere l'esecuzione di **iisreset/noforce** sul server e cancellare i file temporanei da Internet Explorer in base alle esigenze.

