---
title: 'Avviare o interrompere una ricerca eDiscovery In locale: Exchange 2013 Help'
TOCTitle: Avviare o interrompere una ricerca eDiscovery In locale
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 50479982
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Avviare o interrompere una ricerca eDiscovery In locale

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-07-14_

Consente di arrestare o riavviare una ricerca eDiscovery In locale in qualsiasi momento. Ad esempio, se si desidera modificare le proprietà di ricerca come cercare parole chiave o le cassette postali, è necessario arrestare una ricerca. È quindi possibile riavviare la ricerca dopo aver apportato le modifiche necessarie.


> [!WARNING]
> Se si riavvia una ricerca eDiscovery In locale, vengono rimossi i risultati della ricerca copiati nella cassetta postale di individuazione specificata nella ricerca.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "EDiscovery in locale" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EAC per avviare o interrompere una ricerca eDiscovery In locale

1.  Accedere a **Gestione conformità** \> **eDiscovery sul posto e conservazione**.

2.  Per interrompere una ricerca in corso, selezionare la ricerca e quindi fare clic su **Interrompi ricerca**.

3.  Per avviare una ricerca che è stata arrestata, selezionare la ricerca e quindi fare clic su **Riprendi Cerca**.

## Utilizzo della Shell per avviare o interrompere una ricerca eDiscovery In locale

Per un esempio di come avviare una ricerca eDiscovery In locale, vedere "esempio 1" in [Start-MailboxSearch](https://technet.microsoft.com/it-it/library/dd351245\(v=exchg.150\)).

Per un esempio di come interrompere una ricerca eDiscovery In locale, vedere "esempio 1" in [Stop-MailboxSearch](https://technet.microsoft.com/it-it/library/dd351075\(v=exchg.150\)).

