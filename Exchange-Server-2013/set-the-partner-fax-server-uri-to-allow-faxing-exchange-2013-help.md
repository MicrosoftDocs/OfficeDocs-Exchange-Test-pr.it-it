---
title: "Impostare il partner fax URI del server a consentire l'invio di fax: Exchange 2013 Help"
TOCTitle: Impostare il partner fax URI del server a consentire l'invio di fax
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52057271
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare il partner fax URI del server a consentire l'invio di fax

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile abilitare e disabilitare i fax in ingresso per gli utenti associati a un criterio cassetta postale di messaggistica unificata. Per impostazione predefinita, quando vengono abilitati gli utenti per la messaggistica unificata, questi non possono ricevere messaggi fax fino all'abilitazione dei fax in ingresso nei criteri cassetta postale di messaggistica unificata e fino a che non viene specificato l'URI per il server fax del partner. Se gli URI sono configurati nei criteri cassetta postale di messaggistica unificata, ma l'opzione per consentire i fax in ingresso è disabilitata sul dial plan di messaggistica unificata o per un singolo utente, gli utenti abilitati alla messaggistica unificata collegati ai criteri cassetta postale di messaggistica unificata non potranno ricevere fax.

Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per altre attività di gestione relative all'invio e alla ricezione di fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzo dell'interfaccia di amministrazione di Exchange per impostare l'URI del partner fax

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Generale**, nella casella **URI del server fax partner**, inserire l'URI TCP o TLS. Ad esempio: *sip:faxserver1.contoso.com:5060;transport=tcp* oppure *sip:faxserver2.contoso.com:5061;transport=tls*
    

    > [!NOTE]
    > Sebbene la casella possa contenere più di un URI del server fax, ne verrà utilizzato solamente uno. Se vengono inseriti due URI, verrà utilizzato solamente il primo.



4.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzo di Shell per impostare l'URI del partner fax

Questo esempio consente agli utenti collegati con il criterio cassetta postale di messaggistica unificata `UMDialPlan Default Policy` a utilizzare TCP con la porta 5060 per il server fax partner `faxserver1`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

Questo esempio consente agli utenti collegati con il criterio cassetta postale di messaggistica unificata `UMDialPlan Default Policy` a utilizzare TLS con la porta 5061 per il server fax partner `faxserver2`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

