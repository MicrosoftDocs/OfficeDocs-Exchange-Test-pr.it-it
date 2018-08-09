---
title: "Autorizza chiamate dell'operatore automatico: Exchange 2013 Help"
TOCTitle: Autorizzare chiamate per i chiamanti dell'operatore automatico
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51407410
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzare chiamate per i chiamanti dell'operatore automatico

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile abilitare le autorizzazioni di composizione per un operatore automatico di messaggistica unificata. Le autorizzazioni di composizione su un operatore automatico vengono utilizzate per impedire agli utenti che chiamano l'operatore automatico di effettuare telefonate nazionali o internazionali o *chiamate esterne*. La composizione di chiamate esterne avviene quando la messaggistica unificata effettua una chiama in uscita per un utente dopo che tale utente ha chiamato un numero configurato in un operatore automatico di messaggistica unificata.

Per altre attività di gestione relative alla composizione di chiamate esterne, vedere [Che consente agli utenti di effettuare chiamate procedure](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che le regole di composizione nazionali e internazionali siano state create in un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creare regole di composizione per gli utenti](create-dialing-rules-for-users-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per abilitare le autorizzazioni di composizione su un operatore automatico di messaggistica unificata per gruppi di regole nazionali

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera creare un'autorizzazione di composizione, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Autorizzazione di composizione**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") sotto **Gruppi di regole di composizione nazionali consentiti**.

4.  Nella pagina **Seleziona gruppi di regole di composizione da consentire**, selezionare il gruppo di regole di composizione e fare clic su **OK**, quindi scegliere **Salva**.

## Utilizzo di EAC per abilitare le autorizzazioni di composizione su un operatore automatico di messaggistica unificata per gruppi di regole internazionali

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera creare un'autorizzazione di composizione, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Autorizzazione di composizione**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") sotto **Gruppi di regole di composizione internazionali consentiti**.

4.  Nella pagina **Seleziona gruppi di regole di composizione da consentire**, selezionare il gruppo di regole di composizione e fare clic su **OK**, quindi scegliere **Salva**.

## Utilizzo di Shell per abilitare le autorizzazioni di composizione nazionali e internazionali su un operatore automatico di messaggistica unificata

Con questo esempio vengono abilitate le restrizioni di composizione InCountry/RegionGroup1, InCountry/RegionGroup2. Autorizzazioni di composizione InternationalGroup1 e InternationalGroup2 su un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

