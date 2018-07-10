---
title: 'Aggiornamento di un elenco di indirizzi: Exchange 2013 Help'
TOCTitle: Aggiornamento di un elenco di indirizzi
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 50480041
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: MT
---

# Aggiornamento di un elenco di indirizzi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-14_

Gli elenchi indirizzi sono una raccolta di oggetti destinatario e altri oggetti Active Directory. Applicare un elenco di indirizzi una volta modificata la regola del filtro dell'elenco di indirizzi. Per aggiornare l'appartenenza all'elenco di indirizzi per includere nuovi destinatari e rimuovere i destinatari che non soddisfano più i criteri di filtro, è necessario applicare l'elenco di indirizzi.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Il completamento di questo processo potrebbe richiede più tempo in base al numero di destinatari presenti nell'elenco indirizzi.

  - Alcuni elenchi indirizzi contengono migliaia o decine di migliaia di destinatari a seconda della dimensione dell'organizzazione e dei filtri aggiunti all'elenco indirizzi. L'aggiornamento degli elenchi indirizzi può occupare una notevole quantità di risorse del computer. Quindi, può essere opportuno aggiornare l'elenco indirizzi nelle ore di minor traffico.

  - Se l'elenco indirizzi contiene 3.000 destinatari, è consigliabile utilizzare Exchange Management Shell per aggiornare l'elenco indirizzi.

Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'aggiornamento di un elenco indirizzi

1.  Accedere a **Organizzazione** \> **Elenchi di indirizzi**.

2.  Nell'elenco, selezionare l'elenco indirizzi che si desidera aggiornare.

3.  Nel riquadro dei dettagli, fare clic su **Aggiorna**.

## Utilizzo di Shell per l'aggiornamento di un elenco indirizzi

In questo esempio, viene applicato l'elenco indirizzi Washington State.

    Update-AddressList "Washington State"

Se si dispone di più elenchi di indirizzi con lo stesso nome, è necessario specificare il percorso completo per l'elenco di indirizzi che si desidera aggiornare. Ad esempio, se si desidera aggiornare l'elenco di indirizzi Vendite sotto Nord America, ma è presente un elenco di indirizzi Vendite anche sotto Europa, utilizzare il seguente comando:

    Update-AddressList "North America\Sales"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Update-AddressList](https://technet.microsoft.com/it-it/library/aa997982\(v=exchg.150\)).

