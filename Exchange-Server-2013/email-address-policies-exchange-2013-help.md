---
title: 'Criteri degli indirizzi di posta elettronica: Exchange 2013 Help'
TOCTitle: Criteri degli indirizzi di posta elettronica
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50481488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri degli indirizzi di posta elettronica

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-07-21_

I destinatari (inclusi utenti, risorse, contatti e gruppi) sono costituiti da qualsiasi oggetto abilitati alla posta elettronica in Active Directory a cui Microsoft Exchange possa recapitare o instradare messaggi tramite. Affinché possa inviare o ricevere messaggi di posta elettronica, è necessario che il destinatario disponga di un indirizzo di posta elettronica. I criteri degli indirizzi di posta elettronica consentono di creare gli indirizzi di posta elettronica primario e secondario per i destinatari in modo che siano in grado di inviare e ricevere messaggi di posta elettronica.

Per impostazione predefinita, in Exchange è presente un criterio degli indirizzi di posta elettronica per ogni utente abilitato alla posta. Questo criterio predefinito specifica l'alias del destinatario come parte locale dell'indirizzo di posta elettronica e utilizza il dominio predefinito accettato. La parte locale di un indirizzo di posta elettronica è il nome che viene visualizzato prima del simbolo (@). Tuttavia è possibile modificare la modalità di visualizzazione degli indirizzi di posta elettronica dei destinatari. Ad esempio, è possibile specificare che gli indirizzi vengano visualizzati come *nome*.*cognome*@contoso.com.

Inoltre, se si desidera specificare ulteriori indirizzi di posta elettronica per tutti i destinatari o soltanto per un sottoinsieme, è possibile modificare il criterio predefinito o creare criteri aggiuntivi. Ad esempio, la cassetta postale dell'utente David Hamilton può ricevere i messaggi di posta elettronica indirizzati a hdavid@mail.contoso.com e hamilton.david@mail.contoso.com.

Per informazioni sulle attività di gestione relative ai criteri degli indirizzi di posta elettronica, vedere [Procedure relative al criterio indirizzo posta elettronica](email-address-policy-procedures-exchange-2013-help.md).

## Comportamenti dei criteri destinatari

Exchange applica un criterio a tutti i destinatari che corrispondono ai criteri di filtro destinatario:

  - Criteri relativi ai destinatari vengono applicate in ordine dalla priorità più alta a priorità più bassa. In caso di conflitto tra due o più criteri, verrà applicato il criterio con la priorità più alta. Il criterio del destinatario è sempre ha la priorità più bassa e verrà applicata se altri criteri non sono soddisfatte.
    
    Quando si crea un criterio destinatario ma non viene specificato in modo esplicito una priorità, verrà aggiunto come la priorità più alta. Se si specifica una priorità già associato a un criterio esistente, il criterio esistente e tutti i criteri con una priorità più bassa verranno spostati verso il basso da uno. Il nuovo criterio verrà inserito la priorità specificata.
    
    La funzione dei criteri destinatari si divide in due funzionalità: criteri degli indirizzi di posta elettronica e domini accettati. Per ulteriori informazioni sui domini accettati, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

  - Quando si esegue il cmdlet **Update-EmailAddressPolicy** in Exchange Management Shell, l'oggetto destinatario viene aggiornato con il criterio degli indirizzi di posta elettronica.

  - Ogni volta che un oggetto destinatario viene modificato e salvato, Exchange impone la corretta applicazione dei criteri e delle impostazioni di indirizzo di posta elettronica. Quando un indirizzo di posta elettronica viene modificato e salvato, con la modifica vengono aggiornati tutti i destinatari associati. Inoltre, se un oggetto destinatario viene modificato, viene rivalutato e applicato il criterio degli indirizzi di posta elettronica di tale destinatario.

## Creazione dei criteri degli indirizzi di posta elettronica

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

