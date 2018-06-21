---
title: 'Requisiti dei certificati per le distribuzioni ibride: Exchange 2013 Help'
TOCTitle: Requisiti dei certificati per le distribuzioni ibride
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 50482145
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisiti dei certificati per le distribuzioni ibride

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

In una distribuzione ibrida i certificati digitali costituiscono un aspetto importante per la protezione delle comunicazioni fra l'organizzazione di Exchange locale e Office 365. I certificati consentono a ciascuna organizzazione di Exchange di considerare attendibile l'identità dell'altra. I certificati assicurano inoltre che ciascuna organizzazione di Exchange comunichi con l'origine corretta.

In una distribuzione ibrida sono presenti vari servizi che utilizzano i certificati:

  - **Azure Active Directory Connect (Azure AD Connect) con Active Directory Federation Services (AD FS)**   Se si sceglie di implementare Azure AD Connect con AD FS nell'ambito della distribuzione ibrida, viene utilizzato un certificato emesso da un'autorità di certificazione (CA) attendibile di terze parti per instaurare una relazione di trust tra i client Web e i proxy dei server federativi, con lo scopo di firmare e decrittografare i token di protezione.
    
    Per ulteriori informazioni, vedere [Certificati](http://go.microsoft.com/fwlink/p/?linkid=205993).

  - **Federazione di Exchange**   Viene utilizzato un certificato autofirmato per creare una connessione protetta tra i server locali di Exchange e il sistema di autenticazione di Azure Active Directory.
    
    Per ulteriori informazioni, vedere [Condivisione](https://technet.microsoft.com/it-it/library/dd638083\(v=exchg.150\)).

  - **Servizi di Exchange**   I certificati emessi da Autorità di certificazione di terze parti vengono utilizzati per proteggere le comunicazioni SSL (Secure Sockets Layer) tra i server Exchange e i client. I servizi che utilizzano i certificati includono Outlook sul Web, Exchange ActiveSync, Outlook via Internet e il trasporto sicuro dei messaggi.

  - **Server Exchange esistenti**   I server Exchange possono fare uso di certificati per rafforzare la sicurezza delle comunicazioni Outlook sul Web, il trasporto dei messaggi e così via. A seconda di come vengono utilizzati i certificati nei server Exchange, è possibile utilizzare certificati autofirmati o certificati emessi da un'Autorità di certificazione attendibile di terze parti.

## Requisiti dei certificati per una distribuzione ibrida

Quando si configura una distribuzione ibrida è necessario utilizzare e configurare certificati acquistati da un'autorità di certificazione attendibile di terze parti. Il certificato utilizzato per il trasporto ibrido sicuro della posta deve essere installato in tutti i server Cassette postali (Exchange 2016 e versioni successive) locali e nei server Cassette postali e Accesso client (Exchange 2013 e versioni precedenti).


> [!IMPORTANT]
> Se si sta configurando una distribuzione ibrida in un'organizzazione nella quale i server di Exchange sono distribuiti in più foreste Active Directory, è necessario utilizzare un certificato CA di terze parti per ogni foresta <EM>Active Directory</EM>.




> [!NOTE]
> Quando si implementano i server Trasporto Edge di Exchange nell'organizzazione locale, questo certificato deve essere installato anche in tutti i server Trasporto Edge. Tutti i server di trasporto devono utilizzare un certificato con la stessa CA emittente e lo stesso soggetto, affinché la posta ibrida protetta possa funzionare correttamente.



Se sono presenti più servizi, ad esempio AD FS, federazione Exchange, servizi ed Exchange, è necessario un certificato per ciascuno. In base alle necessità dell'organizzazione si può decidere di fare una delle cose seguenti:

  - Utilizzare un certificato di terze parti che viene utilizzato da tutti i servizi su più server.

  - Utilizzare un certificato di terze parti per ogni server che fornisce servizi.

La scelta di utilizzare lo stesso certificato per tutti i servizi o di utilizzare un certificato dedicato per ciascun servizio dipende dall'organizzazione e dal servizio che si sta implementando. Di seguito vengono riportate alcune considerazioni da tenere presente per ciascuna opzione:

  - **Certificati di terze parti su più server**   I certificati di terze parti utilizzati da servizi su più server possono essere più convenienti da ottenere ma possono complicare le operazioni di rinnovo e sostituzione. Le complicazioni avvengono perchè quando è necessario sostituire un certificato, è necessario effettuare la sostituzione su tutti i server sui quali è stato installato.

  - **Certificati di terze parti per ciascun server**   Utilizzare un certificato dedicato per ciascun server che ospita servizi consente di configurare un certificato specificamente per quel servizio su quel server. Se è necessario sostituire il certificato o rinnovarlo e necessario farlo solo sul server sul quale è installato il servizio. Gli altri server non sono coinvolti.

È consigliabile utilizzare un certificato di terze parti dedicato per ogni server AD FS facoltativo, un altro certificato per i servizi di Exchange per la distribuzione ibrida e, se necessario, un altro certificato nei server Exchange per tutti gli altri servizi o funzionalità necessari. Per il trust federativo locale configurato nell'ambito della condivisione federata in una distribuzione ibrida viene utilizzato un certificato autofirmato per impostazione predefinita. Se non esistono requisiti specifici, non è necessario utilizzare un certificato di terze parti per il trust federativo configurato nell'ambito di una distribuzione ibrida.

I servizi installati su un singolo server possono richiedere di configurare multipli nomi di dominio completi (FQDN) per il server. È consigliabile acquistare un certificato che consente il numero massimo di FQDN richiesto. I certificati sono composti dal nome del soggetto (altrimenti detto nome dell'entità) e da uno o più nomi alternativi del soggetto (SAN). Il nome del soggetto è l'FQDN per cui viene emesso il certificato e deve utilizzare il dominio SMTP primario che viene condiviso fra l'organizzazione locale e l'organizzazione di Exchange Online. I SAN sono ulteriori FQDN che possono essere aggiunti nel certificato al nome del soggetto. Se il certificato deve supportare cinque FQDN, acquistare un certificato che consenta di aggiungere cinque domini: un nome del soggetto e quattro SAN.

La tabella seguente illustra il numero minimo di FQDN che è consigliabile includere nei certificati configurati per l'utilizzo in una distribuzione ibrida.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servizio</th>
<th>FQDN suggeriti</th>
<th>Campo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dominio SMTP condiviso primario</p></td>
<td><p>contoso.com</p></td>
<td><p>Nome soggetto</p></td>
</tr>
<tr class="even">
<td><p>Individuazione automatica</p></td>
<td><p>Etichetta che corrisponde all'FQDN esterno di individuazione automatica del server Accesso client di Exchange 2013, ad esempio autodiscover.contoso.com</p></td>
<td><p>Nome alternativo soggetto</p></td>
</tr>
<tr class="odd">
<td><p>Trasporto</p></td>
<td><p>Etichetta che corrisponde all'FQDN esterno dei server Trasporto Edge, ad esempio mail.contoso.com</p></td>
<td><p>Nome alternativo soggetto</p></td>
</tr>
</tbody>
</table>

