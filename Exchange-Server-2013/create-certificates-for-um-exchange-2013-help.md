---
title: 'Creare certificati per la messaggistica unificata: Exchange 2013 Help'
TOCTitle: Creare certificati per la messaggistica unificata
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54652870
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare certificati per la messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-29_

È possibile utilizzare la procedura guidata Nuovo certificato di Exchange nell'interfaccia di amministrazione di Exchange o Shell per creare certificati autofirmati o richieste di certificati per una infrastruttura a chiave pubblica interna. Per la messaggistica unificata, è possibile utilizzare uno di questi certificati sia per il servizio di messaggistica unificata che per i servizi Router chiamate di messaggistica unificata di Microsoft Exchange. È possibile utilizzare lo stesso certificato per entrambi i servizi o un certificato diverso per ogni servizio. È inoltre possibile acquistare e importare un certificato commerciale di terze parti per i servizi di messaggistica unificata. Se si utilizza un certificato autofirmato per la messaggistica unificata, potrebbe essere necessario includere nel nome alternativo del soggetto il nome dei server Accesso client e Cassette postali.

Per impostazione predefinita, quando si installa Exchange Server 2013, vengono creati due certificati autofirmati: **Microsoft Exchange Server Auth Certificate** e **Microsoft Exchange**. Il certificato autofirmato **Microsoft Exchange** può essere utilizzato dalla messaggistica unificata per crittografare i dati, ma è necessario assegnare il certificato alla messaggistica unificata e ai servizi Router chiamate della stessa. Dopo aver assegnato il certificato ai servizi di messaggistica unificata, è possibile copiarlo e importarlo nei gateway VoIP, in IP PBX e nel PBX abilitato per SIP. Tuttavia, invece di utilizzare i certificati autofirmati predefiniti, potrebbe essere necessario crearne un altro specifico per la messaggistica unificata.


> [!WARNING]
> Non è possibile utilizzare i certificati autofirmati quando si sta integrando la messaggistica unificata con Microsoft Lync Server.



Per le altre attività di gestione relative alla gestione dei certificati per la messaggistica unificata, vedere [Distribuzione di certificati per le procedure di messaggistica unificata](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione dei certificati" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) e "Servizio di messaggistica unificata" in [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md). È inoltre necessario effettuare l'accesso utilizzando un account appartenente al gruppo di amministratori locale del computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di una richiesta di certificato per la messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Certificati**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo certificato di Exchange**, selezionare **Crea la richiesta per un certificato emesso da un'autorità di certificazione**, quindi fare clic su **Avanti**.

3.  Immettere un nome descrittivo per il certificato, quindi fare clic su **Avanti**.

4.  Se non è necessario un certificato con caratteri jolly, fare clic su **Avanti**. Se è necessario un certificato con caratteri jolly, selezionare **Richiedi un certificato con caratteri jolly. Un certificato con caratteri jolly ti consente di proteggere tutti i sottodomini all'interno del dominio radice con un singolo certificato**, immettere il nome del dominio principale, quindi fare clic su **Avanti**.

5.  In **Archivia la richiesta di certificato sul server**, fare clic **Sfoglia** per accedere al percorso in cui si intende archiviare il file. È possibile archiviare la richiesta di certificato su qualsiasi server Accesso client o Cassette postali nell'organizzazione di Exchange. Selezionare il percorso, fare clic su **OK**, quindi fare clic su **Avanti**.

6.  Se si è richiesto un certificato con caratteri jolly, procedere al passaggio 9.

7.  Se, al contrario, non si è effettuata la richiesta, è necessario specificare i domini che si intende includere nel certificato. Per modificare un dominio, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"), quindi fare clic su **Avanti**.

8.  In **In base alle tue scelte, i seguenti domini verranno inclusi nel certificato. Qui puoi aggiungere altri domini o apportare delle modifiche.**, è possibile aggiungere, modificare, rimuovere o controllare il nome dei domini elencati in **Dominio**. Quindi fare clic su **Avanti**.

9.  In **Specifica le informazioni sulla tua organizzazione richieste dall'autorità di certificazione. La specificazione è richiesta dall'autorità di certificazione**, immettere quanto segue:
    
      - **Nome dell'organizzazione**
    
      - **Nome reparto**
    
      - **Città/Località**
    
      - **Stato/Provincia**
    
      - **Nome paese/area geografica**   Per questa opzione, utilizzare l'elenco a discesa per selezionare il paese o l'area geografica.

10. In **Specifica il file dove salvare la richiesta di certificato**, immettere il nome file del certificato, quindi fare clic su**Fine**.

## Creazione di una richiesta di certificato tramite Shell

In questo esempio viene creata una nuova richiesta di certificato in Exchange per un server Cassette postali denominato `MyMailboxServer` con un nome descrittivo di `CertUM`.

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## Creazione di un certificato autofirmato per messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Certificati**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo certificato di Exchange**, scegliere **Crea un certificato autofirmato**, quindi selezionare **Avanti**.

3.  Immettere un nome descrittivo per il certificato, quindi selezionare **Avanti**.

4.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per selezionare i server Exchange a cui si intende applicare il certificato, quindi scegliere **Avanti**.

5.  Specificare i domini che si intende includere nel certificato, quindi selezionare **Avanti**. Per aggiungere un dominio a un servizio, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

6.  Verificare che i domini inclusi siano corretti, quindi selezionare **Fine**.


> [!IMPORTANT]
> Quando si utilizza l'interfaccia di amministrazione di Exchange per creare un certificato autofirmato, non viene chiesto di attivare i servizi per il certificato. Una volta creato il certificato, è possibile utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet <STRONG>Enable-ExchangeCertificate</STRONG> in Shell per attivare i servizi di Exchange. Per ulteriori informazioni sull'assegnazione di un certificato ai servizi di messaggistica unificata, vedere <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata</A>.



## Creazione di un certificato autofirmato per messaggistica unificata tramite Shell

In questo esempio viene creato un nuovo certificato autofirmato di Exchange per un server Cassette postali denominato `MyMailboxServer` con un nome descrittivo di `UMCert`.

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true


> [!TIP]
> Quando si specificano i servizi che si intende attivare utilizzando il parametro <EM>Services</EM>, viene richiesto di assegnare tali servizi. In questo esempio, viene richiesto di attivare il certificato per la messaggistica unificata e i servizi Router chiamate della stessa. Per ulteriori informazioni sull'attivazione di un certificato per i servizi, vedere <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata</A>.


