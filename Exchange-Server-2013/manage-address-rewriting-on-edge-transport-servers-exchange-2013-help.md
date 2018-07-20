---
title: 'Gestire la riscrittura degli indirizzi nei server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Gestire la riscrittura degli indirizzi nei server Trasporto Edge
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060526
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire la riscrittura degli indirizzi nei server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Si usa Exchange Management Shell in un server Trasporto Edge per tutte le attività di gestione correlate alla riscrittura degli indirizzi e agli agenti di riscrittura degli indirizzi. Per ulteriori informazioni sulla riscrittura degli indirizzi, vedere [Indirizzo riscrittura su server Trasporto Edge](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

È possibile creare voci di riscrittura degli indirizzi validi per un solo destinatario, per tutti i destinatari in un dominio o sottodominio specifico o a tutti i destinatari in più sottodomini. La riscrittura degli indirizzi può essere solo in uscita o in entrata e in uscita (bidirezionale). Quando si creano voci di riscrittura degli indirizzi, tenere presente quanto segue:

  - Verificare che gli indirizzi di posta elettronica risultanti siano univoci all'interno dell'organizzazione.

  - Nei valori degli indirizzi di posta elettronica sono supportate solo stringhe letterali.

  - Il carattere jolly (\*) è supportato solo nell'indirizzo interno (l'indirizzo da modificare). La sintassi valida per usare il carattere jolly è **\*.contoso.com**. I valori **\*contoso.com** o **sales.\*.com** non sono consentiti.

  - Quando si usa il carattere jolly, è necessario configurare la riscrittura degli indirizzi solo in uscita (è necessario impostare il parametro *OutboundOnly* su `$true`).

  - Quando si configura la riscrittura degli indirizzi solo in uscita (configurando il parametro *OutboundOnly* su `$true`), è necessario configurare indirizzi proxy nei destinatari interessati. In questo modo la posta inviata all'indirizzo riscritto viene recapitata correttamente.

  - Per impostazione predefinita, la riscrittura degli indirizzi è bidirezionale per singoli destinatari o per tutti i destinatari in un dominio o sottodominio specifico (il valore predefinito del parametro *OutboundOnly* è `$false`).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Prestare attenzione quando si configura la riscrittura degli indirizzi. Le modifiche apportate vengono applicate immediatamente quando si esegue il comando. Si consiglia di eseguire il comando con il parametro *WhatIf*. Per ulteriori informazioni sul parametro *WhatIf*, vedere [Opzioni WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione della riscrittura degli indirizzi tramite Shell

Per attivare o disattivare completamente la riscrittura degli indirizzi, è possibile attivare o disattivare gli agenti di riscrittura. Per impostazione predefinita, gli agenti di riscrittura degli indirizzi in un server Trasporto Edge sono abilitati.

Per disabilitare la riscrittura degli indirizzi, eseguire i seguenti comandi:

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

Per attivare la riscrittura degli indirizzi, eseguire i seguenti comandi:

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la riscrittura degli indirizzi sia stata abilitata o disabilitata correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-TransportAgent

2.  Verificare che i valori della proprietà **Attivata** dell'agente di riscrittura degli indirizzi in entrata e in uscita siano i valori configurati.

## Visualizzazione delle voci di riscrittura degli indirizzi tramite Shell

Per visualizzare un elenco riepilogativo di tutte le voci di riscrittura degli indirizzi, eseguire il seguente comando.

    Get-AddressRewriteEntry

Per visualizzare i dettagli di una voce di riscrittura degli indirizzi, utilizzare la seguente sintassi.

    Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List

Il seguente esempio visualizza i dettagli della voce di riscrittura degli indirizzi da Rewrite Contoso.com a Northwindtraders.com:

    Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List

## Creazione delle voci di riscrittura degli indirizzi tramite Shell

## Riscrivere gli indirizzi di posta elettronica di destinatari singoli

Per riscrivere l'indirizzo di posta elettronica di un singolo destinatario, utilizzare la sintassi seguente:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

Nel seguente esempio viene riscritto l'indirizzo di posta elettronica di tutti i messaggi in entrata e in uscita dall'organizzazione di Exchange per il destinatario joe@contoso.com. I messaggi in uscita vengono riscritti in modo che sembrino provenire da support@nortwindtraders.com. I messaggi in entrata inviati a support@northwindtraders.com vengono riscritti in joe@contoso.com per il recapito al destinatario (il parametro *OutboundOnly* é `$false` per impostazione predefinita).

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## Riscrivere gli indirizzi di posta elettronica per destinatari in un solo dominio o sottodominio

Per riscrivere l'indirizzo di posta elettronica di destinatari in un solo dominio o sottodominio, utilizzare la sintassi seguente:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

Nel seguente esempio vengono riscritti gli indirizzi di posta elettronica di tutti i messaggi in entrata e in uscita dall'organizzazione di Exchange per destinatari nel dominio contoso.com. I messaggi in uscita vengono riscritti in modo che sembrino provenire dal dominio fabrikam.com. Gli indirizzi di posta elettronica dei messaggi in entrata inviati a fabrikam.com vengono riscritti come contoso.com per il recapito ai destinatari (il parametro *OutboundOnly* è `$false` per impostazione predefinita).

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

Nel seguente esempio vengono riscritti gli indirizzi di posta elettronica di tutti i messaggi in uscita dall'organizzazione di Exchange inviati dai destinatari nel sottodominio sales.contoso.com. I messaggi in uscita vengono riscritti in modo che sembrino provenire dal dominio contoso.com. Non vengono riscritti i messaggi in entrata inviati agli indirizzi di posta elettronica contoso.com.

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## Riscrivere gli indirizzi di posta elettronica per i destinatari in più sottodomini

Per riscrivere l'indirizzo di posta elettronica di destinatari in un dominio e in tutti i sottodomini, utilizzare la sintassi seguente:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

Nel seguente esempio vengono riscritti gli indirizzi di posta elettronica di tutti i messaggi in uscita dall'organizzazione di Exchange inviati dai destinatari nel dominio contoso.com e in tutti i sottodomini. I messaggi in uscita vengono riscritti in modo che sembrino provenire dal dominio contoso.com. I messaggi in entrata inviati ai destinatari di contoso.com non possono essere riscritti perché nel parametro *InternalAddress* viene usato un carattere jolly.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

L'esempio seguente è identico a quello precedente, tranne che in questo i messaggi inviati dai destinatari nei sottodomini legal.contoso.com e corp.contoso.com non vengono mai riscritti:

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che le voci di riscrittura degli indirizzi siano state create correttamente, procedere come segue:

1.  Eseguire il comando `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` e verificare che le impostazioni visualizzate siano le impostazioni configurate.

2.  Da una cassetta postale interessata da una voce di riscrittura degli indirizzi, inviare un messaggio di prova a una cassetta postale esterna. Verificare che il messaggio appaia come proveniente dall'indirizzo di posta elettronica riscritto.

3.  Rispondere al messaggio di prova dalla cassetta postale esterna. Verificare che la cassetta postale originale riceva il messaggio.

## Modifica delle voci di riscrittura degli indirizzi tramite Shell

Le opzioni di configurazione disponibili quando si modifica una voce di riscrittura degli indirizzi esistente sono identiche alle opzioni di configurazione disponibili quando si crea una nuova voce di riscrittura degli indirizzi.

## Modificare voci di riscrittura degli indirizzi per destinatari singoli

Per modificare una voce di riscrittura degli indirizzi che riscrive l'indirizzo di posta elettronica di un solo destinatario, utilizzare la seguente sintassi:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

Nel seguente esempio vengono modificate le seguenti proprietà della voce di riscrittura del singolo destinatario "joe@contoso.com in support@nortwindtraders.com":

  - l'indirizzo esterno viene modificato in support@northwindtraders.net.

  - Il nome della voce di riscrittura degli indirizzi per "joe@contoso.com viene modificato in support@northwindtraders.net".

  - Il valore di *OutboundOnly* viene modificato in `$true`. Tenere presente che questa modifica richiede la configurazione di support@northwindtraders.net come indirizzo proxy nella cassetta postale di Joe.

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## Modificare le voci di riscrittura degli indirizzi per destinatari in singoli domini o sottodomini

Per modificare una voce di riscrittura degli indirizzi che riscrive l'indirizzo di posta elettronica di destinatari di un solo dominio o sottodominio, utilizzare la seguente sintassi.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

Nel seguente esempio il valore dell'indirizzo interno della voce di riscrittura degli indirizzi del singolo dominio viene modificata da "Northwind Traders a Contoso".

    Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net

## Modificare voci di riscrittura degli indirizzi per destinatari in più sottodomini

Per modificare una voce di riscrittura degli indirizzi che riscrive l'indirizzo di posta elettronica di destinatari in un un dominio e in tutti i sottodomini, utilizzare la seguente sintassi.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

Per sostituire il valore dell'elenco delle eccezioni esistente di una voce di riscrittura degli indirizzi di più sottodomini, utilizzare la seguente sintassi:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

Nel seguente esempio l'elenco di eccezioni esistente per la voce di riscrittura degli indirizzi di più sottodomini Contoso to Northwind Traders viene sostituito con i valori marketing.contoso.com e legal.contoso.com:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

Per aggiungere o rimuovere valori dall'elenco delle eccezioni in modo selettivo dalla voce di riscrittura degli indirizzi di più sottodomini senza modificare i valori dell'elenco delle eccezioni esistente, utilizzare la seguente sintassi:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Nel seguente esempio viene aggiunto finanace.contoso.com e rimosso marketing.contoso.com dall'elenco delle eccezioni della voce di riscrittura degli indirizzi di più sottodomini Contoso to Northwind Traders:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la voce di riscrittura degli indirizzi sia stata modificata correttamente, procedere come segue:

1.  Eseguire il comando `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` e verificare che le impostazioni visualizzate siano le impostazioni configurate.

2.  Da una cassetta postale interessata da una voce di riscrittura degli indirizzi, inviare un messaggio di prova a una cassetta postale esterna. Verificare che il messaggio appaia come proveniente dall'indirizzo di posta elettronica riscritto.

3.  Dalla cassetta postale esterna, rispondere al messaggio di prova. Verificare che la cassetta postale originale riceva il messaggio.

## Rimozione delle voci di riscrittura degli indirizzi tramite Shell

Per rimuovere una voce di riscrittura degli indirizzi, utilizzare la seguente sintassi.

    Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>

Nell'esempio riportato di seguito viene rimossa la voce di riscrittura degli indirizzi "Contoso.com to Northwindtraders.com":

    Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"

Per rimuovere più voci di riscrittura degli indirizzi, utilizzare la seguente sintassi:

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

Nell'esempio riportato di seguito vengono rimosse tutte le voci di riscrittura degli indirizzi:

    Get-AddressRewriteEntry | Remove-AddressRewriteEntry

Il seguente esempio simula la rimozione delle voci di riscrittura degli indirizzi che contengono nel nome il testo "to contoso.com". Lo switch *WhatIf* consente di visualizzare in anteprima il risultato senza apportare modifiche.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

Se si è soddisfatti del risultato, eseguire nuovamente il comando senza lo switch *WhatIf* per rimuovere le voci di riscrittura degli indirizzi.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la voce di riscrittura degli indirizzi sia stata rimossa correttamente, procedere come segue:

1.  Eseguire il comando `Get-AddressRewriteEntry` e verificare che le voci di riscrittura degli indirizzi rimosse non siano elencate.

2.  Da una cassetta postale interessata da una voce di riscrittura degli indirizzi, inviare un messaggio di prova a una cassetta postale esterna. Verificare che il messaggio di prova non sia più interessato dalla voce di riscrittura degli indirizzi rimossa.

3.  Dalla cassetta postale esterna, rispondere al messaggio di prova. Verificare che la cassetta postale originale riceva la risposta e che il messaggio non sia interessato dalla voce di riscrittura degli indirizzi rimossa.

