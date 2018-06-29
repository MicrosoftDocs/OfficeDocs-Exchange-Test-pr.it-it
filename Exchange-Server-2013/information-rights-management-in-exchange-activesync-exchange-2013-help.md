---
title: 'Information Rights Management in Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Information Rights Management in Exchange ActiveSync
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 50481984
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Information Rights Management in Exchange ActiveSync

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Gli Information Worker utilizzano spesso la posta elettronica per scambiare informazioni riservate. Per proteggere queste informazioni, le organizzazioni possono utilizzare Information Rights Management (IRM) per applicare una protezione permanente al contenuto dei messaggi. Poiché i cellulari vengono sempre più utilizzati per accedere alla posta elettronica, è importante che gli utenti di tali apparati siano in grado di creare e utilizzare contenuti protetti tramite IRM.

**Sommario**

Protezione mobile IRM in Exchange 2013

Requirements

Security

Enabling IRM in Exchange ActiveSync

Per informazioni sulle attività di gestione relative a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Protezione mobile IRM in Exchange 2013

In Exchange 2013 IRM in Microsoft Exchange ActiveSync consente agli utenti di accedere alle avanzate funzionalità di IRM in tutti i dispositivi supportati Exchange ActiveSync senza la necessità di configurare le autorizzazioni AD RMS o connettere il dispositivo a un computer e attivazione di IRM. Il dispositivo mobile, inoltre, non ha necessità di eseguire Windows. Exchange ActiveSync viene concesso in licenza da Microsoft per produttori di dispositivi mobili, produttori di apparecchiature originali (OEM) e altri utenti. Per un elenco dei licenziatari Exchange ActiveSync corrente, espandere la sezione "Protocollo Exchange ActiveSync" nella pagina [Licenze tecnologia Microsoft](https://go.microsoft.com/fwlink/p/?linkid=198562) .

Sono necessari i seguenti requisiti:

  - Sui server Accesso client dell'organizzazione deve essere in esecuzione UNRESOLVED\_TOKEN\_VAL(exExchange2010) SP1 o versioni successive.

  - Nell'organizzazione deve essere distribuito un server AD RMS.

  - IRM deve essere abilitato per i messaggi interni. Questo è un prerequisito per tutte le funzionalità IRM UNRESOLVED\_TOKEN\_VAL(exExchange2010). Per ulteriori informazioni, vedere [Abilitazione o disabilitazione di IRM per i messaggi interni](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

IRM deve essere abilitato nei criteri delle cassette postali di Exchange ActiveSync. È possibile abilitare o disabilitare IRM per diversi gruppi di utenti utilizzando diversi criteri delle cassette postali di Exchange ActiveSync.

## Requisiti

Inizio pagina

  - I server Accesso Client all'interno dell'organizzazione devono eseguire Exchange 2010 SP1 o versione successiva.

  - Quando si abilita IRM in Exchange ActiveSync, il server Accesso client effettua la decrittografia dei messaggi protetti tramite IRM prima di rendere i messaggi accessibili dai dispositivi mobili supportate. Subito dopo la sincronizzazione, i messaggi protetti tramite IRM risiedono sul dispositivo mobile in un formato decrittografato. La protezione IRM viene realizzata dall'applicazione client di posta elettronica abilitata IRM sul dispositivo mobile.

  - IRM devono essere abilitati per i messaggi interni. Questo è un prerequisito per tutte le funzionalità IRM in Exchange 2010. Per ulteriori informazioni, vedere [Abilitazione o disabilitazione di IRM per i messaggi interni](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Quando si abilita IRM in Exchange ActiveSync, si raccomanda di utilizzare le impostazioni dei criteri di Exchange ActiveSync mostrate nella tabella seguente per aiutare a rendere sicuri i dispositivi mobili.

  - I dispositivi che supportano Exchange ActiveSync protocol versione 14.1, inclusi i telefoni Windows, possono supportare IRM in Exchange ActiveSync. Applicazione del dispositivo mobile deve supportare il tag RightsManagementInformation definito nella versione Exchange ActiveSync 14.1.

Impostazione

## Sicurezza

Configurare utilizzando il cmdlet New-ActiveSyncMailboxPolicy

IRM in Exchange ActiveSync non decrittografare protetti tramite IRM allegati sul server Accesso Client. Accesso ai file protetti da IRM viene applicata l'applicazione utilizzata per creare o visualizzare il file. Ad esempio, un telefono Windows, viene applicata la protezione IRM per i file di Microsoft Office[Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121). Per accedere ai file protetti da IRM Office, gli utenti devono connettere il dispositivo a un computer e attivazione Office Mobile con il server RMS.

Selezionare la casella di controllo **Richiedere password**.

### Impostazioni dei criteri di Exchange ActiveSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Abilitare la crittografia per un dispositivo mobile.</th>
<th>Selezionare la casella di controllo <strong>Richiedi password</strong>, e selezionare la casella di controllo <strong>Richiedi crittografia del dispositivo</strong>.</th>
<th>Imposta il parametro <em>RequireDeviceEncryption</em> su <code>$true</code>.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Quando si imposta il parametro <em>RequireDeviceEncryption</em> su <code>$true</code>, i dispositivi mobili che non supportano la crittografia non saranno in grado di collegarsi.</p></td>
<td><p>Non consentire ai dispositivi mobili senza provisionig di sincronizzarsi con in il server Exchange.</p></td>
<td><p>Deselezionare la casella di controllo <strong>Consenti dispositivi senza provisionig</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Imposta il parametro <em>AllowNonProvisionableDevices</em> su <code>$false</code>.</p></td>
<td><p>Per ulteriori informazioni, vedere <a href="mobile-device-mailbox-policies-exchange-2013-help.md">Criteri cassetta postale di dispositivo mobile</a>.</p></td>
<td><p>Impostare il parametro <em>RequireDeviceEncryption</em> su <code>$true</code>.</p>

> [!IMPORTANT]
> Quando si imposta il parametro <EM>RequireDeviceEncryption</EM> a <CODE>$true</CODE>, i dispositivi mobili che non supportano la crittografia del dispositivo non potranno connettersi.


</td>
</tr>
<tr class="odd">
<td><p>Per abilitare IRM in Exchange ActiveSync, eseguire le seguenti operazioni:</p></td>
<td><p>Aggiungere la cassetta postale federata (una cassetta postale di sistema creata durante l'installazione di Exchange 2013 ed UNRESOLVED_TOKEN_VAL(exExchange2010)) al gruppo di utenti con privilegi avanzati in AD RMS. Ciò consente ai server Exchange 2013 ed UNRESOLVED_TOKEN_VAL(exExchange2010) di accedere ai messaggi protetti da IRM.  Per ulteriori informazioni, vedere <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS</a>.</p></td>
<td><p>Utilizzare il cmdlet <a href="https://technet.microsoft.com/it-it/library/dd979792(v=exchg.150)">Set-IRMConfiguration</a> in Exchange Management Shell per abilitare IRM sul server Accesso client. Si abilita così IRM in Exchange ActiveSync e IRM in Microsoft OfficeOutlook Web App per l'organizzazione. Per ulteriori informazioni, vedere <a href="enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md">Attivare o disattivare Information Rights Management sui server Accesso Client</a>.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni, vedere [Criteri cassetta postale di dispositivo mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

Inizio pagina

## Abilitazione di IRM in Exchange ActiveSync

Per abilitare IRM in Exchange ActiveSync, eseguire le attività seguenti:

1.  Aggiungere la cassetta postale di federazione (una cassetta postale di sistema creata Exchange 2013 e Exchange 2010 il programma di installazione) al gruppo di utenti con privilegi avanzati in AD RMS. Che consente ai server Exchange 2013 e Exchange 2010 per accedere ai messaggi protetti tramite IRM. Per ulteriori informazioni, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

2.  Utilizzare il cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)) in Exchange Management Shell per abilitare IRM sul server Accesso Client. In questo modo IRM in Exchange ActiveSync e IRM in Microsoft OfficeOutlook Web App per l'organizzazione. Per ulteriori informazioni, vedere [Attivare o disattivare Information Rights Management sui server Accesso Client](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

Inizio pagina

