---
title: "Semplificazione dell'URL di Outlook Web App: Exchange 2013 Help"
TOCTitle: Semplificazione dell'URL di Outlook Web App
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54652868
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Semplificazione dell'URL di Outlook Web App

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-07-16_

**Riepilogo:**  Usare le procedure descritte in questo articolo per semplificare l'URL che gli utenti dell'organizzazione utilizzano per accedere a OWA in Exchange 2013.

È possibile semplificare l'URL di MicrosoftOutlook Web App che consente agli utenti di accedere alla propria cassetta postale di Exchange Server 2013.

Per semplificare l'accesso a Outlook Web App per gli utenti, è possibile configurare la pagina Web di Outlook Web App, che di solito è il sito Web predefinito in IIS, in modo che reindirizzi automaticamente gli utenti a https. La procedura di semplificazione dell'URL di Outlook Web App e reindirizzamento forzato a SSL (Secure Sockets Layer) consente di inviare una richiesta per l'indirizzo http://*server* a https://*server*/owa. Per proteggere le informazioni inviate tra il client e il server, il sito Web predefinito viene impostato in modo da richiedere SSL (Secure Sockets Layer) durante l'installazione.

Quando si configura il reindirizzamento da una directory di primo livello in Windows Server 2008, le impostazioni vengono propagate alle directory di livello inferiore. Ad esempio, quando si configura il reindirizzamento sul sito Web predefinito alla directory virtuale /owa, le impostazioni configurate vengono visualizzate anche nella pagina di reindirizzamento HTTP di tutte le directory virtuali, quali /Autodiscover, /Exchange e /Public. È necessario, pertanto, rimuovere il reindirizzamento da tutte le directory virtuali, fatta eccezione per quella che si desidera reindirizzare.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione IIS" nella sezione Autorizzazioni Outlook Web App dell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Passaggio 1: Semplificazione dell'URL di Outlook Web App e reindirizzamento forzato a SSL tramite Gestione IIS

1.  Avviare Gestione IIS.

2.  Espandere il computer locale, espandere **Siti**, quindi fare clic su **Sito Web predefinito**.

3.  Nella parte inferiore del riquadro Home sito Web predefinito, fare clic su **Visualizzazione funzionalità** se questa opzione non risulta già selezionata.

4.  Nella sezione**IIS** fare doppio clic su **Reindirizzamento HTTP**.

5.  Selezionare la casella di controllo **Reindirizza le richieste a questa destinazione**.

6.  Digitare il percorso assoluto della directory virtuale /owa. Ad esempio, digitare **https://mail.contoso.com/owa**.

7.  In **Comportamento di reindirizzamento** selezionare la casella di controllo **Reindirizza le richieste solo al contenuto di questa directory (non directory secondarie)**.

8.  Nell'elenco **Codice di stato** fare clic su **Trovato (302)**.

9.  Nel riquadro Azioni fare clic su **Applica**.

10. Fare clic su **Sito Web predefinito**.

11. Nel riquadro della Home del sito Web predefinito fare doppio clic su **Impostazioni SSL**.

12. In **Impostazioni SSL** deselezionare **Richiedi SSL**.
    

    > [!NOTE]
    > Se non si deseleziona <STRONG>Richiedi SSL</STRONG>, gli utenti non vengono reindirizzati quando immettono un URL non protetto. Ricevono invece un messaggio di errore che indica che l'accesso è stato negato.



## Passaggio 2: Rimozione del reindirizzamento dalle directory virtuali

Per rimuovere il reindirizzamento da una directory virtuale, attenersi alla seguente procedura:

1.  Aprire una finestra del prompt dei comandi.

2.  Passare a \<*Window directory*\>\\System32\\Inetsrv.

3.  Eseguire i comandi seguenti:
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  Completare la procedura eseguendo il comando `iisreset/noforce`.

Quando si configura il reindirizzamento da una directory di livello superiore, è possibile che in \<*drive*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab venga creato un file web.config. In tal caso, se in seguito il reindirizzamento viene rimosso, è possibile che Outlook si blocchi quando gli utenti fanno clic su **Invia/Ricevi**. Per evitare che si verifichi questo problema dopo che il reindirizzamento è stato rimosso, eliminare il file web.config da \<*drive*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'URL Outlook Web App sia stato correttamente semplificato e reindirizzato a una connessione SSL, procedere come segue:

1.  Aprire un Web browser e immettere il nuovo URL per Outlook Web App, utilizzando il formato http://\<*URL*\>.

2.  L'utente è reindirizzato alla pagina di accesso Outlook Web App attraverso una connessione SSL.

