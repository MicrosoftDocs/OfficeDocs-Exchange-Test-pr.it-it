---
title: 'Configurazione del client Outlook blocco: Exchange 2013 Help'
TOCTitle: Configurazione del client Outlook blocco
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51407354
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione del client Outlook blocco

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In Exchange Server 2013, è possibile utilizzare i criteri di conservazione o le cartelle gestite per la messaggistica (MRM) della gestione dei record. Solo gli utenti che eseguono Microsoft Outlook 2010 e versioni successive hanno accesso a tutte le funzionalità client per i criteri di conservazione. Tuttavia, i criteri di conservazione vengono applicati nel server cassette postali dall'Assistente cartelle gestite, indipendentemente dalla versione client Outlook utilizzata dall'utente. Client di Outlook precedenti non devono esporre le funzionalità di gestione record di messaggistica di queste funzionalità. Ad esempio, poiché Outlook 2007 non supporta i criteri di conservazione, gli utenti non possono applicare i tag personali per gli elementi o delle cartelle.

È possibile bloccare gli utenti che eseguono versioni precedenti di Outlook di accedere alle loro cassette postali Exchange. È inoltre possibile bloccare l'accesso in una per cassetta postale o in un singolo server di accesso al Client.

Per le altre attività di gestione relative a Gestione record di messaggistica, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Disponibilità delle funzionalità MRM da applicazioni Client e la versione

Nella tabella seguente sono elencate le caratteristiche di gestione record di messaggistica disponibili in diverse applicazioni client e le versioni.

### Funzionalità di gestione record di messaggistica

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Applicazione client</th>
<th>Funzionalità client MRM disponibili</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 e Outlook 2010</p></td>
<td><p>Tutti</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Cartelle gestite</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 e meno recenti</p></td>
<td><p>Non supportata</p></td>
</tr>
<tr class="even">
<td><p>Altro software client di posta elettronica</p></td>
<td><p>Nessuna</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente sono riportati i numeri di versione per Outlook.

### Versioni di Outlook

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione di Outlook</th>
<th>Numero di versione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8.5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Prima di apportare modifiche, tenere presente che le versioni pacchetto hotfix e il servizio possono avere effetto sulla stringa della versione client. Prestare attenzione quando si limita l'accesso client in quanto componenti sul lato server Exchange inoltre necessario utilizzare MAPI per eseguire l'accesso. Alcuni componenti segnalano versione del client come nome del componente (ad esempio SMTP o OLE DB), mentre altri report Exchange al numero di build (ad esempio 6.0.4712.0). Per questo motivo, evitare di limitazione dei client che dispongono di numeri di versione che iniziano con 6. &lt;<EM>x</EM>. <EM>x</EM>. &gt;. Ad esempio, per impedire l'accesso MAPI completamente, anziché specificare <STRONG>0.0.0-6.5535.65535.65535</STRONG>, specificare i due intervalli in modo che i componenti server possono accedere. Ad esempio, specificare quanto segue: <STRONG>0.0.0-5.9.9; 7.0.0-</STRONG>.



Dopo aver eseguito queste procedure, tenere presente che quando gli utenti non possono accedere alle loro cassette postali, si riceverà il messaggio di avviso seguenti.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>L'amministratore di Server Exchange ha bloccato la versione di Outlook che si sta utilizzando. Per assistenza, contattare l'amministratore.</p></td>
</tr>
</tbody>
</table>


Per ignorare l'avviso di funzionalità MRM non sono supportate per i client di posta elettronica che eseguono versioni precedenti a Outlook 2010Outlook, è possibile utilizzare il parametro *ManagedFolderMailboxPolicyAllowed* dei cmdlet **New-Mailbox**, **Enable-Mailbox**e **Set-Mailbox** in Shell. Quando un criterio cassetta postale di cartelle gestite viene assegnato a una cassetta postale utilizzando il parametro *ManagedFolderMailboxPolicy* , viene visualizzato il messaggio di avviso per impostazione predefinita a meno che non si utilizza il parametro *ManagedFolderMailboxPolicyAllowed* .

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire queste procedure. È necessario utilizzare la shell.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Operazione desiderata

## Blocca le versioni di Outlook singoli per cassetta postale

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali utenti" voce nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

In questo esempio consente di bloccare tutte le versioni Outlook precedenti a 11.8010.8036.

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"

In questo esempio consente di ripristinare l'accesso a una cassetta postale viene bloccata da una versione di Outlook.

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Bloccare le versioni di Outlook in un server Accesso Client

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Impostazioni accesso Client RPC" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md) .

In questo esempio consente di bloccare i client Outlook prima della versione 12.0.0 di accedere alle cassette postali in un Exchange 2010 o versione successiva server Accesso Client.


> [!IMPORTANT]
> I valori utilizzati con il parametro <EM>BlockedClientVersions</EM> sono esemplificativi. È possibile stabilire le versioni del software client corrette eseguendo l'analisi dei file di registro di Accesso client RPC che si trovano in <CODE>%ExchangeInstallPath%Logging\RPC Client Access</CODE>.



    Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"

Per informazioni dettagliate sulla sintassi e definizione dei parametri, vedere [Set-RpcClientAccess](https://technet.microsoft.com/it-it/library/dd351072\(v=exchg.150\)).

