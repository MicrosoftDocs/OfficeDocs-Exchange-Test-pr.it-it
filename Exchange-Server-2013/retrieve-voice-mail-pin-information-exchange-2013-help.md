---
title: 'Recuperare le informazioni sul PIN di segreteria telefonica: Exchange 2013 Help'
TOCTitle: Recuperare le informazioni sul PIN di segreteria telefonica
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54652827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperare le informazioni sul PIN di segreteria telefonica

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-03_

È possibile recuperare le informazioni sul PIN per un utente che è abilitato per la messaggistica unificata. Dopo aver abilitato un utente per la messaggistica unificata e dopo aver generato o creato un PIN, quest'ultimo viene crittografato e archiviato nella cassetta postale dell'utente.

Quando vengono recuperate le informazioni sul PIN di un utente abilitato all'utilizzo della messaggistica unificata, le informazioni restituite vengono calcolate utilizzando i dati crittografati del PIN archiviati nella cassetta postale dell'utente. Questo consente di visualizzare le informazioni della cassetta postale dell'utente e di determinare se è stato bloccato l'accesso dell'utente alla cassetta postale.

Per le attività aggiuntive relative alla protezione del PIN, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md)

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare l'interfaccia di amministrazione di Exchange per recuperare le informazioni sul PIN per un utente abilitato alla messaggistica unificata

1.  In EAC accedere a **Destinatari**. Nella visualizzazione elenco selezionare la cassetta postale utente che si desidera visualizzare.

2.  Nel riquadro dei dettagli in **Funzionalità telefono e vocali** fare clic su **Visualizza dettagli**.

3.  Nella pagina **Cassetta postale di messaggistica unificata** \> **Impostazioni cassetta postale di messaggistica unificata**, visualizzare lo **stato del PIN** dell'utente. In questa pagina, è anche possibile ripristinare il PIN delle caselle vocali dell'utente.

## Utilizzo di Shell per recuperare le informazioni sul PIN di un utente abilitato alla messaggistica unificata

In questo esempio viene visualizzato l'ID utente, se un PIN è scaduto, la cassetta postale di messaggistica unificata è bloccata se Tony è al suo primo accesso.

    Get-UMMailboxPIN -identity tony@contoso.com

