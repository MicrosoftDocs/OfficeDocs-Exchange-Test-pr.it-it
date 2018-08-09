---
title: 'Imposta numero prec. PIN segreteria telefonica: Exchange 2013 Help'
TOCTitle: Impostare il numero di precedente segreteria telefonica PIN riciclo
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50555664
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare il numero di precedente segreteria telefonica PIN riciclo

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

Quando gli utenti di Outlook Voice Access chiamano un numero di Outlook Voice Access, verrà richiesta l'immissione del PIN per l'autenticazione da parte del sistema di caselle vocali. Una volta autenticati, gli utenti potranno accedere alla casella vocale, alla posta elettronica, al calendario e alle informazioni personali sui contatti nella propria cassetta postale da un qualsiasi telefono.

È possibile configurare diverse impostazioni del PIN in un criterio cassetta postale di messaggistica unificata. L'impostazione **Numero di ricicli del PIN** consente di specificare il numero di PIN univoci che gli utenti devono utilizzare prima di poter riutilizzare un PIN precedente. Il valore di questa impostazione è compreso tra 1 e 20. Per quasi tutte le organizzazioni, il valore dovrebbe essere impostato su quello predefinito, ovvero su 5 PIN. Se il valore impostato è troppo alto, gli utenti potrebbero riscontrare qualche difficoltà nella creazione e nella memorizzazione di un numero elevato di PIN. Un valore troppo basso potrebbe costituire una minaccia al sistema di protezione della rete.


> [!IMPORTANT]
> Il numero di ricicli del PIN non può essere disabilitato.



Per ulteriori attività relative alla protezione del PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Modifica del numero di ricicli del PIN tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Fare clic su **Criteri PIN** e, accanto a **Numero di ricicli del PIN**, immettere un valore compreso tra 1 e 20.

5.  Fare clic su **Salva**.

## Modifica del numero di ricicli del PIN tramite Shell

Con questo esempio viene impostato su 10 il numero di ricicli del PIN per il criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

