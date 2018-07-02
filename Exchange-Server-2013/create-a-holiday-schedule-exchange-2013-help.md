---
title: 'Creare una pianificazione di festività: Exchange 2013 Help'
TOCTitle: Creare una pianificazione di festività
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 50479979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una pianificazione di festività

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-19_

È possibile definire le date e gli orari di chiusura dell'organizzazione per festività e altri eventi. Nell'intervallo compreso tra le date di inizio e di fine specificate, i chiamanti che contattano l'operatore automatico di messaggistica unificata sentiranno il messaggio di saluto impostato durante la configurazione della pianificazione delle festività. Dopo il messaggio di saluto specificato, verranno riprodotti i messaggi di saluto per gli orari non di ufficio e i prompt menu.

Inoltre, è possibile creare una pianificazione delle festività all'interno di una pianificazione esistente. Se si creano più pianificazioni delle festività, la messaggistica unificata permette di sovrapporre gli orari di festività pianificati. Ad esempio, è possibile definire una pianificazione delle festività dal 15 al 31 dicembre quando l'organizzazione verrà chiusa per lavori, e un'altra pianificazione delle festività dal 24 al 26 dicembre. Se i chiamanti contattano l'operatore automatico tra il 15 e il 23 dicembre e tra il 27 e il 31 dicembre, verrà riprodotto il messaggio di saluto per le festività specificato per questa pianificazione. indicante, ad esempio, la chiusura dell'organizzazione per lavori. Se i chiamati contattano l'operatore automatico tra il 24 e il 26 dicembre, verrà riprodotto un altro messaggio di saluto per le festività indicante, ad esempio, la chiusura dell'organizzazione per le festività natalizie.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Definizione della pianificazione delle festività per un operatore automatico di messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera impostare la pianificazione delle festività. Sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") nella barra degli strumenti.

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Orario di ufficio**, in **Pianificazione festività**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella pagina **Nuova festività**, configurare quanto segue:
    
      - **Nome**   Immettere un nome per la pianificazione della festività.
    
      - **Messaggio di saluto festività**   Selezionare il file .wav che si desidera utilizzare come messaggio di saluto. Questo campo è obbligatorio.
    
      - **Data di inizio**   Utilizzare questo elenco per selezionare la data in cui si desidera far iniziare il periodo di festività. La pianificazione della festività inizierà dalla mezzanotte della data specificata in questo elenco.
    
      - **Data di fine**   Utilizzare questo elenco per selezionare la data in cui si desidera far terminare il periodo di festività. La pianificazione della festività terminerà alle 23:59 della data specificata in questo elenco.

5.  Una volta configurata la pianificazione delle festività, fare clic su **OK** e su **Salva**.

## Definizione della pianificazione delle festività per un operatore automatico di messaggistica unificata tramite Shell

In questo esempio, viene configurato l'operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` con gli orari di ufficio configurati su 10:45 - 13:15 (domenica), 09:00 - 17:00 (lunedì) e 09:00 - 16:30 (sabato) e il periodo di festività con i relativi messaggi di saluto configurati su "Buon anno" per il 2 gennaio 2013 e "Edificio chiuso per lavori" dal 24 al 28 aprile 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

