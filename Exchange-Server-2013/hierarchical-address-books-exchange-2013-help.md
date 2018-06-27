---
title: 'Rubriche gerarchiche: Exchange 2013 Help'
TOCTitle: Rubriche gerarchiche
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 50481346
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rubriche gerarchiche

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-03-26_

La rubrica gerarchica consente agli utenti finali di cercare i destinatari nella propria rubrica tramite una gerarchia organizzativa. In genere gli utenti sono limitati all'elenco indirizzi globale predefinito e relative proprietà dei destinatari, ma struttura dell'elenco indirizzi globale spesso non rispecchia accuratamente le relazioni o l'anzianità di lavoro dei destinatari presenti nell'organizzazione. La capacità di personalizzare una rubrica gerarchica associata alla struttura aziendale univoca dell'organizzazione offre agli utenti un metodo efficace per l'individuazione dei destinatari interni.

## Utilizzo delle rubriche gerarchiche

In una rubrica gerarchica, l'organizzazione radice (ad esempio, Contoso, Ltd) viene utilizzata come primo livello. Al di sotto del primo livello, è possibile aggiungere dei livelli figlio al fine di creare una rubrica gerarchica personalizzata segmentata in base alla divisione, al reparto o a qualsiasi altro livello organizzativo che si desidera specificare. Nella figura che segue è illustrata una rubrica gerarchica per Contoso, Ltd con la struttura seguente:

  - Il primo livello rappresenta l'organizzazione radice Contoso, Ltd.

  - Il secondo livello figlio rappresenta le divisioni aziendali in Contoso, Ltd: Corporate Office, Product Support Organization e Sales & Marketing Organization.

  - Il terzo livello figlio rappresenta i reparti all'interno della divisione Corporate Office: Human Resources, Accounting Group e Administration Group.

**Esempio di rubrica gerarchica (HAB) per Contoso,Ltd**

![Finestra di dialogo della rubrica gerarchica](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Finestra di dialogo della rubrica gerarchica")

È possibile fornire un ulteriore livello di struttura gerarchica utilizzando il parametro *SeniorityIndex*. Quando si crea una rubrica gerarchica, utilizzare il parametro *SeniorityIndex* per classificare i singoli destinatari o gruppi organizzativi in base all'anzianità all'interno di tali livelli organizzativi. Questa classificazione consente di specificare l'ordine di visualizzazione dei destinatari o dei gruppi nella rubrica gerarchica. Ad esempio, nell'esempio sopra riportato il parametro *SeniorityIndex* per i destinatari nella divisione Corporate Office è impostato come segue:

  - `100` per David Hamilton

  - `50` per Rajesh M. Patel

  - `25` per Amy Alberts


> [!NOTE]
> Se il parametro <EM>SeniorityIndex</EM> non è impostato o è lo stesso per due o più utenti, l'ordinamento della rubrica gerarchica (HAB) utilizzerà il parametro <EM>PhoneticDisplayName</EM> per elencare gli utenti in ordine alfabetico crescente. Se il valore del parametro <EM>PhoneticDisplayName</EM> non è impostato, l'ordinamento della rubrica gerarchica (HAB) verrà impostato sul parametro predefinito <EM>DisplayName</EM> e gli utenti saranno elencati in ordine alfabetico crescente.



## Configurazione delle rubriche gerarchiche

Istruzione dettagliate per la creazione delle rubriche gerarchiche incluse nell'argomento [Abilitare o disabilitare rubriche gerarchiche](enable-or-disable-hierarchical-address-books-exchange-2013-help.md). In generale, i passi sono i seguenti:

1.  Creare un gruppo di distribuzione che verrà utilizzato per l'organizzazione radice (primo livello). Utilizzare eventualmente un'unità organizzativa esistente nella foresta di Exchange per il gruppo di distribuzione.

2.  Creare gruppi di distribuzione per i livelli figlio e designarli come membri della rubrica gerarchica. Modificare il parametro *SeniorityIndex* di tali gruppi in modo che vengano elencati nel corretto odine gerarchico nell'organizzazione radice.

3.  Aggiungere i membri dell'organizzazione. Modificare il parametro *SeniorityIndex* dei membri in modo che vengano elencati nel corretto ordine gerarchico nei livelli figlio.

4.  Per l'accesso facilitato, è possibile utilizzare il parametro *PhoneticDisplayName* che consente di specificare la pronuncia fonetica del parametro *DisplayName*.

