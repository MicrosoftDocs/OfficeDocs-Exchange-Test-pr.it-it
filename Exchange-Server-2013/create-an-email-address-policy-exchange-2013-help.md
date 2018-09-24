---
title: 'Creare un criterio indirizzo di posta elettronica: Exchange 2013 Help'
TOCTitle: Creare un criterio indirizzo di posta elettronica
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 50481928
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# Creare un criterio indirizzo di posta elettronica

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-12-10_

Per inviare o ricevere messaggi di posta elettronica, il destinatario deve disporre di un indirizzo di posta elettronica. I criteri degli indirizzi di posta elettronica generano gli indirizzi di posta elettronica principali e secondari per i destinatari, inclusi utenti, contatti e gruppi, in modo che siano in grado di inviare e ricevere posta elettronica.

Per la creazione di un criterio degli indirizzi di posta elettronica è possibile utilizzare i seguenti tipi di indirizzi di posta elettronica:

  - **Indirizzo di posta elettronica SMTP predefinito**. Gli indirizzi di posta elettronica SMTP *predefiniti* sono i tipi di indirizzi utilizzati più comunemente a disposizione dell'utente.

  - **Indirizzo di posta elettronica SMTP personalizzato**. Se non si desidera utilizzare uno degli indirizzi di posta elettronica SMTP predefiniti, è possibile specificare un indirizzo di posta elettronica SMTP personalizzato.
    
    Per creare un indirizzo di posta elettronica SMTP personalizzato, è possibile utilizzare le variabili elencate nella tabella seguente per specificare valori alternativi per la parte locale dell'indirizzo.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variabile</th>
    <th>Valore</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Nome specificato</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Iniziale secondo nome</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Cognome</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Nome visualizzato</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Alias di Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Utilizza le prime <em>x</em> lettere del cognome. Ad esempio, se <em>x</em>=2, vengono utilizzate le prime due lettere del cognome.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Utilizza le prime <em>x</em> lettere del nome specificato. Ad esempio, se <em>x</em>=2, vengono utilizzate le prime due lettere del nome.</p></td>
    </tr>
    </tbody>
    </table>


  - **Indirizzo di posta elettronica non SMTP**. Sono supportati i seguenti tipi di indirizzi di posta elettronica non SMTP:
    
      - EX (DisplayName del prefisso dell'indirizzo proxy per il DN legacy)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - EUM (indirizzo proxy della messaggistica unificata di Exchange)
    

    > [!IMPORTANT]
    > In Exchange tutti gli indirizzi di posta elettronica non SMTP sono considerati indirizzi personalizzati. Exchange non prevede finestre di dialogo o pagine delle proprietà univoche per indirizzi di posta elettronica di tipo X.400, GroupWise o Lotus Notes. Se si aggiunge un indirizzo non SMTP personalizzato, è necessario disporre dei file DLL appropriati. Se non si forniscono i file DLL appropriati, non sarà possibile creare alcun criterio degli indirizzi di posta elettronica personalizzato. Nel Visualizzatore eventi verrà registrato il seguente errore: "L'oggetto descrizione indirizzo di posta elettronica nella directory di Microsoft Exchange per il tipo di indirizzo 'SADF' nei computer 'i386' risulta mancante."



Per istruzioni dettagliate sulla creazione di criteri degli indirizzi di posta elettronica, vedere gli argomenti seguenti:

[Creare un criterio indirizzo di posta elettronica](create-an-email-address-policy-exchange-2013-help.md)

[Creare un criterio indirizzo di posta elettronica utilizzando i filtri destinatari](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri degli indirizzi di posta elettronica" nell'argomento [Indirizzi di posta elettronica e rubriche](email-addresses-and-address-books-exchange-2013-help.md).

  - Prima di poter utilizzare un dominio con indirizzo SMTP in un criterio indirizzo di posta elettronica, è necessario configurare un dominio accettato. Per ulteriori informazioni, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un criterio dell'indirizzo di posta elettronica tramite l'interfaccia di amministrazione di Exchange

1.  Passare a **Flusso di posta** \> **Criteri degli indirizzi di posta elettronica**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  In **Criterio indirizzo di posta elettronica** completare i seguenti campi:
    
      - **Nome criterio**
    
      - **Formato dell'indirizzo di posta elettronica**
    
      - **Specificare i tipi di destinatari a cui verrà applicato questo indirizzo di posta elettronica**

3. Fare clic su **Aggiungi una regola** per limitare ulteriormente i destinatari a cui verrà applicato il criterio. In questo modo verrà creata un'istruzione booleana **And**.
    

    > [!Caution]
    > Se si applicano troppe regole, è possibile limitare il criterio dell'indirizzo di posta elettronica fino a quando non conterrà alcun utente.



4.  Fare clic su **Visualizza un'anteprima dei destinatari a cui si applica il criterio** per visualizzare i destinatari a cui verrà applicato il criterio.

5.  Fare clic su **Salva** per salvare le modifiche e creare il criterio.

6.  L'utente riceverà un messaggio di avviso con la comunicazione che il criterio dell'indirizzo di posta elettronica non verrà applicato fino all'aggiornamento. Una volta creato, selezionarlo e fare clic su **Applica** nel riquadro dei dettagli.

## Creazione di un criterio dell'indirizzo di posta elettronica tramite Shell

In questo esempio viene creato un criterio dell'indirizzo di posta elettronica che include gli utenti di cassette postali che lavorano presso le sedi sudorientali della società i cui indirizzi di posta elettronica sono formati dal cognome seguito dalle prime due lettere del nome.
```powershell
    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-EmailAddressPolicy](https://technet.microsoft.com/it-it/library/aa996800\(v=exchg.150\)).

