---
title: 'Creazione di una cassetta postale di cartelle pubbliche: Exchange 2013 Help'
TOCTitle: Creazione di una cassetta postale di cartelle pubbliche
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 50480773
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creazione di una cassetta postale di cartelle pubbliche

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2014-10-23_

Prima di creare una cartella pubblica, dapprima è necessario creare una cassetta postale della cartella pubblica. Le cassette postali della cartella pubblica contengono le informazioni gerarchiche oltre al contenuto per le cartelle pubbliche. La prima cassetta postale della cartella pubblica che si crea è rappresentata dalla principale cassetta postale in base alla gerarchia e contiene l'unica copia scrivibile della gerarchia. Ulteriori casette postali della cartelle pubbliche create sono di ordine secondario e contengono una copia di sola lettura della gerarchia.


> [!NOTE]
> Per ulteriori informazioni sulle quote di archiviazione e sui limiti relativi alle cartelle pubbliche, consultare i seguenti argomenti: 
> <UL>
> <LI>
> <P>Per ulteriori informazioni sulle cartelle pubbliche di Office 365, vedere <A href="https://go.microsoft.com/fwlink/?linkid=391188">Limiti di Exchange Online</A>.</P>
> <LI>
> <P>Per informazioni sulle cartelle pubbliche su Exchange Server 2013 locale, vedere <A href="limits-for-public-folders-exchange-2013-help.md">Limiti per le cartelle pubbliche</A>.</P></LI></UL>



Per ulteriori attività di gestione relative alle cartelle pubbliche in Exchange 2013, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche in Exchange Online, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 5 minuti.

  - Le cartelle pubbliche di Exchange 2013 e le cartelle pubbliche nei server Exchange legacy non possono esistere contemporaneamente nell'organizzazione. Se si tenta di creare una cassetta postale di cartelle pubbliche quando si dispone ancora di cartelle pubbliche legacy, viene visualizzato l'errore **È stata rilevata una distribuzione di cartelle pubbliche esistente. Per migrare i dati delle cartelle pubbliche esistenti, creare una nuova cassetta postale delle cartelle pubbliche utilizzando l'opzione -HoldForMigration switch.**
    
    Prima di creare cartelle pubbliche in Exchange 2013, è necessario eseguire la migrazione delle cartelle pubbliche legacy a Exchange 2013. A tale scopo, seguire la procedura in [Utilizzo della migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti](https://technet.microsoft.com/it-it/library/jj150486\(v=exchg.150\)). Questi passaggi mostrano come creare una cassetta postale di cartelle pubbliche che può essere utilizzata per archiviare le cartelle pubbliche migrate.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Creazione di una cartella pubblica tramite l'interfaccia di amministrazione di Exchange

1.  Accedere a **Cartelle pubbliche** \> **Cassette postali delle cartelle pubbliche**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Cassetta postale delle cartelle pubbliche**, specificare un nome per la cassetta postale delle cartelle pubbliche.

3.  Fare clic su **Salva**.

## Creazione di una cassetta postale delle cartelle pubbliche tramite Shell

In questo esempio viene creata la cassetta postale principale delle cartelle pubbliche.

    New-Mailbox -PublicFolder -Name MasterHierarchy

In questo esempio viene creata una cassetta postale secondaria delle cartelle pubbliche. L'unica differenza tra la creazione della cassetta postale principale e di una cassetta postale secondaria è che quella principale viene antecedentemente creata all'interno dell'organizzazione. È possibile creare ulteriori cassette postali delle cartelle pubbliche per bilanciare il carico.

    New-Mailbox -PublicFolder -Name Istanbul 

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la cassetta postale delle cartelle pubbliche principale sia stata creata correttamente, eseguire il seguente comando di Shell:

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997571\(v=exchg.150\)).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

