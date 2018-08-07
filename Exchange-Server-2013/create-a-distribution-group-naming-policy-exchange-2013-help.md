---
title: 'Crea gruppo distribuzione dei criteri di denominazione: Exchange 2013 Help'
TOCTitle: Creare un gruppo di distribuzione dei criteri di denominazione
ms:assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218693(v=EXCHG.150)
ms:contentKeyID: 50479781
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un gruppo di distribuzione dei criteri di denominazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-01_

Tramite i *criteri di denominazione dei gruppi* è possibile standardizzare e gestire i nomi dei gruppi di distribuzione creati dagli utenti nell'organizzazione. È possibile richiedere un prefisso e un suffisso specifici da aggiungere al nome per il gruppo di distribuzione al momento della creazione e bloccare l'utilizzo di parole specifiche. In questo modo, viene ridotto l'utilizzo di parole inadatte nei nomi del gruppo.

I criteri di denominazione dei gruppi:

  - Applicano una strategia di denominazione coerente per i gruppi creati dagli utenti.

  - Identificano gruppi di distribuzione nella rubrica condivisa.

  - Suggeriscono la funzione o l'appartenenza del gruppo.

  - Identificano i tipi di utenti probabili membri del gruppo.

  - Identificano l'area geografica nella quale viene utilizzato il gruppo.

  - Bloccano le parole inadatte nei nomi di gruppo.

Modalità di funzionamento dei criteri di denominazione dei gruppi Quando un utente crea un gruppo, specifica un nome nel campo Nome visualizzato. Dopo la creazione del gruppo, in Microsoft Exchange vengono applicati i criteri di denominazione dei gruppi mediante l'aggiunta di un prefisso o di un suffisso definito in tali criteri. Il nome completo viene visualizzato nell'elenco dei gruppi di distribuzione in Interfaccia di amministrazione di Exchange nella rubrica condivisa e nei campi A, Cc e Da. campi nei messaggi di posta elettronica. Se un utente tenta di utilizzare una parola bloccata, al tentativo di salvare il nuovo gruppo verrà visualizzato un messaggio di errore e verrà richiesto di rimuovere la parola bloccata e salvare nuovamente il gruppo.

Di seguito vengono riportati alcuni esempi dei criteri di denominazione dei gruppi. In ciascun esempio, **\<Nome gruppo\>** è un nome descrittivo fornito dalla persona che crea il gruppo. In Exchange vengono aggiunti nel nome visualizzato i prefissi e i suffissi definiti dai criteri quando viene creato il gruppo.

  - Stringhe di testo, con caratteri di sottolineatura, utilizzate per un solo prefisso (**DG**) e suffisso (**Users**):
    
    **DG\_\<Group Name\>\_Users**

  - Più prefissi (**DG** e **Contoso**) e un suffisso (**Utenti**), mediante stringhe di testo:
    
    **DG\_Contoso\_\<Group Name\>\_Users**

  - Un attributo (**Department**) utilizzato per il prefisso:
    
    **Department\_\<Group Name\>**
    
    Ad esempio, si supponga che una scuola compili l'attributo Facoltà per i docenti. Di seguito, viene fornito un esempio di nome di gruppo creato da un docente della facoltà di Psicologia:
    
    **Psicologia\_Cognitiva201**
    
    In questo esempio, il carattere di sottolineatura (\_) viene fornito come unica stringa di testo di un secondo prefisso per separare il nome della facoltà dal nome del gruppo.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - La lunghezza massima per il nome di un gruppo è 64 caratteri. Questo valore include il numero combinato di caratteri di prefisso, nome del gruppo fornito dall'utente e suffisso.

  - I criteri di denominazione dei gruppi sono applicati solo ai gruppi creati dagli utenti. Quando l'utente o un amministratore utilizza Interfaccia di amministrazione di Exchange per creare gruppi di distribuzione, i criteri di denominazione dei gruppi vengono ignorati e non vengono applicati al nome del gruppo.

  - I nomi di gruppo vengono creati senza spazi. Si consiglia di utilizzare un carattere di sottolineatura (\_) o un altro segnaposto tra le stringhe di testo, gli attributi e il nome del gruppo.

  - È possibile utilizzare Windows PowerShell per ignorare i criteri di denominazione dei gruppi quando si crea e si modifica un gruppo di distribuzione. Per ulteriori informazioni, vedere [Eseguire l'override del gruppo di distribuzione dei criteri di denominazione](override-the-distribution-group-naming-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare Interfaccia di amministrazione di Exchange per creare i criteri di denominazione dei gruppi

1.  In EAC, selezionare **gruppi** \> **ulteriori**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **gruppo configurazione dei criteri di denominazione**.

2.  In **Criteri di denominazione dei gruppi** configurare il prefisso selezionando **Attributo** o **Testo** nel menu a discesa.
    
      - **Attributo**   Selezionare l'attributo e fare clic su **OK**.
    
      - **Testo**   Digitare la stringa di testo e fare clic su **OK**.
    
    Si noti che la stringa di testo digitata o l'attributo selezionato viene visualizzato come collegamento ipertestuale. Fare clic sul collegamento ipertestuale per modificare la stringa di testo o l'attributo.

3.  Fare clic su **Aggiungi** per aggiungere altri prefissi.

4.  Per il suffisso, nel menu a discesa selezionare **Attributo** o **Testo** e configurare il suffisso.

5.  Fare clic su **Aggiungi** per aggiungere altri suffissi.
    
    Dopo l'aggiunta di un prefisso o di un suffisso, viene visualizzata un'anteprima dei criteri di denominazione dei gruppi.

6.  Per eliminare un prefisso o un suffisso dai criteri, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

7.  Fare clic su **Parole bloccate** per aggiungere o rimuovere le parole bloccate.
    
      - Per aggiungere una parola all'elenco, digitare la parola da bloccare e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").
    
      - Per rimuovere una parola dall'elenco, selezionarla e fare clic su **Rimuovi**.
    
      - Per modificare una parola bloccata esistente, selezionarla e fare clic su **Modifica**.

8.  Al termine, fare clic su **Save**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione dei criteri di denominazione dei gruppi, effettuare le seguenti operazioni:

  - In Stima al completamento selezionare **Gruppi** \> **Altri** \> **Configura criteri di denominazione dei gruppi**.
    
    Nella pagina **Criteri di denominazione dei gruppi** i criteri di denominazione dei gruppi definiti dall'utente sono visualizzati sotto **Anteprima dei criteri**.

  - In Windows PowerShell eseguire il comando riportato di seguito per visualizzare i criteri di denominazione dei gruppi.
    
        Get-OrganizationConfig | FL DistributionGroupNamingPolicy

