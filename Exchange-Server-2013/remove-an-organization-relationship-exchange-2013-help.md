---
title: "Rimuovere una relazione dell'organizzazione: Exchange 2013 Help"
TOCTitle: Rimuovere una relazione dell'organizzazione
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 50482103
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una relazione dell'organizzazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-04_

Una relazione dell'organizzazione consente agli utenti dell'organizzazione di Exchange di condividere informazioni sulla disponibilità del calendario con una organizzazione di Office 365 o con un'altra organizzazione locale di Exchange. È possibile rimuovere una regolazione dell'organizzazione per disattivare la condivisione del calendario con l'altra organizzazione.

Per poter condividere i calendari con un'altra organizzazione, è necessario impostare una relazione di autenticazione con il sistema di autenticazione Azure Active Directory (noto anche come "federazione") e deve soddisfare i requisiti software minimi. Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Rimozione di una relazione organizzativa tramite l'interfaccia di amministrazione di Exchange

1.  Su un server Exchange 2013 della propria organizzazione locale, andare a **organizzazione** \> **condivisione**.

2.  In **Condivisione organizzativa** selezionare una relazione organizzativa, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina") per rimuoverla.

3.  Nell'avviso che viene visualizzato, fare clic su **sì**.

## Rimozione di una relazione dell'organizzazione tramite Shell

In questo esempio viene rimossa la relazione organizzativa Contoso dall'organizzazione Exchange

```powershell
Remove-OrganizationRelationship -Identity "Contoso"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-OrganizationRelationship](https://technet.microsoft.com/it-it/library/ee332362\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la relazione organizzativa sia stata rimossa correttamente, effettuare una delle seguenti operazioni:

  - In EAC, accedere a **Organizzazione** \> **Condivisione** e verificare che la relazione organizzativa non sia presente nella visualizzazione elenco in **Condivisione organizzativa**.

  - Eseguire il comando di Shell riportato di seguito per verificare che le informazioni sulla relazione organizzativa siano state rimosse.
    
    ```powershell
Get-OrganizationRelationship | Format-List
```


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


