---
title: 'Interfaccia di amministrazione di Exchange in Exchange 2013: Exchange 2013 Help'
TOCTitle: Interfaccia di amministrazione di Exchange in Exchange 2013
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 50481398
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Interfaccia di amministrazione di Exchange in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-17_

L'interfaccia di amministrazione di Exchange (EAC) è una console di gestione basata sul Web in Microsoft Exchange Server 2013, ottimizzata per le distribuzioni locali, online e ibride di Exchange. EAC sostituisce Exchange Management Console (EMC) e il Pannello di controllo di Exchange (ECP), ovvero le interfacce utilizzate per la gestione di Exchange Server 2010.

Uno dei vantaggi forniti dall'interfaccia di amministrazione di Exchange basata sul Web è la possibilità di eseguire la partizione dell'accesso Internet e intranet dalla directory virtuale IIS del Pannello di controllo di Exchange. Questa funzionalità consente di controllare se agli utenti è consentito l'accesso a EAC tramite Internet dall'esterno dell'organizzazione permettendo nel contempo a un utente finale di accedere alle opzioni di Outlook Web App. Per ulteriori informazioni, vedere [Disattivare l'accesso all'interfaccia di amministrazione di Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Per informazioni sulla versione di Exchange Online in questo argomento, vedere [Interfaccia di amministrazione di Exchange in Exchange Online](https://technet.microsoft.com/it-it/library/jj200743\(v=exchg.150\)).

Versione di Exchange Online Protection di questo argomento Vedere [Interfaccia di amministrazione di Exchange in Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj723141\(v=exchg.150\)).

Sommario

Accesso a EAC

Elementi comuni dell'interfaccia utente in EAC

Browser supportati

## Accesso a EAC

