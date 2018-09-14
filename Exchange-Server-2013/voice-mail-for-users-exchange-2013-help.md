---
title: 'Segreteria telefonica per gli utenti: Exchange 2013 Help'
TOCTitle: Segreteria telefonica per gli utenti
ms:assetid: 48e1f43b-fb7e-4a52-a2cb-0fb5da6ca65f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997885(v=EXCHG.150)
ms:contentKeyID: 50480521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Segreteria telefonica per gli utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-19_

Con la messaggistica unificata, gli utenti in un'organizzazione di Exchange possono ricevere in un'unica cassetta postale tutti i messaggi vocali e di posta elettronica. La funzionalità di messaggistica unificata e le funzionalità del sistema di caselle vocali aumentano notevolmente la produttività degli utenti e consentono una messaggistica più flessibile all'interno dell'organizzazione.

Quando si aggiunge un utente all'organizzazione, viene data la possibilità di creare una cassetta postale o di connettersi a una cassetta postale esistente. Dopo aver creato la cassetta postale per l'utente o dopo che l'utente si è connesso a una cassetta postale esistente, è possibile abilitare la cassetta postale per la messaggistica unificata in modo che sia possibile utilizzare il sistema di caselle vocali e le funzionalità che vi sono incluse. Una volta abilitato l'utente per la messaggistica unificata, tutti i messaggi di posta elettronica, vocali e fax saranno recapitati nella cassetta postale dell'utente. Utilizzando Microsoft Office Outlook 2007 o versioni successive, Outlook Web App, un telefono cellulare abilitato per Microsoft Exchange ActiveSync oppure un telefono normale o cellulare, gli utenti possono accedere ai messaggi di posta elettronica, ai messaggi vocali, ai contatti personali nonché alle informazioni del calendario.

**Sommario**

Proprietà per l'utente del sistema di caselle vocali

Il rapporto tra un utente del sistema di caselle vocali e gli altri componenti della messaggistica unificata

Extension numbers and SIP addresses

Using the EAC to enable a user for UM and voice mail

Using the Shell to enable a user for UM and voice mail

Disabling UM for a user

## Proprietà per l'utente del sistema di caselle vocali

Un utente deve avere una cassetta postale prima di poter essere abilitato alla messaggistica unificata. Per impostazione predefinita, un utente che dispone di una cassetta postale non è abilitato alla messaggistica unificata. Una volta abilitato, l'utente potrà gestire, modificare e configurare le proprietà relative alla messaggistica unificata e le funzionalità del sistema di caselle vocali. È possibile abilitare un utente per la messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange o Shell. Per ulteriori informazioni, vedere [Consentire a un utente per la segreteria telefonica](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail). Per abilitare più utenti di messaggistica unificata, utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet **Enable-UMMailbox** in Exchange Management Shell.

## Il rapporto tra un utente del sistema di caselle vocali e gli altri componenti della messaggistica unificata

Quando si abilita un utente alla messaggistica unificata, è necessario associare o collegare l'utente a un criterio cassetta postale di messaggistica unificata esistente nonché fornirgli il numero di interno. Per l'associazione di un utente a un criterio cassetta postale di messaggistica unificata è possibile utilizzare il cmdlet **Enable-UMMailbox** in Shell o selezionare il criterio cassetta postale di messaggistica unificata quando si abilita l'utente alla messaggistica unificata. Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, viene creato anche un criterio cassetta postale di messaggistica unificata. È possibile modificare questo criterio o creare un altro criterio e collegarlo al dial plan per determinare quali funzionalità o impostazioni verranno applicate a un utente o gruppo di utenti.

Un criterio cassetta postale di messaggistica unificata contiene le impostazioni, ad esempio le restrizioni di composizione e i criteri PIN per un utente. Quando viene creato un criterio cassetta postale di messaggistica unificata, deve essere associato a un solo dial plan di messaggistica unificata. Qualsiasi server di Exchange possono risposta alle chiamate in arrivo e fornire servizi di posta elettronica per tutti gli utenti abilitati alla messaggistica unificata che sono collegati vocale con il dial plan di messaggistica unificata. Dopo che l'utente è abilitato per la messaggistica unificata, vengono applicate le impostazioni di un criterio cassetta postale di messaggistica unificata per l'utente abilitato alla messaggistica unificata.

