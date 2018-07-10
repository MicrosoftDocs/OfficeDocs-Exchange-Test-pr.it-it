---
title: 'Gestione del carico di lavoro di Exchange: Exchange 2013 Help'
TOCTitle: Gestione del carico di lavoro di Exchange
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 50480282
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione del carico di lavoro di Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-11-16_

Un carico di lavoro di Exchange è una funzionalità, un protocollo o un servizio di Exchange Server esplicitamente definito allo scopo di gestire le risorse di sistema di Exchange. Ciascun carico di lavoro di Exchange consuma risorse di sistema, quali CPU, operazioni di database delle cassette postali o richieste Active Directory per eseguire le richieste utente o il lavoro in background. Esempi di carichi di lavoro di Exchange includono Outlook Web App, Exchange ActiveSync, migrazione delle cassette postali e assistenti di cassette postali.

Per gestire carichi di lavoro di Exchange, controllo delle risorse impiegate da singoli utenti (detti anche limitazione in Exchange 2010). Controllo Exchange system risorse impiegate da singoli utenti era possibile in Exchange Server 2010 e questa funzionalità è stata espansa per Exchange Server 2013.


> [!NOTE]
> Gestione dei carichi di lavoro tramite il monitoraggio dell'integrità delle risorse di sistema sui server Exchange nell'organizzazione deve essere eseguita solo seguendo le istruzioni del cliente servizio supporto tecnico Microsoft.



## Gestione dei carichi di lavoro tramite il controllo del modo in cui i singoli utenti consumano le risorse

La funzionalità di limitazione è stata migliorata in Exchange 2013. La funzionalità avanzata consente di verificare che il consumo eccessivo di risorse da parte dei singoli utenti non influisca in modo negativo sulle prestazioni del server o sull'esperienza dell'utente.

Per impostazione predefinita, limitazione Exchange 2013 consente agli utenti di aumentare il consumo di risorse per brevi periodi senza che si verifichino la riduzione della larghezza di banda. Inoltre, il blocco completo di utenti che utilizzano una quantità elevata di risorse raramente oppure non si verificano. Anziché completamente il blocco di un utente di eseguire operazioni, si verifica di limitazione e i processi sono ritardati per brevi periodi di tempo (interazione utente di esse come "microdelays"), che si verificano prima che provocano un impatto significativo in un server.

**Attività di rilievo delle funzionalità**

Di seguito, sono riportate alcune attività di rilievo relative al modo in cui Exchange controlla come i singoli utenti consumano le risorse in Exchange 2013:

  - **Burst concessi**   Burst concessi consente agli utenti di consumare un numero maggiore di risorse per brevi periodi senza che si verifichino limitazioni.

  - **Frequenza di ricarica**   Frequenza di ricarica gestisce il consumo di risorse degli utenti utilizzando una sistema di budget delle risorse. È possibile impostare la frequenza di ricarica dei budget delle risorse degli utenti. Ad esempio, un valori pari a 600.000 (in millisecondi) implica che i budget degli utenti vengono ricaricati ogni dieci minuti di utilizzo per ora.

  - **Regolazione del traffico**   Quando l'utilizzo delle risorse di un utente raggiunge il limite configurato per un periodo di tempo, tale utente viene ritardato per periodi di tempo molto brevi per evitare un impatto significativo su un server. Generalmente, gli utenti non notano questi "microritardi". Questo processo consente a Exchange 2013 di regolare il traffico senza impedire agli utenti di essere produttivi. La regolazione del traffico ha meno impatto sugli utenti rispetto al blocco precedente e riduce, in modo significativo, le possibilità che si verifichi un blocco.

  - **Utilizzo massimo**   In rari casi, un utente potrebbe consumare una quantità molto elevata di risorse per un breve periodo di tempo. A titolo di precauzione, è possibile che venga impedito a un utente che raggiunge la soglia di utilizzo massimo di utilizzare temporaneamente le risorse. Gli utenti a cui è stato temporaneamente impedito di utilizzare le risorse, vengono sbloccati non appena vengono ricaricati i loro budget di utilizzo.

Per un elenco dei cmdlet che è possibile utilizzare per controllare risorse impiegate da singoli utenti, vedere "Cmdlet per l'utilizzano delle risorse da singoli utenti di controllo" più avanti in questo argomento.

**Considerazioni sulla distribuzione e sulla funzionalità di limitazione di Exchange 2013**

