---
title: 'Creazione di un elenco di indirizzi: Exchange 2013 Help'
TOCTitle: Creazione di un elenco di indirizzi
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50481907
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# Creazione di un elenco di indirizzi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-12_

Gli elenchi indirizzi sono una raccolta di oggetti destinatario e altri oggetti Active Directory. ‎Ogni elenco indirizzi può contenere uno o più tipi di oggetti (ad esempio utenti, contatti, gruppi, cartelle pubbliche, conferenze e altre risorse). Gli elenchi indirizzi di forniscono anche un meccanismo per suddividere gli oggetti abilitati alla posta elettronica in Active Directory a vantaggio di gruppi specifici di utenti.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di elenchi di indirizzi tramite l'interfaccia di amministrazione di Exchange

1.  Passare a **Organizzazione** \> **Elenchi indirizzi**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  In **Elenco indirizzi** digitare un nome e specificare i tipi di destinatari da includere nell'elenco.

3.  Per impostazione predefinita, Exchange crea elenchi di indirizzi che contengono tutti i membri dell’organizzazione. Per creare un elenco di indirizzi personalizzato univoco, fare clic su **Aggiungi una regola**.
    

    > [!IMPORTANT]
    > Se non si intende aggiungere una regola, verrà creato un elenco di indirizzi ridondante con uno degli elenchi di indirizzi predefinito.



4.  Nell'elenco, selezionare un'opzione di filtro (ad esempio, **Attributo predefinito 1**).

5.  In **Specifica parole o frasi** digitare le parole o le frasi in base alle quali filtrare, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi fare clic su **OK**.
    
    Per continuare ad aggiungere alcune frasi o parole, ripetere il passaggio 4. Il filtro è un'istruzione booleana **OR**. Ad esempio, è possibile creare un filtro che applicherà l'elenco di indirizzi agli utenti il cui attributo Personalizzato 1 è uguale a **Oregon**, **Idaho** o **Washington**.

6.  (Opzionale) Fare di nuovo clic su **Aggiungi una regola** per aggiungere ulteriori filtri. I filtri aggiuntivi creano un'istruzione booleana **And**. Più filtri si creano, minore sarà il numero di utenti a cui sarà applicato l'elenco di indirizzi.

7.  Fare clic su **Visualizza un'anteprima dei destinatari inclusi nell'elenco di indirizzi** per visualizzare i destinatari a cui verrà applicato l'elenco di indirizzi.

8.  Fare clic su **Salva**.

9.  L'utente riceverà un messaggio di avviso con l'informazione che l'indirizzo non verrà applicato fino all'aggiornamento dell'indirizzo stesso. In base alle dimensioni dell'organizzazione e ai filtri aggiunti all'elenco di indirizzi, alcuni elenchi di indirizzi possono contenere migliaia o decine di migliaia di destinatari. L'aggiornamento degli elenchi di indirizzi può incidere sulle risorse, quindi potrebbe essere opportuno aggiornare l'indirizzo durante gli orari di scarso traffico.
    
    Per ulteriori informazioni sull'aggiornamento degli elenchi di indirizzi, vedere [Aggiornamento di un elenco di indirizzi](update-an-address-list-exchange-2013-help.md).

## Utilizzare la shell per creare un elenco indirizzi

In questo esempio viene creato l'elenco indirizzi MyAddressList utilizzando il parametro *RecipientFilter* e includendo i destinatari che sono utenti delle cassette postali e per i quali `StateOrProvince` è impostato su `Washington` o `Oregon`:
```powershell
    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}
```
In questo esempio viene creato l'elenco indirizzi secondario Building 34 Meeting Rooms nel contenitore principale All Rooms utilizzando condizioni incorporate.
```powershell
    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-AddressList](https://technet.microsoft.com/it-it/library/aa996912\(v=exchg.150\)).

