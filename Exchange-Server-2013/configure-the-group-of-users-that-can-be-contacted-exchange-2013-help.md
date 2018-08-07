---
title: 'Configura gruppo di utenti che possono essere contattati: Exchange 2013 Help'
TOCTitle: Configurare il gruppo di utenti che possono essere contattati
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52057237
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il gruppo di utenti che possono essere contattati

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-09_

È possibile specificare il gruppo di utenti che è possibile contattare quando si chiama un operatore automatico di messaggistica unificata. Per impostazione predefinita, i chiamanti possono contattare gli utenti nello stesso dial plan associato all'operatore automatico di messaggistica unificata. Tuttavia, è possibile modificare il gruppo di utenti per consentire ai chiamanti di trasferire le chiamate o inviare messaggi vocali agli utenti che si trovano nell'elenco di indirizzi dell'organizzazione o a un determinato insieme di utenti.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Gestire un operatore automatico di messaggistica unificata](manage-a-um-auto-attendant-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione del gruppo di utenti contattabili tramite l'Interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera configurare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Accesso operatore e rubrica**, in **Opzioni per la ricerca nella rubrica**, scegliere dalle seguenti opzioni:
    
      - **Solo in questo dial plan**   Selezionare questa opzione per consentire ai chiamanti che si collegano all'operatore automatico di messaggistica unificata di individuare e contattare gli utenti all'interno del dial plan associato all'operatore automatico di messaggistica unificata.
    
      - **Nell'intera organizzazione**   Selezionare questa opzione per consentire ai chiamanti che si collegano all'operatore automatico di messaggistica unificata di individuare e contattare un utente elencato nella rubrica dell'organizzazione. Sono inclusi tutti gli utenti che sono abilitati all'utilizzo della cassetta postale.

4.  Fare clic su **Salva**.

## Configurazione del gruppo di utenti contattabili tramite Shell

In questo esempio viene impostato l'ambito degli utenti contattabili per tutti gli utenti elencati nella rubrica dell'organizzazione su un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

