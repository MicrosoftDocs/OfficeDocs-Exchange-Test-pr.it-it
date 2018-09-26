---
title: 'Abilitare la pubblicazione del calendario Internet: Exchange 2013 Help'
TOCTitle: Abilitare la pubblicazione del calendario Internet
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50555668
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare la pubblicazione del calendario Internet

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-08-22_

**Riepilogo:**  utilizzare queste procedure per consentire agli utenti OWA nella propria organizzazione di Exchange 2013 condividere le informazioni di disponibilità del calendario con organizzazioni esterne.

Gli utenti delle organizzazioni di Microsoft Exchange Server 2013 possono condividere le informazioni sulla disponibilità del calendario con utenti di organizzazioni non Exchange e con altri utenti con accesso a Internet. La pubblicazione del calendario Internet ha migliorato la flessibilità e aumenta il numero di utenti che possono condividere le informazioni sulla disponibilità del calendario.

L'abilitazione della pubblicazione del calendario Internet consiste di tre passaggi generali:

1.  Configurare l'URL del proxy Web per il server cassette postali (questo passaggio è necessario solo se un proxy Web URL esiste già nell'organizzazione, altrimenti andare al passaggio 2).

2.  Abilitazione della directory virtuale di pubblicazione per il server Accesso client.

3.  Creazione di un criterio di condivisione dedicato specifico per la pubblicazione del calendario Internet o aggiornamento del criterio di condivisione predefinito per supportare il dominio **anonimo**. Ciascun metodo consente agli utenti dell'organizzazione di Exchange di invitare altri utenti che dispongono dell'accesso a Internet a visualizzare informazioni limitate sulla disponibilità del calendario tramite l'accesso a un URL pubblicato.


> [!IMPORTANT]
> Al termine dell'esecuzione passaggio 3, gli utenti saranno quindi necessario pubblicare i calendari di Outlook. Pubblicazione del calendario consente di creare gli URL che gli utenti possono assegnare agli utenti esterni all'organizzazione. Un URL consente a destinatari di sottoscrivere calendari utilizzando Outlook o Outlook Web App e l'altro consente la visualizzazione del destinatario un calendario in un Web browser. Ogni utente può controllare il livello di dettaglio gli utenti possono visualizzare.



Per le attività di gestione aggiuntive relative ai criteri di condivisione, vedere [Criteri di condivisione](sharing-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Un server Accesso client di Exchange 2013 sia presente nell'organizzazione di Exchange che utilizza la condivisione delle informazioni sul calendario degli utenti.

  - Le cassette postali degli utenti si trovino sui server Cassette postali di Exchange 2013 nell'organizzazione di Exchange che utilizza la condivisione delle informazioni sul calendario degli utenti.

  - Solo gli utenti di Outlook 2010 o versioni successive e di Outlook Web App possano creare inviti di condivisione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Configurazione dell'URL del proxy Web tramite Shell


> [!NOTE]
> Questa operazione è necessaria solo se esiste già un URL proxy Web all'interno dell'organizzazione. In caso contrario, procedere al passaggio 2.<BR>Non è possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) per configurare l'URL del proxy Web.



In questo esempio viene configurato un URL proxy Web sul server Cassette postali MAIL01.

```powershell
Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ExchangeServer](https://technet.microsoft.com/it-it/library/bb123716\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta configurazione dell'URL del proxy Web, eseguire il comando Shell seguente e controllare le informazioni del parametro *InternetWebProxy*.

```powershell
Get-ExchangeServer | format-list
```

## Passaggio 2: Abilitazione della pubblicazione della directory virtuale tramite Shell


> [!NOTE]
> Non è possibile utilizzare EAC per abilitare la pubblicazione della directory virtuale.



In questo esempio viene abilitata la pubblicazione della directory virtuale sul server Accesso client CAS01.
```powershell
    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true
