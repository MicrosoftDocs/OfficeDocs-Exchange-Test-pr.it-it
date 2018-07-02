---
title: 'Applicare un criterio di condivisione alle cassette postali: Exchange 2013 Help'
TOCTitle: Applicare un criterio di condivisione alle cassette postali
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 50481854
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Applicare un criterio di condivisione alle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-15_

I criteri di condivisione fanno parte della condivisione federata e consentono la condivisione stabilita dall'utente e tra utenti delle informazioni di calendario con tipi diversi di utenti esterni. Il criterio di condivisione che un amministratore applica alla cassetta postale dell'utente consente di determinare il livello di accesso che un utente può condividere e con chi. Se non vengono modificate impostazioni, il criterio di condivisione predefinito viene applicato a tutti gli utenti. Se si crea un nuovo criterio di condivisione, è necessario applicarlo alle cassette postali prima che diventi effettivo. Il criterio di condivisione può essere applicato alla cassetta postale di un singolo utente o alle cassette postali di più utenti contemporaneamente. Un amministratore può disabilitare il criterio di condivisione di un utente al fine di impedire accessi esterni ai calendari.

Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere La voce *Recipient Provisioning Permissions* nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Deve essere presente un criterio di condivisione. Per ulteriori informazioni, vedere [Creare un criterio di condivisione](create-a-sharing-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Applicazione di un criterio di condivisione a un'unica cassetta postale tramite l'interfaccia di amministrazione di Exchange

1.  Accedere a **destinatari** \> **cassette postale**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale desiderata e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Cassetta postale utente**, fare clic su **funzionalità delle cassette postali**.

4.  Nell'elenco **Criteri di condivisione** selezionare il criterio di condivisione da applicare alla cassetta postale.

5.  Fare clic su **salva** per applicare il criterio di condivisione.

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'applicazione di un criterio di condivisione a più cassette postali

1.  Accedere a **destinatari** \> **cassette postale**.

2.  Nella visualizzazione elenco, tenere premuto il tasto CTRL mentre si selezionano più cassette postali.

3.  Nel riquadro dei dettagli, le proprietà delle cassette postali saranno configurate per la modifica in blocco. Fare clic su **Altre opzioni**.

4.  In **Criteri di condivisione** fare clic su **Aggiorna**.

5.  In **assegnazione in blocco dei criteri di condivisione**, utilizzare l'elenco **Seleziona criterio di condivisione** per selezionare un criterio di condivisione da assegnare alle cassette postali.

6.  Fare clic su **salva** per applicare il criterio di condivisione alle cassette postali selezionate.

## Applicazione di un criterio di condivisione a una o più cassette postali tramite Shell

In questo esempio il criterio di condivisione Contoso viene applicato a un'unica cassetta postale dell'utente Barbara.

    Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"

In questo esempio viene specificato che tutte le cassette postali dell'utente nel reparto Marketing utilizzano il criterio di condivisione Contoso Marketing.

    Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"

In questo esempio vengono restituite tutte le cassette postali a cui è stato applicato il criterio di condivisione Contoso e gli utenti vengono ordinati in una tabella che visualizza solo gli alias e gli indirizzi di posta elettronica.

    Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta applicazione del criterio di condivisione alla cassetta postale di un utente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**, quindi selezionare la cassetta postale a cui è stato applicato il criterio di condivisione. Fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"), quindi su **funzionalità delle cassette postali** e confermare che il criterio di condivisione appropriato viene visualizzato nell'elenco **Criteri di condivisione**.

  - Eseguire il comando della shell riportato di seguito per verificare che il criterio di condivisione sia stato assegnato alla cassetta postale di un utente. Verificare che il criterio di condivisione corretto sia elencato nel parametro *SharingPolicy*.
    
        Get-Mailbox <user name> | format-list


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


