---
title: "Configurare un dominio accettato nell'organizzazione di Exchange come autorevole: Exchange 2013 Help"
TOCTitle: Configurare un dominio accettato nell'organizzazione di Exchange come autorevole
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 50481880
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un dominio accettato nell'organizzazione di Exchange come autorevole

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-17_

Viene considerato autorevole il dominio appartenente all'organizzazione che ospita le cassette postali di tutti i destinatari nell'ambito dello spazio dei nomi SMTP. Per impostazione predefinita, viene configurato come autorevole un dominio accettato per l'organizzazione Exchange. Se l'organizzazione dispone di più spazi dei nomi SMTP, è possibile configurare più domini accettati come autorevoli.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere La voce "Domini accettati" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Se si dispone di un server Trasporto Edge nella propria rete perimetrale, è necessario configurare i domini accettati su un server di cassette postali dell'organizzazione di Exchange. La configurazione dei domini accettati viene replicata nel server Trasporto Edge durante la sincronizzazione EdgeSync. Per ulteriori informazioni, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

  - Non è possibile creare un dominio accettato con lo stesso nome di un dominio remoto già configurato. Ad esempio, se fabrikam.com è configurato come dominio remoto, non è possibile creare un dominio accettato per fabrikam.com.

  - Prima di configurare il dominio accettato, è necessario verificare l'esistenza di un record delle risorse DNS MX pubblico per lo spazio dei nomi SMTP e che il record delle risorse MX faccia riferimento a un nome di server e a un indirizzo IP associati all'organizzazione di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione di un dominio accettato come autorevole tramite l'interfaccia di amministrazione di Exchange

Se un dominio accettato per l'organizazione Exchange ospita tutte le cassette postali nell'ambito dello spazio dei nomi SMTP del dominio, potrebbe essere opportuno configurarlo come dominio autorevole.

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Domini accettati**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nel campo **Nome** immettere il nome visualizzato per il dominio accettato. Ogni dominio accettato per l'organizzazione deve disporre di un nome visualizzato univoco. Quest'ultimo può essere diverso da quello del dominio accettato. Ad esempio, il nome visualizzato del dominio Contoso.com potrebbe essere Dominio accettato locale Contoso.

3.  Nel campo **Dominio accettato** immettere il dominio accettato. Specifica uno spazio dei nomi SMTP per il quale l'organizzazione accetta i messaggi di posta elettronica. Ad esempio, Contoso.com.

4.  Selezionare **Dominio autorevole**. Questa opzione è riservata alla posta elettronica inoltrata ai server all'interno dell'organizzazione Exchange per un dominio accettato che ospita le cassette postali di tutti i destinatari nell'ambito di uno spazio dei nomi SMTP.

5.  Fare clic su **Salva**.


> [!TIP]
> Per configurare un dominio accettato che è già stato creato, selezionare il dominio dall'elenco dei domini accettati e fare clic su <STRONG>Modifica</STRONG><IMG title="Icona Modifica" alt="Icona Modifica" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">. È possibile configurare più domini come autorevoli.



## Come verificare se l'operazione ha avuto esito positivo

Il nuovo dominio accettato sarà visualizzato nell'elenco dei domini accettati nell'interfaccia di amministrazione di Exchange. Per verificare che il dominio accettato come autorevole sia stato configurato correttamente, inviare un messaggio di posta elettronica al dominio e verificarne la ricezione.

