---
title: 'Creazione di un dial plan di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Creazione di un dial plan di messaggistica unificata
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 50481241
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: MT
---

# Creazione di un dial plan di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-16_

Un dial plan di messaggistica unificata contiene le informazioni di configurazione relative alla rete telefonica. Un dial plan di messaggistica unificata stabilisce un collegamento da un numero di interno telefonico di un utente abilitato alla segreteria telefonica alla relativa cassetta postale. Quando si crea un dial plan di messaggistica unificata, è possibile configurare il numero di cifre di un numero interno, il tipo di URI (Uniform Resource Identifier) e le impostazioni di protezione VoIP (Voice over IP) per il dial plan.

Ogni volta che viene creato un dial plan di messaggistica unificata, viene creato anche un criterio cassetta postale di messaggistica unificata. Il criterio cassetta postale di messaggistica unificata viene denominato Criterio predefinito \<*DialPlanName*\>.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzare EAC per creare un dial plan di messaggistica unificata

1.  
    
    In EAC accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata** e fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata**, completare le seguenti caselle:
    
      - **Nome** Digitare il nome del dial plan. Il nome del dial plan di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, viene utilizzato solo per la visualizzazione in EAC e in Shell. Se si desidera modificare il nome visualizzato del dial plan al termine del processo di creazione, prima è necessario eliminare il dial plan esistente e crearne un'altro con il nome corretto. Se l'organizzazione utilizza più dial plan di messaggistica unificata, si consiglia di utilizzare nomi significativi per tali dial plan. La lunghezza massima per il nome di un dial plan di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Anche se è possibile includere spazi nel nome di un dial plan di messaggistica unificata, è necessario evitare l'uso degli spazi se la messaggistica unificata viene integrata con Office Communications Server 2007 R2 o Microsoft Lync Server. Di conseguenza, se è stato creato un dial plan con spazi nel nome visualizzato e la messaggistica unificata viene integrata con Office Communications Server 2007 R2 o Lync Server, è necessario prima eliminare il dial plan, quindi crearne un altro il cui nome visualizzato non contenga spazi.
        

        > [!IMPORTANT]
        > Anche se la casella per il nome del dial plan può contenere fino a 64 caratteri, il nome del dial plan non può superare i 49 caratteri. Se si cerca di creare un nome di dial plan che contiene più di 49 caratteri, verrà visualizzato un messaggio di errore. Il messaggio indicherà che non è possibile generare criteri per le cassette postali di messaggistica unificata, poiché il nome del dial plan di messaggistica unificata è troppo lungo. Ciò accade perché, come precedentemente affermato, quando si crea un dial plan, viene creato anche un criterio per le cassette postali di messaggistica unificata predefinito nominato criterio predefinito <EM>&lt;DialPlanName&gt;</EM>. Quando i 15 caratteri nel criterio predefinito vengono aggiunti al nome del dial plan, i caratteri totali superano il limite. Il parametro <EM>name</EM> può contenere 64 caratteri per il dial plan e il criterio cassetta postale di messaggistica unificata. Tuttavia, se il nome del dial plan è più lungo di 49 caratteri, il nome del criterio cassetta postale di messaggistica unificata predefinito sarà più lungo di 64 caratteri e il sistema non lo consente.

    
      - **Lunghezza numero interno (cifre)**  Immettere il numero di cifre per il dial plan. Il numero di cifre per i numeri degli interni è basato sul dial plan di telefonia creato su un PBX (Private Branch eXchange) o su un IP-PBX. Ad esempio, se un utente associato a un dial plan di telefonia compone un numero di interno di quattro cifre per chiamare un altro utente nello stesso dial plan, occorre selezionare 4 come numero di cifre dell'interno.
        
        Questa è una casella obbligatoria che ha un intervallo di valori che va da 1 a 20. La lunghezza dell'interno tipica va da 3 a 7. Se l'ambiente di telefonia esistente include numeri di interni, è necessario specificare un numero di cifre che corrisponda al numero di cifre presenti in tali interni.
        
        Quando viene creato un dial plan SIP o E.164 e al dial plan viene associato un utente abilitato alla messaggistica unificata, è necessario inserire comunque un numero di interno relativo all'utente. Questo numero viene utilizzato dagli utenti di Outlook Voice Access per accedere alla cassetta postale.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Protezione UI\_VoIP)
    
      - **Lingua audio**   Questo elenco consente di specificare la lingua predefinita che deve essere utilizzata dagli utenti di Outlook Voice Access. Questa impostazione non si applica all'impostazione della lingua per un operatore automatico di messaggistica unificata. È possibile impostare per Outlook Voice Access la stessa lingua utilizzata da un operatore automatico di messaggistica unificata oppure una lingua diversa. Quando un utente effettua una chiamata a un utente associato al dial plan, la lingua audio è la lingua predefinita utilizzata dall'operatore per i messaggi registrati. Le istruzioni vocali del sistema che verranno ascoltate dall'utente sono riprodotte nella stessa lingua. La lingua scelta nel dial plan di messaggistica unificata è utilizzata per leggere i messaggi di posta elettronica, i messaggi vocali e gli elementi di calendario, pronunciare il nome dell'utente se non è stato registrato un messaggio di saluto personale, trascrivere un messaggio vocale utilizzando la funzionalità Anteprima segreteria telefonica, abilitare il funzionamento corretto del riconoscimento vocale automatico.
    
      - **Codice paese**   Utilizzare questa casella per digitare il numero del codice paese utilizzato per le chiamate in uscita. Questo numero precederà il numero di telefono composto. La casella consente di immettere da 1 a 4 cifre. Ad esempio, negli Stati Uniti il codice paese è 1, nel Regno Unito è 44.

3.  Fare clic su **Salva**.

## Creazione di un dial plan di messaggistica unificata tramite Shell

In questo esempio viene creato un nuovo dial plan di messaggistica unificata denominato `MyUMDialPlan` che utilizza numeri di interni a 4 cifre.

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

In questo esempio viene creato un nuovo dial plan di messaggistica unificata denominato `MyUMDialPlan` che utilizza numeri di interno a 5 cifre e che supporta gli URI SIP.

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

