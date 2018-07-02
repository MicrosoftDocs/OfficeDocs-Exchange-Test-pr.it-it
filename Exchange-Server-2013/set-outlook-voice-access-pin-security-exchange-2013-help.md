---
title: 'Configurare la protezione di Outlook Voice Access PIN: Exchange 2013 Help'
TOCTitle: Configurare la protezione di Outlook Voice Access PIN
ms:assetid: ef6d9151-d333-4f52-9338-273f7a291e54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125162(v=EXCHG.150)
ms:contentKeyID: 50555709
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la protezione di Outlook Voice Access PIN

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-16_

Quando gli utenti di messaggistica unificata si connettono al sistema di caselle vocali dal telefono, utilizzano Outlook Voice Access per accedere al sistema dei menu. Prima che gli utenti possano accedere al sistema di caselle vocali, viene richiesto loro di immettere il PIN. Analogamente all'amministratore, l'utente può configurare le impostazioni e i requisiti relativi al PIN nonché eseguire le attività di gestione del PIN. Dopo che un utente è stato abilitato per la posta vocale e che è stato generato un PIN, il PIN dell'utente viene crittografato e archiviato nella cassetta postale Una dell'utente.


> [!NOTE]
> Gli utenti di Outlook Voice Access devono utilizzare input a toni (denominato anche DTMF, Dual Tone Multiple Frequency) per immettere il PIN di accesso alla cassetta postale abilitata alla messaggistica unificata. Il riconoscimento vocale non è disponibile per l'immissione del PIN.



**Sommario**

PIN overview

PIN requirements

Managing Outlook Voice Access PINs

## Cenni preliminari sul PIN

Il PIN è una stringa numerica utilizzata in determinati sistemi per consentire l'autenticazione e l'accesso dell'utente al sistema. I PIN sono utilizzati più frequentemente per i Bancomat. Vengono inoltre utilizzati al posto delle password alfanumeriche per sistemi di caselle vocali. La complessità del PIN dipende dalla relativa lunghezza, dal livello di protezione e dalla difficoltà con cui viene identificato.

Nella messaggistica unificata gli utenti di Outlook Voice Access immettono il PIN su un telefono analogico, digitale o mobile in modo che possano accedere alla posta elettronica, alla posta vocale, ai contatti e alle informazioni di calendario nella propria cassetta postale di Exchange Server.

Nella messaggistica unificata, i criteri del PIN vengono definiti e configurati su un criterio cassetta postale di messaggistica unificata. È possibile creare più criteri cassetta postale di messaggistica unificata in base alle proprie esigenze. Quando viene abilitato alla posta vocale, l'utente viene collegato a un criterio cassetta postale di messaggistica unificata esistente. I criteri del PIN di messaggistica unificata configurati sul criterio di messaggistica unificata devono essere basati sui requisiti di protezione dell'organizzazione.

## Requisiti del PIN

Di seguito sono riportate diverse impostazioni di configurazione del PIN che possono essere definite su un criterio di messaggistica unificata.

## Lunghezza minima PIN

L'impostazione **Lunghezza minima PIN** indica il numero minimo di cifre di un PIN della cassetta postale. L'intervallo è compreso tra 4 e 24 e l'impostazione predefinita è 6. Se si immette 0, non verrà richiesto alcun PIN.


> [!IMPORTANT]
> Non è tuttavia consigliabile configurare l'impostazione su 0 poiché verrebbe ridotto notevolmente il livello di protezione della rete.



Se il valore della lunghezza minima del PIN viene modificato con un valore superiore, per continuare, agli utenti esistenti di Outlook Voice Access verrà richiesto di creare un nuovo PIN contenente il nuovo numero minimo di cifre.


> [!NOTE]
> Se viene impostato un numero maggiore, l'ambiente di messaggistica unificata sarà più protetto. Tuttavia, un numero troppo elevato di cifre potrebbe risultare difficile da ricordare per gli utenti.



## Imponi durata PIN

L'impostazione **Imponi durata PIN** controlla l'intervallo di tempo, espresso in giorni, compreso tra la data dell'ultima modifica del PIN da parte dell'utente di Outlook Voice Access e quella in cui verrà richiesto di modificarlo nuovamente. L'intervallo è compreso tra 0 e 999 e il valore predefinito è 60 giorni. Se si immette 0, il PIN non ha scadenza.


> [!NOTE]
> La messaggistica unificata non avvisa l'utente quando il PIN sta per scadere.



## Numero di errori di accesso prima della reimpostazione del PIN

L'impostazione **Numero di errori di accesso prima della reimpostazione del PIN** specifica il numero di tentativi di accesso sequenziali non riusciti prima della reimpostazione automatica del PIN della cassetta postale. Per disabilitare questa funzionalità, impostare un numero di tentativi illimitato. In caso contrario, deve essere impostato su un numero inferiore al valore dell'impostazione **Numero di errori accesso prima del blocco**. L'intervallo è compreso tra 1 e 998 e il valore predefinito è 5.


