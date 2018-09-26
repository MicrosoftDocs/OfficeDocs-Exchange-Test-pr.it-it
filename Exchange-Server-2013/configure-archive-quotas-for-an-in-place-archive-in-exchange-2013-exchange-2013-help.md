---
title: 'Config. quote archiviazione sul posto di Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurare quote di archiviazione per un archivio sul posto di Exchange 2013
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50555708
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare quote di archiviazione per un archivio sul posto di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-12-04_

Nelle distribuzioni on-premises vengono creati, per impostazione predefinita, archivi locali con quote di archiviazione illimitate. Di conseguenza sarà necessario modificare le proprietà della cassetta postale per impostare le quote di archiviazione. È possibile impostare le quote seguenti per un archivio:

  - **Quota avviso archiviazione**   Se un archivio locale supera la quota di avviso specificata, viene registrato un evento per l'amministratore di Exchange e all'utente della cassetta postale viene inviato un messaggio di avviso.

  - **Quota archiviazione**   Se un archivio locale supera la quota di archiviazione specificata, i messaggi non vengono più spostati nell'archivio e all'utente della cassetta postale viene inviato un messaggio di avviso.

Per ulteriori informazioni sugli archivi locali, vedere [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - In Interfaccia di amministrazione di Exchange è possibile utilizzare un elenco a discesa con valori fissi per configurare la quota di archiviazione e la quota di avviso per l'archiviazione. Se si desidera impostare la quota su un valore non elencato in EAC, utilizzare Shell.

  - Configurare la quota di avviso per l'archiviazione su un valore inferiore rispetto alla quota di archiviazione. In base alla velocità di crescita dell'archivio dell'utente, la differenza tra la quota di avviso per l'archiviazione e la quota di archiviazione deve consentire una quantità di tempo sufficiente all'utente per eseguire le azioni opportune, quali l'eliminazione degli elementi dall'archivio oppure richiedere all'amministratore o al supporto tecnico IT di aumentare la quota di archiviazione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Configurazione della quota di archiviazione e della quota di avviso per l'archiviazione di una cassetta postale tramite EAC

1.  Accedere a **Destinatari** \> **Cassette postale**

2.  Nella visualizzazione elenco, selezionare una cassetta postale,

3.  Nel riquadro dei dettagli, sotto **Archivio locale**, fare clic **Visualizza dettagli**.

4.  In **Cassetta postale di archiviazione** utilizzare gli elenchi **Valore quota (GB)** e **Invia avviso a (GB)** per selezionare i valori desiderati.

5.  Fare clic su **OK**.

## Configurazione della quota di archiviazione e della quota di avviso per l'archiviazione di una cassetta postale tramite Shell

Con questo esempio la quota di archiviazione della cassetta postale di Chris Ashton viene impostata sul valore di 10 GB, raggiunto il quale l'utente riceverà un messaggio di avviso che indica che l'archivio locale è pieno e che non sarà più possibile trasferire messaggi nell'archivio. Con questo esempio, inoltre, la quota di avviso di archiviazione viene impostata sul valore di 9,5 GB, raggiunto il quale l'utente riceverà un messaggio di avviso che indica che l'archivio locale è quasi pieno.

```powershell
Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare l'avvenuta abilitazione di un archivio locale per una cassetta postale esistente, effettuare una delle seguenti operazioni:

  - In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali** e selezionare la cassetta postale desiderata. Nel riquadro dei dettagli, sotto **Archivio locale**, fare clic **Visualizza dettagli** e verificare le impostazioni della quota di archiviazione.

  - In Shell, eseguire il comando riportato di seguito per visualizzare le informazioni sulla quota di archiviazione.
    ```powershell
        Get-Mailbox <Name> | FL Name,Archive*Quota
    ```
