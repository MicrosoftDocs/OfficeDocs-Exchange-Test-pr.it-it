---
title: 'Modificare un ambito di ruolo: Exchange 2013 Help'
TOCTitle: Modificare un ambito di ruolo
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 50481205
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare un ambito di ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Gli ambiti del ruolo di gestione consentono di determinare gli oggetti disponibili, in modo che l'utente possa modificarli utilizzando i cmdlet e i parametri relativi. Modificando un ambito, è possibile modificare gli oggetti disponibili per gli utenti da creare, modificare o rimuovere.

È possibile modificare un ambito di gestione personalizzato. È possibile modificare gli ambiti esclusivi o regolari. Se si modifica un ambito esclusivo, il nuovo ambito diventa immediatamente effettivo. Se si desidera modificare un'assegnazione del ruolo di gestione con un ambito di gestione predefinito o di unità organizzativa, vedere [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

Per ulteriori informazioni sugli ambiti e le assegnazioni del ruolo di gestione in Microsoft Exchange Server 2013, vedere i seguenti argomenti:

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

Per informazioni sulle altre attività di gestione relative agli ambiti di ruolo, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ambiti di gestione" nell'argomento[Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Modifica del nome di un ambito

Per modificare il nome di un ambito, utilizzare la seguente sintassi.

```powershell
Set-ManagementScope <current scope name> -Name <new scope name>
```

In questo esempio l'ambito Seattle Servers viene modificato in Seattle Exchange Servers.

```powershell
Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ManagementScope](https://technet.microsoft.com/it-it/library/dd297996\(v=exchg.150\)).

## Modifica di un filtro destinatario per un ambito

Per modificare il filtro destinatario su un ambito, utilizzare la sintassi seguente.

```powershell
Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }
```

In questo esempio viene modificato il filtro destinatario per far corrispondere tutti gli oggetti destinatario in cui la proprietà **Company** è impostata su Contoso.

```powershell
Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementScope](https://technet.microsoft.com/it-it/library/dd297996\(v=exchg.150\)).

Per ulteriori informazioni sui filtri destinatario e per visualizzare un elenco delle proprietà che è possibile filtrare, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

## Modifica della radice di unità organizzativa per un ambito

Per modificare la radice dell'unità organizzativa per un ambito, utilizzare la seguente sintassi.

```powershell
Set-ManagementScope <scope name> -RecipientRoot <OU>
```

In questo esempio, la radice dell'unità organizzativa Sales Users viene modificata in North America/Sales nel dominio contoso.com.

```powershell
Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementScope](https://technet.microsoft.com/it-it/library/dd297996\(v=exchg.150\)).

## Modifica di un filtro su server per un ambito

Per modificare il filtro server su un ambito, utilizzare la sintassi seguente.

```powershell
Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }
```

In questo esempio viene modificato il filtro del server per ottenere la corrispondenza con tutti gli oggetti server in cui la proprietà **ServerSite** è impostata su 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com'.
```powershell
    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementScope](https://technet.microsoft.com/it-it/library/dd297996\(v=exchg.150\)).

Per ulteriori informazioni sui filtri server e per visualizzare un elenco delle proprietà server che è possibile filtrare, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

## Modifica dell'elenco server per un ambito

Non è possibile modificare l'elenco dei server per un ambito. Se l'elenco dei server deve essere modificato, è necessario procedere come segue:

1.  Se necessario, recuperare l'elenco corrente dei server nell'ambito da sostituire utilizzando la procedura "Visualizzazione di uno specifico ambito" nell'argomento [Ruolo Visualizza ambiti](view-role-scopes-exchange-2013-help.md).

2.  Creare un ambito con il nuovo elenco di server utilizzando la procedura "Passo 1: Creare un ambito personalizzato" nell'argomento [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

3.  Modificare tutte le assegnazioni del ruolo di gestione che utilizzano l'ambito precedente per utilizzare il nuovo ambito tramite la procedura "Modifica del filtro server o dell'ambito basato su elenco per un'assegnazione di ruoli tramite Shell" nell'argomento [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

4.  Per rimuovere l'ambito precedente, utilizzare la procedura descritta nell'argomento [Rimuovere un ambito di ruolo](remove-a-role-scope-exchange-2013-help.md).

## Modifica di un filtro del database in un ambito

Per modificare il filtro del database in un ambito, utilizzare la sintassi seguente.

```powershell
Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }
```

In questo esempio viene modificato il filtro del database per far corrispondere tutti gli oggetti del database in cui la proprietà **Name** contiene la stringa "Executive".
```powershell
    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementScope](https://technet.microsoft.com/it-it/library/dd297996\(v=exchg.150\)).

Per ulteriori informazioni sui filtri del database e per visualizzare un elenco delle proprietà del database che è possibile filtrare, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

## Modifica dell'elenco di database in un ambito

Non è possibile modificare l'elenco di database in un ambito. Se è necessario modificare l'elenco dei database, fare quanto segue:

1.  Se necessario, recuperare l'elenco corrente dei database nell'ambito da sostituire utilizzando la procedura "Visualizzazione di un ambito specifico" nell'argomento [Ruolo Visualizza ambiti](view-role-scopes-exchange-2013-help.md).

2.  Creare un ambito con il nuovo elenco di database utilizzando la procedura "Passo 1: creare un ambito personalizzato" nell'argomento [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

3.  Modificare tutte le assegnazioni del ruolo di gestione che utilizzano l'ambito precedente per utilizzare il nuovo ambito tramite la procedura "Modifica del filtro del database o dell'ambito basato su elenco per un'assegnazione di ruoli tramite Shell" nell'argomento [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

4.  Per rimuovere l'ambito precedente, utilizzare la procedura descritta nell'argomento [Rimuovere un ambito di ruolo](remove-a-role-scope-exchange-2013-help.md).

