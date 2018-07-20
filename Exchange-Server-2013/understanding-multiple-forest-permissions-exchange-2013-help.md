---
title: 'Informazioni sulle autorizzazioni di più foreste: Exchange 2013 Help'
TOCTitle: Informazioni sulle autorizzazioni di più foreste
ms:assetid: 8241033f-e201-4799-b17c-4f120c6e6445
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298099(v=EXCHG.150)
ms:contentKeyID: 50481059
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sulle autorizzazioni di più foreste

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Molte organizzazioni distribuiscono più foreste per creare confini di protezione al loro interno. L'utilizzo di più foreste consente agli amministratori di definire questi confini di protezione in modo più adeguato ai loro requisiti, assicurando che abbia accesso alle risorse il minor numero possibile di persone oppure segmentando i reparti dell'organizzazione.

Microsoft Exchange Server 2013 supporta due tipi di topologie a più foreste:

  - **Tra foreste**   Le topologie tra foreste possono presentare più foreste, ognuna con la propria installazione di Exchange.

  - **Foresta di risorse**   Le topologie a foresta di risorse presentano una foresta Exchange e uno o più foreste di account.

Ai fini di questo argomento, la foresta che contiene i gruppi di protezione universali (USG, Universal Security Group) e gli utenti all'esterno della foresta in cui è installato Exchange 2013, sia che si tratti di una foresta di account o di un'altra foresta di risorse, è denominata foresta esterna.

La configurazione delle autorizzazioni in una topologia a più foreste si basa sulla corretta configurazione dei trust tra foreste e della sincronizzazione dell'elenco indirizzi globale (GAL, Global Address List) per la creazione di cassette postali collegate. La foresta Exchange 2013 deve considerare attendibile la foresta esterna che contiene i gruppi di protezione universali associati a gruppi di ruoli collegati e utenti associati alle cassette postali collegate.

Exchange 2013 utilizza un modello di autorizzazioni di controllo di accesso basato sui ruoli (RBAC, Role Based Access Control). I gruppi di ruoli di gestione di cui gli amministratori sono membri e i criteri di assegnazione dei ruoli di gestione a cui gli utenti finali sono associati determinato le operazioni che ogni amministratore e ogni utente finale può eseguire. Per comprendere le autorizzazioni per più foreste, è necessario avere familiarità con il controllo di accesso basato sui ruoli. Per ulteriori informazioni sul controllo di accesso basato sui ruoli, sui gruppi di ruoli e sui criteri di assegnazione dei ruoli, vedere gli argomenti seguenti:

  - [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md)

  - [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md)

  - [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md)

Per informazioni sulle attività relative alla gestione delle autorizzazioni? vedere [Autorizzazioni](permissions-exchange-2013-help.md).

**Sommario**

Permissions in a Multiple Forest Topology

Cross-Boundary Permissions

Configure Cross-Boundary Permissions

## Autorizzazioni in una topologia a più foreste

Il controllo di accesso basato sui ruoli applica autorizzazioni a tutti gli oggetti Exchange in un'unica foresta e la configurazione del controllo di accesso basato sui ruoli in ogni foresta è impostata in modo indipendente da tutte le altre foreste. Quando si crea un gruppo di ruoli in una foresta, tale gruppo di ruoli non è presente in alcuna altra foresta e le autorizzazioni concesse da tale gruppo di ruoli si applicano esclusivamente alla foresta in cui è stato creato. Ad esempio, un membro di un gruppo di ruoli che concede autorizzazioni per la creazione di una cassetta postale può creare una cassetta postale solo nella foresta che contiene tale gruppo di ruoli.

Se sono presenti più foreste di Exchange e si desidera configurare le autorizzazioni in maniera identica in ogni foresta, è necessario applicare esplicitamente la stessa configurazione in ogni foresta. Ad esempio, se sono presenti due foreste di Exchange 2013 e si desidera creare un gruppo di ruoli Compliance Management per gestire le autorizzazioni per il reparto legale, è necessario procedere come segue:

  - In ogni foresta, creare un gruppo di ruoli denominato Compliance Management. Se gli amministratori appartengono a una foresta esterna separata da qualsiasi foresta Exchange, creare entrambi i gruppi di ruoli come gruppi di ruoli collegati. Per ulteriori informazioni sui gruppi di ruoli, vedere la sezione Cross-Boundary Permissions.

  - In ogni foresta, creare assegnazioni di ruolo tra i nuovi gruppi di ruoli e i ruoli che si desidera utilizzare.

  - Come parte delle nuove assegnazioni di ruolo, facoltativamente è possibile aggiungere ambiti che includano gli oggetti server e destinatario in ogni foresta.

  - Se i gruppi di ruoli sono stati creati come gruppi di ruoli collegati, aggiungere membri al gruppo di protezione universale associato nella foresta esterna.

