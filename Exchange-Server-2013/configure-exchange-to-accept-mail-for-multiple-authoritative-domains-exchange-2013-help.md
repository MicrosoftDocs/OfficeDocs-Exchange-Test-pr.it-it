---
title: 'Config. Exchange affinché accetti posta più dom. autorevoli:Exchange 2013 Help'
TOCTitle: Configurare Exchange affinché accetti posta per più domini autorevoli
ms:assetid: 11801f73-4934-4025-a1c1-3935dada7e9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996314(v=EXCHG.150)
ms:contentKeyID: 51407338
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare Exchange affinché accetti posta per più domini autorevoli

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-06-15_

In Microsoft Exchange Server 2013, è semplice aggiungere più domini attendibili all'organizzazione. Tuttavia, dopo aver aggiunto il dominio attendibile, è necessario decidere come utilizzare il dominio attendibile nell'organizzazione. Esempio:

  - Se si desidera aggiungere un indirizzo di posta elettronica nel nuovo dominio attendibile per destinatari all'interno dell'organizzazione, si desidera sostituire l'indirizzo principale esistente (di risposta) dei destinatari o aggiungere il nuovo di indirizzo di posta elettronica come indirizzo proxy (secondario)?

  - Si desidera che l'indirizzo di posta elettronica nel nuovo dominio attendibile si applichi a tutti i destinatari e a tutti i tipi di destinatario? Oppure si desidera che il nuovo indirizzo di posta elettronica venga applicato a tipi di destinatari specifici o a specifici destinatari in base alle proprietà utente, ad esempio, solo utenti dell'ufficio amministrazione?

Nei seguenti esempi vengono descritti scenari in cui è possibile che l'organizzazione di Exchange debba ricevere ed elaborare messaggi di posta elettronica per più domini SMTP attendibili:

  - Si modifica il nome del dominio SMTP, ma per un certo periodo di tempo è necessario continuare ad accettare messaggi di posta elettronica per il nome del dominio precedente, nel caso in cui i clienti inviino messaggi di posta elettronica agli indirizzi precedenti. È possibile impostare il nuovo indirizzo di posta elettronica come indirizzo (di risposta) primario. In questo modo il nuovo indirizzo sarà l'indirizzo di posta elettronica predefinito visualizzato su tutti i messaggi di posta elettronica inviati dal destinatario. È possibile impostare l'indirizzo di posta elettronica precedente come indirizzo secondario. In questo modo, il destinatario può continuare a ricevere i messaggi di posta elettronica inviati all'indirizzo di posta elettronica precedente.

  - Si desidera predisporre indirizzi di posta elettronica diversi per unità aziendali all'interno dell'organizzazione. Ad esempio, se la foresta Active Directory contoso.com contiene sottodomini per le filiali Tailspin Toys e Fourth Coffee, è possibile assegnare i nomi di dominio SMTP contoso.com, tailspintoys.com e fourthcoffee.com ai destinatari delle relative unità aziendali.

  - Si forniscono servizi di hosting della posta elettronica ed è necessario accettare messaggi di posta elettronica per più di un nome di dominio SMTP.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 30 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Domini accettati" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md) e "Criteri degli indirizzi di posta elettronica" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Se si dispone di un server Trasporto Edge nella propria rete perimetrale, è necessario configurare i domini accettati su un server di cassette postali dell'organizzazione di Exchange. La configurazione dei domini accettati viene replicata nel server Trasporto Edge durante la sincronizzazione EdgeSync. Per ulteriori informazioni, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

  - Quando si crea un dominio accettato, è possibile utilizzare un carattere jolly (\*) nello spazio degli indirizzi per indicare che l'organizzazione di Exchange accetta anche tutti i sottodomini dello spazio degli indirizzi SMTP. Ad esempio, per configurare contoso.com e tutti i relativi sottodomini come domini accettati, immettere **\*.contoso.com** come spazio indirizzo SMTP. Se, tuttavia, i nomi dei sottodomini vengono utilizzati in un criterio degli indirizzi di posta elettronica, è necessario che ciascun sottodominio abbia una voce esplicita di dominio accettato.

  - È necessario un record MX del DNS pubblico per ciascun dominio SMTP per il quale si accettano messaggi di posta elettronica da Internet. Ciascun record MX deve risolvere il server con accesso a Internet che riceve messaggi di posta elettronica per l'organizzazione.

  - È necessario configurare connettori di invio e ricezione affinché l'organizzazione di Exchange possa inviare messaggi di posta elettronica a e riceverli da Internet. La configurazione dei connettori di invio e dei connettori di ricezione da Internet è determinata dalla topologia di Exchange. Per ulteriori informazioni sulla configurazione dei connettori, vedere [Connettori](connectors-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Creare un dominio attendibile

