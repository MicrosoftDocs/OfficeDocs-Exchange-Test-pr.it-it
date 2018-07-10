---
title: "modalità di coordinamento dell'attivazione del centro dati: Exchange 2013 Help"
TOCTitle: modalità di coordinamento dell'attivazione del centro dati
ms:assetid: 57e4bf22-eeae-42a5-beb3-d68d06489592
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979790(v=EXCHG.150)
ms:contentKeyID: 50480659
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# modalità di coordinamento dell'attivazione del centro dati

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-07-14_

La modalità di coordinamento dell'attivazione del centro dati (DAC) è una proprietà di un gruppo di disponibilità del database (DAG). La modalità DAC è disabilitata per impostazione predefinita, ma deve essere abilitata per tutti i gruppi di disponibilità del database con due o più membri che utilizzano la replica continua. La modalità DAC non deve essere abilitata per i DAG che usano la modalità di replica di terze parti a meno che non sia specificato dal fornitore di terze parti.

La modalità DAC viene usata per controllare il montaggio del database al comportamento di avvio di un DAG. Questo controllo è progettato per impedire che si verifichi split brain a livello di database durante il cambio di datacenter. Split brain, noto anche come sindrome split brain, è una condizione che causa che una copia di database venga montata come copia attiva su due membri dello stesso DAG che non possono comunicare. Lo split brain viene impedito utilizzando la modalità DAC perché questa chiede ai membri DAG di ottenere l'autorizzazione per montare i database prima di poterlo fare.

Ad esempio, si prenda il caso in cui un datacenter principale contenga due membri e il server di controllo del gruppo DAG e un secondo datacenter contenga altri due membri del gruppo DAG. In questo scenario, il DAG non è in modalità DAC. Il datacenter primario perde potere, è quindi possibile attivare il DAG nel secondo datacenter. Alla fine, il datacenter primario viene ripristinato e i membri DAG nel datacenter primario, che avevano un quorum prima dell'interruzione di alimentazione, verranno avviati e monteranno i propri database. Poiché il datacenter principale è stato ripristinato senza connettività di rete al secondo datacenter e, poiché il DAG non è in modalità DAC, i database attivi all'interno di DAG hanno immesso condizione split brain.

## Funzionamento della modalità DAC

La modalità DAC è progettata per prevenire la sindrome split brain con l'inclusione di un protocollo chiamato Datacenter Activation Coordination Protocol (DACP). Quando la modalità DAC è abilitata, i membri DAG non monteranno automaticamente database anche se hanno quorum. Il protocollo DACP viene utilizzato invece per stabilire quale sia lo stato corrente del gruppo DAG e se Active Manager deve provare a installare i database.

La modalità DAC può essere intesa come livello applicativo del quorum per l'installazione dei database. Per comprendere lo scopo del protocollo DACP e il suo funzionamento, è importante capire lo scenario primario in cui si trova ad essere gestito. Si consideri uno scenario con due datacenter. Si supponga che vi sia una totale interruzione di alimentazione al datacenter primario. In tal caso, tutti i server e la rete WAN non funzionano, quindi l'organizzazione prende la decisione di attivare il datacenter di standby. In quasi tutti gli scenari di ripristino, quando viene ripristinata l'alimentazione al datacenter primario, in genere la connettività WAN non viene subito ripristinata. Questo significa che i membri del gruppo DAG nel datacenter primario verranno di nuovo alimentati, ma non potranno comunicare con i membri del gruppo DAG nel datacenter di standby attivato. Il datacenter primario deve contenere sempre la maggioranza dei votanti del quorum del gruppo DAG, il che significa che quando viene ripristinata l'alimentazione, anche in assenza della connettività WAN con i membri del gruppo DAG nel datacenter di standby, i membri del gruppo DAG nel datacenter primario hanno la maggioranza e quindi il quorum. Questo rappresenta un problema perché con il quorum questi server potrebbero essere in grado di installare i loro database, il che potrebbe evidenziare una divergenza dagli effettivi database attivi che sono installati al momento nel datacenter di standby attivato.

