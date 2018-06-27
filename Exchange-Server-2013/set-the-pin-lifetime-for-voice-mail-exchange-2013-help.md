---
title: 'Impostare la durata del PIN per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Impostare la durata del PIN per la segreteria telefonica
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50555698
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la durata del PIN per la segreteria telefonica

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile configurare la durata del PIN per gli utenti abilitati alla messaggistica unificata. La durata del PIN è il periodo massimo di validità per un PIN di Outlook Voice Access per i destinatari abilitati alla messaggistica unificata. Le impostazioni della durata del PIN sono configurate in un criterio cassetta postale di messaggistica unificata e si applicano a tutti gli utenti abilitati alla messaggistica unificata associati a tale criterio.

È possibile configurare diverse impostazioni del PIN in criteri di messaggistica unificata. L'impostazione di durata del PIN controlla l'intervallo di tempo, espresso in giorni, compreso tra la data dell'ultima modifica del PIN da parte dell'utente di Outlook Voice Access e quella in cui verrà richiesto di modificarlo nuovamente. L'intervallo è compreso tra 0 e 999 e il valore predefinito è 60 giorni. Se si immette 0, il PIN dell'utente non avrà scadenza. Si consiglia di non configurare l'impostazione su 0 perché in tal modo si riduce notevolmente la protezione della rete.


> [!IMPORTANT]
> Il sistema di messaggistica unificata non avvisa l'utente quando il PIN sta per scadere.



Per ulteriori attività relative alla protezione del PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione della durata del PIN tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Fare clic su **Criteri PIN** e, accanto a **Imponi durata PIN (giorni)**, immettere un valore compreso tra 0 e 999.

5.  Fare clic su **Salva**.

## Configurazione della durata del PIN tramite Shell

Con questo esempio viene impostato su 30 il numero di giorni di utilizzo di un PIN da parte degli utenti di Outlook Voice Access associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

Con questo esempio vengono configurate le seguenti impostazioni del PIN per gli utenti di Outlook Voice Access associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`:

  - Consente di impostare su 3 il numero di tentativi di accesso non riusciti prima della reimpostazione del PIN.

  - Consente di impostare su 5 il numero massimo di tentativi di accesso.

  - Consente di impostare su 9 cifre la lunghezza minima del PIN.

  - Consente di impostare su 40 giorni la durata del PIN.

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

