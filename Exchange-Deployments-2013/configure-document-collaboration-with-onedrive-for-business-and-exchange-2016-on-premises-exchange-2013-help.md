---
title: 'Configurare gli allegati più recenti utilizzando le versioni in locale di OneDrive for Business ed Exchange 2016: Exchange 2013 Help'
TOCTitle: Configurare gli allegati più recenti utilizzando le versioni in locale di OneDrive for Business ed Exchange 2016
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70319590
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurare gli allegati più recenti utilizzando le versioni in locale di OneDrive for Business ed Exchange 2016

 

_**Si applica a:**Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

**Riepilogo:** Come consentire agli utenti di Exchange Server 2016 locali di trarre vantaggio dalla collaborazione dei documenti con OneDrive for Business e SharePoint Online in una configurazione ibrida.

Recentemente, in Office 365 è stata resa disponibile una nuova opzione per gli allegati. In Exchange 2016, questa opzione, nota come *Collaborazione dei documenti*, consente agli utenti locali di integrare allegati archiviati in OneDrive for Business direttamente nel propri client di Outlook sul web.


> [!NOTE]
> A partire dalla release di Exchange Server 2016, Outlook Web App è ora noto come Outlook sul web.



In genere, un utente invia un file ad altri utenti allegandolo a un messaggio. Quindi uno o più destinatari apportano modifiche alle rispettive copie del file che a un certo punto devono essere unite nello stesso documento. Inoltre, i file allegati occupano spazio di archiviazione nella cassetta postale di ogni utente. La collaborazione dei documenti consente invece agli utenti di inserire un collegamento a un file archiviato in un account OneDrive for Business. Ciò permette che il file venga modificato da più utenti nella stessa posizione di origine, senza bisogno di spazio di archiviazione aggiuntivo.

Prima che l'ambiente Exchange 2016 venga configurato correttamente per la collaborazione dei documenti, verrà visualizzata una finestra di dialogo allegati predefinita dell'utente di Outlook sul web simile alla seguente:

![finestra di dialogo degli allegati tradizionali](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "finestra di dialogo degli allegati tradizionali")

Dopo aver configurato l'ambiente con le istruzioni riportate di seguito, le finestre di dialogo allegati di Outlook sul web saranno simili alla seguente:

![finestra di dialogo degli allegati con gli allegati moderni abilitati](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "finestra di dialogo degli allegati con gli allegati moderni abilitati")

Gli utenti dell'organizzazione con cassette postali locali e che dispongono di un account OneDrive for Business in Office 365 sono idonei per utilizzare il metodo allegato moderno, che consente di condividere un documento archiviato in OneDrive for Business con più destinatari. La posizione dei destinatari non ha importanza (online o locale).

Per maggiori informazioni sulle distribuzioni ibride, vedere [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15 minuti

  - Leggere l'argomento [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) e assicurarsi di avere identificato tutte le aree interessate dalla configurazione di una distribuzione ibrida.

  - Esaminare e completare tutti i requisiti di distribuzione ibrida illustrati in [Prerequisiti per la distribuzione ibrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](https://technet.microsoft.com/it-it/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurare Exchange 2016 per abilitare la collaborazione dei documenti in un ambiente ibrido

Verificare che siano state completate le seguenti operazioni preliminari, quindi utilizzare la procedura seguente per abilitare la collaborazione dei documenti.

**Prerequisiti**

  - Configurare l'ambiente ibrido di Exchange utilizzando [Procedura guidata di configurazione ibrida](hybrid-configuration-wizard-exchange-2013-help.md) (HCW).

  - Exchange 2016 deve essere installato nell'organizzazione locale. Exchange 2016 può coesistere con versioni precedenti di Exchange, ma la collaborazione dei documenti funziona solo per le cassette postali in un server Exchange 2016.

  - Il server di autenticazione deve essere installato con tutti gli utenti sincronizzati. È possibile utilizzare il cmdlet [Get-AuthServer](https://technet.microsoft.com/it-it/library/jj218613\(v=exchg.150\)) per trovare il server di autenticazione. È consigliabile usare HCW da un server Exchange 2016 per qualsiasi configurazione OAuth necessaria.
    

    > [!IMPORTANT]
    > OAuth deve essere configurato correttamente tra 2016 Exchange e Office 365. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/dn594521(v=exchg.150)">Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online</A>.



  - Gli utenti devono disporre delle licenze appropriate. Gli utenti con un account OneDrive for Business devono disporre della licenza per SharePoint Online o OneDrive for Business. È possibile verificare una licenza utente selezionando l'utente nel portale di Office 365 e selezionando il pulsante **Modifica**.
    

    > [!NOTE]
    > Vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=627455">Configurare OneDrive for Business in Office 365</A> per ulteriori informazioni.



Eseguire le operazioni seguenti:

1.  Configurare il criterio per le cassette postali predefinito in Outllok sul web in modo che imposti l’URL dell’host di OneDrive for Business.
    

    > [!NOTE]
    > È possibile passare all’amministratore tenant di Office 365 SharePoint Online per l'URL host di OneDrive for Business. Ad esempio https://contoso-my.sharepoint.com è un URL Host di Sito personale nel tenant di Office 365 di Contoso.<BR>Anche se il criterio per le cassette postali di Outlook sul web fornito con Exchange 2016 è denominato "Predefinito", non viene automaticamente applicato a tutte le cassette postali a meno che l’utente non lo renda il criterio predefinito o lo assegni direttamente a una cassetta postale.

    
    Come nell'esempio seguente, utilizzare Exchange Management Shell per configurare l'URL di Sito personale interno ed esterno nel criterio per le cassette postali di Outlook sul web:
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  Successivamente, impostare il criterio appena configurato come criterio predefinito, in modo che verrà applicato a tutte le cassette postali oppure assegnare il criterio ai singoli utenti.
    
    Per renderlo il criterio per le cassette postali predefinito di Outlook sul web, digitare il comando seguente in Exchange Management Shell:
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    Per assegnare il criterio alla cassetta postale di una persona, digitare il seguente comando in Exchange Management Shell:
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (Facoltativo) In ogni server di Exchange 2016, riavviare **OWAApplicationPool**, che consente alla configurazione di lavorare immediatamente. Se non si esegue questo comando, saranno necessari alcuni minuti prima che i server di Exchange 2016 applichino il criterio cassetta postale aggiornato. Nel Exchange Management Shell eseguire:
    
        Restart-WebAppPool MSExchangeOWAAppPool

Dopo la configurazione, gli utenti di Outlook sul web avranno l’opzione di scegliere il tipo di allegato che desiderano applicare ai propri messaggi: tradizionale o moderno.

![finestra di dialogo delle opzioni in allegato, Condividi con OneDrive o Invia come allegato](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "finestra di dialogo delle opzioni in allegato, Condividi con OneDrive o Invia come allegato")

