---
title: 'Informazioni sui ambiti esclusivi: Exchange 2013 Help'
TOCTitle: Informazioni sui ambiti esclusivi
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 50480283
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sui ambiti esclusivi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Gli *ambiti esclusivi* sono un tipo speciale di ambiti di gestione espliciti che possono essere associati alle assegnazioni dei ruoli di gestione. Gli ambiti esclusivi sono progettati per le situazioni in cui si desidera controllare in modo rigoroso l'accesso a un gruppo di oggetti particolarmente preziosi, come, ad esempio, la cassetta postale di un amministratore delegato.

Un'assegnazione di ruolo che dispone di un ambito esclusivo è detta *assegnazione di ruolo esclusiva*.

Quando si crea un ambito esclusivo, solo gli utenti assegnati a tale ambito esclusivo o a un ambito esclusivo equivalente possono modificare gli oggetti corrispondenti all'ambito. Gli utenti non assegnati a tale ambito esclusivo, o a un ambito equivalente, non possono modificare gli oggetti corrispondenti all'ambito, nemmeno se i loro ruoli dispongono di ambiti che altrimenti includerebbero gli oggetti. Gli ambiti esclusivi sostituiscono qualsiasi altro ambito normale e non esclusivo. Questo comportamento è simile al funzionamento di una voce di controllo di accesso (ACE, access control entry) di negazione in un elenco di controllo di accesso (ACL, access control list) di Active Directory.

Un *ambito esclusivo equivalente* fa riferimento a un altro ambito esclusivo che corrisponde ad alcuni degli stessi oggetti di un altro ambito esclusivo. Gli ambiti non devono corrispondere allo stesso insieme completo di oggetti. Entrambi gli ambiti possono modificare solo alcuni o tutti gli oggetti a loro corrispondenti.

## Creazione di ambiti esclusivi

Gli ambiti esclusivi possono essere creati come qualsiasi altro ambito esplicito. È possibile specificare un ambito relativo generato in precedenza, un filtro destinatari, database o server oppure un elenco di database o di server. A differenza degli ambiti normali, che non hanno effetto finché non si associa un ambito a un'assegnazione del ruolo di gestione, l'aspetto di negazione di un ambito esclusivo ha effetto immediato. In pratica, non appena viene creato un ambito esclusivo, gli oggetti contenuti in tale ambito non sono più accessibili a qualsiasi utente, fino alla creazione dell'assegnazione di ruolo.

Una volta creata l'assegnazione, l'ambito esclusivo concede l'accesso agli utenti a cui sono assegnati il ruolo di gestione e l'ambito. Se un altro ambito esclusivo equivalente corrisponde agli stessi oggetti, l'assegnazione di ruolo associata a tale ambito esclusivo è tuttora in grado di accedere agli oggetti.

Per ulteriori informazioni sui filtri dell'ambito di gestione, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).


> [!IMPORTANT]
> È opportuno tenere conto dei tempi di replica di Active Directory quando si apportano modifiche ai componenti di un ruolo di gestione, compresi gli ambiti esclusivi.



Se alcuni oggetti sono contenuti in più ambiti esclusivi, per ottenere l'accesso a tali oggetti è sufficiente l'assegnazione a uno di tali ambiti esclusivi. Per ulteriori informazioni, vedere Exclusive and regular scope interaction più avanti in questo argomento.

Gli ambiti esclusivi controllano solo l'ambito di scrittura esplicito della configurazione o del destinatario di un'assegnazione di ruolo. L'ambito di lettura implicito della configurazione o del destinatario relativo al ruolo assegnato a un utente o a un gruppo è tuttora valido. Tutto questo significa che:

  - Gli utenti assegnati a un ruolo continuano a vedere gli oggetti corrispondenti all'ambito di lettura implicito del ruolo.

  - Gli utenti assegnati ad altri ruoli potrebbero vedere gli oggetti contenuti in un ambito esclusivo, se gli ambiti di lettura degli altri ruoli comprendono gli oggetti. Tuttavia, gli oggetti possono essere modificati solo dagli utenti a cui è assegnato un ruolo associato all'ambito esclusivo.

Gli ambiti esclusivi possono essere utilizzati esclusivamente con ruoli di amministrazione o specialista; non possono essere utilizzati con i ruoli degli utenti finali. Per ulteriori informazioni sui ruoli, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

