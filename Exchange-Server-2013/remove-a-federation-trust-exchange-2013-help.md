---
title: 'Rimuovere una relazione di trust federativa: Exchange 2013 Help'
TOCTitle: Rimuovere una relazione di trust federativa
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 50481848
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una relazione di trust federativa

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-01-04_

Una relazione di trust federativa stabilisce una relazione di trust tra un'organizzazione di Exchange 2013 Microsoft e il sistema di autenticazione Azure Active Directory e supporta la condivisione con altre organizzazioni Exchange federate. Rimozione di una relazione di trust federativa da locale organizzazione di Exchange disabiliterà condivisione federata con altre organizzazioni Exchange federate e con le organizzazioni di Office 365 connessione all'organizzazione come parte di una distribuzione ibrida. Necessario valutare attentamente l'impatto globale dell'organizzazione prima di rimuovere una relazione di trust federativa.

Per altre attività di gestione relative alle relazioni di trust federative, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Una volta rimossa la relazione di trusta federativa, è possibile rimuovere i record TXT dal server DNS pubblico per ogni dominio federato. Esaminare i requisiti per la rimozione di un record TXT con l'organizzazione che ospita i record DNS pubblici.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Rimozione di una relazione di trust federativa tramite l'interfaccia di amministrazione di Exchange

1.  Su un server Exchange 2013 della propria organizzazione locale, andare a **organizzazione** \> **condivisione**.

2.  Nella sezione **Trust federativo** fare clic su **Rimuovi**.

3.  Nel messaggio di avviso fare clic su **sì** per confermare la rimozione della relazione di trust federativa.

4.  Una volta rimossa la relazione di trust federativa, fare clic su **Chiudi**.

## Rimozione di una relazione di trust federativa tramite Shell

In questo esempio viene rimossa la relazione di trust federativa.

    Remove-FederationTrust

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-FederationTrust](https://technet.microsoft.com/it-it/library/dd351153\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la relazione di trust federativa sia stata rimossa correttamente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **organizzazione** \> **condivisione**. Se la relazione di trust federativa è stata rimossa correttamente, in **Trust federativo** sarà disponibilie solo il pulsante **Abilita**.

  - Nella shell, eseguire il comando riportato di seguito per verificare che non siano restituite le informazioni sulla relazione di trust federativa per l'organizzazione Exchange.
    
        Get-FederationTrust
    
    Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-FederationTrust](https://technet.microsoft.com/it-it/library/dd351262\(v=exchg.150\)).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

