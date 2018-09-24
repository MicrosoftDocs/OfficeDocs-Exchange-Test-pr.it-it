---
title: 'Config. periodo mantenimento eliminati e ripristinabili: Exchange 2013 Help'
TOCTitle: Configurare il periodo di mantenimento degli elementi eliminati e delle quote di elementi ripristinabili
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50555701
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il periodo di mantenimento degli elementi eliminati e delle quote di elementi ripristinabili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Quando un utente elimina elementi dalla cartella Posta eliminata predefinita, premendo CANC o MAIUSC+CANC oppure tramite il comando **Svuota cartella Posta eliminata**, tali elementi vengono spostati nella cartella **Elementi ripristinabili\\Eliminazioni**. Il periodo di tempo per cui gli elementi eliminati rimangono in tale cartella dipende dalle impostazioni di mantenimento degli elementi eliminati configurate per il database delle cassette postali o per la cassetta postale. Per impostazione predefinita, il database delle cassette postali è configurato in modo da conservare gli elementi eliminati per 14 giorni, mentre le opzioni Quota di avviso elementi recuperabili e Quota elementi recuperabili sono impostate, rispettivamente, su 20 GB e 30 GB.


> [!NOTE]
> Prima il periodo di mantenimento per gli elementi eliminati trascorre, Microsoft Outlook e Microsoft OfficeOutlook Web App gli utenti possono recuperare gli elementi eliminati utilizzando la caratteristica Recupera elementi eliminati. Per ulteriori informazioni su queste funzionalità, vedere l'argomento "Recupera posta eliminata" per <A href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</A>.



È possibile utilizzare la Shell per configurare le impostazioni di mantenimento elementi eliminati e le quote degli elementi recuperabili per una cassetta postale o i database delle cassette postali. Mantenimento elementi eliminati impostazioni vengono ignorate quando una cassetta postale si trova in conservazione In locale o conservazione per controversia attesa.

Per ulteriori informazioni sulla conservazione degli elementi eliminati, la cartella degli elementi ripristinabili, l'archiviazione sul posto e la conservazione per controversia legale, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurare la conservazione degli elementi eliminati per una cassetta postale

**Utilizzare EAC per configurare il mantenimento degli elementi eliminati per una cassetta postale**

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Nella visualizzazione elenco, selezionare una cassetta postale, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà delle cassette postali, fare clic su **utilizzo cassetta postale**, fare clic su **altre opzioni** e quindi selezionare una delle operazioni seguenti
    
      - **Utilizzare le impostazioni di conservazione predefinito del database delle cassette postali**    Utilizzare questa opzione per utilizzare l'impostazione di mantenimento elementi eliminati configurato per il database delle cassette postali.
    
      - **Personalizzare le impostazioni per la cassetta postale**    Utilizzare questa impostazione per configurare le impostazioni di mantenimento elementi eliminati per la cassetta postale.
        
        **Mantieni elementi eliminati per (giorni)**    Consente di visualizzare questa casella periodo di mantenimento degli elementi eliminati vengono mantenuti prima di essere eliminati in modo definitivo e non possono essere recuperati dall'utente. Quando viene creata la cassetta postale, questo valore si basa sulle impostazioni di mantenimento elementi eliminati configurate per il database delle cassette postali. Per impostazione predefinita, un database delle cassette postali è configurato per conservare gli elementi eliminati 14 giorni. Intervallo di valori per questa proprietà è compreso tra 0 e 24,855 giorni.
    
      - **Non eliminare definitivamente questi elementi prima di aver creato una copia di backup del database**   Selezionare questa casella di controllo per impedire che le cassette postali e i messaggi di posta elettronica vengano eliminati prima che sia stato eseguito il backup del database in cui si trova la cassetta postale in questione.

**Utilizzo della Shell per configurare il mantenimento degli elementi eliminati per una cassetta postale**

In questo esempio la cassetta postale di April Stewart viene configurata in modo da mantenere gli elementi eliminati per 30 giorni.

```powershell
Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Utilizzo della Shell per configurare le quote degli elementi recuperabili per una cassetta postale


> [!NOTE]
> Non è possibile utilizzare EAC per configurare le quote degli elementi ripristinabili per una cassetta postale.



Con questo esempio vengono configurate la quota di avviso degli elementi recuperabili e la quota degli elementi recuperabili della cassetta postale di April Stewart rispettivamente su 12 GB e 15 GB.

```powershell
    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false
```

> [!NOTE]
> Per configurare una cassetta postale in modo da utilizzare quote per gli elementi recuperabili diverse da quella del database delle cassette postali in cui risiede, è necessario impostare il parametro <EM>UseDatabaseQuotaDefaults</EM> su <CODE>$false</CODE>.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Utilizzo della Shell per configurare il mantenimento degli elementi eliminati per un database delle cassette postali


> [!NOTE]
> Non è possibile utilizzare EAC per configurare la conservazione degli elementi eliminati per un database delle cassette postali.



In questo esempio viene configurato un periodo di mantenimento di 10 giorni per il database delle cassette postali MDB2.

```powershell
Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)).

## Utilizzo della Shell per configurare le quote degli elementi recuperabili per un database delle cassette postali


> [!NOTE]
> Non è possibile utilizzare EAC per configurare le quote degli elementi ripristinabili per un database delle cassette postali



Con questo esempio vengono configurate la quota di avviso degli elementi recuperabili e la quota degli elementi recuperabili del database delle cassette postali MDB2 rispettivamente su 15 GB e 20 GB.

```powershell
Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)).