Il protocollo DACP è stato creato per risolvere questo problema. Active Manager salva un bit in memoria (0 o 1) che indica al gruppo DAG se è autorizzato a installare i database locali assegnati come attivi sul server. Quando un gruppo DAG è in modalità DAC, ogni volta che Active Manager si avvia il bit è impostato su 0, il che significa che non è autorizzato a installare i database. Poiché è in modalità DAC, il server deve provare a comunicare con tutti gli altri membri del gruppo DAG che conosce affinché un altro membro del gruppo DAG fornisca una risposta alla domanda se può installare i database locali assegnati ad esso come attivi. La risposta arriva sotto forma di impostazione del bit per altri Active Manager nel gruppo DAG. Se un altro server risponde che il suo bit è impostato su 1, vuol dire che i server sono autorizzati a installare i database, quindi il server che si avvia imposta il suo bit su 1 e installa i database.

Ma quando si ristabilisce l'alimentazione al datacenter primario dopo un'interruzione ripristinando i server ma non la connettività WAN, tutti i membri del gruppo DAG nel datacenter primario avranno il valore 0 come bit DACP e quindi nessun dei server in fase di riavvio nel datacenter ripristinato installerà i database, perché nessuno di loro può comunicare con un membro del gruppo DAG che ha il valore 1 come bit DACP.

## Modalità DAC per i DAG con due membri

I DAG con due membri hanno in sé delle limitazioni che impediscono al bit DACP da solo di proteggersi completamente dalla sindrome split brain a livello dell'applicazione. Per i DAG con due soli membri, la modalità DAC utilizza anche il tempo di avvio del server di controllo di DAG per determinare se è possibile installare i database all'avvio. Il tempo di avvio del server testimone è confrontato al tempo che occorre quando il bit di DACP è impostato su 1.

  - Se il tempo su cui era impostato il bit DACP è precedente al tempo di avvio del server di controllo, il sistema suppone che il membro del gruppo DAG e il server di controllo siano stati avviati allo stesso tempo (forse a causa dell'interruzione di alimentazione nel datacenter primario) e al membro del gruppo DAG non viene consentito di installare i database.

  - Se il tempo del bit DACP è successivo al tempo di avvio del server di controllo, il sistema suppone che il membro del gruppo DAG sia stato riavviato per qualche altra ragione (forse un'interruzione programmata per effettuare la manutenzione o forse un'interruzione anomala o interruzione di alimentazione isolata al membro del gruppo DAG) e quindi gli viene consentito di installare i database.


> [!IMPORTANT]
> Poiché il tempo di avvio del server di controllo è utilizzato per determinare se a un membro del gruppo DAG è consentito di installare i database attivi all'avvio, non bisognerebbe mai riavviare il server di controllo ed un membro del solo gruppo DAG allo stesso tempo. Altrimenti, il membro del gruppo di disponibilità del database potrebbe trovarsi in uno stato in cui non gli è consentito montare i database all'avvio. Se ciò accade, sarà necessario eseguire il cmdlet <A href="https://technet.microsoft.com/it-it/library/dd351169(v=exchg.150)">Restore-DatabaseAvailabilityGroup</A> sul DAG. Ciò ripristina il bit DACP e consente al membro del gruppo DAG di installare i database.



## Altri benefici della modalità DAC

Oltre ad impedire la sindrome split brain a livello dell'applicazione, anche la modalità DAC abilita l'uso dei cmdlet della resilienza incorporata del sito utilizzati per eseguire i passaggi di datacenter. Sono inclusi:

  - [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd335133\(v=exchg.150\))

  - [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351169\(v=exchg.150\))

  - [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd335076\(v=exchg.150\))

L'esecuzione di un passaggio di datacenter per i DAG che non sono in modalità DAC comporta l'uso di una combinazione di strumenti Exchange  e strumenti di gestione cluster. Per ulteriori informazioni, vedere [Passaggi centro dati](datacenter-switchovers-exchange-2013-help.md).

## Abilitazione della modalità DAC

La modalità DAC può essere abilitata solo con Exchange Management Shell. In particolare, è possibile utilizzare il cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) per abilitare la modalità DAC, come illustrato nell'esempio seguente.

    Set-DatabaseAvailabilityGroup -Identity DAG2 -DatacenterActivationMode DagOnly

Nell'esempio precedente, il gruppo DAG2 è stato abilitato per la modalità DAC.

Per ulteriori informazioni sull'abilitazione della modalità DAC, vedere[Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md) e [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)).