```
Dove l' identità `CAS01\owa (Default Web Site)` è il nome del server sia la directory virtuale di Outlook Web App.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione della pubblicazione della directory virtuale, eseguire il comando Shell seguente e controllare le informazioni del parametro *ExternalURL*.

```powershell
Get-OwaVirtualDirectory | format-list
```

## Passaggio 3: Creare o configurare un criterio di condivisione specifico per la pubblicazione del calendario Internet


> [!NOTE]
> Le opzioni seguenti nel passaggio 3 si applicano solo per gli ambienti Exchange Online.



È possibile scegliere di creare un criterio di condivisione per Internet (opzione 1) la pubblicazione del calendario o la configurazione predefinita criterio di condivisione del calendario Internet publishing (opzione 2). Con entrambe le opzioni è possibile scegliere di utilizzare EAC o Shell.

## Opzione 1: Creare un criterio di condivisione specifico per la pubblicazione del calendario Internet

Per creare un criterio di condivisione specifico per la pubblicazione del calendario Internet, completare i passaggi seguenti.

## Utilizzo dell'interfaccia di amministrazione di Exchange

1.  Accedere a **Organizzazione**\> **Condivisione**.

2.  Nella visualizzazione elenco, sotto **Condivisione singola**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella finestra di dialogo **Criterio di condivisione** digitare il nome descrittivo per il criterio di condivisione nel campo **Nome criterio** (ad esempio, **Internet**).

4.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per definire le regole di condivisione per il criterio di condivisione.

5.  In **Regola di condivisione** fare clic su **Condivisione con uno specifico dominio**, quindi digitare **Anonymous** nella casella corrispondente.

6.  Per specificare i livelli di condivisione del calendario da applicare al criterio di condivisione, selezionare la casella di controllo **Condividi la tua cartella del calendario** e selezionare una delle opzioni seguenti:
    
      - **Informazioni sulla disponibilità solo con l'ora**
    
      - **Informazioni sulla disponibilità di calendario con ora, oggetto e posizione**
    
      - **Tutte le informazioni di calendario sull'appuntamento, incluse ora, oggetto, posizione e titolo**

7.  Fare clic su **Salva** per impostare le regole per il criterio di condivisione.

8.  In **Criterio di condivisione**, fare clic su **Salva** per creare il criterio.

## Utilizzo di Shell

Con questo esempio viene creato il criterio di condivisione per la pubblicazione del calendario denominato Internet e viene configurato il criterio che consente di condividere solo le informazioni sulla disponibilità. Il criterio è abilitato.
```powershell
    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
```
In questo esempio viene aggiunto il criterio di condivisione del calendario Internet a una cassetta postale utente.

```powershell
Set-Mailbox -Identity <user name> -SharingPolicy "Internet"
```

In questo esempio viene aggiunto il criterio di condivisione del calendario Internet a un'unità organizzativa (OU).

```powershell
Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-SharingPolicy](https://technet.microsoft.com/it-it/library/dd298186\(v=exchg.150\)) e [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la creazione corretta del criterio di condivisione, eseguire il comando Shell seguente per controllare le informazioni sul criterio di condivisione.

```powershell
Get-SharingPolicy <policy name> | format-list
```

## Opzione 2: Configurare l'impostazione predefinita criterio di condivisione per la pubblicazione del calendario Internet

Per configurare un criterio di condivisione predefinito specifico per la pubblicazione del calendario Internet, completare i passaggi seguenti.

## Utilizzo dell'interfaccia di amministrazione di Exchange

1.  Accedere a **Organizzazione** \> **Condivisione**.

2.  Nella visualizzazione elenco sotto **Condivisione singola** selezionare il criterio di condivisione predefinito, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Criterio di condivisione** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere una regola di condivisione al criterio.

4.  In **Regola di condivisione** fare clic su **Condivisione con uno specifico dominio**, quindi digitare **Anonymous** nella casella corrispondente.

5.  Per specificare i livelli di condivisione del calendario da applicare al criterio di condivisione, selezionare la casella di controllo **Condividi la tua cartella del calendario** e selezionare una delle opzioni seguenti:
    
      - **Informazioni sulla disponibilità solo con l'ora**
    
      - **Informazioni sulla disponibilità di calendario con ora, oggetto e posizione**
    
      - **Tutte le informazioni di calendario sull'appuntamento, incluse ora, oggetto, posizione e titolo**

6.  Fare clic su **Salva** per impostare le regole per il criterio di condivisione.

7.  In **Criterio di condivisione**, fare clic su **Salva** per salvare le modifiche.

## Utilizzo di Shell

Con questo esempio viene aggiornato il criterio di condivisione predefinito e configurato il criterio per condividere solo le informazioni sulla disponibilità. Il criterio è abilitato.
```powershell
    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare l'aggiornamento corretto del criterio di condivisione predefinito, eseguire il comando Shell seguente per controllare le informazioni sul criterio di condivisione.

```powershell
Get-SharingPolicy <policy name> | format-list
```

