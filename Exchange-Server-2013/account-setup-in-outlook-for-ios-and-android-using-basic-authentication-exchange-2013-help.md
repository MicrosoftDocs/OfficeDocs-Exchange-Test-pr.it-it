---
title: 'Account setup in Outlook for iOS and Android using basic authentication: Exchange 2013 Help'
TOCTitle: Account setup in Outlook for iOS and Android using basic authentication
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518381
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Account setup in Outlook for iOS and Android using basic authentication

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-04-30_

**Sintesi:**  Informazioni su come gli utenti nell'organizzazione di Exchange 2013 possono configurare rapidamente i propri account di Outlook per iOS e Android tramite l'autenticazione di base.

Outlook per iOS e Android offre agli amministratori di Exchange la possibilità di "distribuire" le configurazioni degli account agli utenti locali che usano l'autenticazione di base tramite il protocollo ActiveSync. Questa funzionalità è compatibile con qualsiasi provider Mobile Device Management (MDM) che utilizza il canale [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) per iOS o il canale [Android in the Enterprise](https://developer.android.com/samples/apprestrictions/index.html) per Android.

Per gli utenti locali registrati in Microsoft Intune, è possibile distribuire le impostazioni di configurazione degli account utilizzando Intune nel Portale di Azure.

Dopo aver creato la configurazione dell'account e dopo che l'utente registra il proprio dispositivo, Outlook per iOS e Android rileva che un account viene "trovato" e richiede quindi all'utente di aggiungere tale account. L'unica informazione che l'utente deve inserire per completare la procedura di configurazione è la propria password. Successivamente, il contenuto della cassetta postale dell'utente viene caricato e l'utente può iniziare a usare l'app.

Nelle figure seguenti viene mostrato un esempio della procedura di configurazione dell'utente finale una volta configurato Outlook per iOS e Android in Intune nel Portale di Azure.

![Configurazione dell'account per Outlook per iOS e Android locale](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Configurazione dell'account per Outlook per iOS e Android locale")

## Creare un criterio di configurazione dell'app per Outlook per iOS e Android tramite Microsoft Intune

Se è in uso Microsoft Intune come provider di gestione dei dispositivi mobili, la procedura seguente consente di distribuire le impostazioni di configurazione dell'account per le cassette postali locali che sfruttano l'autenticazione di base con il protocollo ActiveSync. Una volta creata la configurazione, è possibile assegnare le impostazioni a gruppi di utenti, come descritto nella sezione successiva, Assegnare impostazioni di configurazione.


> [!NOTE]
> Se gli utenti nell'organizzazione usano dispositivi iOS e Android for Work, sarà necessario creare un criterio di configurazione dell'app separato per ogni piattaforma.



1.  Accedere al portale di Azure.

2.  Selezionare **Altri servizi \> Monitoraggio + Gestione \> Intune**.

3.  Nel pannello **App mobili** dell'elenco Gestione, selezionare **Criteri di configurazione app**.

4.  Nel pannello **Criteri di configurazione app**, scegliere **Aggiungi**.

5.  Nel pannello **Aggiungi la configurazione dell'app**, immettere un **nome** e una **descrizione** facoltativa per le impostazioni di configurazione dell'app.

6.  Per il tipo **Registrazione del dispositivo**, scegliere **Dispositivi gestiti**.

7.  Per **Piattaforma**, scegliere **iOS** o **Android for Work**.

8.  Scegliere **App associate**, quindi nel pannello **App di destinazione**, scegliere **Microsoft Outlook per iOS** o **Microsoft Outlook per Android**.

9.  Fare clic su **OK** per tornare al pannello **Aggiungi la configurazione dell'app**.

10. Scegliere **Impostazioni di configurazione**. Nel pannello **Impostazioni di configurazione**, definire le coppie di valori chiave che forniranno configurazioni a Outlook per iOS e Android. Le coppie di valori chiave immesse sono definite in questo articolo, nella sezione Coppie di valori chiave.
    

    > [!NOTE]
    > Per immettere le coppie di valori chiave, è possibile scegliere tra l'uso della finestra di progettazione per la configurazione o l'inserimento di un elenco proprietà XML.



11. Al termine, scegliere **OK**.

12. Nel pannello **Aggiungi la configurazione dell'app**, scegliere **Crea**.

I criteri di configurazione appena creati verranno visualizzati nel pannello **Criteri di configurazione dell'app**.

## Assegnare impostazioni di configurazione

Le impostazioni create nella sezione precedente vengono assegnate a gruppi di utenti in Azure Active Directory. Quando un utente ha installato l'app Microsoft Outlook, l'app verrà gestita con le impostazioni specificate. Per eseguire l'operazione:

1.  Nel pannello **App per dispositivi mobili** del dashboard di gestione delle applicazioni mobili, scegliere **Criteri di configurazione dell'app**.

2.  Nell'elenco dei criteri di configurazione dell'app, selezionare quello che si desidera assegnare, quindi scegliere **Assegnazioni**.

3.  Nel pannello **Assegnazioni**, scegliere **Seleziona gruppi**.

4.  Nel pannello **Seleziona gruppi**, selezionare il gruppo Azure AD al quale assegnare la configurazione dell'app, quindi scegliere **Seleziona** e infine **Salva**.

## Coppie di valori chiave

Quando si crea un criterio di configurazione dell'app nel portale di Azure o tramite il provider MDM, sono necessarie le seguenti coppie di valori chiave:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiave</th>
<th>Valori</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>Questo valore consente di specificare l'account di posta elettronica del nome visualizzato come viene visualizzato dagli utenti sui propri dispositivi. </p>
<p><strong>Valori accettati</strong>: Stringa</p>
<p><strong>Valore predefinito non specificato</strong>: &lt;vuoto&gt;</p>
<p><strong>Esempio</strong>: utente@nomeazienda.com</p>
<p><strong>Token Intune*</strong>: {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>Questo valore specifica l'indirizzo di posta elettronica da usare per inviare e ricevere posta.</p>
<p><strong>Valori accettati</strong>: Stringa</p>
<p><strong>Valore predefinito non specificato</strong>: &lt;vuoto&gt;</p>
<p><strong>Esempio</strong>: utente@nomeazienda.com</p>
<p><strong>Token Intune*</strong>: {{mail}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>Questo valore specifica il nome dell'entità utente per il profilo di posta elettronica che verrà usato per autenticare l'account.</p>
<p><strong>Valori accettati</strong>: Stringa</p>
<p><strong>Valore predefinito non specificato</strong>: &lt;vuoto&gt;</p>
<p><strong>Esempio</strong>: upnutente@nomeazienda.com</p>
<p><strong>Token Intune*</strong>: {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>Questo valore indica il metodo di autenticazione dell'utente.</p>
<p><strong>Valori accettati</strong>: 'Username and Password'; 'Certificates'</p>
<p><strong>Valore predefinito non specificato</strong>: 'Username and Password'</p>
<p><strong>Esempio</strong>: 'Username and Password'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>Questo valore specifica il nome host del server Exchange.</p>
<p><strong>Valori accettati</strong>: Stringa</p>
<p><strong>Valore predefinito non specificato</strong>: &lt;vuoto&gt;</p></td>
</tr>
</tbody>
</table>


**\*** Gli utenti di Microsoft Intune possono utilizzare i token che si espandono al valore corretto secondo l'utente registrato di MDM. Per ulteriori informazioni, vedere [Aggiungere criteri di configurazione delle app per i dispositivi iOS gestiti](https://docs.microsoft.com/it-it/intune/app-configuration-policies-use-ios).

