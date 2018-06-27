---
title: 'Visualizzazione dei membri di un gruppo di distribuzione dinamico: Exchange 2013 Help'
TOCTitle: Visualizzazione dei membri di un gruppo di distribuzione dinamico
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 50479723
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzazione dei membri di un gruppo di distribuzione dinamico

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2018-03-02_

I gruppi di distribuzione dinamici sono particolari gruppi di distribuzione nei quali l'appartenenza si basa su specifici filtri dei destinatari piuttosto che su un gruppo definito di destinatari. MicrosoftExchange fornisce una serie di filtri predefiniti che semplificano la creazione dei filtri dei destinatari per i gruppi di distribuzione dinamici. Un *filtro predefinito* è un filtro di uso comune che può essere utilizzato per soddisfare un'ampia gamma di criteri di filtro destinatario. È possibile specificare i tipi di destinatari che si desidera includere nel gruppo di distribuzione dinamico. È inoltre possibile specificare un elenco di condizioni che i destinatari devono soddisfare. Shell consente di visualizzare l'anteprima dell'elenco dei destinatari per un gruppo di distribuzione dinamico che utilizza filtri predefiniti.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione dinamici" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare Shell per visualizzare in anteprima l'elenco dei membri di un gruppo di distribuzione dinamico

In questo esempio viene restituito l'elenco dei membri per il gruppo di distribuzione dinamico denominata dipendenti a tempo pieno. Il primo comando viene archiviato l'oggetto gruppo di distribuzione dinamico nella variabile `$FTE`. Il secondo comando utilizza il cmdlet **Get-Recipient** per elencare i destinatari che soddisfano i criteri definiti per il gruppo di distribuzione dinamico.

    $FTE = Get-DynamicDistributionGroup "Full Time Employees"

    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb124762\(v=exchg.150\)) e [Get-Recipient](https://technet.microsoft.com/it-it/library/aa996921\(v=exchg.150\)).


> [!NOTE]
> È possibile visualizzare i membri di un gruppo di distribuzione dinamici utilizzando la shell.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente visualizzati i membri di un gruppo di distribuzione dinamico, eseguire le operazioni seguenti:

  - In Shell, quando si esegue il suddetto comando per visualizzare l'anteprima di un elenco dei membri di un gruppo di distribuzione dinamico, viene restituito un elenco dei membri. Ad esempio, se è stata creata una nuova cassetta postale utente le cui proprietà corrispondono al filtro destinatari del gruppo di distribuzione dinamico, questo nuovo utente verrà visualizzato nell'elenco dei membri del gruppo.

