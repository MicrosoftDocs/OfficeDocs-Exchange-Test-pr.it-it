---
title: 'Accesso Single Sign-On con distribuzioni ibride: Exchange 2013 Help'
TOCTitle: Accesso Single Sign-On con distribuzioni ibride
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 50482141
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Accesso Single Sign-On con distribuzioni ibride

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-01-29_

Single Sign-On permette agli utenti di accedere a entrambe le organizzazioni, locali e di Office 365, con una singola combinazione di nome utente e password. Offre agli utenti un'esperienza di accesso familiare e consente agli amministratori di controllare facilmente i criteri di account per le cassette postali dell'organizzazione di Exchange Online utilizzando gli strumenti di gestione di Active Directory locali. Anche se non è necessario configurare una distribuzione ibrida con Single Sign-On abilitato, è consigliabile farlo. Senza Single Sign-On, gli utenti dovranno ricordare due diversi set di credenziali, uno per l'organizzazione locale e uno per Office 365. Ecco alcuni altri vantaggi dell'accesso Single Sign-On:

  - **Archiviazione Exchange Online**   Quando Single Sign-On viene distribuito, agli utenti locali di Outlook vengono richieste le credenziali quando accedono per la prima volta al contenuto archiviato nell'organizzazione Exchange Online. Tuttavia, gli utenti possono temporaneamente evitare di fornire le credenziali selezionando "salva la password", che gli verranno richieste solo quando la password dell'account locale verrà cambiata. Se il Single Sign-On non viene distribuito nelle organizzazioni di Exchange e Archiviazione Exchange Online è abilitata, il nome dell'entità utente (UPN) locale deve corrispondere al rispettivo account di Exchange Online e agli utenti verranno sempre chieste le credenziali quando accedono al loro archivio.

  - **Controllo dei criteri**   È possibile controllare i criteri relativi agli account tramite Active Directory, che consente di gestire i criteri relativi alle password, le restrizioni relative alle workstation, i controlli di blocco e altro ancora, senza dover eseguire ulteriori attività nell'organizzazione di Office 365.

  - **Riduzione delle chiamate al supporto**   Le password dimenticate costituiscono una causa comune di chiamata al supporto in tutte le società. Se gli utenti hanno meno password da ricordare, è meno probabile che le dimentichino.

Sono disponibili due opzioni per la distribuzione di Single Sign-On: sincronizzazione password e Active Directory Federation Services (AD FS). Entrambe le opzioni vengono fornite da Azure Active Directory Connect. È consigliabile utilizzare il metodo di sincronizzazione password a meno che non sia presente la specifica esigenza di utilizzare AD FS. La sincronizzazione password offre la maggior parte degli stessi vantaggi di AD FS senza la complessità della sua distribuzione. Nella tabella riportata di seguito vengono mostrati alcuni vantaggi e svantaggi comuni associati a ogni opzione.


> [!NOTE]
> Per impostazione predefinita, se si distribuisce AD FS e i server AD FS locali non sono raggiungibili da Internet per qualsiasi motivo, Office 365 eseguirà il fallback alla sincronizzazione password per l'autenticazione degli utenti. In questo modo gli utenti con cassette postali di Office 365 continuare a lavorare senza interruzioni, anche se i server locali non sono disponibili.



Per ulteriori informazioni su ogni opzione, vedere [Opzioni di accesso utente di Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Metodo Single Sign-On</p></th>
<th><p>Vantaggi</p></th>
<th><p>Svantaggi</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sincronizzazione password (consigliata)</p></td>
<td><ul>
<li><p>Notevolmente meno complessa rispetto ad AD FS</p></li>
<li><p>Gli utenti possono accedere a Office 365 anche se Active Directory locale non è disponibile.</p></li>
<li><p>Meno server aggiuntivi necessari per distribuire sincronizzazione password.</p></li>
<li><p>Certificati di terze parti non necessari.</p></li>
<li><p>Accesso esterno ad Active Directory locale tramite AD FS non necessario.</p></li>
<li><p>La distribuzione spesso può essere completata in poche ore.</p></li>
</ul></td>
<td><ul>
<li><p>La disattivazione di un account utente in Active Directory locale non lo disattiva in Office 365. È necessario disattivare manualmente l'account nel portale di amministrazione di Office 365.</p></li>
<li><p>Richiede Active Directory locale. Altri servizi directory non sono supportati.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>La modifica della password è immediata.</p></li>
<li><p>La disattivazione di un utente in Active Directory locale comporta la disattivazione dell'accesso di rete locale e dell'account di Office 365.</p></li>
<li><p>Supporta i servizi directory diversi da Active Directory.</p></li>
<li><p>Supporta distribuzioni molto grandi e diverse.</p></li>
<li><p>Supporto dell'autenticazione a due fattori.</p></li>
</ul></td>
<td><ul>
<li><p>Richiede più server, almeno uno dei quali deve trovarsi nella rete perimetrale.</p></li>
<li><p>Richiede un indirizzo IP pubblico e una porta TCP 443 aperta nel firewall.</p></li>
<li><p>La connettività con Active Directory locale è necessaria per il rilevamento delle modifiche delle password degli account e con un account recentemente abilitato o disabilitato.</p></li>
</ul></td>
</tr>
</tbody>
</table>

