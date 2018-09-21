---
title: 'Configura cassetta postale quarantena posta indesiderata: Exchange 2013 Help'
TOCTitle: Configurare una cassetta postale di quarantena della posta indesiderata
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 50481170
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare una cassetta postale di quarantena della posta indesiderata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-19_

I messaggi considerati come posta indesiderata dall'agente Filtro contenuto possono essere indirizzati a una cassetta postale di quarantena per la posta indesiderata. Se viene abilitata la soglia di quarantena del livello di probabilità di posta indesiderata (SCL), tutti i messaggi che vengono messi in quarantena vengono inclusi in rapporti di mancato recapito e inviati all'indirizzo SMTP specificato come cassetta postale per la quarantena della posta indesiderata. È quindi possibile rivedere i messaggi in quarantena e, se necessario, inviarli ai destinatari specificati utilizzando la funzionalità Invia di nuovo in Microsoft Outlook.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 45 minuti.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - La persona responsabile della cassetta postale per la quarantena della posta indesiderata può visualizzare messaggi potenzialmente privati e riservati e inviare messaggi per conto di chiunque all'interno dell'organizzazione di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Verifica dell'abilitazione del filtro contenuto

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

1.  Eseguire il comando riportato di seguito per verificare che l'agente Filtro contenuto sia installato e abilitato sul server di Exchange:
    
    ```powershell
Get-TransportAgent "Content Filter Agent"
```

2.  Eseguire il comando riportato di seguito per verificare che il filtro contenuto sia abilitato:
    
    ```powershell
Get-ContentFilterConfig | Format-List Enabled
```

Per ulteriori informazioni, vedere [Gestire il filtro contenuto](manage-content-filtering-exchange-2013-help.md).

## Passaggio 2: Creare una cassetta postale dedicata alla quarantena della posta indesiderata

