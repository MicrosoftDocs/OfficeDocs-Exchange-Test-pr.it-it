---
title: 'Personalizza accesso, selez. lingua/errore-Outlook Web App: Exchange 2013 Help'
TOCTitle: Personalizzare le pagine di accesso, di selezione della lingua e di errore di Outlook Web App
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54652888
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizzare le pagine di accesso, di selezione della lingua e di errore di Outlook Web App

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento viene illustrato come personalizzare il colore e le immagini delle pagine di accesso, selezione della lingua ed errore per Outlook Web App.

Il Outlook Web App accesso, la selezione della lingua e pagine di errore vengono create base nei file con estensione CSS e grafica nella cartella risorse di temi. Outlook Web App utilizza solo un set di accesso, la selezione della lingua e le pagine di errore per tutti i temi. Modifiche alle pagine verranno visualizzate da tutti gli utenti. È possibile trovare la cartella di risorse tema nella directory di installazione Exchange in V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources. È necessario un editor di testo per cambiare i colori predefiniti e un editor di grafica per modificare le immagini. Se deve corrispondere a un colore specifico e non è possibile trovare una corrispondenza nella [Tabella dei colori](https://go.microsoft.com/fwlink/p/?linkid=280679), è possibile utilizzare un'immagine dello strumento di modifica per campionare un colore e determinare il relativo valore RGB HTML.

In presenza di più server che supportano Outlook Web App, se si desidera che tutti utilizzino le stesse pagine di accesso, selezione della lingua ed errore, è necessario copiare i file modificati su ogni server. È inoltre necessario creare una copia di backup dei file personalizzati. Se viene reinstallato o aggiornato Exchange, tutti i file presenti nelle cartelle dei temi verranno sovrascritti. Al termine della reinstallazione o dell'aggiornamento, sarà necessario ricopiare i file personalizzati nella cartella appropriata.


> [!IMPORTANT]
> Creare le copie di backup di tutti i file da modificare prima di iniziare a creare le pagine di accesso e disconnessione personalizzate.



Per informazioni relative alla creazione di un tema personalizzato, vedere [Creare un tema per Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 45 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Editor grafici" sotto \&quot;Autorizzazioni di Outlook Web App\&quot; nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Personalizzazione del colore della pagina di accesso

1.  Accedere al server Exchange e utilizzare Esplora risorse per andare alla directory di installazione e individuare \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<versione\>\\themes\\resources.

2.  Per aprire il file login.css utilizzare un editor di testo, ad esempio Blocco note.

3.  Cercare il c valore \#0072 colore predefinito 6 e sostituirlo con il valore RGB HTML per il colore che si desidera utilizzare. È possibile trovare valori RGB HTML: [Tavolozza colori](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salvare e chiudere il file.

## Personalizzazione del colore della pagina di errore

1.  Accedere al server Exchange e utilizzare Esplora risorse per andare alla directory di installazione e individuare \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<versione\>\\themes\\resources.

2.  Per aprire il file errorFE.css utilizzare un editor di testo, ad esempio Blocco note.

3.  Cercare il c valore \#0072 colore predefinito 6 e sostituirlo con il valore RGB HTML per il colore che si desidera utilizzare. È possibile trovare valori RGB HTML: [Tavolozza colori](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salvare e chiudere il file.

## Personalizzazione del colore della pagina di selezione della lingua

1.  Accedere al server Exchange e utilizzare Esplora risorse per andare alla directory di installazione e individuare \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles.

2.  Per aprire il file languageselection.css utilizzare un editor di testo, ad esempio, il Blocco note.

3.  Cercare il c valore \#0072 colore predefinito 6 e sostituirlo con il valore RGB HTML per il colore che si desidera utilizzare. È possibile trovare valori RGB HTML: [Tavolozza colori](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salvare e chiudere il file.

## Personalizzazione delle immagini delle pagine di accesso e di errore

Utilizzare uno strumento di editing delle immagini per modificare le immagini usate per creare le pagine di accesso e di errore.

1.  Accedere al server Exchange e utilizzare Esplora risorse per andare alla directory di installazione e individuare \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<versione\>\\themes\\resources.

2.  Utilizzare un editor grafico per aprire e modificare i seguenti file:
    
      - owa\_text\_blue.png, per modificare il logo del testo \&quot;Outlook Web App\&quot;.
    
      - olk\_logo\_white.png, per modificare il logo dell'app nella barra sinistra.
    
      - olk\_logo\_white\_cropped.png, per modificare l'immagine nel pannello laterale sinistro della pagina di errore.
    
      - sign\_in\_arrow.png, per modificare l'icona a sinistra del pulsante di accesso.
    
      - olk\_exchange\_text\_blue.png, per modificare il logo di \&quot;Outlook Mobile\&quot; nel layout tnarrow.
    
      - olk\_logo\_white\_small.png è utilizzato in tnarrow.
    
      - olk\_exchange\_text\_stacked\_white\_small.png è utilizzato in tnarrow.

3.  Cercare il c valore \#0072 colore predefinito 6 e sostituirlo con il valore RGB HTML per il colore che si desidera utilizzare. È possibile trovare valori RGB HTML: [Tavolozza colori](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salvare e chiudere il file.

## Come verificare se l'operazione ha avuto esito positivo

Aprire la pagina di accesso di Outlook Web App in Internet Explorer. Se si intende verificare le modifiche apportate al sito Web predefinito sul server che ospita la directory virtuale di Outlook Web App, è possibile eseguire la prova aprendo Internet Explorer ed inserendo l'URL https://localhost/owa.

Se le modifiche non vengono visualizzate, procedere come segue:

1.  Nella barra degli strumenti, selezionare **Impostazioni** \> **Opzioni Internet** \> **Generale**.

2.  Sotto **Cronologia esplorazioni** selezionare **Elimina**.

3.  Selezionare **File temporanei Internet e file di siti Web**, quindi scegliere **Elimina**.

4.  Al termine dell'eliminazione, selezionare **OK** per chiudere le **Opzioni Internet**.

5.  Aggiornare la finestra del browser.


> [!TIP]
> Per visualizzare gli effetti delle modifiche, è possibile tenere aperto il file CSS in corso di modifica e aggiornare la finestra del browser dopo aver salvato ogni modifica.


