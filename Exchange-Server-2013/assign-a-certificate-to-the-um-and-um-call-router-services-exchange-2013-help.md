---
title: 'Assegna certificato mess. unif./routing chiamate: Exchange 2013 Help'
TOCTitle: Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54652877
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-29_

È possibile utilizzare EAC o Shell per assegnare un certificato autofirmato, un certificato di infrastruttura a chiave pubblica (PKI) interna oppure un certificato commerciale di terze parti per servizi specifici di Exchange. Quando si utilizza il cmdlet **New-ExchangeCertificate** per assegnare il certificato ai servizi di Exchange con il parametro *Services*, viene richiesto all'utente di assegnare il certificato ai servizi di Exchange. Se si utilizza EAC per creare un certificato, la procedura guidata Nuovo certificato di Exchange non richiederà all'utente di assegnare il certificato ai servizi di Exchange. È necessario modificare le proprietà del certificato e assegnare il certificato selezionando i servizi a cui si desidera assegnarlo.

Servizi diversi hanno requisiti dei certificati differenti. Ad esempio, alcuni servizi potrebbero richiedere solo un nome server nella casella **Nome soggetto** o **Nome alternativo soggetto** di un certificato e altri servizi potrebbero richiedere un nome di dominio completo. Assicurarsi che il nome del certificato supporti gli utilizzi richiesti dai servizi per i quali viene abilitato.


> [!WARNING]
> I certificati autofirmati non possono essere utilizzati durante l'integrazione della messaggistica unificata con Microsoft Lync Server.



Per informazioni sulle altre attività di gestione relative alla gestione dei certificati per Messaggistica unificata, vedere [Distribuzione di certificati per le procedure di messaggistica unificata](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione certificati" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) e "Servizio di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md). Accedere al sistema utilizzando un account appartenente al gruppo di amministratori locale del computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Assegnazione di un certificato ai servizi di Messaggistica unificata e di routing delle chiamate di messaggistica unificata tramite EAC

1.  In EAC, accedere a **Server** \> **Certificati**.

2.  Nella visualizzazione elenco, selezionare il certificato a cui si desidera assegnare i servizi di Messaggistica unificata e di routing delle chiamate di messaggistica unificata, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina *\<Nome del certificato\>*, selezionare **Servizi**, quindi **Messaggistica unificata** e **Routing delle chiamate di messaggistica unificata**.

4.  Fare clic su **Salva**.

## Assegnazione di un certificato ai servizi di Messaggistica unificata e di routing delle chiamate di messaggistica unificata tramite Shell

Nell'esempio riportato viene assegnato un certificato ai servizi di Messaggistica unificata e di routing delle chiamate di messaggistica unificata.
```powershell
    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'
```
