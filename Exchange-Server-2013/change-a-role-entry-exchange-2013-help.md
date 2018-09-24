---
title: 'Modificare una voce di ruolo: Exchange 2013 Help'
TOCTitle: Modificare una voce di ruolo
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 50480673
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare una voce di ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Ogni voce di ruolo di gestione contenuta in un ruolo di gestione rappresenta un cmdlet. Aggiungendo o rimuovendo determinati parametri da una voce di ruolo, che poi verrà aggiunta a un ruolo di gestione, si può stabilire se tali parametri debbano essere disponibili in quel dato cmdlet. Per ulteriori informazioni sulle voci del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Non è possibile modificare le voci di ruolo contenute nei ruoli di gestione incorporati.


> [!NOTE]
> In questo argomento non si descrive come modificare le voci di ruolo di gestione senza ambito contenute in un ruolo di gestione senza ambito. Per ulteriori informazioni su come modificare le voci di ruolo senza ambito, vedere <A href="create-a-role-exchange-2013-help.md">Creare un ruolo</A>.




> [!WARNING]
> Per aggiungere o rimuovere parametri da una voce di ruolo, utilizzare il parametro <EM>AddParameter</EM> o <EM>RemoveParameter</EM>. Se si omette il parametro <EM>AddParameter</EM> o <EM>RemoveParameter</EM> durante l'esecuzione del cmdlet <STRONG>Set-ManagementRoleEntry</STRONG>, nella voce di ruolo verranno inclusi i soli parametri specificati tramite il parametro <EM>Parameters</EM>. Tutti gli altri parametri presenti nella voce di ruolo verranno rimossi.



Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Se si desidera aggiungere parametri a una voce di ruolo, questi devono necessariamente essere presenti nella voce di ruolo contenuta nel ruolo padre. I parametri devono essere presenti anche nel cmdlet che si specifica.

  - Se si desidera rimuovere dei parametri da una voce di ruolo, questi non potranno essere presenti anche nelle voci dei ruoli figlio. Pertanto, occorrerà rimuovere i parametri dalle voci dei ruoli figlio. Seguire la procedura "Utilizzo di Shell per rimuovere uno o più parametri da una voce di ruolo", esposta più avanti in questo argomento, per rimuovere i parametri dalle voci di tutti i ruoli figlio.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per aggiungere uno o più parametri a una voce di ruolo

Per aggiungere parametri a una voce di ruolo, è necessario specificare quelli che si desidera aggiungere tramite il parametro *Parameters*. Quindi, occorre impostare il parametro *AddParameter* per specificare che si desidera eseguire un'operazione di aggiunta.

Per aggiungere parametri a una voce di ruolo, utilizzare la seguente sintassi.

```powershell
    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter
```

In questo esempio viene mostrato come aggiungere i parametri *EmailAddresses* e *Type* al cmdlet **Set-Mailbox** nel ruolo Recipient Administrators.

```powershell
    Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Utilizzo di Shell per rimuovere uno o più parametri da una voce di ruolo

Per rimuovere parametri da una voce di ruolo, è necessario specificarli tramite il parametro *Parameters*. Quindi, occorre impostare il parametro *RemoveParameter* per specificare che si desidera eseguire un'operazione di rimozione.

Per rimuovere parametri da una voce di ruolo, utilizzare la seguente sintassi.

```powershell
    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter
```
In questo esempio viene mostrato come rimuovere i parametri *Port*, *ProtocolLoggingLevel* e *SmartHostAuthMechanism* dal cmdlet **Set-SendConnector** nel ruolo Tier 1 Server Administrators.

```powershell
    Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Utilizzo di Shell per rimuovere tutti i parametri da una voce di ruolo

Per rimuovere tutti i parametri da una voce di ruolo, è necessario specificare il valore `$Null` nel parametro *Parameters*. Non è necessario includere il parametro *RemoveParameters*.

La rimozione di tutti i parametri da una voce di ruolo è particolarmente utile quando in un cmdlet si desidera rendere disponibili solo alcuni parametri, escludendo tutti gli altri. Se non si desidera che un ruolo abbia accesso a un cmdlet, anziché rimuovere i parametri, eliminare completamente dal ruolo la voce di ruolo associata. Per ulteriori informazioni sulla rimozione di una voce da un ruolo, vedere [Rimuovere una voce di ruolo da un ruolo](remove-a-role-entry-from-a-role-exchange-2013-help.md).


> [!WARNING]
> Non è possibile annullare le operazioni di rimozione. Se si rimuovono erroneamente tutti i parametri da una voce di ruolo, è necessario aggiungerli di nuovo manualmente.



Per rimuovere tutti i parametri da una voce di ruolo, utilizzare la seguente sintassi.

```powershell
    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 
```

In questo esempio, vengono rimossi tutti i parametri dal cmdlet **Set-CASMailbox** nel ruolo Recipient Administrators.

```powershell
    Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Utilizzo di Shell per applicare un determinato insieme di parametri

Se si desidera che in una voce di ruolo sia incluso solo un gruppo specifico di parametri, impostare solo il parametro *Parameters*. Non includere i parametri *AddParameter* o *RemoveParameter*. Quando si specifica solo il parametro *Parameters*, vengono inclusi nella voce di ruolo solo i parametri specificati nel comando. Tutti gli altri parametri vengono rimossi.

Per specificare un determinato insieme di parametri, utilizzare la seguente sintassi.

```powershell
    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>
```

In questo esempio viene mostrato come includere soltanto i parametri *Identity*, *DisplayName*, *MissedCallNotificationEnabled* e *PersonalAuthAttendantEnabled* nel cmdlet **Set-UMMailbox** del ruolo Seattle Mail Recipients.

```powershell
    Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

