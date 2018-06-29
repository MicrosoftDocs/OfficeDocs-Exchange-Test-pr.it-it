---
title: 'Inserimento del codice Product Key di Exchange 2013: Exchange 2013 Help'
TOCTitle: Inserimento del codice Product Key di Exchange 2013
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51407423
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: MT
---

# Inserimento del codice Product Key di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Un codice product key indica Exchange Server 2013 ha acquistato una licenza Standard o Enterprise Edition. Se il codice "product key" è stato acquistato è di una licenza Enterprise Edition, che consente di installare più di cinque database per ogni server oltre a tutti gli elementi che è disponibile con una licenza Standard Edition. Per ulteriori informazioni sulle licenze di Exchange, vedere [Edizioni e versioni di Exchange 2013](exchange-2013-editions-and-versions-exchange-2013-help.md).

Se non si immette un codice product key, il server viene concesso automaticamente come una versione di valutazione. Le funzioni di versione di valutazione semplicemente come un server Standard Edition Exchange ed è utile se si desidera provare Exchange prima di acquistare o eseguire in un laboratorio di test. L'unica differenza consiste è possibile utilizzare solo un server Exchange con contratto multilicenza come una versione di valutazione per un massimo di 180 giorni. Se si desidera continuare a utilizzare server oltre 180 giorni, è necessario immettere un codice "product key" o il centro di amministrazione di Exchange (EAC) verrà avviato mostrare i promemoria che è necessario immettere un codice "product key" per assegnare la licenza server.


> [!TIP]
> Alcuni visitatori di questa pagina ricercano informazioni su come installare o attivare Office. Se è questo il caso, consultare queste pagine: 
> <UL>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403360">Installare Office</A></P>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403361">Assistenza per il codice Product Key di Office</A></P></LI></UL>Se si desidera inserire un codice Product Key su un server Exchange&nbsp;2010, andare su <A href="http://go.microsoft.com/fwlink/p/?linkid=403370">Inserire un codice Product Key per Exchange 2010</A>.<BR>Se si desidera inserire un codice Product Key su un server Exchange 2013, consultare il seguente argomento. Continuare a leggere.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa procedura: meno di 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Codice Product Key" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Se si è acquisito una licenza per un server Exchange che esegue il ruolo di server della cassetta postale, sarà necessario riavviare il servizio Archivio informazioni di Microsoft Exchange sul server dopo aver inserito il codice Product Key.

  - Se si desidera aggiornare un server Exchange da una licenza Standard Edition a una Enterprise Edition, seguire i passaggi in questo argomento.

  - Se si desidera effettuare un downgrade di un server Exchange da una licenza Enterprise Edition a una Standard Edition, sarà necessario reinstallare Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Immissione del codice Product Key tramite EAC

1.  Aprire l'interfaccia di amministrazione di Exchange andando a https://\<*nome di dominio completo del server Accesso Client*\>/ecp.

2.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

3.  Andare a **Server** \> **Server**. Selezionare il server per cui si desidera la licenza, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  (Facoltativo) Se si desidera aggiornare il server da una licenza Standard Edition a una licenza Enterprise Edition, nella pagina **Generale**, selezionare **Cambia "Product Key"**. Sarà possibile visualizzare questa opzione solo se il server dispone già di licenza.

5.  Nella pagina **Generale**, immettere il proprio codice "Product Key" nelle caselle di testo **Immettere un codice "Product Key" valido**.

6.  Fare clic su **Salva**.

7.  Se si è acquisito una licenza per un server Exchange che esegue il ruolo di server della cassetta postale, riavviare il servizio Archivio informazioni di Microsoft Exchange come riportato di seguito:
    
    1.  Aprire **Pannello di controllo**, andare a **Strumenti di amministrazione**, quindi aprire **Servizi**.
    
    2.  Fare clic con il pulsante destro del mouse su **Archivio informazioni di Microsoft Exchange** e fare clic su **Riavvia**.

## Utilizzo della shell per immettere il codice "Product Key"

In questo esempio viene utilizzato il cmdlet **set-ExchangeServer** per immettere il codice "Product Key".


> [!NOTE]
> È possibile eseguire di nuovo questo comando sullo stesso server per aggiornarlo da una licenza Standard Edition a una licenza Enterprise Edition.



    Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ExchangeServer](https://technet.microsoft.com/it-it/library/bb123716\(v=exchg.150\)).

Se si è acquisito una licenza per un server Exchange che esegue il ruolo di server della cassetta postale, riavviare il servizio Archivio informazioni di Microsoft Exchange come riportato di seguito:

1.  Aprire **Pannello di controllo**, andare a **Strumenti di amministrazione**, quindi aprire **Servizi**.

2.  Pulsante destro del mouse **Archivio informazioni di Microsoft Exchange** e fare clic su **Riavvia**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare tramite EAC di aver ottenuto la licenza del server come Standard Edition o Enterprise Edition, procedere come segue:

1.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

2.  Andare a **Server** \> **Server**.

3.  Selezionare il server da visualizzare, quindi consultare il riquadro dei dettagli del server. Se il codice "Product Key" è stato accettato, apparirà la dicitura **Concesso in licenza** insieme all'edizione di Exchange 2013.

Per verificare tramite Shell di aver ottenuto la licenza del server come Standard Edition o Enterprise Edition, procedere come segue:

1.  Aprire Shell.

2.  Utilizzare il seguente comando per visualizzare lo stato di licenza di uno specifico server Exchange
    
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*

3.  (Facoltativo) Utilizzare il seguente comando per visualizzare lo stato di licenza di tutti i server Exchange dell'organizzazione.
    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto

