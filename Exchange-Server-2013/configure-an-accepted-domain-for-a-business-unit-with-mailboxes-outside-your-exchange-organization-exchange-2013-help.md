---
title: "Configurare un dominio accettato per una business unit con cassette postali all'esterno dell'organizzazione di Exchange: Exchange 2013 Help"
TOCTitle: Configurare un dominio accettato per una business unit con cassette postali all'esterno dell'organizzazione di Exchange
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 50482137
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un dominio accettato per una business unit con cassette postali all'esterno dell'organizzazione di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-08-06_

In alcuni casi, potrebbe essere opportuno configurare un dominio accettato per una business unit in cui alcuni o tutti i destinatari nel dominio non dispongono di cassette postali nell'organizzazione Exchange. Ciò può verificarsi, ad esempio, quando un'organizzazione condivide lo stesso spazio degli indirizzi SMTP tra due o più sistemi di posta elettronica diversi. In tali scenari, è possibile configurare un dominio accettato come dominio di inoltro interno.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere La voce "Domini accettati" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Se si dispone di un server Trasporto Edge nella propria rete perimetrale, è necessario configurare i domini accettati su un server di cassette postali dell'organizzazione di Exchange. La configurazione dei domini accettati viene replicata nel server Trasporto Edge durante la sincronizzazione EdgeSync. Per ulteriori informazioni, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

  - Prima di configurare un dominio accettato, è necessario verificare l'esistenza di un record delle risorse DNS MX pubblico per lo spazio dei nomi SMTP e che il record delle risorse MX faccia riferimento a un nome di server e a un indirizzo IP associati all'organizzazione di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione di un dominio accettato come dominio di inoltro interno tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Domini accettati**, selezionare il domio che si desidera configurare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nel campo **Nome** immettere il nome visualizzato per il dominio accettato. Ogni dominio accettato per l'organizzazione deve disporre di un nome visualizzato univoco. Quest'ultimo potrebbe non coincidere con il nome del dominio accettato. Ad esempio, il nome visualizzato del dominio Contoso.com potrebbe essere Dominio accettato locale Contoso.

3.  Selezionare **Dominio di inoltro interno**.

4.  Fare clic su **Salva**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il dominio accettato sia stato configurato correttamente come dominio di inoltro interno, inviare un messaggio dal dominio di inoltro interno alla cassetta postale nell'organizzaizone Exchange e verificarne la ricezione.