## Indirizzi SIP e numeri dell'interno

Quando si abilita un utente alla messaggistica unificata, è necessario definire almeno un numero di interno affinché venga utilizzato dalla messaggistica unificata quando un messaggio vocale viene inviato alla cassetta postale dell'utente. Dopo aver abilitato l'utente alla messaggistica unificata, è possibile aggiungere numeri secondari dell'interno alla cassetta postale dell'utente oppure modificarli o rimuoverli configurando l'indirizzo proxy di messaggistica unificata di Exchange (indirizzo proxy EUM) sulla cassetta postale dell'utente. È possibile rimuovere il numero di interno principale nell'interfaccia di amministrazione di Exchange rimuovendo l'indirizzo proxy EUM, ma si consiglia di non rimuoverlo. La rimozione del numero interno principale impedirà il corretto inoltro delle chiamate alla cassetta postale di un utente.


> [!NOTE]
> Non c'è limite al numero dei numeri di interni secondari che è possibile aggiungere per un utente abilitato alla messaggistica unificata ma può esserci solo un numero di interno principale per utente.



La cassetta postale di un utente abilitato alla messaggistica unificata può essere associata a un unico dial plan di messaggistica unificata. All'utente abilitato alla messaggistica unificata può essere assegnato quanto segue:

  - Un unico numero di interno principale, un indirizzo SIP (Session Initiation Protocol) o un indirizzo E.164 su un unico dial plan.

  - Più numeri di interno secondari, indirizzi SIP o indirizzi E.164 su un unico dial plan.

  - Più numeri di interno principali, indirizzi SIP o indirizzi E.164 su due dial plan separati.


> [!NOTE]
> Ciascun numero di interno, indirizzo SIP e numero E.164 deve essere univoco all'interno di un dial plan e il numero di cifre nel dial plan verrà utilizzato per tutti gli utenti che sono collegati al dial plan.



Ad esempio, un utente abilitato alla messaggistica unificata viaggia spesso da New York a Tokyo. La cassetta postale dell'utente è associata al dial plan di New York e un unico numero di interno è configurato sulla cassetta postale dell'utente. Un secondo numero di interno è configurato sulla cassetta postale dell'utente per il dial plan di Tokyo. Quando i chiamanti compongono uno dei numeri di interno e lasciano un messaggio vocale per l'utente, il messaggio vocale viene recapitato nella stessa cassetta postale abilitata alla messaggistica unificata.

Inizio pagina

## Utilizzo dell'interfaccia di amministrazione di Exchange per abilitare un utente alla messaggistica unificata e al sistema di caselle vocali

Dopo aver creato una cassetta postale di Exchange per l'utente, è possibile configurare le impostazioni della cassetta postale di messaggistica unificata utilizzando **Visualizza dettagli** sotto **Messaggistica unificata** nell'interfaccia di amministrazione di Exchange. Quando si abilita un utente, è necessario configurare diverse impostazioni:

1.  **Indirizzo SIP** Questo è l'indirizzo SIP per l'utente. Questa impostazione sarà visualizzata se l'utente che si sta abilitando per la messaggistica unificata è stato assegnato a un criterio cassetta postale di messaggistica unificata che è collegato a un dial plan impostato su URI SIP. I dial plan impostati su URI SIP vengono utilizzati quando si effettua l'integrazione di Office Communications Server 2007 R2 o Microsoft Lync Server. Quando si assegna l'utente a un criterio cassetta postale di messaggistica unificata collegato a un dial plan E.164 o URI SIP, è ancora necessario immettere l'interno dell'utente. Il numero di interno principale viene utilizzato dall'utente per accedere a Outlook Voice Access.

2.  **Numero dell'interno**   È necessario immettere manualmente il numero dell'interno per l'utente che si sta abilitando per la messaggistica unificata.
    
    È necessario fornire un numero di interno valido per l'utente che contenga lo stesso numero di cifre specificato nel dial plan. È possibile immettere solo caratteri numerici o cifre da 1 a 20. Il numero di interno tipico è lungo da 3 a 7 cifre ed è configurato sul dial plan con cui il criterio cassetta postale di messaggistica unificata è collegato e assegnato all'utente.

3.  **Impostazioni del PIN per l'utente:** 
    
      - **Genera automaticamente PIN**    Questa impostazione genera automaticamente un PIN per l'utente abilitato alla messaggistica unificata da utilizzare per l'accesso al sistema di caselle vocali tramite Outlook Voice Access. Questa impostazione è quella predefinita. Quando si fa clic su questo pulsante, viene generato automaticamente un PIN in base ai criteri del PIN configurati nel criterio cassetta postale di messaggistica unificata associato all'utente. È consigliabile utilizzare questa impostazione per proteggere il PIN dell'utente. Il PIN viene inviato all'utente nel messaggio di benvenuto che riceve quando viene abilitato per la messaggistica unificata. Per impostazione predefinita, dovranno modificare questo PIN la prima volta che accedono alla loro cassetta postale per utilizzare la posta vocale.
    
      - **Digita un PIN**   Questa impostazione consente di specificare manualmente un PIN che l'utente utilizzerà per accedere al sistema di caselle vocali.
        
        Il PIN deve essere conforme alle impostazioni del criterio del PIN configurate nel criterio cassetta postale di messaggistica unificata associato a questo utente abilitato alla messaggistica unificata. Ad esempio, se il criterio cassetta postale di messaggistica unificata è configurato per accettare solo PIN contenenti sette o più cifre, il PIN immesso in questa casella deve contenere almeno sette cifre.
    
      - **Richiedi all'utente di reimpostare il PIN al primo accesso**   Questa impostazione forza l'utente a reimpostare il PIN del sistema di caselle postali quando accede al sistema per la prima volta da un telefono tramite Outlook Voice Access. Verranno invitati a immettere un PIN che è più significativo per loro. Per motivi di sicurezza, è consigliabile richiedere agli utenti abilitati alla messaggistica unificata di modificare il loro PIN al primo accesso per evitare accessi non autorizzati ai loro dati e alla loro cartella Posta in arrivo. Questa casella di controllo è selezionata per impostazione predefinita.

## Utilizzo di Shell per abilitare un utente alla messaggistica unificata e al sistema di caselle vocali

In questo esempio viene abilitata la messaggistica unificata e il sistema di caselle vocali sulla cassetta postale di tonysmith@contoso.com, viene impostato l'interno e manualmente il PIN per l'utente, quindi l'utente viene assegnato a un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

In questo esempio viene abilitata la messaggistica unificata e il sistema di caselle vocali sulla cassetta postale di tonysmith@contoso.com, quindi l'utente viene assegnato a un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy` e viene impostato il numero dell'interno, l'indirizzo SIP e manualmente il PIN per l'utente.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

## Disabilitazione della messaggistica unificata per un utente

Dopo aver disabilitato la messaggistica unificata per un utente, l'account utente potrebbe ancora essere in elenco quando un chiamante effettua una ricerca all'interno di una directory mediante un menu operatore automatico di messaggistica unificata oppure mediante Outlook Voice Access. Il chiamante può essere in grado di individuare un utente nella directory, ma se invece il chiamante cerca di contattare l'utente, verrà visualizzato nuovamente il menu principale della messaggistica unificata. Tale sistema potrebbe risultare fastidioso per i chiamanti. Per impedire ai chiamanti di ricorrere alla ricerca all'interno della directory per contattare un utente disabilitato alla messaggistica unificata collegandolo a un altro sistema di caselle vocali, rimuovere l'utente dalla ricerca nella directory dell'operatore automatico di messaggistica unificata oppure rimuovere l'account dell'utente.

Dopo aver disabilitato un account utente abilitato alla messaggistica unificata, l'utente potrebbe ancora avere accesso alla propria cassetta postale abilitata alla messaggistica unificata mediante Outlook Voice Access o Microsoft Outlook. Questo può verificarsi quando non tutte le modifiche nella directory sono coerenti. Per ridurre il rischio che un utente ottenga l'accesso alla cassetta postale anche se il relativo account è stato disabilitato alla messaggistica unificata, è possibile eseguire manualmente la replica o rimuovere tutte le informazioni di messaggistica unificata dalla cassetta postale dell'utente quando quest'ultimo viene disabilitato alla messaggistica unificata.

