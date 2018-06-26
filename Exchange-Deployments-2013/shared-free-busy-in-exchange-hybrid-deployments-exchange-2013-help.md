---
title: 'Condivisione delle informazioni sulla disponibilità nelle distribuzioni ibride di Exchange: Exchange 2013 Help'
TOCTitle: Condivisione delle informazioni sulla disponibilità nelle distribuzioni ibride di Exchange
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 50482157
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Condivisione delle informazioni sulla disponibilità nelle distribuzioni ibride di Exchange

 

_<strong>Si applica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-04-29_

La condivisione delle informazioni sulla disponibilità (disponibilità di calendario) tra gli utenti locali e nell'organizzazione di Exchange Online è uno dei principali vantaggi offerti da una distribuzione ibrida. Gli utenti in entrambe le organizzazioni possono consultare i calendari gli uni degli altri come se fossero ubicati nella stessa organizzazione fisica. Questo rende la pianificazione delle risorse e delle riunioni, facile ed efficiente.

Per abilitare la funzionalità di condivisione delle informazioni sulla disponibilità tra l'organizzazione di Exchange locale e Exchange Online in una distribuzione ibrida sono necessari diversi componenti.

  - **Trust federativo**   Entrambe le organizzazioni del servizio Office 365 e locali devono avere stabilito una relazione di trust federativa con il sistema di autenticazione Azure AD. Un trust federativo è una relazione uno-a-uno con il sistema di autenticazione Azure AD che definisce i parametri per l'organizzazione Exchange. Il sistema utilizza questi parametri quando funge da mediatore tra l'organizzazione locale e l'organizzazione del servizio Office 365 per lo scambio delle informazioni sulla disponibilità tra gli utenti delle organizzazioni locali e di Exchange Online.
    
    In fase di creazione dell'account viene configurata automaticamente una relazione di trust federativa con il sistema per l'organizzazione del servizio Office 365. La procedura guidata per la configurazione ibrida controlla automaticamente se esiste già una relazione di trust federativa con il sistema di autenticazione Azure AD configurata per l'organizzazione locale. Se presente, la relazione di trust federativa esistente verrà utilizzata per supportare la distribuzione ibrida. Se non è presente, la procedura guidata crea una relazione di trust federativa con il sistema di autenticazione Azure AD configurata per l'organizzazione locale. Vengono inoltre aggiunti alla relazione di trust federativa dell'organizzazione locale tutti i domini selezionati nella procedura guidata per la configurazione ibrida.
    
    Per ulteriori informazioni, vedere [Condivisione](https://technet.microsoft.com/it-it/library/dd638083\(v=exchg.150\)).

  - **Relazioni dell'organizzazione**   Le relazioni dell'organizzazione sono necessarie per entrambe le organizzazioni (locale e di Exchange Online) e vengono configurate automaticamente dalla procedura guidata di configurazione ibrida. Una relazione organizzativa definisce il livello delle informazioni sulla disponibilità condivise tra le organizzazioni.
    
    Per impostazione predefinita, il livello di condivisione dell'accesso alle informazioni sulla disponibilità è **Accesso disponibilità con ora, oggetto e luogo** per entrambe le organizzazioni, locale e di Exchange Online. Per modificare l'accesso in condivisione alle informazioni sulla disponibilità tra gli utenti delle organizzazioni locale e di Exchange Online, è possibile configurare manualmente il livello di accesso alle relazioni dell'organizzazione una volta completata la procedura guidata di configurazione ibrida.
    
    Per ulteriori informazioni, vedere [Condivisione](https://technet.microsoft.com/it-it/library/dd638083\(v=exchg.150\)).

Nella configurazione dell'organizzazione per una distribuzione ibrida, l'accesso alle informazioni sulla disponibilità di calendario condivise viene configurato automaticamente dalla procedura guidata per la configurazione ibrida in tutti gli scenari. La creazione di una relazione di trust federativa con il sistema di autenticazione Azure AD e la configurazione di relazioni dell'organizzazione per le organizzazioni locale e di Exchange Online sono requisiti per la distribuzione ibrida. Se non si desidera consentire la condivisione delle informazioni sulla disponibilità tra gli utenti delle organizzazioni locale e di Exchange Online nella distribuzione ibrida, è possibile disabilitare manualmente tale condivisione utilizzando la Exchange Management Shell e il cmdlet [Set-HybridConfiguration](https://technet.microsoft.com/it-it/library/hh529932\(v=exchg.150\)) una volta completata la procedura guidata per la configurazione ibrida.

Le funzionalità di distribuzione ibrida mostrate nella tabella seguente dipendono dalle relazioni di trust federative e dalle relazioni dell'organizzazione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Area di messaggistica</th>
<th>Funzionalità</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client di posta elettronica</p></td>
<td><ul>
<li><p>Monitoraggio messaggi</p></li>
<li><p>Avviso messaggi</p></li>
<li><p>Ricerca in più cassette postali</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Conformità</p></td>
<td><ul>
<li><p>Archiviazione online di Exchange</p></li>
<li><p>Exchange eDiscovery in locale</p></li>
</ul></td>
</tr>
</tbody>
</table>