Nella figura seguente viene illustrato come i gruppi di ruoli configurati nelle foreste Exchange 2013 sono associati alle loro foreste rispettive. Il gruppo di ruoli Organization Management nella foresta Exchange 2013 A concede le autorizzazioni solo per la gestione delle cassette postali e dei server in tale foresta. Analogamente, i gruppi di ruoli nella foresta Exchange 2013 B concedono autorizzazioni solo per le cassette postali e i server in tale foresta.

Nella figura è inoltre illustrato che in ogni foresta viene creato il gruppo di ruoli personalizzato A. Anche se sono stati creati con lo stesso nome, ognuno è un'entità separata. Infatti, come mostrato nella figura, a ognuno possono essere assegnati ruoli di gestione diversi nelle rispettive foreste. Al gruppo di ruoli personalizzato A nella foresta Exchange 2013 A sono assegnati i ruoli di ricerca delle cassette postali e di verifica dei messaggi mentre al gruppo di ruoli personalizzato A nella foresta Exchange 2013 B sono assegnati i ruoli di ricerca delle cassette postali e di gestione conservazione.

Infine, anche gli ambiti di gestione creati in ogni foresta sono vincolati dalla foresta. Gli ambiti server creati in ogni foresta possono contenere esclusivamente i server membri di tale foresta. L'ambito server A può contenere solo i server all'interno della foresta Exchange 2013 A mentre l'ambito server B può contenere solo i server all'interno della foresta Exchange 2013 B. Analogamente, l'ambito destinatario nella foresta Exchange 2013 B può contenere solo cassette postali che si trovano all'interno della foresta Exchange 2013 B.

**Relazione tra controllo di accesso basato sui ruoli e confine di ambito della foresta**

![Relazioni tra ambiti limite della foresta e RBAC](images/Dd298099.220da7c3-cbb8-42ac-9d58-084d996bf837(EXCHG.150).gif "Relazioni tra ambiti limite della foresta e RBAC")

## Autorizzazioni oltre i limiti

Le autorizzazioni concesse dal controllo di accesso basato sui ruoli consentono esclusivamente agli utenti di visualizzare o modificare gli oggetti Exchange in una foresta specifica. Tuttavia, è possibile concedere autorizzazioni per la visualizzazione e la modifica di oggetti Exchange in una foresta a utenti all'esterno di tale foresta. Utilizzando le autorizzazioni tra confini, è possibile centralizzare gli account di gestione di Exchange in un'unica foresta anziché dover autenticare ogni singola foresta per l'esecuzione delle attività.


> [!NOTE]
> Le autorizzazioni concesse a un utente all'esterno di una foresta Exchange verranno comunque applicate solo a tale foresta Exchange specifica. Ad esempio, se un utente in una foresta è membro del gruppo di ruoli collegato Organization Management contenuto in ForestA, l'utente potrà gestire solo gli oggetti Exchange contenuti in ForestA. Un utente deve essere reso membro di gruppi di ruoli collegati in ogni foresta Exchange per ottenere le autorizzazioni per la gestione di ogni foresta.



Le autorizzazioni oltre i limiti consentono inoltre di applicare criteri di assegnazione di ruolo alle cassette postali degli utenti che possiedono cassette postali in una foresta di Exchange, ma i cui account utente risiedono in una foresta di account. Exchange 2013 supporta le autorizzazioni oltre i limiti utilizzando gruppi di ruoli collegati e cassette postali collegati, come spiegato nelle sezioni successive.

## Autorizzazioni amministrative

Le autorizzazioni amministrative vengono concesse tra i confini delle foreste mediante l'uso di gruppi di ruoli collegati e di cassette postali collegate.

Un gruppo di ruoli collegato viene creato nell'organizzazione Exchange 2013 e collegato a un gruppo di protezione universale tra il confine delle foreste nella foresta esterna. Il gruppo di protezione universale a cui il gruppo di ruoli è collegato può essere:

  - Un gruppo di protezione universale dedicato per l'utilizzo specifico del gruppo di ruoli collegato

  - Un gruppo di protezione universale collegato a gruppi di ruoli in più foreste Exchange 2013

  - Un gruppo di protezione universale di gruppo di ruoli in un altra foresta Exchange 2013

  - Un gruppo di protezione universale associata a un gruppo di ruoli Exchange Server 2007Exchange 2010 o ruoli amministrativo

Il gruppo di protezione universale a cui il gruppo di ruoli è collegato deve trovarsi in un'altra foresta. È possibile collegare un gruppo di ruoli collegato a un gruppo di protezione universale nella stessa foresta.

