---
title: "Configurare l'elenco ricerca suffissi DNS per un spazio dei nomi disgiunto: Exchange 2013 Help"
TOCTitle: Configurare l'elenco ricerca suffissi DNS per un spazio dei nomi disgiunto
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 50481735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare l'elenco ricerca suffissi DNS per un spazio dei nomi disgiunto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

In questo argomento viene spiegato come utilizzare Group Policy Management Console (GPMC, Group Policy Management Console) per configurare l'elenco di ricerca suffissi DNS. In alcuni scenari di Exchange 2013, se è presente uno spazio dei nomi disgiunto, è necessario configurare l'elenco di ricerca suffissi DNS per includere più suffissi.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - Per eseguire questa procedura, è necessario utilizzare un account che disponga della delega di appartenenza al gruppo Domain Admins.

  - Verificare di aver installato .NET Framework 3.0 nel computer in cui verrà installato GPMC.
    

    > [!NOTE]
    > La versione corrente di GPMC che è possibile scaricare dall'Area download di Microsoft funziona con le versioni a 32 bit dei sistemi operativi Windows Server 2003 e Windows&nbsp;XP&nbsp;ed è in grado di gestire in remoto gli oggetti Criteri di gruppo su controller di dominio a 32 bit e 64 bit. Questa versione di GPMC non include una versione a 64 bit e la versione a 32 bit non è eseguibile su piattaforme a 64 bit. La versione a 32 bit di Windows Server 2008&nbsp;e la versione a 32 bit di Windows Vista&nbsp;includono entrambe una versione a 32 bit di GPMC. La versione a 64 bit di Windows Server 2008&nbsp;e la versione a 64 bit di Windows Vista&nbsp;includono entrambe una versione a 64 bit di GPMC.



  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione dell'elenco di ricerca suffissi DNS tramite GPMC

1.  In un computer a 32 bit nel dominio, installare Gestione criteri di GRUPPO con Service Pack 1 (SP1). Per informazioni sul download, vedere [Console Gestione criteri di gruppo con Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=100126).
    

    > [!NOTE]
    > Se nel dominio è disponibile un computer su cui è in esecuzione Windows Server 2008 o Windows Vista, è possibile saltare questo passaggio.



2.  Fare clic su **Start** \> **Programmi** \> **Strumenti di amministrazione** \> **Group Policy Management**.

3.  In **Gestione Criteri di gruppo** espandere la foresta e il dominio in cui verranno applicati i Criteri di gruppo. Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo**, quindi fare clic su **Nuovo**.

4.  In **Nuovo oggetto Criteri di gruppo** digitare un nome per il criterio, quindi fare clic su **OK**.

5.  Fare clic con il pulsante destro del mouse sul criterio creato nel passaggio 4, quindi fare clic su **Modifica**.

6.  In **Editor Gestione Criteri di gruppo**, espandere **Configurazione computer**, **Criteri**, **Modelli amministrativi**, **Rete**, quindi fare clic su **Client DNS**.

7.  Fare clic con il pulsante destro del mouse su **Elenco di ricerca suffissi DNS**, scegliere **Tutte le attività**, quindi fare clic su **Modifica**.

8.  Nella pagina **Proprietà elenco di ricerca suffissi DNS** selezionare **Abilitato**. Nella casella **Suffissi DNS** digitare il suffisso DNS primario del computer disgiunto, il nome del dominio DNS ed eventuali altri spazi dei nomi per altri server con i quali Exchange potrebbe interagire, ad esempio server di monitoraggio o server per applicazioni di terze parti. Fare clic su **OK**.

9.  In **Gestione Criteri di gruppo**, espandere **Oggetti Criteri di gruppo**, quindi selezionare il criterio creato nel passaggio 4. Nella scheda **Ambito**, applicare l'ambito al criterio in modo da applicarlo solamente ai computer non contigui.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Dopo aver installato Exchange 2013, verificare di poter inviare messaggi di posta elettronica all'interno e all'esterno dell'organizzazione.

## Ulteriori informazioni

[Criteri di gruppo di Windows](https://go.microsoft.com/fwlink/p/?linkid=100128)

[Criteri di gruppo](https://go.microsoft.com/fwlink/?linkid=268043)

[Scenari di spazio dei nomi disgiunto](disjoint-namespace-scenarios-exchange-2013-help.md)

