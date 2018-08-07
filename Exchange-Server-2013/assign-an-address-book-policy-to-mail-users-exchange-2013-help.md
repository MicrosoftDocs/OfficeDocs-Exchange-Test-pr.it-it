---
title: 'Assegna criterio Rubrica per gli utenti di posta: Exchange 2013 Help'
TOCTitle: Assegnare un criterio della Rubrica per gli utenti di posta
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 50481547
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Assegnare un criterio della Rubrica per gli utenti di posta

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-11_

Dopo aver creato un criterio della rubrica è necessario assegnarlo agli utenti delle cassette postali. Agli utenti non viene assegnato un criterio della rubrica predefinito alla creazione dell'account. Se non si assegna un criterio della rubrica a un utente, quest'ultimo potrà accedere all'Elenco indirizzi globale dell'intera organizzazione tramite Outlook e Outlook Web App. Per ulteriori informazioni, vedere [Criteri delle rubriche](address-book-policies-exchange-2013-help.md).

Per ulteriori attività di gestione relative ai criteri della rubrica, consultare [Procedure relative al criterio della Rubrica indirizzi](address-book-policy-procedures-exchange-2013-help.md).

Per gli utenti interessati agli scenari che utilizzano questa procedura vedere [Scenario: Distribuzione di criteri della Rubrica](scenario-deploying-address-book-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri delle rubriche" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di EMC per assegnare un criterio della rubrica a un utente della cassetta postale

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Nella visualizzazione elenco, selezionare l'utente a cui si desidera assegnare il criterio, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Fare clic su **Funzionalità delle cassette postali**.

4.  Nell'elenco **Criterio della rubrica** selezionare il criterio della rubrica da applicare all'utente.

5.  Fare clic su **Salva**.

## Utilizzo di EAC per assegnare un criterio rubrica a più utenti delle cassette postali

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Nella visualizzazione elenco utilizzare il tasto CTRL per selezionare più utenti.

3.  Nel riquadro dei dettagli, fare clic su **Altre opzioni**.

4.  In **Criterio della rubrica** fare clic su **Aggiorna**.

5.  Nell'elenco **Seleziona criterio della rubrica** selezionare il criterio della rubrica da applicare agli utenti.

6.  Fare clic su **Salva**.

## Utilizzare la Shell per assegnare un criterio della rubrica agli utenti delle cassette postali

In questo esempio il criterio della rubrica denominato All Fabrikam viene assegnato all'utente della cassetta postale esistente joe@fabrikam.com.

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

In questo esempio il criterio della rubrica denominato ABP\_EngineeringDepartment viene assegnato a tutti gli utenti di cassetta postale per cui il valore `CustomAttribute11` contiene "Engineering Department".

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).

