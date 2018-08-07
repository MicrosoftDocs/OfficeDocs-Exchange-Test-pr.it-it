---
title: 'Config. cartelle pubb. Exchange Online per distrib. ibrida: Exchange 2013 Help'
TOCTitle: Configurare le cartelle pubbliche di Exchange Online per una distribuzione ibrida
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768734
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le cartelle pubbliche di Exchange Online per una distribuzione ibrida

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-15_

**Riepilogo:**  istruzioni per l'attivazione locale Exchange 2013 agli utenti di accedere alle cartelle pubbliche in Exchange Online.

In una distribuzione ibrida, gli utenti possono essere in Exchange Online, locale o entrambe e le cartelle pubbliche sono costituiti in Exchange Online o locale. In alcuni casi gli utenti in linea potrebbe essere necessario per accedere alle cartelle pubbliche nell'ambiente locale di Exchange Server 2013. Analogamente, gli utenti di Exchange 2013 potrebbe essere necessario accedere alle cartelle pubbliche in Office 365 o Exchange Online.

In questo articolo viene descritto come abilitare gli utenti nell'ambiente locale di Exchange 2013 per accedere alle cartelle pubbliche di Exchange Online/Office 365. Per consentire agli utenti di Exchange Online/Office 365 accedere alle cartelle pubbliche di Exchange 2013 locale, vedere [Configurare le cartelle pubbliche di Exchange 2013 per una distribuzione ibrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).


> [!NOTE]
> Se si dispone di cartelle pubbliche di Exchange 2010 o Exchange 2007, vedere <A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Configurare cartelle pubbliche locali legacy per una distribuzione ibrida</A>.



## Che cosa è necessario sapere prima di iniziare