> [!NOTE]
> Per aumentare la protezione degli utenti abilitati alla messaggistica unificata, immettere un numero minore di 5.



## Numero di errori accesso prima del blocco

L'impostazione **Numero di errori accesso prima del blocco** specifica il numero di errori di immissione del PIN in chiamate successive che gli utenti di Outlook Voice Access hanno a disposizione prima che la cassetta postale venga bloccata. Per impostazione predefinita, dopo 5 tentativi, il PIN viene automaticamente ripristinato. L'intervallo è compreso tra 1 e 999 e il valore predefinito è 15.


> [!NOTE]
> Per aumentare la protezione, diminuire il numero di tentativi non riusciti consentiti. Tuttavia, tenere presente che se viene impostato un numero notevolmente inferiore a quello predefinito, l'accesso degli utenti potrebbe essere bloccato senza motivo. La messaggistica unificata genera eventi di avviso che possono essere visualizzati con il Visualizzatore eventi in caso di mancata autenticazione del PIN di un utente abilitato alla messaggistica unificata oppure nel caso di un tentativo non riuscito di accesso al sistema da parte dell'utente.



## Consenti modelli di PIN comuni

L'impostazione **Consenti modelli di PIN comuni** è utilizzata per abilitare o disabilitare l'utilizzo dei modelli di numero comuni utilizzati nella creazione di un PIN. Per impostazione predefinita, questa funzione è disabilitata. Gli utenti di Outlook Voice Access non potranno pertanto immettere i modelli di numero seguenti:

  - **Numeri sequenziali**   Valori del PIN composti esclusivamente da numeri consecutivi. Ad esempio, 1234 e 65432.

  - **Numeri che si ripetono**   Valori del PIN composti da numeri ripetuti. ad esempio 11111 e 22222.

  - **Suffisso dell'estensione della cassetta postale**   Valori del PIN composti dal suffisso dell'estensione della cassetta postale utente. Se l'estensione della cassetta postale è 36697, il PIN non può essere 6697.

## Numero di ricicli del PIN

L'impostazione **Numero di ricicli del PIN** consente di configurare il numero dei diversi PIN che un utente deve utilizzare prima di poter utilizzare di nuovo i PIN precedentemente utilizzati. L'intervallo è compreso tra 1 e 20 e il valore predefinito è 5.

## Gestione dei PIN di Outlook Voice Access

Quando si pianificano i PIN per Outlook Voice Access, è necessario scegliere i livelli appropriati di sicurezza dell'organizzazione. È necessario considerare attentamente i requisiti del PIN di Outlook Voice Access e definire se le impostazioni di protezione del PIN soddisferanno o supereranno i criteri di protezione dell'organizzazione.


> [!IMPORTANT]
> Per una maggiore sicurezza, si consiglia di implementare requisiti del PIN complessi per gli utenti di Outlook Voice Access. Il livello di protezione della rete può essere aumentato creando per il PIN criteri cassetta postale di messaggistica unificata che richiedono più di 6 cifre.



Una volta impostati i requisiti di PIN per Outlook Voice Access, è necessario creare e configurare un criterio cassetta postale di messaggistica unificata per applicare i requisiti del PIN dell'organizzazione. Per informazioni dettagliate sulla creazione di un criterio cassetta postale di messaggistica unificata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md). Per informazioni dettagliate sulla gestione dei criteri cassetta postale di messaggistica unificata, vedere [Gestire i criteri cassetta postale di messaggistica unificata](manage-a-um-mailbox-policy-exchange-2013-help.md).


> [!NOTE]
> Una volta creato il criterio di messaggistica unificata, è necessario collegare gli utenti abilitati alla messaggistica unificata ai criteri cassetta postale di messaggistica unificata appropriati. A questo scopo, utilizzare il cmdlet <STRONG>Enable-UMMailbox</STRONG> in Exchange Management Shell oppure tramite l'interfaccia di amministrazione di Exchange (EAC). Per ulteriori informazioni sul cmdlet Exchange Management Shell, vedere <A href="https://technet.microsoft.com/it-it/library/aa998033(v=exchg.150)">Enable-UMMailbox</A>.



È possibile che gli utenti di Outlook Voice Access dimentichino il PIN o che venga bloccato l'accesso della posta vocale alla cassetta postale. In entrambi i casi, può essere necessario reimpostare il PIN dell'utente abilitato alla messaggistica unificata. Per ulteriori informazioni, vedere [Reimpostare un PIN della casella vocale](reset-a-voice-mail-pin-exchange-2013-help.md).

È possibile recuperare le informazioni sul PIN per un utente che è abilitato alla messaggistica unificata. Le informazioni restituite vengono calcolate utilizzando i dati sul PIN crittografati archiviati nella cassetta postale dell'utente. In tal modo è possibile visualizzare le informazioni del PIN dell'utente e determinare se per l'utente è stato bloccato l'accesso alla cassetta postale. Per ulteriori informazioni, vedere [Recuperare le informazioni sul PIN di segreteria telefonica](retrieve-voice-mail-pin-information-exchange-2013-help.md).

