---
title: 'Creazione di una Rubrica fuori rete: Exchange 2013 Help'
TOCTitle: Creazione di una Rubrica fuori rete
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 50481470
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: MT
---

# Creazione di una Rubrica fuori rete

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-24_

Una rubrica offline in Exchange Server 2013 è una copia scaricata di una rubrica che consente agli utenti di Outlook di accedere alle informazioni quando sono scollegati dal server. Gli amministratori di Exchange possono scegliere le rubriche da rendere disponibili agli utenti che lavorano in modalità non linea, oltre a poter configurare il metodo di distribuzione delle rubriche (distribuzione basata sul Web o delle cartelle pubbliche).

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare la shell per creare una Rubrica offline con la distribuzione basata sul Web

In questo esempio viene creata la rubrica offline OAB\_Contoso che utilizza la distribuzione basata sul Web per i client Outlook 2007 o versioni successive utilizzando la directory virtuale predefinita.

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-OfflineAddressBook](https://technet.microsoft.com/it-it/library/bb123692\(v=exchg.150\)).