Sia che si esegua un'installazione corretta di Exchange 2013 o si installi Exchange 2013 in un ambiente di coesistenza comprendente computer Exchange 2010, tutti gli utenti con cassette postali su computer che utilizzano Exchange 2013 vengono limitati tramite l'uso della nuova funzionalità di limitazione di Exchange 2013. Tuttavia, le cassette postali di Exchange 2010 continueranno a essere limitate dalla funzionalità di limitazione di Exchange 2010 quando accedono alle proprie cassette postali da server Accesso client di Exchange 2010.

Quando si installa Exchange 2013 in un ambiente di coesistenza, il processo di installazione di Exchange 2013 potrebbe tentare di riportare alcune delle impostazioni di limitazione effettuate nella configurazione di Exchange 2010. Tuttavia, la funzionalità di limitazione di Exchange 2013 è talmente differente che, generalmente, l'impatto di qualsiasi impostazione di limitazione legacy non influirà sulla modalità di funzionamento della limitazione in Exchange 2013.

**Gestione dei criteri di limitazione tramite l'uso degli ambiti**

In modo analogo a Exchange 2010, Exchange 2013 dispone di un singolo criterio di limitazione predefinito. In Exchange 2013, il criterio di limitazione predefinito è denominato **GlobalThrottlingPolicy**. Tale criterio dispone dell'ambito **Global**. Altri ambiti di limitazione utente disponibili sono **Organization** e **Regular**. A causa dell'introduzione dell'assegnazione degli ambiti per i criteri di limitazione utente in Exchange 2013, i criteri di limitazione vengono gestiti in maniera differente rispetto a Exchange 2010. Il criterio **GlobalThrottlingPolicy** definisce le impostazioni di limitazione di base predefinite per tutti gli utenti nuovi ed esistenti all'interno dell'organizzazione, a meno che non si disponga di criteri di limitazione personalizzati per l'organizzazione. In molti scenari di distribuzione di Exchange tipici, il criterio **GlobalThrottlingPolicy** sarà adatto alla gestione dei propri utenti.

Si consiglia di non personalizzare le impostazioni di limitazione modificando il criterio **GlobalThrottlingPolicy**. Piuttosto, è necessario creare ulteriori criteri di limitazione. La creazione di ulteriori criteri di limitazione consentirà di gestire meglio i carichi di lavoro. Eviterà anche che le modifiche apportate alle impostazioni dei criteri di limitazione vengano sovrascritte da aggiornamenti di Exchange 2013 futuri.

Per personalizzare le impostazioni di limitazione applicate a tutti gli utenti dell'organizzazione, creare un nuovo criterio di limitazione con l'assegnazione dell'ambito **Organization**. Nei nuovi criteri con ambito organizzazione, è sufficiente configurare le impostazioni di limitazione che differiscono da quelle del criterio **GlobalThrottlingPolicy**. Per personalizzare le impostazioni di limitazione applicate a determinati utenti dell'organizzazione, creare un nuovo criterio di limitazione con l'assegnazione dell'ambito **Regular**. Nei nuovi criteri con ambito regolare, è sufficiente configurare le impostazioni di limitazione che differiscono da quelle del criterio **GlobalThrottlingPolicy** e di qualsiasi altro criterio di organizzazione. Ciò consentirà di ereditare il resto delle impostazioni dei criteri dal criterio **GlobalThrottlingPolicy** e di trarre vantaggi da tutti gli aggiornamenti apportati ai criteri di limitazione aggiunti negli aggiornamenti futuri di Exchange.

## Gestione delle impostazioni di limitazione dei carichi di lavoro

Gestire le impostazioni di limitazione dei carichi di lavoro di Exchange utilizzando Exchange Management Shell.

**Cmdlet per controllare il modo in cui i singoli utenti utilizzano le risorse**

Gestire le impostazioni di limitazione utilizzando i seguenti cmdlet, introdotti in Exchange 2010:

Gestione dei criteri di limitazione

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/it-it/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/it-it/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/it-it/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/it-it/library/dd298094\(v=exchg.150\))

Assegnazione dei criteri di limitazione

  - [Get-ThrottlingPolicyAssociation](https://technet.microsoft.com/it-it/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/it-it/library/ff459231\(v=exchg.150\))


> [!NOTE]
> I cmdlet di gestione del carico di lavoro di sistema <STRONG>*-ResourcePolicy</STRONG>, <STRONG>*-WorkloadManagementPolicy</STRONG> e <STRONG>*-WorkloadPolicy</STRONG> sono diventati obsoleti. Impostazioni di gestione del carico di lavoro di sistema devono essere personalizzate solo seguendo le istruzioni del cliente servizio supporto tecnico Microsoft.


