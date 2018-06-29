---
title: 'Ereditarietà (ACL) elenco di controllo accesso è blocked_InhBlockPublicFolderTree: Exchange 2013 Help'
TOCTitle: Ereditarietà (ACL) elenco di controllo accesso è blocked_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 50481890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ereditarietà (ACL) elenco di controllo accesso è blocked\_InhBlockPublicFolderTree

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2015-03-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft Exchange Server 2007 o Exchange Server 2010 le autorizzazioni non sono stati in grado di propagazione.

Installazione di Exchange richiede che sia attivato l'ereditarietà delle autorizzazioni per gli oggetti Exchange seguenti:

  - Oggetto organizzazione di Exchange

  - Oggetto gruppo amministrativo di Exchange

  - Oggetto contenitore dei server di Exchange

  - Oggetto elenco di indirizzi di Exchange

  - Oggetto della cartella pubblica di Exchange

  - Oggetto struttura di cartelle pubbliche di Exchange

L'impossibilità di abilitare l'ereditarietà delle autorizzazioni per gli oggetti potrebbe causare problemi di flusso di posta elettronica, installazione dell'archivio e interruzione di altri servizi.

Per risolvere questo problema, verificare che i "Consenti di propagare autorizzazioni all'oggetto e agli oggetti figlio" impostazione è abilitata per l'oggetto e quindi rieseguire il programma di installazione di Exchange Server 2007 o Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Per riattivare l'ereditarietà delle autorizzazioni per un oggetto di configurazione di Exchange con Exchange Server 2003 Exchange System Manager</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Attivare la scheda <strong>protezione</strong> per la proprietà object del gestore di sistema di Exchange, impostando un parametro del Registro di sistema.</p>
<ol>
<li><p>Avviare l'Editor del Registro di sistema (Regedt32.exe).</p></li>
<li><p>Individuare la seguente chiave del Registro di sistema:</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p>Dal menu <strong>Modifica</strong>, fare clic su <strong>Nuovo</strong> e quindi aggiungere il valore del Registro di sistema seguente:</p>
<p><strong>Nome valore</strong>: ShowSecurityPage</p>
<p><strong>Tipo di dati</strong>: REG_DWORD</p>
<p><strong>Radice</strong>: binario</p>
<p><strong>Valore</strong>: 1</p></li>
<li><p>Chiudere l'Editor del Registro di sistema.</p></li>
</ol>

> [!NOTE]
> Per impostazione predefinita, nella casella proprietà oggetto di configurazione non è abilitata la scheda <STRONG>protezione</STRONG>.


</li>
<li><p>Aprire Exchange System Manager, trovare l'oggetto in questione, l'oggetto di mouse e scegliere <strong>proprietà</strong>.</p></li>
<li><p>Selezionare la scheda <strong>protezione</strong> e quindi fare clic su <strong>Avanzate</strong>.</p></li>
<li><p>Selezionare <strong>Consenti propagare dall'elemento padre di propagare a questo oggetto e tutti gli oggetti figlio</strong> per riabilitare l'ereditarietà delle autorizzazioni.</p></li>
<li><p>Riavviare il Server di Exchange.</p></li>
</ol></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Se si modificano erroneamente gli attributi degli oggetti di Active Directory quando si utilizza ADSI Edit, lo strumento LDP o un altro client LDAP versione 3, possono verificarsi gravi problemi. Questi problemi possono richiedere la reinstallazione di Microsoft Windows Server™ 2003, Exchange Server o entrambi. Modificare gli attributi degli oggetti di Active Directory a proprio esclusivo rischio.




<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Per riattivare l'ereditarietà delle autorizzazioni per un oggetto di configurazione di Exchange utilizzando ADSI Edit da Exchange Server 2007 o Exchange Server 2010</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Installare ADSI Edit.</p></li>
<li><p>Avviare ADSI Edit. Fare clic su <strong>Start</strong>, scegliere <strong>Esegui</strong>, digitare <strong>ADSIEdit. msc</strong> nella casella di testo e quindi fare clic su OK.</p></li>
<li><p>Accedere all'oggetto in questione, l'oggetto pulsante destro del mouse e scegliere <strong>proprietà</strong>.</p></li>
<li><p>Selezionare la scheda <strong>protezione</strong> e quindi fare clic su <strong>Avanzate</strong>.</p></li>
<li><p>Selezionare <strong>Consenti propagare dall'elemento padre di propagare a questo oggetto e tutti gli oggetti figlio</strong> per riabilitare l'ereditarietà delle autorizzazioni.</p></li>
<li><p>Selezionare <strong>Ok</strong> due volte per rendere effettive le modifiche.</p></li>
<li><p>Attendere la replica di Active Directory propaga le modifiche oppure forzare la replica di Active Directory, seguendo le istruzioni nell'articolo della Microsoft Knowledge Base 232072, &quot;Si avvia la replica tra Active Directory replica partner diretti&quot; (<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>).</p></li>
</ol></td>
</tr>
</tbody>
</table>