1.  Per queste istruzioni si presume che sia stata utilizzata la procedura guidata di configurazione ibrida per configurare e sincronizzare gli ambienti locale e Exchange Online e che i record DNS utilizzati per il servizio di individuazione automatica della maggior parte degli utenti faccia riferimento a un endpoint locale. Per ulteriori informazioni, vedere [Procedura guidata di configurazione ibrida](https://technet.microsoft.com/it-it/library/hh529921\(v=exchg.150\)).

2.  Queste istruzioni si presuppone che Outlook via Internet è attivato e funzionalità nei server di Exchange locale. Per informazioni su come abilitare Outlook via Internet, vedere [Outlook via Internet](outlook-anywhere-exchange-2013-help.md).

3.  Implementazione della coesistenza della cartella pubblica per una distribuzione ibrida di Exchange con Office 365, potrebbe essere necessario per risolvere i conflitti durante la procedura di importazione. Conflitti possono verificarsi a causa di indirizzo di posta elettronica non instradabili assegnato a cartelle pubbliche abilitate, in conflitto con altri utenti e gruppi in Office 365 e gli altri attributi di posta elettronica.

4.  Per accedere alle cartelle pubbliche in più strutture locali, è necessario aggiornare i relativi client Outlook con l'aggiornamento pubblico di Outlook di novembre 2012 o successivo.
    
    1.  Per scaricare novembre 2012 aggiornamento di Outlook per Outlook 2010, vedere [aggiornamenti per Microsoft Outlook 2010 (KB2687623) a 32-Bit Edition](https://www.microsoft.com/en-us/download/details.aspx?id=35702).
    
    2.  Scaricare novembre 2012 aggiornamento di Outlook per Outlook 2007, vedere [aggiornamento per Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/en-us/download/details.aspx?id=35718).

5.  Outlook 2011 per Mac e Outlook per Mac per Office 365 non sono supportati per cartelle pubbliche cross-premise. Per accedere alle cartelle pubbliche con Outlook 2011 per Mac o Outlook per Mac per Office 365, il percorso delle cartelle deve corrispondere a quello degli utenti. Inoltre, gli utenti le cui cassette postali sono in Exchange Online non saranno in grado di accedere alle cartelle pubbliche locali tramite Outlook Web App.
    

    > [!NOTE]
    > 2016 di Outlook per Mac è supportato per le cartelle pubbliche tra locali. Se i client nell'organizzazione utilizzano 2016 Outlook per Mac, assicurarsi di che aver installato l'aggiornamento di aprile 2016. In caso contrario, gli utenti non potranno accedere alle cartelle pubbliche in una coesistenza o di una topologia ibrida. Per ulteriori informazioni, vedere <A href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Accesso alle cartelle pubbliche con Outlook 2016 per Mac</A>.



## Passaggio 1: Download degli script

1.  Scaricare i file seguenti [dall'Abilitati alla posta elettronica le cartelle pubbliche - sincronizzazione della directory da EXO allo script % su beni](https://go.microsoft.com/fwlink/p/?linkid=797795).
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  Salvare i file nel computer locale da cui si eseguirà PowerShell. Ad esempio, C:\\PFScripts.

## Passaggio 2: Configurare la sincronizzazione delle directory

Esecuzione di script `Sync-MailPublicFoldersCloudToOnprem.ps1` verranno sincronizzate le cartelle pubbliche abilitate alla posta tra Exchange Online e l'ambiente locale di Exchange 2013. Autorizzazioni speciali assegnate alle cartelle pubbliche abilitate alla posta saranno necessario ricreare nel cloud dopo cross-premise autorizzazioni non sono supportate negli scenari di distribuzione ibrida. Per ulteriori informazioni, vedere [Exchange hybrid deployment documentation](https://technet.microsoft.com/it-it/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).


> [!NOTE]
> Verranno visualizzata sincronizzate le cartelle pubbliche abilitate alla posta ai fini del flusso di posta oggetti contatto di posta elettronica e non sarà visualizzato nell'interfaccia di amministrazione di Exchange. Vedere il comando Get-MailPublicFolder. Per ricreare le autorizzazioni SendAs nel cloud, utilizzare il comando Add-RecipientPermission.



1.  Nel server Exchange 2013, eseguire il comando seguente per sincronizzare abilitati alla posta elettronica delle cartelle pubbliche da Exchange Online/Office 365 ad Active Directory locale in locale.
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    Dove `Credential` è il nome utente di Office 365 e la password.


> [!NOTE]
> È consigliabile eseguire questo script ogni giorno per sincronizzare le cartelle pubbliche abilitate alla posta.



## Passaggio 3: Configurare gli utenti locali per accedere a cartelle pubbliche di Exchange Online

Il passaggio finale di questa procedura consiste nel configurare l'organizzazione locale di Exchange 2013 per consentire l'accesso alle cartelle pubbliche di Exchange Online.

Esecuzione di script `Import-PublicFolderMailboxes.ps1` verrà importare gli oggetti cassetta postale di cartelle pubbliche dal cloud come utenti abilitati alla posta elettronica per l'ambiente locale. Lo script configura anche gli oggetti importati come cassette postali delle cartelle pubbliche remote.

1.  Nel server Exchange 2013, eseguire il comando seguente per importare gli oggetti cassetta postale di cartelle pubbliche dal cloud in Active Directory locale.
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    Dove `Credential` è il nome utente di Office 365 e la password.
    

    > [!NOTE]
    > È consigliabile eseguire questo script ogni giorno per importare gli oggetti cassetta postale di cartelle pubbliche in quanto ogni volta che le cassette postali di cartelle pubbliche raggiungono le capacità di soglia, vengono divise automaticamente in più cassette postali di nuove. Di conseguenza, si desidera sempre assicurarsi di che aver importato le cassette postali delle cartelle pubbliche più recenti dal cloud.



2.  Abilitare l'organizzazione di Exchange 2013 locale accedere a cartelle pubbliche di Exchange Online.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote


> [!NOTE]
> È necessario attendere fino a quando non ha completato la sincronizzazione di ActiveDirectory per visualizzare le modifiche. Questo processo può richiedere fino a 3 ore. Se non si desidera attendere la sincronizzazione ricorrente che si verificano ogni tre ore, è possibile forzare la sincronizzazione delle directory in qualsiasi momento. Per informazioni dettagliate sulla procedura per forzare la sincronizzazione delle directory, vedere <A href="http://technet.microsoft.com/en-us/library/jj151771.aspx">forzare la sincronizzazione delle directory</A>.



## Come verificare se l'operazione ha avuto esito positivo

1.  Accedere a Outlook per un utente in Exchange Online ed effettuare i seguenti test sulle cartelle pubbliche:
    
      - Visualizzare la gerarchia.
    
      - Controllare le autorizzazioni.
    
      - Creare ed eliminare cartelle pubbliche.
    
      - Pubblicare il contenuto ed eliminare il contenuto da una cartella pubblica.