## Utilizzare l'interfaccia di amministrazione di Exchange per creare un dominio attendibile

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Domini accettati**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nel campo **Nome** immettere il nome visualizzato per il dominio accettato. Ogni dominio accettato per l'organizzazione deve disporre di un nome visualizzato univoco. Quest'ultimo potrebbe non coincidere con il nome del dominio accettato. Ad esempio, il nome visualizzato del dominio Contoso.com potrebbe essere Dominio accettato locale Contoso.

3.  Nel campo **Dominio accettato**, specificare uno spazio dei nomi SMTP per il quale l'organizzazione accetta i messaggi di posta elettronica. Ad esempio, contoso.com.

4.  Selezionare **Dominio attendibile**.

5.  Fare clic su **Salva**.

## Utilizzare Shell per creare un dominio attendibile

Per creare un nuovo dominio attendibile, utilizzare la seguente sintassi.

    New-AcceptedDomain -Name "<Unique Name>" -DomainName <SMTP domain> -DomainType Authoritative

Ad esempio, per creare un nuovo dominio attendibile denominato "Fourth Coffee secondario" per il dominio fourthcoffee.com, eseguire il seguente comando:

    New-AcceptedDomain -Name "Fourth Coffee subsidiary" -DomainName fourthcoffee.com -DomainType Authoritative

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che la creazione di un dominio attendibile sia stata eseguita correttamente, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Domini accettati**. Verificare che il dominio accettato creato venga visualizzato e che il valore **Tipo di dominio** sia **Attendibile**.

  - In Shell, eseguire il comando **Get-AcceptedDomain**. Verificare che il dominio accettato creato venga visualizzato e che il valore **DomainType** sia `Authoritative`.

## Passaggio 2: Configurare un criterio di indirizzo di posta elettronica per il dominio attendibile

Per utilizzare il dominio accettato attendibile creato, è necessario configurare un criterio di indirizzo di posta elettronica per il dominio attendibile che soddisfi gli obiettivi del proprio scenario. Ad esempio, potrebbe essere necessario creare un nuovo criterio di indirizzo di posta elettronica o modificarne uno esistente. Si può scegliere di sostituire l'indirizzo di posta elettronica principale per alcuni o per tutti i destinatari e si può scegliere di conservare o rimuovere l'indirizzo di posta elettronica principale precedente. In questa sezione vengono presentati due scenari di esempio.

## Modificare l'indirizzo di posta elettronica principale esistente

Per modificare l'indirizzo di posta elettronica (di risposta) primario assegnato ai destinatari e mantenere l'indirizzo di posta elettronica principale precedente come indirizzo proxy (secondario), eseguire la procedura riportata di seguito:

## Utilizzare EAC per modificare l'indirizzo di posta elettronica principale esistente

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Criteri dell'indirizzo di posta elettronica**. Selezionare il criterio dell'indirizzo di posta elettronica da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Criterio degli indirizzi di posta elettronica**, fare clic sulla scheda **Formato dell'indirizzo di posta elettronica**. Nella sezione **Formato dell'indirizzo di posta elettronica**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Formato dell'indirizzo di posta elettronica** che viene visualizzata, impostare le seguenti opzioni:
    
      - **Selezionare un dominio accettato**   Fare clic sull'elenco a discesa e selezionare il nuovo dominio attendibile.
    
      - Selezionare **Imposta questo formato come indirizzo di risposta**.
    
    Al termine, fare clic su **Salva**.

4.  Nella pagina **Criterio degli indirizzi di posta elettronica**, fare clic su **Salva** per salvare le modifiche al criterio.

5.  L'utente riceverà un messaggio di avviso con la comunicazione che il criterio dell'indirizzo di posta elettronica non verrà applicato fino all'aggiornamento. Una volta creato, selezionarlo e fare clic su **Applica** nel riquadro dei dettagli.

