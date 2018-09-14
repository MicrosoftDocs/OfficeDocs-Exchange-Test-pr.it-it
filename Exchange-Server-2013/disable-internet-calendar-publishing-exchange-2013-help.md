---
title: 'Disabilitare la pubblicazione del calendario Internet: Exchange 2013 Help'
TOCTitle: Disabilitare la pubblicazione del calendario Internet
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50555711
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare la pubblicazione del calendario Internet

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-15_

La modalità di disabilitazione della pubblicazione del calendario Internet dipende dalla modalità di abilitazione. Se è stato creato un criterio di condivisione dedicato nella pubblicazione del calendario Internet, è possibile disabilitare il criterio o eliminarlo. Se è stato configurata la pubblicazione del calendario Internet come regola di condivisione nel criterio di condivisione predefinito, è possibile rimuovere la regola di condivisione per il dominio **anonimo**.

Quando si disabilita la pubblicazione del calendario Internet, gli utenti sottoposti a provisioning per utilizzarlo non saranno in grado di condividere le informazioni del calendario con il dominio Internet **anonimo** specificato nel criterio. Non è tuttavia possibile eliminare o disabilitare un criterio di condivisione dedicato alla pubblicazione del calendario Internet fino a quando per tutti gli utenti sottoposti a provisioning per l'utilizzo del criterio viene rimossa l'impostazione del criterio dalle proprie cassette postali. Per informazioni dettagliate sulle modifiche dell'impostazione del criterio di condivisione per un utente, vedere [Gestire le cassette postali degli utenti](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).


> [!NOTE]
> Se si disabilita o elimina il criterio di condivisione, gli utenti sottoposti a provisioning per l'utilizzo del criterio continuano a condividere le informazioni finché l'Assistente criterio condivisione è in esecuzione. Per specificare la frequenza di esecuzione di Assistente criterio condivisione, utilizzare il cmdlet <A href="https://technet.microsoft.com/it-it/library/aa998651(v=exchg.150)">Set-MailboxServer</A> con il parametro <EM>SharingPolicySchedule</EM>.



Per disabilitare completamente la pubblicazione del calendario Internet, occorre disabilitare anche la directory virtuale di Outlook Web App utilizzata per la pubblicazione. In questo modo viene impedito l'accesso ai collegamenti del calendario pubblicati, condivisi precedentemente dagli utenti dell'organizzazione Exchange con utenti Internet esterni. Questo passaggio viene descritto dettagliatamente più avanti in questo argomento.

Per ulteriori informazioni sulla pubblicazione del calendario Internet e sui criteri di condivisione, vedere [Condivisione](sharing-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: disabilitare o eliminare il criterio di condivisione per la pubblicazione del calendario Internet tramite EAC o Shell

## Utilizzo dell'interfaccia di amministrazione di Exchange

1.  Accedere a **Organizzazione** \> **Condivisione**.

2.  Nella visualizzazione elenco, sotto **Condivisione singola**, eseguire uno dei passaggi seguenti:
    
      - Se è stato creato un criterio di condivisione appositamente per la pubblicazione del calendario Internet, selezionare il criterio, quindi deselezionare la casella di controllo nella colonna **On** per disabilitare il criterio di condivisione oppure fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina") per eliminarlo.
    
      - Se è stata configurata la pubblicazione del calendario Internet come regola di condivisione nel criterio di condivisione predefinito, eseguire i passaggi seguenti:
        
        1.  Selezionare il criterio di condivisione predefinito, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
        
        2.  In **criterio di condivisione** selezionare la regola di condivisione **anonimo**, quindi fare clic su **rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per rimuovere la regola di condivisione.
        
        3.  Fare clic su **Salva**.

## Utilizzo di Shell

Con questo esempio viene disabilitato il criterio di condivisione per la pubblicazione del calendario Internet denominato **Internet**.

    Set-SharingPolicy -Identity "Internet" -Enabled $false

Con questo esempio viene eliminato il criterio di condivisione per la pubblicazione del calendario Internet denominato **Internet**.

    Remove-SharingPolicy -Identity "Internet"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-SharingPolicy](https://technet.microsoft.com/it-it/library/dd297931\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la rimozione o l'aggiornamento corretti del criterio di condivisione, eseguire il comando Shell seguente e controllare le informazioni sul criterio di condivisione.

    Get-SharingPolicy <policy name> | format-list

Se è stato rimosso il criterio di condivisione per la pubblicazione del calendario Internet dedicato, nei risultati del cmdlet non verrà visualizzato il criterio.

Se è stato aggiornato il criterio di condivisione predefinito, verificare che il dominio di `Anonymous` sia stato rimosso dal parametro *Domains*.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-SharingPolicy](https://technet.microsoft.com/it-it/library/dd335081\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Passaggio 2: Disabilitazione delle funzionalità anonimo di una directory virtuale di Outlook Web App tramite Shell


> [!NOTE]
> Non è possibile utilizzare EAC per disabilitare le funzionalità anonimo per la directory virtuale di Outlook Web App.



Con questo esempio vengono disabilitate le funzionalità anonimo per la directory virtuale di Outlook Web App sul server Accesso client CAS01.

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver disabilitato correttamente le funzionalità anonimo per la directory virtuale di Outlook Web App sul server Accesso client, eseguire il comando Shell e verificare che il parametro *AnonymousFeaturesEnabled* sia impostato su `$false`.

    Get-OwaVirtualDirectory | format-list

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/aa998588\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


