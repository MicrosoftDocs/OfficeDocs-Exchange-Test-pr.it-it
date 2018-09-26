---
title: 'Modificaree impostazioni utenti organizz. limitazione: Exchange 2013 Help'
TOCTitle: Modificare le impostazioni per tutti gli utenti nell'organizzazione di limitazione
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50555679
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare le impostazioni per tutti gli utenti nell'organizzazione di limitazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-08-05_

È possibile controllare risorse impiegate da singoli utenti nell'organizzazione di Exchange per modificare le impostazioni di limitazione predefinito.

Controllo risorse impiegate da singoli utenti era possibile in Exchange Server 2010 e questa funzionalità è stata espansa per Exchange Server 2013. Il criterio denominato GlobalThrottlingPolicy definisce le impostazioni di limitazione per tutti gli utenti nuovi ed esistenti all'interno dell'organizzazione a meno che non è stato personalizzato i criteri di limitazione predefinito. In molti tipica Exchange scenari di distribuzione, il criterio denominato GlobalThrottlingPolicy è sufficiente per gestire gli utenti.

Per personalizzare le impostazioni di limitazione che si applicano a tutti gli utenti nell'organizzazione, creare un nuovo criterio di limitazione con l'assegnazione dell'ambito dell'organizzazione. È possibile modificare solo l'impostazione predefinita le impostazioni di limitazione utilizzando Shell.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Limitazione utente" nell'argomento [Autorizzazioni di integrità e prestazioni del server](server-health-and-performance-permissions-exchange-2013-help.md) .

  - In nuovi criteri dell'ambito dell'organizzazione, è necessario impostare solo le impostazioni di limitazione che differiscono da quello del criterio denominato GlobalThrottlingPolicy e tutti gli altri criteri dell'organizzazione. In questo modo, il resto delle impostazioni di criteri dal criterio denominato GlobalThrottlingPolicy verrà ereditato, così come tutti gli aggiornamenti vengono aggiunti successivamente che Exchange Aggiorna i criteri di limitazione. È consigliabile leggere la sezione "Gestisci criteri utilizzando gli ambiti di limitazione" nel argomento [Gestione del carico di lavoro di Exchange](exchange-workload-management-exchange-2013-help.md) prima di eseguire la procedura seguente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare la Shell per modificare il modo in cui risorse può essere utilizzato da tutti gli utenti all'interno dell'intera organizzazione

In questo esempio viene creato un criterio di limitazione che si applica a tutti gli utenti nell'organizzazione. Qualsiasi parametro che si omette eredita i valori dal criterio GlobalThrottlingPolicy di limitazione predefinito.

```powershell
New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-ThrottlingPolicy](https://technet.microsoft.com/it-it/library/dd351045\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente il criterio di limitazione dell'organizzazione, eseguire le operazioni seguenti:

1.  Eseguire il comando riportato di seguito.
    
    ```powershell
        Get-ThrottlingPolicy | Format-List
    ```

2.  Verificare che l'organizzazione limitazione criterio che appena creato sia elencato nella colonna che mostra l'oggetto GlobalThrottlingPolicy.

3.  Eseguire il comando riportato di seguito.
    
    ```powershell
    Get-ThrottlingPolicy | Format-List
    ```

4.  Verificare che le proprietà per il nuovo criterio organizzazione corrispondano i valori configurati.

