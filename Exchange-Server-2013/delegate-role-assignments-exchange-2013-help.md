---
title: 'Delegare le assegnazioni di ruolo: Exchange 2013 Help'
TOCTitle: Delegare le assegnazioni di ruolo
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 50481989
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Delegare le assegnazioni di ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-02_

La delega del ruolo di gestione consente agli utenti di assegnare un ruolo di gestione specifico ad altri gruppi del ruolo di gestione, a criteri di assegnazione del ruolo di gestione, a utenti o a gruppi di protezione universali (USG). Per impostazione predefinita, solo i membri del gruppo del ruolo di gestione Gestione organizzazione possono delegare le assegnazioni di ruolo. Quando viene distribuita una nuova installazione di Microsoft Exchange Server 2013, solo l'account utente che ha installato Exchange 2013 è membro del gruppo di ruolo Gestione organizzazione.

Se si assegna un ruolo di delega a un gruppo di ruolo, tutti i membri del gruppo possono delegare il ruolo di gestione associato ad altri assegnatari.


> [!IMPORTANT]
> La delega delle assegnazioni di ruolo non concede ai destinatari le autorizzazioni definite dal ruolo, ma solo la capacità di assegnare il ruolo ad altri. Se si desidera concedere anche le autorizzazioni definite dal ruolo all'assegnatario, è necessario creare anche un'assegnazione di ruolo normale. Per creare un'assegnazione di ruolo normale, vedere i seguenti argomenti:<BR><A href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</A><BR><A href="manage-role-assignment-policies-exchange-2013-help.md">Gestire i criteri di assegnazione dei ruoli</A><BR><A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Aggiungere un ruolo di un utente o gruppo di protezione universale</A>




> [!NOTE]
> In questo argomento viene presentata la delega dell'assegnazione del ruolo di gestione. Per delegare la possibilità di aggiungere o rimuovere membri dai gruppi di ruolo (è questo il metodo di delega consigliato), vedere <A href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</A>.



Per ulteriori informazioni sulle assegnazioni del ruolo normali e la delega delle assegnazioni del ruolo di gestione, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alla gestione delle autorizzazioni, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Assegnazioni ruolo" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Delega di un ruolo di gestione tramite Shell

È possibile creare assegnazioni di ruolo di delega utilizzando gli stessi ambiti predefiniti, basati su filtri destinatari o server, basati su elenchi di server o di tipo unità organizzativa che possono essere utilizzati per creare ambiti normali o esclusivi. L'unica differenza tra la creazione di un'assegnazione di ruolo normale e l'assegnazione di un ruolo di delega è l'aggiunta dell'opzione *Delegating* al comando. Per ulteriori informazioni sulla creazione di assegnazioni di ruolo, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)


> [!NOTE]
> Non è possibile creare un'assegnazione di ruolo di delega a un criterio di assegnazione del ruolo di gestione.



Con questo esempio viene creata un'assegnazione di ruolo di delega per consentire ai membri del gruppo di ruolo Senior Admins di assegnare il ruolo Destinatari posta a qualsiasi utente nell'organizzazione di Exchange.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

Con questo esempio viene creata un'assegnazione di ruolo di delega per consentire ai membri del gruppo di ruolo Senior Admins di assegnare il ruolo Destinatari posta solo agli utenti nell'unità organizzativa Sales/Users OU del dominio contoso.com.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

