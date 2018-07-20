---
title: 'Aggiungere una copia del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Aggiungere una copia del database delle cassette postali
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 50481006
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere una copia del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-30_

Quando si aggiunge una copia di un database delle cassette postali, la replica continua tra il database esistente e la copia del database viene abilitata automaticamente. Alle copie del database viene assegnata automaticamente un'identità nel formato di \<*DatabaseName*\>\\\<*HostMailboxServerName*\>. Ad esempio, un copia del database DB1 ospitata sul server MBX3 verrebbe denominata DB1\\MBX3.

Per informazioni sulle altre attività di gestione che hanno per oggetto le copie del database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 2 minuti più il tempo necessario per eseguire il seeding della copia del database, che dipende da un'ampia gamma di fattori quali la dimensione del database, la velocità, la larghezza di banda disponibile, la latenza della rete e la velocità di archiviazione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copia attiva del database deve essere installata.

  - Sul server di cassette postali specificato non deve già essere presente una copia del database.

  - Il percorso per la copia del database e i relativi file di registro devono essere disponibili sul server di cassette postali selezionato.

  - Il server che ospita la copia attiva e il server che ospiterà la copia passiva devono trovarsi entrambi nello stesso gruppo di disponibilità del database (DAG). Il DAG deve anche disporre di un quorum ed essere integro.

  - Se si aggiunge la seconda copia di un database (ad esempio, creando la prima copia passiva del database), è necessario che per il database delle cassette postali specificato non sia abilitata la registrazione circolare. Se è abilitata la registrazione circolare, è necessario prima disabilitarla. Una volta aggiunta la copia del database delle cassette postali, è possibile abilitare la registrazione circolare. Dopo aver abilitato la registrazione circolare per un database delle cassette postali replicato, viene utilizzata la registrazione circolare CRCL invece che JET. Se si sta aggiungendo la terza copia di un database (o una copia successiva), la registrazione circolare CRCL può restare abilitata.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Aggiunta di una copia del database delle cassette postali tramite l'interfaccia di amministrazione di Exchange

1.  
    
    Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database che si desidera copiare e fare clic su ![Aggiunta di una copia del database](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "Aggiunta di una copia del database").

3.  
    
    Nella pagina **Aggiungi copia del database delle cassette postali**, fare clic su **Sfoglia...**, selezionare il server cassette postali che ospiterà la copia del database, quindi fare clic su **OK**.

4.  Facoltativamente, configurare il **Numero di preferenza di attivazione** per la copia del database.

5.  Fare clic su **Altre opzioni…** per impostare la copia del database come copia del database ritardata configurando un intervallo di riesecuzione o posporre il seeding automatico della copia del database.

6.  Fare clic su **Salva** per salvare le modifiche di configurazione e aggiungere la copia del database delle cassette postali.

7.  Fare clic su **OK** per riconoscere i messaggi che appaiono.

## Aggiunta di una copia del database delle cassette postali tramite Shell

In questo esempio, una copia del database delle cassette postali DB1 viene aggiunta al server Cassette postali MBX3. L'intervallo di riesecuzione e l'intervallo di troncamento rimangono sul valore predefinito pari a zero e la preferenza di attivazione viene configurata su un valore pari 2.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2

In questo esempio, una copia del database delle cassette postali DB2 viene aggiunta al server Cassette postali MBX4. L'intervallo di riesecuzione e l'intervallo di troncamento rimangono sul valore predefinito pari a zero e la preferenza di attivazione viene configurata sul valore `5`. Inoltre, il seeding viene rimandato per questa copia in modo che possa essere sottoposta a seeding utilizzando un server di origine locale anziché la copia di database attiva corrente, geograficamente distante da MBX4.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed

In questo esempio, una copia del database delle cassette postali DB3 viene aggiunta al server Cassette postali MBX5. L'intervallo di riesecuzione è impostato su 3 giorni mentre l'intervallo di troncamento rimane sul valore predefinito pari a zero e la preferenza di attivazione viene configurata sul valore `4`.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta creazione di una copia del database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database che è stato copiato. Nel riquadro dei dettagli vengono visualizzati lo stato della copia del database e del relativo indice di contenuto, insieme alla lunghezza della coda di copia corrente.

  - Nella shell eseguire il comando riportato di seguito per verificare che la copia del database delle cassette postali sia stata creata e che sia integra.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    I campi Stato e Stato indice contenuto devono essere entrambi integri.

## Ulteriori informazioni

[Copie del database delle cassette postali](mailbox-database-copies-exchange-2013-help.md)

[Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md)

