---
title: 'Modificare la configurazione di AD LDS: Exchange 2013 Help'
TOCTitle: Modificare la configurazione di AD LDS
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61183405
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare la configurazione di AD LDS

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare lo script **ConfigureAdam.ps1** (al percorso $env:ExchangeInstallPath\\Scripts) per modificare la configurazione predefinita dei servizi Active Directory Lightweight Directory Services (AD LDS) nei server Trasporto Edge prima di sottoscrivere il server Trasporto Edge nell'organizzazione di Exchange.


> [!IMPORTANT]
> Lo script <STRONG>ConfigureAdam.ps1</STRONG> richiama il comando <STRONG>dsdbutil</STRONG> per modificare le impostazioni del Registro di sistema di AD&nbsp;LDS. Il comando <STRONG>dsdbutil</STRONG> è uno strumento di gestione di AD&nbsp;LDS inteso per essere utilizzato solo da amministratori con esperienza; l'uso di <STRONG>ConfigureAdam.ps1</STRONG> è il modo consigliato in cui modificare la configurazione dei servizi AD&nbsp;LDS.



I parametri nella seguente tabella sono disponibili per lo script **ConfigureAdam.ps1**. È possibile utilizzare uno, tutti o una qualsiasi combinazioni di tali parametri per modificare AD LDS.

### Parametri disponibili per lo script ConfigureAdam.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>Consente di modificare la porta utilizzata per la comunicazione LDAP. Per impostazione predefinita, il server Trasporto Edge utilizza la porta non standard 50389.</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>Consente di modificare la porta utilizzata per la comunicazione LDAP protetta. Per impostazione predefinita, il server Trasporto Edge utilizza la porta non standard 50636.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>Consente di modificare la posizione del file di registro. Per impostazione predefinita, il server Trasporto Edge crea file di registro nel percorso %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>Consente di modificare la posizione del file del database di directory. Per impostazione predefinita, il server Trasporto Edge archivia il database di directory nel percorso %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
</tbody>
</table>


## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: cinque minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Trasporto Edge" in [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Se è necessario apportare modifiche alla configurazione dei servizi AD LDS del server Trasporto Edge, farlo prima di sottoscrivere il server Trasporto Edge nell'organizzazione di Exchange. Se si modifica la configurazione dei servizi AD LDS di un server Trasporto Edge sottoscritto, sarà quindi necessario risottoscrivere il server Trasporto Edge nell'organizzazione di Exchange.

  - Utilizzare sempre lo script per modificare le impostazioni del Registro di sistema. Apportare modifiche manuali del Registro di sistema alla configurazione dei servizi AD LDS potrebbe rendere l'istanza AD LDS non disponibile.

  - Se si deve modificare la porta LDAP o la porta SSL che viene utilizzata da AD LDS, verificare in primo luogo che la porta selezionata non sia utilizzata da un'altra applicazione. È possibile utilizzare il comando **netstat** per visualizzare le porte in uso nel server Trasporto Edge.

  - È possibile utilizzare solo Shell per eseguire questa procedura.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Modificare la configurazione di AD LDS in un server Trasporto Edge

In questo esempio viene modifica la porta LDAP utilizzata da AD LDS su 5000. La e commerciale (&) fa parte della sintassi del comando.

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

In questo esempio vengono apportate le seguenti modifiche alla configurazione di AD LDS. La e commerciale (&) fa parte della sintassi del comando. Notare i due punti (:) tra ogni parametro e il relativo valore:

  - Imposta la porta 5000 come porta LDAP

  - Consente di impostare la porta SSL su 500

  - Imposta il percorso del registro su D:\\Exchange Server\\Data\\ADLDS

  - Imposta il percorso dei dati su D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"

