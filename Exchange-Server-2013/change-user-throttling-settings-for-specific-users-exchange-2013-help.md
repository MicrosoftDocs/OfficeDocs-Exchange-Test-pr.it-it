---
title: 'Modificare le impostazioni per utenti specifici di limitazione: Exchange 2013 Help'
TOCTitle: Modificare le impostazioni per utenti specifici di limitazione
ms:assetid: c5f834d6-189d-485e-9800-5e0066815ecf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863577(v=EXCHG.150)
ms:contentKeyID: 50555690
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare le impostazioni per utenti specifici di limitazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-08-05_

È possibile controllare risorse impiegate da singoli utenti nell'organizzazione di Exchange per modificare le impostazioni di limitazione predefinito.

Controllo risorse impiegate da singoli utenti era possibile in Exchange Server 2010 e questa funzionalità è stata espansa per Exchange Server 2013. Il criterio denominato GlobalThrottlingPolicy definisce le impostazioni di limitazione per tutti gli utenti nuovi ed esistenti all'interno dell'organizzazione a meno che non è stato personalizzato i criteri di limitazione predefinito. In molti tipica Exchange scenari di distribuzione, il criterio denominato GlobalThrottlingPolicy è sufficiente per gestire gli utenti.

Per personalizzare le impostazioni di limitazione da applicare solo a specifici utenti all'interno dell'organizzazione, creare un nuovo criterio di limitazione con Regular l'assegnazione dell'ambito. È possibile modificare solo l'impostazione predefinita le impostazioni di limitazione utilizzando Shell.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Limitazione utente" nell'argomento [Autorizzazioni di integrità e prestazioni del server](server-health-and-performance-permissions-exchange-2013-help.md) .

  - In nuovi criteri regolari ambito, è necessario impostare solo le impostazioni di limitazione che differiscono da quello del criterio denominato GlobalThrottlingPolicy e tutti gli altri criteri dell'organizzazione. In questo modo, il resto delle impostazioni di criteri dal criterio denominato GlobalThrottlingPolicy verrà ereditato, così come tutti gli aggiornamenti vengono aggiunti successivamente che Exchange Aggiorna i criteri di limitazione. È consigliabile leggere la sezione "Gestisci criteri utilizzando gli ambiti di limitazione" nel argomento [Gestione del carico di lavoro di Exchange](exchange-workload-management-exchange-2013-help.md) prima di eseguire la procedura seguente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare la Shell per modificare il modo in cui risorse può essere utilizzato da utenti specifici in tutta l'organizzazione

In questo esempio viene creato un utente non predefinito denominato ITStaffPolicy che può essere associata a utenti specifici di criteri di limitazione. Qualsiasi parametro che si omette eredita i valori dal criterio GlobalThrottlingPolicy di limitazione predefinito. Dopo aver creato il criterio, è necessario associarlo a utenti specifici.

    New-ThrottlingPolicy -Name ITStaffPolicy -EwsMaxConcurrency 4 -ThrottlingPolicyScope Regular

In questo esempio consente di associare un utente con il nome di utente tonysmith con il criterio di limitazione ITStaffPolicy (che con limiti più).

    Set-ThrottlingPolicyAssociation -Identity tonysmith -ThrottlingPolicy ITStaffPolicy

Non è necessario utilizzare il cmdlet **Set-ThrottlingPolicyAssociation** per associare un utente a un criterio. Il comando seguente mostra un altro modo per associare il criterio di limitazione ITStaffPolicy tonysmith.

```
$b = Get-ThrottlingPolicy ITStaffPolicy
```

```
Set-Mailbox -Identity tonysmith -ThrottlingPolicy $b
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-ThrottlingPolicy](https://technet.microsoft.com/it-it/library/dd351045\(v=exchg.150\)) e [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/it-it/library/ff459231\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente alle normali criterio di limitazione, eseguire le operazioni seguenti:

1.  Eseguire il comando riportato di seguito.
    
        Get-ThrottlingPolicy | Format-List

2.  Verificare che nella colonna che mostra l'oggetto GlobalThrottlingPolicy sia elencato regolari limitazione criterio che appena creato.

3.  Eseguire il comando riportato di seguito.
    
        Get-ThrottlingPolicy | Format-List

4.  Verificare che le proprietà per il nuovo criterio regolare corrispondano i valori configurati.

5.  Eseguire il comando riportato di seguito.
    
        Get-ThrottlingPolicyAssociation

6.  Verificare che il nuovo criterio regolare sia associato all'utente o gli utenti si a esso associati.

