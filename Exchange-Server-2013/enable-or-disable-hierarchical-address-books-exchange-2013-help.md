---
title: 'Abilitare o disabilitare rubriche gerarchiche: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare rubriche gerarchiche
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 50481483
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare rubriche gerarchiche

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile configurare una rubrica gerarchica, una funzionalità disponibile agli utenti finali in Microsoft Outlook 2010 o versioni successive. Con una rubrica gerarchica gli utenti possono cercare i destinatari nella propria organizzazione Exchange utilizzando una gerarchia organizzativa basata sull'anzianità o sulla struttura di gestione. Per ulteriori informazioni sulle rubriche gerarchiche, vedere [Rubriche gerarchiche](hierarchical-address-books-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 ora.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Prima di iniziare, leggere l'argomento [Rubriche gerarchiche](hierarchical-address-books-exchange-2013-help.md). È importante appurare se una rubrica gerarchica è appropriata per la propria organizzazione di Exchange.

  - Comprendere in che modo le unità organizzative (OU, Organization unit), i gruppi, gli utenti e i contatti sono attualmente configurati nell'organizzazione di Exchange.

  - Conoscere i cmdlet e i parametri associati indicati nella tabella seguente, indispensabili per la configurazione di una rubrica gerarchica.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Cmdlet</th>
    <th>Parametro</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/it-it/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/it-it/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/it-it/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/it-it/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione di una rubrica gerarchica tramite Shell


> [!NOTE]
> Sebbene l'abilitazione di una rubrica gerarchica non possa essere eseguita tramite Interfaccia di amministrazione di Exchange, è possibile utilizzare questa funzionalità per gestire l'appartenenza dei gruppi nella gerarchia dell'organizzazione, una volta completata l'abilitazione.