## Utilizzare Shell per modificare l'indirizzo di posta elettronica principale esistente

In Shell, utilizzare due comandi separati: un comando per modificare il criterio dell'indirizzo di posta elettronica esistente e un altro comando per applicare il criterio aggiornato ai destinatari dell'organizzazione.

Per modificare l'indirizzo di posta elettronica principale esistente e trasformare quello precedente in un indirizzo proxy, eseguire il seguente comando:

    Set-EmailAddressPolicy <EmailAddressPolicyIdentity> -EnabledEmailAddressTemplates SMTP:<NewPrimaryEmailAddress>,smtp:<OldPrimaryEmailAddress>

Ad esempio, supponiamo che il criterio dell'indirizzo di posta elettronica nell'organizzazione utilizzi il formato di indirizzo di posta elettronica *useralias*`@contoso.com`. In questo esempio viene cambiato il dominio dell'indirizzo principale (di risposta) nel criterio dell'indirizzo di posta elettronica denominato "Criterio predefinito" in `@fourthcoffee.com` e viene conservato l'indirizzo di risposta principale nel dominio `@contoso.com` come indirizzo proxy (secondario).

    Set-EmailAddressPolicy "Default Policy" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com,smtp:@contoso.com


> [!NOTE]
> Il qualificatore <CODE>SMTP</CODE> in lettere maiuscole specifica l'indirizzo principale (di risposta). Il qualificatore <CODE>smtp</CODE> in lettere minuscole specifica un indirizzo proxy (secondario).



Per applicare il criterio dell'indirizzo di posta elettronica aggiornato ai destinatari, utilizzare la seguente sintassi.

    Update-EmailAddressPolicy <EamilAddressPolicyIdentity>

Ad esempio, per aggiornare un criterio dell'indirizzo di posta elettronica denominato "Criterio predefinito", eseguire il comando riportato di seguito:

    Update-EmailAddressPolicy "Default Policy"

## Sostituire l'indirizzo di posta elettronica principale esistente per un set di destinatari filtrato

Non è possibile modificare il criterio dell'indirizzo di posta elettronica predefinito da applicare a un set di destinatari filtrato. È necessario creare un nuovo criterio dell'indirizzo di posta elettronica o modificarne uno esistente personalizzato. Nell'esempio in questa sezione creare un nuovo criterio dell'indirizzo di posta elettronica. In questi esempi, l'indirizzo principale (di risposta) nel nuovo dominio accettato sostituisce l'indirizzo principale precedente per i destinatari specificati senza conservare l'indirizzo principale precedente come indirizzo di posta elettronica proxy (secondario). Pertanto, i destinatari interessati non potranno più ricevere posta elettronica al loro precedente indirizzo di posta elettronica principale.

Inoltre, i criteri dell'indirizzo di posta elettronica validi per specifici utenti dovrebbero avere una priorità superiore (indicata da un valore intero inferiore) rispetto ad altri criteri dell'indirizzo di posta elettronica, compreso il criterio predefinito, in modo che il criterio specifico venga applicato per primo. Poiché due criteri non possono avere lo stesso valore di priorità, potrebbe essere necessario abbassare il valore della priorità del criterio predefinito dell'indirizzo di posta elettronica dell'organizzazione.

## Utilizzare l'interfaccia di amministrazione di Exchange per sostituire l'indirizzo di posta elettronica principale esistente per un set di destinatari filtrato

Per creare indirizzi di posta elettronica aggiuntivi da utilizzare come indirizzi di posta elettronica primari per un gruppo di destinatari filtrato, seguire la procedura riportata di seguito.

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Flusso di posta** \> **Criteri degli indirizzi di posta elettronica**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Criterio degli indirizzi di posta elettronica** completare i seguenti campi:
    
    1.  **Nome criterio**   Immettere un nome descrittivo univoco.
    
    2.  **Formato dell'indirizzo di posta elettronica**   Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella pagina **Formato dell'indirizzo di posta elettronica** che viene visualizzata, impostare le seguenti opzioni:
        
          - **Selezionare un dominio accettato**   Fare clic sull'elenco a discesa e selezionare il nuovo dominio attendibile.
        
          - **Formato dell'indirizzo di posta elettronica**   Selezionare il formato di indirizzo di posta elettronica appropriato per la propria organizzazione.
        
          - Selezionare **Imposta questo formato come indirizzo di risposta**.
        
        Al termine, fare clic su **Salva**.