Nella figura seguente è illustrato che i gruppi di protezione universale di una foresta di account possono essere associati a gruppi di ruoli in una o più foreste di risorse Exchange 2013. I membri dei gruppi di protezione universale nella foresta di account diventano effettivamente membri dei gruppi di ruoli tramite i gruppi di protezione universale.

**Gruppi di ruoli collegati associati a gruppi di protezione universale in una foresta separata**

![Relazioni tra gruppo di ruoli collegato e gruppo di protezione universale](images/Dd298099.23f245e8-b80f-4082-8628-ee6701259be6(EXCHG.150).gif "Relazioni tra gruppo di ruoli collegato e gruppo di protezione universale")

Quando si crea un gruppo di ruoli collegato, si assegnano ruoli al gruppo di ruoli collegato nella foresta Exchange 2013. Le assegnazioni che associano i ruoli al gruppo di ruoli collegato possono includere ambiti di gestione, se necessario. Questi ambiti sono limitati alla foresta in cui il gruppo di ruoli collegato è creato.

L'appartenenza del gruppo di ruoli collegato è gestita aggiungendo e rimuovendo membri dal gruppo di protezione universale nella foresta esterna. Quando si aggiungono membri a questo gruppo di protezione universale, a tali membri sono concesse le autorizzazioni assegnate al gruppo di ruoli collegato nella foresta Exchange 2013. Se si sono collegati più gruppi di ruoli allo stesso gruppo di protezione universale, ai membri di tale gruppo di protezione universale sono concesse le autorizzazioni assegnate a ogni gruppo di ruoli collegato in ogni foresta Exchange 2013.

Non è possibile gestire l'appartenenza di un gruppo di ruoli collegato dalla foresta Exchange 2013.

Un secondo metodo per assegnare autorizzazioni amministrative tra i confini delle foreste è tramite l'uso di cassette postali collegate. Perché gli utenti di una foresta di account possano utilizzare una distribuzione Exchange 2013 in una foresta di risorse Exchange 2013 separata, è necessario configurare cassette postali collegate per ogni utente. Le cassette postali collegate possono essere aggiunte come membri ai gruppi di ruoli nella foresta Exchange 2013. Quando una cassetta postale collegata diventa membro di un gruppo di ruoli, a tale cassetta postale collegata, e a sua volta all'utente nella foresta di account associata alla cassetta postale collegata, vengono concesse le autorizzazioni fornite dal gruppo di ruoli.

Nella figura seguente è illustrata la relazione tra gli utenti in una foresta di account, le cassette postali collegate ad essi associate e i gruppi di ruolo di cui sono membri.

**Utenti in una foresta di account associata a cassette postali, le quali sono membri di gruppi di ruoli**

![Relazioni tra gruppo di ruoli e cassetta postale collegata](images/Dd298099.e59242f6-5c63-4114-90f7-6b6c2478570c(EXCHG.150).gif "Relazioni tra gruppo di ruoli e cassetta postale collegata")

I gruppi di ruoli collegati e le cassette postali collegate presentano vantaggi e svantaggi, quando utilizzati per assegnare autorizzazioni amministrative tra i confini delle foreste. Nella tabella seguente ne vengono descritti alcuni.

### Vantaggi e svantaggi di gruppi di ruoli collegati e cassette postali collegate

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppi di ruoli collegati o cassette postali collegate</th>
<th>Vantaggio</th>
<th>Svantaggio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gruppi di ruoli collegati</p></td>
<td><p>È possibile associare più gruppi di ruoli da più foreste Exchange 2013 in un solo gruppo di protezione universale in una foresta di account o in un'altra foresta di risorse Exchange. In questo modo è possibile amministrare topologie di foreste Exchange complesse tramite un insieme ridotto di gruppi di protezione universale in un'unica foresta.</p></td>
<td><p>Un gruppo di ruoli normale non può essere convertito in un gruppo di ruoli collegato. È necessario creare manualmente gruppi di ruoli collegati per sostituire ogni gruppo di ruoli normale che presenta autorizzazioni che si desiderano concedere tra un confine tra foreste. Per ulteriori informazioni, vedere Configure cross-boundary permissions.</p></td>
</tr>
<tr class="even">
<td><p>Cassette postali collegate</p></td>
<td><p>Le cassette postali collegate consente di utilizzare i gruppi di ruoli esistenti nella foresta Exchange. Le cassette postali collegate vengono aggiunte come membri ai gruppi di ruoli esistenti nello stesso modo di cassette normali, gruppi di protezione universale e utenti nella foresta Exchange.</p></td>
<td><p>Se si concedono autorizzazioni in più foreste Exchange 2013 utilizzando cassette postali collegate a un unico utente in una foresta di account, è necessario modificare l'appartenenza del gruppo di ruoli in ogni foresta Exchange 2013 se si desidera modificare le autorizzazioni concesse all'utente.</p></td>
</tr>
</tbody>
</table>


