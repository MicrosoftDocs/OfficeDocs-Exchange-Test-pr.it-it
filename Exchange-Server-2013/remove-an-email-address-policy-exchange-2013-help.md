---
title: 'Rimuovere un criterio indirizzo di posta elettronica: Exchange 2013 Help'
TOCTitle: Rimuovere un criterio indirizzo di posta elettronica
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 50482002
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un criterio indirizzo di posta elettronica

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-13_

Per impostazione predefinita, Exchange contiene un criterio degli indirizzi di posta elettronica in cui l'alias del destinatario viene identificato come parte locale dell'indirizzo di posta elettronica e viene utilizzato il dominio accettato predefinito. La parte locale di un indirizzo di posta elettronica è il nome visualizzato prima della chiocciola (@). Questo criterio dell'indirizzo di posta elettronica si applica a tutti gli utenti dell'organizzazione. Non è possibile rimuovere il criterio dell'indirizzo di posta elettronica.

Per le attività di gestione aggiuntive correlate ai criteri degli indirizzi di posta elettronica, vedere [Procedure relative al criterio indirizzo posta elettronica](email-address-policy-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Se si rimuove un criterio dell'indirizzo di posta elettronica utilizzato dai destinatari come criterio principale e non sono stati configuati altri criteri per i destinatari, verrà utilizzato il criterio predefinito.

  - Non è possibile eliminare il criterio predefinito. Per eliminare il criterio predefinito, è necessario in primo luogo designare un criterio diverso come predefinito.

  - Se il criterio dell'indirizzo di posta elettronica da eliminare contiene più di 3000 destinatari, utilizzare la shell per eseguire la procedura.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri degli indirizzi di posta elettronica" nell'argomento [Indirizzi di posta elettronica e rubriche](email-addresses-and-address-books-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Rimozione di un criterio dell'indirizzo di posta elettronica tramite l'interfaccia di amministrazione di Exchange

1.  Passare a **Flusso di posta** \> **Criteri degli indirizzi di posta elettronica**.

2.  Nella visualizzazione elenco, selezionare il criterio dell'indirizzo di posta elettronica che si intende eliminare e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Nel messaggio di avviso, fare clic su **Sì** per rimuovere il criterio.

## Rimozione di un criterio dell'indirizzo di posta elettronica tramite Shell

Con questo esempio viene rimosso il criterio dell'indirizzo di posta elettronica South East Offices.

    Remove-EmailAddressPolicy -Identity "South East Offices"

Digitare **S** per confermare l'eliminazione del criterio, quindi premere INVIO.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Remove-EmailAddressPolicy](https://technet.microsoft.com/it-it/library/bb124504\(v=exchg.150\)).

