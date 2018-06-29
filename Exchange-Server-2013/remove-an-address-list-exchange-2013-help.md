---
title: 'Rimuovere un elenco di indirizzi: Exchange 2013 Help'
TOCTitle: Rimuovere un elenco di indirizzi
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 50480363
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un elenco di indirizzi

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-14_

In questo argomento è spiegato come rimuovere un elenco indirizzi. Non è possibile rimuovere l'elenco indirizzi globale predefinito.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Non è possibile rimuovere un elenco di indirizzi principale in cui sono contenuti elenchi di indirizzi secondario. Tuttavia, è possibile rimuovere sia gli elenchi di indirizzi principali che secondari premendo CTRL e selezionando gli elenchi di indirizzi principali e secondari. Se si tenta di rimuovere un elenco di indirizzi principale senza rimuovere gli elenchi di indirizzi secondari, verrà visualizzato un messaggio di errore.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la rimozione di un elenco indirizzi

1.  Accedere a **Organizzazione** \> **Elenchi di indirizzi**.

2.  In questo elenco, selezionare l'elenco indirizzi che si desidera rimuovere, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Nell'avviso, fare clic su **Sì** per rimuovere l'elenco indirizzi.

## Rimozione di un elenco di indirizzi tramite Shell

In questo esempio viene rimosso l'elenco di indirizzi Sales Department che non contiene elenchi secondari.

    Remove-AddressList -Identity "Sales Department"

Digitare **S** per confermare la rimozione dell'elenco di indirizzi, quindi premere INVIO.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-AddressList](https://technet.microsoft.com/it-it/library/bb124342\(v=exchg.150\)).

## Rimozione di un elenco di indirizzi contenente elenchi secondari tramite Shell

In questo esempio viene rimosso l'elenco indirizzi Departments e tutti i suoi sottoelenchi.

    Remove-AddressList -Identity Departments -Recursive

Digitare **S** per confermare la rimozione dell'elenco di indirizzi principale e dei relativi elenchi di indirizzi secondari, quindi premere INVIO.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-AddressList](https://technet.microsoft.com/it-it/library/bb124342\(v=exchg.150\)).