Per creare una cassetta postale dedicata alla quarantena della posta indesiderata, attenersi alla seguente procedura:

  - **Creare un database Exchange dedicato**   Si consiglia di creare un database dedicato per la cassetta postale della quarantena per la posta indesiderata. La cassetta postale della quarantena per la posta indesiderata deve avere un database di grandi dimensioni, altrimenti se viene raggiunto il limite di archiviazione, i messaggio andranno perduti. Per ulteriori informazioni, vedere [Gestire il database delle cassette postali in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

  - **Creare una cassetta postale dedicata e un account utente**   Si consiglia di creare una cassetta postale dedicata e un account utente di Active Directory per la cassetta postale di quarantena della posta indesiderata. Per ulteriori informazioni, vedere [Creazione di cassette postali utente](create-user-mailboxes-exchange-2013-help.md).
    
    È possibile applicare criteri destinatari, quali gestione dei record di messaggistica, quote della cassetta postale e diritti di delega, in funzione dei criteri di conformità e delle esigenze dell'organizzazione. Per ulteriori informazioni, vedere [Gestione record di messaggistica](https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/messaging-records-management).
    

    > [!NOTE]
    > Se un messaggio in quarantena viene rifiutato a causa di una quota di archiviazione, il messaggio andrà perduto. Exchange non genera rapporti di mancato recapito per i messaggi in quarantena, perché tali messaggi sono inseriti in un wrapper come rapporti di mancato recapito.



  - **Configurare Outlook**   È necessario configurare le autorizzazioni di accesso delegato di Outlook per soddisfare le esigenze dell'organizzazione. Inoltre, è consigliabile configurare il profilo Outlook per mostrare i campi `Sender[#0x0069001E]`, `Recipient[#0x0E04001E]` e `Bcc[#0x0E02001E]` originali nella visualizzazione **Messaggio**. Per ulteriori informazioni, vedere [Versione messaggi dalla cassetta postale di quarantena della posta indesiderata in quarantena](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

## Passaggio 3: Specificare la cassetta postale di quarantena della posta indesiderata

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

Eseguire il comando indicato di seguito:

```powershell
Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>
```

In questo esempio, tutti i messaggi che superano la soglia di quarantena della posta indesiderata vengono inviati a spamQ@contoso.com.

```powershell
Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta definizione della cassetta postale di quarantena della posta indesiderata, attenersi alla procedura seguente:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-ContentFilterConfig | Format-List QuarantineMailbox
```

2.  Verificare che il valore visualizzato sia quello configurato.

## Passaggio 4: Configurare la soglia di quarantena del livello di probabilità di posta indesiderata

La soglia del livello di probabilità di posta indesiderata per la quarantena è il valore con cui un determinato messaggio identificato come potenziale posta indesiderata viene recapitato alla cassetta postale della quarantena per la posta indesiderata. È possibile impostare la soglia del livello di probabilità di posta indesiderata per la quarantena su un valore compreso tra 0 e 9, dove 0 rappresenta il numero minore di probabilità che il messaggio sia posta indesiderata e 9 il numero maggiore di probabilità che il messaggio sia posta indesiderata.

Per ulteriori informazioni sulla regolazione delle soglie del livello di probabilità di posta indesiderata per la quarantena per soddisfare le esigenze della propria azienda e sulla regolazione di tali soglie per ciascun destinatario, vedere [Gestire il filtro contenuto](manage-content-filtering-exchange-2013-help.md).

## Passaggio 5: Gestire la cassetta postale di quarantena della posta indesiderata

Per gestire la cassetta postale della quarantena per la posta indesiderata, attenersi alla seguente procedura:

  - Sbloccare gli elementi che sono stati inviati alla cassetta postale di quarantena della posta indesiderata utilizzando la funzionalità Invia di nuovo in Outlook per rinviare il messaggio originale.
    
    Per ulteriori informazioni, vedere [Versione messaggi dalla cassetta postale di quarantena della posta indesiderata in quarantena](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

  - Monitorare la cassetta postale per la quarantena della posta indesiderata in modo che la dimensione della cassetta postale rimanga entro un livello accettabile. Il volume dei messaggi di posta elettronica può variare in presenza di un insieme di destinatari più ampio, della tendenza naturale dei messaggi di dimensioni superiori o dell'azione della soglia del livello di probabilità di posta indesiderata per la quarantena.

  - Monitorare la cassetta postale per la quarantena della posta indesiderata per verificare se sono presenti falsi positivi. Se la cassetta postale di quarantena della posta indesiderata include molti falsi positivi, è opportuno regolare la soglia di quarantena del livello di probabilità di posta indesiderata. Per ulteriori informazioni su come determinare le ragioni del recapito di falsi positivi alla cassetta postale per la quarantena della posta indesiderata, vedere [Contrassegni filtro posta indesiderata](anti-spam-stamps-exchange-2013-help.md).

  - Utilizzare lo stesso profilo Outlook per recuperare i messaggi in quarantena dalla cassetta postale della quarantena di posta indesiderata. L'applicazione delle autorizzazioni a un profilo Outlook diverso per recuperare i messaggi non è supportata. Non è possibile utilizzare un profilo Outlook diverso per recuperare o sbloccare i messaggi dalla cassetta postale di quarantena della posta indesiderata.


> [!IMPORTANT]
> I rapporti di mancato recapito identificati come posta indesiderata vengono eliminati anche se il livello di probabilità di posta indesiderata indica che dovrebbero essere messi in quarantena. I rapporti di mancato recapito non vengono recapitati alla cassetta postale per la quarantena della posta indesiderata. Per tenere traccia di tali messaggi, utilizzare il registro agente o il registro di verifica messaggi. Per ulteriori informazioni, vedere <A href="anti-spam-agent-logging-exchange-2013-help.md">Registrazione agente di protezione da posta indesiderata</A>.



## Passaggio 6: Regolare la soglia di quarantena del livello di probabilità di posta indesiderata

Dopo avere configurato la soglia del livello di probabilità di posta indesiderata per la quarantena, monitorare periodicamente le impostazioni e regolarle in base alle esigenze dell'organizzazione. Ad esempio, se nella cassetta postale per la quarantena della posta indesiderata vengono filtrati troppi falsi positivi, aumentare il valore della soglia del livello di probabilità di posta indesiderata per la quarantena. Per ulteriori informazioni sulla regolazione della soglia del livello di probabilità di posta indesiderata per la quarantena, vedere [Soglia del livello di probabilità di posta indesiderata](spam-confidence-level-threshold-exchange-2013-help.md).

