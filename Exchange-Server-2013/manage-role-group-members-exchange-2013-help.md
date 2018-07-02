---
title: 'Gestire i membri del gruppo di ruolo: Exchange 2013 Help'
TOCTitle: Gestire i membri del gruppo di ruolo
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 50481571
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i membri del gruppo di ruolo

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-08_

In questo argomento viene descritta la modalità per aggiungere, rimuovere e visualizzare i membri di un gruppo di ruoli di gestione in Microsoft Exchange Server 2013. Per ulteriori informazioni sui gruppi di ruoli in Exchange 2013, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

Per le attività di gestione aggiuntive relative a gruppi di ruoli, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Aggiunta di membri a un gruppo di ruoli

Per assegnare a un utente le autorizzazioni concesse da un gruppo di ruoli, è necessario aggiungere l'utente, un gruppo di sicurezza universale o un altro gruppo di ruoli di cui faccia parte l'utente, come membro del gruppo di ruoli.

## Aggiunta dei membri a un gruppo di ruoli tramite EAC

1.  In Interfaccia di amministrazione di Exchange (EAC) accedere a **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli a cui si desidera aggiungere i membri e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella sezione **Membri**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Selezionare gli utenti, i gruppi di sicurezza utente o gli altri gruppi di ruoli che si desidera aggiungere al gruppo di ruoli, fare clic su **Aggiungi**, quindi su **OK**.

5.  Fare clic su **Salva** per salvare le modifiche al gruppo di ruoli.

## Aggiunta dei membri a un gruppo di ruoli tramite Shell

Per aggiungere un membro a un gruppo di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638207\(exchg.150\)#examples) in [Add-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638207\(v=exchg.150\)).

Per aggiungere più membri a un gruppo di ruoli o per sostituire tutta l'appartenenza del gruppo di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638116\(exchg.150\)#examples) in [Update-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638116\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver aggiunto correttamente uno o più membri a un gruppo di ruoli, effettuare le operazioni seguenti:

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli a cui sono stati aggiunti i membri.

3.  Nel riquadro dei dettagli del gruppo di ruoli verificare che i membri aggiunti siano presenti nell'elenco.

## Rimozione di membri da un gruppo di ruoli

Per rimuovere da un utente le autorizzazioni concesse da un gruppo di ruoli è necessario rimuovere l'utente, o il gruppo di sicurezza universale a cui appartiene, dall'appartenenza al gruppo di ruoli.

## Rimozione di membri da un gruppo di ruoli tramite EAC

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli da cui si desidera rimuovere i membri, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella sezione **Membri** selezionare i membri da rimuovere, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"), quindi su **Salva**.

## Rimozione di membri da un gruppo di ruoli tramite Shell

Per rimuovere un membro da un gruppo di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638208\(exchg.150\)#examples) in [Remove-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638208\(v=exchg.150\)).

Per rimuovere più membri a un gruppo di ruoli o per sostituire tutta l'appartenenza del gruppo di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638116\(exchg.150\)#examples) in [Update-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638116\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver rimosso correttamente uno o più membri da un gruppo di ruoli, effettuare le operazioni seguenti:

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli da cui sono stati rimossi i membri.

3.  Nel riquadro dei dettagli del gruppo di ruoli verificare che i membri rimossi non siano più presenti nell'elenco.

## Visualizzazione dei membri di un gruppo di ruoli

Ai membri di un gruppo di ruoli sono concesse le autorizzazioni fornite dai ruoli di gestione assegnati al gruppo di ruoli. È possibile visualizzare i membri di un gruppo di ruolo per individuare quali utenti, gruppi di protezione universali (USG, Universal Security Groups) o altri gruppi di ruolo ricevono le autorizzazioni dal gruppo di ruolo specificato.

## Visualizzazione dei membri di un gruppo di ruoli tramite EAC

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli di cui si desidera visualizzare i membri.

3.  Visualizzare i membri nel riquadro dei dettagli del gruppo di ruoli.

## Visualizzazione dei membri di un gruppo di ruolo tramite Shell

Per visualizzare i membri di un gruppo di ruoli, vedere la sezione "Esempi" in [Get-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638093\(v=exchg.150\)).

