---
title: 'Modifica/disabilita/rimuove criterio condivisione: Exchange 2013 Help'
TOCTitle: Modificare, disabilitare o rimuovere un criterio di condivisione
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 50480970
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare, disabilitare o rimuovere un criterio di condivisione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-15_

La condivisione dei criteri consente ai singoli utenti nell'organizzazione di Exchange di condividere le informazioni di disponibilità del calendario con altre organizzazione federate di Exchange, organizzazioni non federate di Exchange e singoli utenti di Internet. Nel corso delle normali operazioni, potrebbe essere necessario modificare alcune proprietà dei criteri di condivisione, come modificare le regole di condivisione, modificare il livello di accesso alla disponibilità del calendario, disattivare temporanemanete un criterio di condivisione o rimuoverlo completamente.

Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md)

Per informazioni dettagliate sulla creazione di un criterio di condivisione, vedere [Creare un criterio di condivisione](create-a-sharing-policy-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per modificare un criterio di condivisione

1.  Accedere a **Organizzazione** \> **Condivisione**.

2.  In **Condivisione singola** selezionare una condivisione e un criterio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Criteri di condivisione**, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  In **Regola di condivisione**, modificare di conseguenza le regole di condivisione. È possibile modificare le impostazioni come il dominio che si desidera condividere e il livello di condivisione per gli appuntamenti del calendario. Al termine, fare clic su **Salva** per chiudere la finestra di dialogo **Regole di condivisione**.

5.  In **Criteri di condivisione**, fare clic su **Salva** per aggiornare il criterio di condivisione.

## Utilizzo dell'interfaccia di amministrazione di Exchange per impostare un criterio di condivisione come criterio di condivisione predefinito

1.  Accedere a **Organizzazione** \> **Condivisione**.

2.  In **Condivisione singola** selezionare una condivisione e un criterio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Criteri di condivisione**, selezionare la casella di controllo **Imposta questo criterio come criterio di condivisione predefinito**.

4.  Fare clic su **Salva** per aggiornare il criterio di condivisione.

## Utilizzare l'interfaccia di amministrazione di Exchange per disattivare un criterio di condivisione

1.  Accedere a **Organizzazione** \> **Condivisione**.

2.  Sotto **Condivisione singola**, selezionare un criterio di condivisione.

3.  Nella colonna**Attivato**, deselezionare la casella di controllo per il criterio di condivisione che si desidera disattivare.

## Eliminazione di un criterio di condivisione tramite l'interfaccia di amministrazione di Exchange


> [!IMPORTANT]
> Prima di essere eliminato un criterio di condivisione deve essere eliminato da tutte le cassette postali degli utenti.



1.  Accedere a **Organizzazione** \> **Condivisione**.

2.  Sotto **Condivisione singola**, selezionare un criterio di condivisione, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Nell'avviso, fare clic su **Sì** per eliminare il criterio di condivisione.

## Modifica, disattivazione o eliminazione di un criterio di condivisione tramite Shell

  - Questo esempio modifica il criterio di condivisione Contoso per contoso.com, ossia un dominio all'esterno dell'organizzazione. Questo criterio consente agli utenti nel dominio Contoso di visualizzare informazioni di disponibilità semplice.
    
        Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'

  - Questo esempio aggiunge un secondo dominio al criterio di condivisione Contoso. Quando si aggiunge un dominio a un criterio esistente, è necessario includere tutti i domini inclusi in precedenza.
    
        Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'

  - In questo esempio il criterio di condivisione Contoso viene impostato come criterio di condivisione predefinita.
    
        Set-SharingPolicy -Identity Contoso -Default $True

  - In questo esempio viene disabilitato il criterio di condivisione Contoso.
    
        Set-SharingPolicy -Identity "Contoso" -Enabled $False

  - In questo esempio viene eliminato il criterio di condivisione Contoso. In questo secondo esempio viene rimosso il criterio di condivisione Contoso e viene eliminata la richiesta di conferma per la rimozione.
      
      ```
      Remove-SharingPolicy -Identity Contoso
      ```
      ```
      Remove-SharingPolicy -Identity Contoso -Confirm
      ```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-SharingPolicy](https://technet.microsoft.com/it-it/library/dd297931\(v=exchg.150\)) e [Remove-SharingPolicy](https://technet.microsoft.com/it-it/library/dd351071\(v=exchg.150\)).