3.  **Eseguire questo criterio in questa sequenza con altri criteri**   Generalmente, i criteri che valgono per utenti specifici dovrebbero avere una priorità superiore (indicata da un valore intero inferiore) rispetto agli altri criteri degli indirizzi di posta elettronica, compreso il criterio predefinito.

4.  **Specificare i tipi di destinatari ai quali si applica questo indirizzo di posta elettronica**   Selezionare i tipi di destinatari ai quali applicare il criterio dell'indirizzo di posta elettronica.

5.  **Creare regole per definire ulteriormente i destinatari ai quali si applica questo criterio di indirizzo di posta elettronica**   Fare clic su **Aggiungi regola** per limitare i destinatari a cui applicare questo criterio. In questo modo verrà creata un'istruzione booleana **And**. Ripetere questo passaggio tutte le volte necessarie.
    

    > [!WARNING]
    > Se si applicano troppe regole, è possibile limitare il criterio dell'indirizzo di posta elettronica fino a quando non conterrà alcun utente.



6.  Fare clic su **Visualizza un'anteprima dei destinatari a cui si applica il criterio** per visualizzare i destinatari a cui verrà applicato il criterio.

7.  
    
    Fare clic su **Salva** per salvare le modifiche e creare il criterio.

8.  L'utente riceverà un messaggio di avviso con la comunicazione che il criterio dell'indirizzo di posta elettronica non verrà applicato fino all'aggiornamento. Una volta creato, selezionarlo e fare clic su **Applica** nel riquadro dei dettagli.

## Utilizzare Shell per sostituire l'indirizzo di posta elettronica principale esistente per un set di destinatari filtrato

Per sostituire l'indirizzo di posta elettronica principale per un set filtrato di destinatari, utilizzare il seguente comando:

    New-EmailAddressPolicy -Name <Policy Name> -Priority <Integer> -IncludedRecipients <RecipientTypes> <Conditional Recipient Properties> -EnabledEmailAddressTemplates SMTP:@<NewPrimaryEmailAddress>

In questo esempio viene creato un criterio dell'indirizzo di posta elettronica denominato "Destinatari Fourth Coffee", viene assegnato tale criterio agli utenti della cassetta postale nel reparto di Fourth Coffee e impostata la priorità massima per tale criterio in modo che venga applicato per primo. Osservare che l'indirizzo di posta elettronica non viene conservato per questi destinatari, pertanto non potranno ricevere posta al loro indirizzo principale di posta elettronica precedente.

    New-EmailAddressPolicy -Name "Fourth Coffee Recipients" -Priority 1 -IncludedRecipients MailboxUsers -ConditionalDepartment "Fourth Coffee" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com

Per applicare il nuovo criterio indirizzo di posta elettronica ai destinatari interessati, eseguire il seguente comando:

    Update-EmailAddressPolicy "Fourth Coffee Recipients"

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver configurato correttamente un criterio dell'indirizzo di posta elettronica per il dominio attendibile, eseguire una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Flusso di posta** \> **Criteri dell'indirizzo di posta elettronica**. Verificare che i criteri vengano applicati nell'ordine corretto. Inoltre, selezionare qualsiasi criterio nuovo o aggiornato e, nel riquadro dei dettagli, verificare il formato dell'indirizzo di posta elettronica, i destinatari inclusi e se il criterio è stato applicato.

  - In Shell, eseguire i comandi **Get-EmailAddressPolicy** e `Get-EmailAddressPolicy "<Policy Name>"| Format-List` per verificare i dettagli dei criteri.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver configurato Exchange affinché accetti posta per più domini attendibili, eseguire una delle seguenti operazioni:

1.  Inviare messaggi a un destinatario interessato da una cassetta postale esterna all'organizzazione di Exchange. Verificare che gli indirizzi di posta elettronica abbiano accettato la posta.

2.  Inviare messaggi da una cassetta postale di un destinatario interessato a un destinatario esterno e verificare l'indirizzo del mittente del messaggio.