## Interazione in ambito esclusivo e regolare

La figura alla fine della sezione mostra l'interazione degli ambiti esclusivi tra loro e con gli ambiti regolari. A tutti gli utenti nella figura sono associati i seguenti attributi.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>City</th>
<th>Title</th>
<th>Department</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>Vancouver</p></td>
<td><p>Accountant</p></td>
<td><p>Accounting</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>Vancouver</p></td>
<td><p>Writer</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>Vancouver</p></td>
<td><p>Manager</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>Vancouver</p></td>
<td><p>CEO</p></td>
<td><p>Board</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>Vancouver</p></td>
<td><p>President</p></td>
<td><p>Board</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>Vancouver</p></td>
<td><p>CFO</p></td>
<td><p>Dirigenti</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>Vancouver</p></td>
<td><p>CIO</p></td>
<td><p>Dirigenti</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice President, Operations</p></td>
<td><p>Dirigenti</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice President, Technology</p></td>
<td><p>Dirigenti</p></td>
</tr>
</tbody>
</table>


Le tre assegnazioni di ruoli di gestione nella figura consentono di gestire gli utenti nella tabella precedente. Ciascuno dispone di un ambito associato, alcuni dei quali sono ambiti esclusivi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Assegnazione di ruolo</th>
<th>Filtro di ambito</th>
<th>Esclusivo o regolare</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Recipient Administrators</p></td>
<td><p>City = Vancouver</p></td>
<td><p>Regolare</p></td>
</tr>
<tr class="even">
<td><p>VIP Administrators</p></td>
<td><p>Title = CEO o CFO o CIO o President</p></td>
<td><p>Esclusivo</p></td>
</tr>
<tr class="odd">
<td><p>Executive Administrators</p></td>
<td><p>Department = Executives</p></td>
<td><p>Esclusivo</p></td>
</tr>
</tbody>
</table>


L'assegnazione di ruolo Recipient Administrators dispone di un ambito che corrisponde a tutti gli utenti, dal momento che ogni utente si trova a Vancouver. Senza alcun ambito esclusivo, l'assegnazione di ruolo Recipient Administrators potrebbe gestire tutti questi utenti. Tuttavia, questa organizzazione ha creato due ambiti esclusivi: VIP Administrators ed Executive Administrators. Questi ambiti esclusivi limitano la possibilità di gestire gli utenti corrispondenti ai rispettivi filtri di ambito. L'assegnazione di ruolo VIP Administrators dispone di un filtro di ambito che corrisponde a qualsiasi utente il cui titolo è CEO, CFO, CIO o President. L'assegnazione di ruolo Executive Administrators dispone di un filtro di ambito che corrisponde a qualsiasi utente appartenente al reparto Executives.

Una volta valutati gli ambiti regolari ed esclusivi, il risultato è il seguente:

  - L'assegnazione di ruolo Recipient Administrators è in grado di gestire gli utenti Terry, David e Walter. Questa assegnazione di ruolo non può gestire gli altri utenti, in quanto corrispondono ai filtri di ambiti esclusivi delle assegnazioni di ruolo VIP Administrators ed Executive Administrators.

  - L'assegnazione di ruolo VIP Administrators è in grado di gestire gli utenti Bob, Christine, Fred e Martin. Ciò si verifica perché il filtro dell'ambito esclusivo associato a questa assegnazione del ruolo corrisponde agli attributi su questi oggetti. Questa assegnazione di ruolo non è in grado di gestire gli utenti Kim e Jennifer, perché i loro attributi non corrispondono a questo ambito esclusivo.

  - L'assegnazione di ruolo Executive Administrators è in grado di gestire gli utenti Kim, Jennifer, Fred e Martin. Ciò si verifica perché il filtro dell'ambito esclusivo associato a questa assegnazione del ruolo corrisponde agli attributi su questi oggetti. Questa assegnazione di ruolo non è in grado di gestire gli utenti Bob e Christine, perché i loro attributi non corrispondono a questo ambito esclusivo.

Fred e Martin sono accessibili da entrambi gli ambiti esclusivi. Questo avviene perché gli attributi di tali utenti corrispondono ai filtri di entrambi gli ambiti esclusivi.

**Interazione tra ambiti esclusivi e ambiti regolari**

![Interazione in ambito esclusivo e regolare](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "Interazione in ambito esclusivo e regolare")

Per ulteriori informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