In questo esempio verrà creata una unità organizzativa (OU) denominata HAB per la rubrica gerarchica. Il nome del dominio dell'organizzazione è Contoso-dom e Contoso,Ltd il sarà il nome dell'organizzazione di livello superiore nella gerarchia (l'*organizzazione radice*). Verranno creati gruppi secondari denominati Corporate Office, Product Support Organization e Sales & Marketing Organization come organizzazioni figlio in Contoso,Ltd. Saranno inoltre creati i gruppi Human Resources, Accounting Group e Administration Group come organizzazioni figlio in Corporate Office.

Per informazioni dettagliate sulla creazione dei gruppi di distribuzione, vedere [Creazione e gestione dei gruppi di distribuzione](create-and-manage-distribution-groups-exchange-2013-help.md).

1.  Creazione di un'unità organizzativa denominata HAB nell'organizzazione Contoso. È possibile utilizzare Utenti e computer di Active Directory oppure digitare quanto segue al prompt dei comandi.
    

    > [!NOTE]
    > In alternativa, è possibile utilizzare un'unità organizzativa esistente nella foresta di Exchange.

    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    

    > [!NOTE]
    > Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=198986">creare una nuova unità organizzativa</A>.



2.  Creazione del gruppo di distribuzione principale Contoso,Ltd per la rubrica gerarchica (HAB).
    

    > [!NOTE]
    > Ai fini di questo argomento, viene fornito un esempio con la shell. È tuttavia possibile utilizzare Interfaccia di amministrazione di Exchange per creare un gruppo di distribuzione. Per informazioni dettagliate, vedere <A href="create-and-manage-distribution-groups-exchange-2013-help.md">Creazione e gestione dei gruppi di distribuzione</A>.

    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  Designazione di Contoso,Ltd come organizzazione principale per la rubrica gerarchica (HAB).
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  Creazione di gruppi di distribuzione per altri livelli nella rubrica gerarchica (HAB). In questo esempio vengono creati i gruppi seguenti: Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group e Administration Group. In questo esempio viene creato il gruppo di distribuzione Corporate Office.
    

    > [!NOTE]
    > Ai fini di questo argomento, viene fornito un esempio con la shell. È tuttavia possibile utilizzare Interfaccia di amministrazione di Exchange per creare gruppi di distribuzione. Per ulteriori informazioni, vedere <A href="create-and-manage-distribution-groups-exchange-2013-help.md">Creazione e gestione dei gruppi di distribuzione</A>.

    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  Designazione di ciascun gruppo come membro della rubrica gerarchica (HAB). In questo esempio, come gruppi gerarchici vengono designati i gruppi seguenti: Contoso,Ltd, Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group e Administration Group. In questo esempio il gruppo di distribuzione Contoso,Ltd viene designato come membro della rubrica gerarchica (HAB).
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  Aggiunta di tutti i gruppi subordinati come membri dell'organizzazione principale. In questo esempio i gruppi di distribuzione Corporate Office, Product Support Organization e Sales & Marketing Organization vengono aggiunti come membri dell'organizzazione radice Contoso,Ltd nella rubrica gerarchica (HAB). In questo esempio il gruppo di distribuzione Corporate Office viene aggiunto come membro del gruppo di distribuzione radice Contoso,Ltd.
    

    > [!NOTE]
    > In questo esempio viene utilizzato l'alias dei gruppi di distribuzione.

    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  Aggiunta di ciascun gruppo subordinato al gruppo di distribuzione Corporate Office come membro del gruppo. In questo esempio i gruppi di distribuzione Human Resources, Accounting Group e Administration Group vengono aggiunti come membri del gruppo di distribuzione Corporate Office. In questo esempio il gruppo di distribuzione Human Resources viene aggiunto come membro del gruppo di distribuzione Corporate Office.
    

    > [!NOTE]
    > In questo esempio viene utilizzato l'alias dei gruppi di distribuzione e si presume che l'alias del gruppo di distribuzione Human Resources sia HumanResources.

    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  Aggiunta di utenti ai gruppi nella rubrica gerarchica (HAB). In questo esempio David Hamilton (indirizzo SMTP DHamilton@contoso.com) è un utente esistente in OU Contoso-dom.Contoso.com/Users e verrà aggiunto al gruppo Corporate Office. Ripetere questo passaggio per aggiungere altri utenti a gruppi nella rubrica gerarchica (HAB).
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  Impostazione del parametro *SeniorityIndex* per i gruppi della rubrica gerarchica (HAB). In questo esempio il gruppo Corporate Office contiene tre gruppi figlio: Human Resources, Accounting Group e Administration Group. Anziché elencare i gruppi in ordine alfabetico crescente in base all'impostazione predefinita, l'ordinamento preferenziale sarà Human Resources (*SeniorityIndex* = 100), Accounting Group (*SeniorityIndex* = 50), quindi Administration Group (*SeniorityIndex* = 25). In questo esempio il parametro *SeniorityIndex* per il gruppo Human Resources è impostato su 100.
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    

    > [!NOTE]
    > Il parametro <EM>SeniorityIndex</EM> è un valore numerico utilizzato per l'ordinamento di gruppi o utenti in ordine numerico decrescente nella rubrica gerarchica (HAB). Se il parametro <EM>SeniorityIndex</EM> non è impostato o è lo stesso per due o più utenti, l'ordinamento della rubrica gerarchica (HAB) utilizzerà il parametro <EM>PhoneticDisplayName</EM> per elencare gli utenti in ordine alfabetico crescente. Se il valore <EM>PhoneticDisplayName</EM> non è impostato, l'ordinamento della rubrica gerarchica (HAB) verrà impostato sul parametro predefinito <EM>DisplayName</EM> e gli utenti saranno elencati in ordine alfabetico crescente.



10. Impostazione del parametro *SeniorityIndex* per gli utenti nei gruppi della rubrica gerarchica (HAB). In questo esempio il gruppo Corporate Office include tre utenti: Amy Alberts, David Hamilton e Rajesh M. Patel. Anziché elencare gli utenti in ordine alfabetico crescente per impostazione predefinita, l'ordinamento preferenziale sarà David Hamilton (*SeniorityIndex* = 100), Rajesh M. Patel (*SeniorityIndex* = 50), quindi Amy Alberts (*SeniorityIndex* = 25). In questo esempio il parametro *SeniorityIndex* per l'utente David Hamilton è impostato su 100.
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

Al termine della procedura, la rubrica gerarchica sarà visibile in Outlook. Per visualizzare la rubrica gerarchica, aprire Outlook e scegliere **Rubrica**. La rubrica gerarchica (HAB) viene visualizzata nella scheda **Organizzazione**, in modo simile alla figura seguente.

**Esempio di rubrica gerarchica (HAB) per Contoso,Ltd**

![Finestra di dialogo della rubrica gerarchica](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Finestra di dialogo della rubrica gerarchica")

Una volta abilitata la rubrica gerarchica, è possibile utilizzare Interfaccia di amministrazione di Exchange per gestire l'appartenenza dei gruppi nella gerarchia organizzativa. Per modificare il parametro *SeniorityIndex* per i nuovi utenti o gruppi, è tuttavia necessario utilizzare la shell.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere l'argomento seguente:

  - [New-DistributionGroup](https://technet.microsoft.com/it-it/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/it-it/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/it-it/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/it-it/library/aa998221\(v=exchg.150\))

## Disabilitazione di una rubrica gerarchica tramite Shell

In questo esempio viene disabilitata l'organizzazione principale utilizzata per la rubrica gerarchica (HAB).

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null


> [!NOTE]
> Questo comando non consente di eliminare l'organizzazione radice o i gruppi figlio utilizzati nella struttura della rubrica gerarchica (HAB) o di reimpostare i valori <EM>SeniorityIndex</EM> per gli utenti o i gruppi. Impedisce solo la visualizzazione della rubrica gerarchica in Outlook. Per abilitare la rubrica gerarchica (HAB) con le stesse impostazioni di configurazione, è sufficiente abilitare&nbsp;nuovamente l'organizzazione radice.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).