Si consiglia di utilizzare gruppi di ruoli collegati per concedere autorizzazioni tra i confini delle foreste se si prevede di avere più foreste di risorse Exchange.

## Autorizzazioni dell'utente finale

Le autorizzazioni dell'utente finale sono assegnate alle singole cassette postali utilizzando criteri di assegnazione dei ruoli. Quando Exchange 2013 viene installato in una foresta di risorse, le cassette postali collegate vengono create nella foresta di risorse e vengono associate agli account utente nella foresta di account.

Quando viene creata una cassetta postale collegata, viene assegnata a un criterio predefinito di assegnazione di ruolo come una cassetta postale normale. Il criterio di assegnazione di ruolo determina quali autorizzazioni dell'utente finale sono concesse alla cassetta postale. Queste autorizzazioni consentono agli utenti di visualizzare e modificare le impostazioni relativa alla seguente e ad altre funzionalità:

  - Informazioni sul profilo dell'utente finale

  - Messaggi vocali degli utenti finali

  - Appartenenza e proprietà distribuzione degli utenti finali

Quando un criterio di assegnazione di ruolo viene assegnato a una cassetta postale collegata, all'utente nella foresta di account associata alla cassetta postale collegata vengono concesse autorizzazioni per la gestione delle funzionalità disponibili a tale utente. Le autorizzazioni si applicano esclusivamente alle risorse nella foresta Exchange in cui è contenuta la cassetta postale collegata. Nella figura seguente viene illustrata la relazione tra l'utente finale nella foresta di account, la relativa cassetta postale associata e il criterio di assegnazione di ruolo assegnato alla cassetta postale collegata. Inoltre, una cassetta postale associata a un utente amministratore nella foresta di account può essere associata a più gruppi di ruoli oltre a una criterio di assegnazione di ruolo.

**Utenti in una foresta di account associata a cassette postali collegate assegnate a un criterio di assegnazione di ruolo**

![Relazioni tra gruppo di ruoli e criteri di assegnazione](images/Dd298099.785b9b35-4292-43ce-917b-117d0174742e(EXCHG.150).gif "Relazioni tra gruppo di ruoli e criteri di assegnazione")

Inizio pagina

## Configurare le autorizzazioni oltre i limiti

Per configurare le autorizzazioni tra confini in una topologia a più foreste, è necessario creare gruppi di ruoli collegati per ognuno dei gruppi di ruoli che si desidera collegare a gruppi di protezione universale in una foresta esterna. È pertanto necessario creare un gruppo di ruoli collegato per ogni gruppo di ruoli incorporato. È necessario:

1.  Creare un gruppo di protezione universale per ogni gruppo di ruoli collegato da creare. Aggiungere membri al gruppo di protezione universale a cui si desidera concedere autorizzazioni.

2.  Creare un gruppo di ruoli collegato per ogni gruppo di ruoli incorporato. Quando viene creato il gruppo di ruoli collegato, si verifica quanto segue:
    
      - Gli stessi ruoli assegnati al gruppo di ruoli incorporato vengono assegnati al nuovo gruppo di ruoli collegato.
    
      - Il gruppo di ruoli collegato viene associato al gruppo di protezione universale nella foresta esterna.

3.  Creare gruppi di ruoli collegati per tutti i gruppi di ruoli personalizzati che si sono creati.

4.  Facoltativamente, assegnare ambiti personalizzati ai nuovi gruppi di ruoli collegati.

Per informazioni dettagliate sull'esecuzione di questi passaggi, vedere gli argomenti seguenti:

  - [Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

  - [Gestire i gruppi di ruoli collegato](manage-linked-role-groups-exchange-2013-help.md)

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

Se è necessario modificare il gruppo di protezione universale a cui è associato un gruppo di ruoli collegato, vedere [Gestire i gruppi di ruoli collegato](manage-linked-role-groups-exchange-2013-help.md).

Quando viene creata una cassetta postale collegata, viene automaticamente assegnata a un criterio di assegnazione di ruolo. È possibile modificare il criterio di assegnazione di ruolo assegnato alla cassetta postale collegata o modificare il criterio di assegnazione di ruolo assegnato alle cassette postali per impostazione predefinita al momento della loro creazione. Per ulteriori informazioni, vedere gli argomenti seguenti:

  - [Modificare il criterio di assegnazione di una cassetta postale](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

  - [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)

