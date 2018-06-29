---
title: 'Rimuovere un criterio della Rubrica: Exchange 2013 Help'
TOCTitle: Rimuovere un criterio della Rubrica
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 50481617
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un criterio della Rubrica

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-03-25_

Utilizzare questa procedura per rimuovere un criterio della rubrica.

Per ulteriori attività di gestione relative ai criteri della rubrica, consultare [Procedure relative al criterio della Rubrica indirizzi](address-book-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri delle rubriche" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Non è possibile rimuovere un criterio della rubrica se è assegnato alla cassetta postale di un utente o a una cassetta postale eliminata in modo reversibile. Per determinare se un criterio della rubrica è assegnato a un utente, eseguire il comando seguente da Shell:
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    Per determinare se un criterio della rubrica è assegnato a una cassetta postale eliminata in modo reversibile, utilizzare il comando seguente:
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - Per rimuovere un criterio della rubrica dalla cassetta postale di un utente, è possibile utilizzare la pagina **Funzionalità delle cassette postali** delle proprietà della cassetta postale oppure il cmdlet **Set-Mailbox**.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per rimuovere il criterio della rubrica. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo della Shell per rimuovere un criterio della rubrica

In questo esempio viene rimosso il criterio della rubrica ABP\_TailspinToys.

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-AddressBookPolicy](https://technet.microsoft.com/it-it/library/hh529929\(v=exchg.150\)).