EAC è una console di gestione basata sul Web, pertanto è necessario accedervi inserendo nel browser Web l'URL della directory virtuale del Pannello di controllo di Exchange. Nella maggior parte dei casi l'URL di EAC sarà simile al seguente:

  - **URL interno: `https://<CASServerName>/ecp`**   L'URL interno viene utilizzato per accedere a EAC dal firewall dell'organizzazione.

  - **URL esterno: `https://mail.contoso.com/ecp`**   L'URL esterno viene utilizzato per accedere a EAC dall'esterno del firewall dell'organizzazione. Alcune organizzazioni potrebbero voler disattivare l'accesso esterno a EAC. Per ulteriori dettagli, vedere [Disattivare l'accesso all'interfaccia di amministrazione di Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Per individuare l'URL interno o esterno per EAC è possibile utilizzare il cmdlet [Get-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd351058\(v=exchg.150\)). Per ulteriori dettagli, vedere [Trovare gli URL interni ed esterni per il centro di amministrazione di Exchange](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md).

In uno scenario di coesistenza, dove vengono eseguiti Exchange 2010 ed Exchange 2013 nella stessa organizzazione e la cassetta postale è ancora ospitata nel server Cassette postali di Exchange 2010, il browser utilizzerà per impostazione predefinita il Pannello di controllo di Exchange 2010. È possibile accedere a EAC aggiungendo la versione di Exchange all'URL. Ad esempio, per accedere a EAC quando la directory virtuale è ospitata sul server Accesso client CAS15-NA, utilizzare l'URL: `https://CAS15-NA/ecp/?ExchClientVer=15`. Se invece si desidera accedere al Pannello di controllo di Exchange 2010 e la cassetta postale risiede in un server Cassette postali di Exchange 2013, utilizzare l'URL seguente: `https://CAS14-NA/ecp/?ExchClientVer=14`

## Elementi comuni dell'interfaccia utente in EAC

In questa sezione sono descritti gli elementi dell'interfaccia utente comuni nell'ambito di EAC.

![Interfaccia di amministrazione di Exchange](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Interfaccia di amministrazione di Exchange")

## Esplorazione tra sedi

L'esplorazione cross-premise permette di passare velocemente dalla distribuzione di Exchange Online alla distribuzione di Exchange locale e viceversa. Se non si dispone di un'organizzazione Exchange Online, il collegamento porterà direttamente alla pagina di accesso di Office 365. Per ulteriori informazioni, vedere [Distribuzioni ibride di Exchange Server](https://technet.microsoft.com/it-it/library/jj200581\(v=exchg.150\)).

## Riquadro delle funzionalità

È il primo livello di esplorazione per la maggior parte delle attività da eseguire in EAC. Il riquadro delle funzionalità è simile all'albero della console di EMC in Exchange 2010. Tuttavia, in Exchange 2013 il riquadro delle funzionalità è organizzato per aree funzionali, anziché per ruolo del server, e sono necessari meno clic per trovare l'elemento desiderato.

  - **Destinatari   **Consente di gestire cassette postali, gruppi, cassette postali delle risorse, contatti, cassette postali condivise, migrazioni e spostamenti di cassette postali.

  - **Autorizzazioni   **Consente di gestire i ruoli di amministratore, i ruoli utente e i criteri di Outlook Web App.

  - **Gestione conformità   **Permette di gestire eDiscovery sul posto, il blocco sul posto, il controllo, la prevenzione della perdita di dati (DLP), i criteri di conservazione, i tag di conservazione e le regole del journal.

  - **Organizzazione   **Consente di gestire le attività pertinenti all'organizzazione Exchange, tra cui la condivisione federata, le app di Outlook e gli elenchi indirizzi.

  - **Protezione   **Consente di gestire la protezione anti-malware per l'organizzazione.

  - **Flusso di posta   **Consente di gestire regole, rapporti di recapito, domini accettati, criteri degli indirizzi di posta elettronica, connettori di invio e ricezione.

  - **Dispositivi mobili   **Consente di gestire i dispositivi mobili che possono connettersi all'organizzazione. È possibile gestire l'accesso e i criteri delle cassette postali dei dispositivi mobili.

  - **Cartelle pubbliche   **In Exchange 2010, le cartelle pubbliche dovevano essere gestite utilizzando la Console Gestione cartelle pubbliche, posta esternamente a EMC nella casella degli strumenti. In Exchange 2013 le cartelle pubbliche possono essere gestite dall'area funzionale delle **cartelle pubbliche**.

  - **Messaggistica unificata   **Consente di gestire dial plan di messaggistica unificata e gateway IP di messaggistica unificata.

  - **Server   **Consente di gestire i server Cassette postali e Accesso client, i database, i gruppi di disponibilità del database (DAG), le directory virtuali e i certificati.

  - **Ibrida   **Consente di installare e configurare un'organizzazione ibrida.

## Tabulazioni

Le schede rappresentano il secondo livello di esplorazione. Ciascuna area funzionale contiene varie schede, ognuna delle quali rappresenta una funzionalità completa. L'unica eccezione a questa regola è l'area funzionale Ibrida. Occorre prima abilitare l'organizzazione alla distribuzione ibrida utilizzando la procedura guidata di configurazione ibrida.

## Barra degli strumenti

Selezionando una scheda in genere viene visualizzata una barra degli strumenti. che include icone che eseguono un'azione specifica. Nella tabella seguente sono descritte le icone più comuni e le loro azioni. Per visualizzare l'azione associata a un'icona, è sufficiente passare il mouse sopra l'icona.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Icona</th>
<th>Nome</th>
<th>Azione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icona Aggiungi" alt="Icona Aggiungi" /></p></td>
<td><p>Aggiungi, Nuovo</p></td>
<td><p>Utilizzare questa icona per creare un nuovo oggetto. Ad alcune icone è associata una freccia in giù sulla quale si può fare clic per mostrare ulteriori oggetti da creare. Ad esempio, in <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong>, facendo clic sulla freccia in giù vengono visualizzate le opzioni <strong>Cassetta postale utente</strong> e <strong>Cassetta postale collegata</strong>.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" /></p></td>
<td><p>Modifica</p></td>
<td><p>Utilizzare questa icona per modificare un oggetto.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="Icona Elimina" alt="Icona Elimina" /></p></td>
<td><p>Elimina</p></td>
<td><p>Utilizzare questa icona per eliminare un oggetto. Ad alcune icone Elimina è associata una freccia in giù su cui si può fare clic per mostrare altre opzioni.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="icona Cerca" alt="icona Cerca" /></p></td>
<td><p>Cerca</p></td>
<td><p>Utilizzare questa icona per aprire una casella di ricerca in cui digitare la frase di ricerca per l'oggetto che si desidera trovare. Per ulteriori opzioni di ricerca, consultare <a href="https://technet.microsoft.com/it-it/library/jj156853(v=exchg.150)">[Destinatari &gt;] Ricerca avanzata</a>.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="Icona Aggiorna" alt="Icona Aggiorna" /></p></td>
<td><p>Aggiorna</p></td>
<td><p>Utilizzare questa icona per aggiornare la visualizzazione elenco.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icona Ulteriori opzioni" alt="Icona Ulteriori opzioni" /></p></td>
<td><p>Altre opzioni</p></td>
<td><p>Utilizzare questa icona per visualizzare le altre azioni da eseguire per gli oggetti della scheda. Ad esempio, in <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong>, se si fa clic su questa icona, vengono visualizzate le opzioni seguenti: <strong>Disabilita</strong>, <strong>Aggiungi/Rimuovi colonne</strong>, <strong>Esporta i dati in un file CSV</strong>, <strong>Connetti una cassetta postale</strong> e <strong>Ricerca avanzata</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="Icona Freccia in su" alt="Icona Freccia in su" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="Icona Freccia in giù" alt="Icona Freccia in giù" /></p></td>
<td><p>Freccia su e freccia giù</p></td>
<td><p>Utilizzare queste icone per spostare la priorità di un oggetto verso l'alto o verso il basso. Ad esempio, in <strong>Flusso di posta</strong> &gt; <strong>Criteri degli indirizzi di posta elettronica</strong>, fare clic sulla freccia in su per aumentare la priorità di un criterio degli indirizzi di posta elettronica. È inoltre possibile utilizzare queste frecce per esplorare la gerarchia delle cartelle pubbliche e spostare le regole verso l'alto o verso il basso nella visualizzazione elenco.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657505.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="Icona Copia" alt="Icona Copia" /></p></td>
<td><p>Copia</p></td>
<td><p>Utilizzare questa icona per copiare un oggetto in modo da potervi apportare modifiche senza cambiare l'oggetto originale. Ad esempio, in <strong>Autorizzazioni</strong> &gt; <strong>Ruoli amministratore</strong>, selezionare un ruolo dalla visualizzazione elenco e fare clic sull'icona per creare un nuovo gruppo di ruoli basato su un gruppo esistente.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="Icona Rimuovi" alt="Icona Rimuovi" /></p></td>
<td><p>Rimuovi</p></td>
<td><p>Questa icona consente di rimuovere un elemento dall'elenco. Ad esempio, la finestra di dialogo <strong>Autorizzazioni cartella pubblica</strong> consente di rimuovere gli utenti dall'elenco di utenti autorizzati ad accedere alla cartella pubblica selezionando l'utente e facendo clic sull'icona.</p></td>
</tr>
</tbody>
</table>


## Visualizzazione elenco

Selezionando una scheda, nella maggior parte dei casi viene attivata una visualizzazione elenco. La visualizzazione elenco in EAC è stata progettata per rimuovere le limitazioni esistenti in ECP. ECP limita la visualizzazione a 500 oggetti e, se si desidera visualizzare gli oggetti non riportati nel riquadro dei dettagli, si deve ricorrere alle opzioni di ricerca e filtraggio per trovare quegli oggetti specifici. In Exchange 2013, il limite visualizzabile nella visualizzazione elenco di EAC è di circa 20.000 oggetti per le distribuzioni locali e 10.000 oggetti in Exchange Online. È inclusa anche la funzione di paging che consente di scorrere fino ai risultati. Nella visualizzazione elenco **Destinatari** è inoltre possibile configurare la dimensione della pagina ed eseguire l'esportazione dei dati in un file CSV.

## Riquadro dei dettagli

Quando si seleziona un oggetto dalla visualizzazione elenco, nel riquadro dei dettagli vengono visualizzate le informazioni relative all'oggetto in questione. In alcuni casi (ad esempio con gli oggetti destinatari) il riquadro dei dettagli contiene attività di gestione rapida. Se si accede, ad esempio, a **Destinatari** \> **Cassette postali** e si seleziona una cassetta postale dalla visualizzazione elenco, nel riquadro dei dettagli viene visualizzata un'opzione per abilitare o disabilitare l'archivio per la cassetta postale. Il riquadro dei dettagli può inoltre essere utilizzato per modificare in blocco più oggetti. Premere il tasto CTRL, selezionare gli oggetti che si desidera modificare in blocco e utilizzare le opzioni presenti nel riquadro dei dettagli. La selezione, ad esempio, di più cassette postali consente di aggiornare in blocco le informazioni sui contatti e l'organizzazione degli utenti, gli attributi personalizzati, la quota della cassetta postale, le impostazioni di Outlook Web App e altro.

## Notifiche

EAC comprende un visualizzatore di notifiche in cui è indicato lo stato dei processi a lunga esecuzione e che fornisce le notifiche al termine del processo. Inoltre, per processi particolarmente lunghi come le richieste di spostamento, è possibile acconsentire esplicitamente alla ricezione di notifiche per posta elettronica.

## Riquadro Io e Guida

Il riquadro *Io* consente di disconnettersi da EAC e accedere come altro utente. Dal menu a discesa Guida ![Icona Guida](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Icona Guida"), è possibile eseguire le seguenti operazioni:

  - **?**   Fare clic su ![Icona Guida](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Icona Guida") per visualizzare il contenuto della Guida.

  - **Disabilita finestra della Guida**   La finestra della Guida visualizza una guida contestuale per i campi relativi alla creazione o alla modifica di un oggetto. È possibile disabilitare la finestra della guida o riattivarla se era stata disabilitata.

  - **Copyright e privacy   **Fare clic sul collegamento privacy o copyright per leggere le informazioni relative per Exchange 2013.

## Browser supportati

Per un'esperienza ottimale con l'interfaccia di amministrazione di Exchange, utilizzare una combinazione di sistema operativo e browser contrassegnata come "Premium".


> [!NOTE]
> Le combinazioni di sistema operativo e browser non incluse nella tabella non sono supportate, incluso touch.



  - **Premium:**  tutte le caratteristiche funzionali sono supportate e completamente testate.

  - **Supportata:**  supporta le stesse caratteristiche funzionali della combinazione Premium. ma nei browser supportati mancano le funzionalità non supportate dalla combinazione di sistema operativo e browser.

  - **Non supportata:**  la combinazione di sistema operativo e browser non è supportata o testata.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Web browser</p></td>
<td><p>Windows XP e Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 e Windows Server 2008</p></td>
<td><p>Windows 8 e Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Premium</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Premium</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 o versioni successive</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 o versioni successive</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="even">
<td><p>Safari 5,1 o versioni successive</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Premium</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 o versioni successive</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Non supportato</p></td>
</tr>
</tbody>
</table>

