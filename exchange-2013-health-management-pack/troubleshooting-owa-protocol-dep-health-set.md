---
title: Risoluzione dei problemi di OWA. Set di integrità Protocol.Dep
TOCTitle: Risoluzione dei problemi di OWA. Set di integrità Protocol.Dep
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54652934
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di OWA. Set di integrità Protocol.Dep

 

_**Si applica a:**Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Set di integrità **OWA.Protocol.DEP** esegue il monitoraggio dell'integrità globale di messaggistica immediata (IM) servizi in Outlook Web App integrata tra Lync 2013 e Exchange 2013. Per ulteriori informazioni sull'abilitazione di messaggistica immediata in Outlook Web App, vedere [integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

Se si riceve un avviso che indica che il set di integrità **OWA.Protocol.DEP** è integro, ciò indica un problema che potrebbe impedire la messaggistica immediata funzioni correttamente in Outlook Web App.

## Descrizione

Il servizio **OWA.Protocol.DEP** viene monitorato utilizzando i seguenti probe e monitor.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>Set di integrità</th>
<th>Controlli associati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio di ripristino dopo che lo ha emesso l'avviso. Pertanto, quando si riceve un avviso che indica che il set di integrità **OWA.Protocol.DEP** non è integro, innanzitutto verificare che il problema persiste. Se il problema esiste, eseguire le azioni di ripristino appropriata descritte nelle sezioni seguenti.

## Azioni di ripristino per errore: "InstantMessageOCSProvider.InitializeEndpointManager. Nessuna impostazione del Registro di sistema per Provider di messaggistica Immediata."

Questo errore indica che una chiave del Registro di sistema necessaria è manca sul server cassette postali. Questa chiave del Registro di sistema dovrebbe essere stata configurata durante l'installazione di Microsoft Unified Communications Managed API (UCMA) 4.0 nel server. La chiave del Registro di sistema mancanti è:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

Questa chiave deve contenere una stringa **ImplementationDLLPath** che punta a `Microsoft.Rtc.Internal.Ucweb` DLL. La posizione predefinita è `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`.

Per risolvere questo problema, reinstallare UCMA 4.0 o creare manualmente la chiave del Registro di sistema. È possibile scaricare UCMA 4.0 qui: [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990).

## Azioni di ripristino per errore: "InstantMessageOCSProvider.InitializeEndpointManager. Provider di messaggistica Immediata non trovata."

Questo errore indica che il file DLL `Microsoft.Rtc.Internal.Ucweb` non è presente sul server cassette postali. Questo file dovrebbe essere installato durante l'installazione di UCMA 4.0 nel server. Il percorso predefinito è `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`.

Per risolvere questo problema, reinstallare UCMA 4.0. Per ulteriori informazioni, vedere [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990).

## Azioni di ripristino per errore: "nome del Server di messaggistica immediata è impostato su null o vuoto nel file Web. config."

Questo errore indica che il server Lync 2013 non è definito nel file di configurazione (config) Outlook Web App applicazione sul server cassette postali. Il file `web.config` si trova in `%ExchangeInstallPath%ClientAccess\Owa`e deve contenere una chiave denominata **IMServerName** che specifica il nome di dominio COMPLETO del server Lync 2013. Per risolvere questo problema, eseguire la procedura seguente:

1.  In una finestra del prompt dei comandi aprire il file Web. config Outlook Web App nel blocco note eseguendo il comando seguente:
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Cerca una chiave denominata **IMServerName**. Se viene trovato, verificare il nome di dominio COMPLETO del server Lync 2013. Se la chiave non viene trovata, aggiungerlo eseguendo la procedura seguente.
    
    1.  Trovare il tag denominato **\<appSettings\>**.
    
    2.  Nel nodo **\<appSettings\>** , aggiungere la riga seguente:
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        Ad esempio:
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  Per applicare le modifiche di Outlook Web App, eseguire il comando seguente:
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Azioni di ripristino per errore: "Identificazione personale del certificato di messaggistica immediata è null o vuoto nel file Web. config".

Questo errore indica il certificato che consente di integrare Lync 2013 e Outlook Web App non è definito nel file di configurazione (config) Outlook Web App applicazione nel server cassette postali. Questo file `web.config` si trova in `%ExchangeInstallPath%ClientAccess\Owa`e deve contenere una chiave denominata **IMCertificateThumbprint** che specifica l'identificazione personale del certificato (hash).

È possibile ottenere il valore di identificazione personale del certificato utilizzando il cmdlet **Get-ExchangeCertificate** o nell'interfaccia di amministrazione di Exchange (EAC) a **server** \> **certificati**.

Per risolvere questo problema, eseguire la procedura seguente:

1.  In una finestra del prompt dei comandi aprire il file Web. config Outlook Web App nel blocco note eseguendo il comando seguente:
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Cerca una chiave denominata **IMCertificateThumbprint**. Se viene trovato, verificare che il valore di identificazione personale sia corretto. Se la chiave non viene trovata, aggiungerlo eseguendo le operazioni seguenti:
    
    1.  Trovare il tag denominato **\<appSection\>**.
    
    2.  Nel nodo **\<appSection\>** , aggiungere la riga seguente:
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        Ad esempio:
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  Per applicare le modifiche di Outlook Web App, eseguire il comando seguente:
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Azioni di ripristino per errore: "Impossibile trovare il certificato di messaggistica Immediata con identificazione personale \< valore \>".

Questo errore indica il certificato che consente di integrare Lync 2013 e Outlook Web App non viene trovato sul server cassette postali. Questo certificato deve essere installato nel server cassette postali e il server Lync 2013 e deve essere considerato attendibile da entrambi i server. Per ulteriori informazioni sui requisiti dei certificati, vedere l'abilitazione della messaggistica istantanea nella sezione Outlook Web App in [integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

È possibile associare il valore di identificazione personale nel messaggio di errore per il certificato utilizzando il cmdlet **Get-ExchangeCertificate** o nell'interfaccia di amministrazione di Exchange (EAC) nei **server** \> **certificati**.

## Azioni di ripristino per errore: "Messaggistica Immediata certificato è scaduto".

Questo errore indica la scadenza del certificato che consente di integrare Lync 2013 e Outlook Web App. Per risolvere questo errore, devi rinnovare il certificato.

È possibile associare il valore di identificazione personale nel messaggio di errore per il certificato utilizzando il cmdlet **Get-ExchangeCertificate** o nell'interfaccia di amministrazione di Exchange (EAC) al **server** \> **certificati**.

## Azioni di ripristino per errore: "Il certificato di messaggistica Immediata non è diventato valido ancora."

Questo errore indica il certificato che consente di integrare Lync 2013Outlook Web App è date non valide. Per risolvere questo errore, è necessario configurare un nuovo certificato e si desidera aggiungere il nuovo valore di identificazione personale nella chiave **IMCertificateThumbprint**`%ExchangeInstallPath%ClientAccess\Owa\web.config` . Per ulteriori informazioni sui requisiti dei certificati, vedere l'abilitazione della messaggistica istantanea nella sezione Outlook Web App in [integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

## Azioni di ripristino per errore: "Il certificato di messaggistica Immediata non possiede una chiave privata."

Questo errore indica il certificato che consente di integrare Lync 2013 e Outlook Web App non dispone di una chiave privata. Per risolvere questo errore, si desidera configurare un nuovo certificato con una chiave privata e si desidera aggiungere il nuovo valore di identificazione personale nella chiave **IMCertificateThumbprint**`%ExchangeInstallPath%ClientAccess\Owa\web.config` . Per ulteriori informazioni sui requisiti dei certificati, vedere l'abilitazione della messaggistica istantanea nella sezione Outlook Web App in [integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

