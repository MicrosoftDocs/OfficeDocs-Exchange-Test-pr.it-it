---
title: 'Modificare il banner SMTP su un connettore di ricezione: Exchange 2013 Help'
TOCTitle: Modificare il banner SMTP su un connettore di ricezione
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52063101
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modificare il banner SMTP su un connettore di ricezione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-08_

Il *banner SMTP* è la risposta alla connessione SMTP ricevuta da un server di messaggistica SMTP remoto dopo il collegamento a un connettore di ricezione configurato su un computer su cui viene eseguito Microsoft Exchange Server 2013.

Questa è la risposta predefinita ricevuta da un server di messaggistica SMTP remoto dopo il collegamento al connettore di ricezione:

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

Se si specifica un valore personalizzato per il banner SMTP su un connettore di ricezione, un server di messaggistica SMTP remoto collegato al connettore di ricezione SMTP riceve la seguente risposta.

    220 <Banner Text>

È possibile modificare il banner SMTP per i connettori di ricezione SMTP con connessione Internet in modo che il nome del server e il software del server di messaggistica non vengono rivelati dal banner SMTP.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Il testo del banner SMTP sostitutivo deve iniziare sempre con `220`. Come definito in RFC 2821, il codice di risposta SMTP di servizio pronto predefinito è 220.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Modifica del banner SMTP su un connettore di ricezione tramite Shell

Eseguire il comando indicato di seguito:

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

Con questo esempio viene modificato il banner SMTP sul connettore di ricezione esistente denominato "From the Internet" in modo che il banner SMTP visualizzi `220 Contoso Corporation`.

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

In questo esempio viene rimosso il banner SMTP personalizzato sul connettore di ricezione denominato "Form the Internet" ripristinando il valore predefinito del banner.

    Set-ReceiveConnector "From the Internet" -Banner $null

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il banner SMTP sia stato modificato correttamente su un connettore di ricezione, procedere come segue:

1.  Aprire il client telnet su un computer che possa accedere al connettore di ricezione ed eseguire il comando di seguito riportato:
    
        open <Connector FQDN or IP address> <Port>

2.  Verificare che la risposta del connettore di ricezione contenga il banner SMTP configurato.

Tenere presente che questa procedura funziona solo sui connettori di ricezione che consentono l'autenticazione anonima o di base. Per ulteriori informazioni, vedere [Utilizzare Telnet per testare le comunicazioni SMTP](use-telnet-to-test-smtp-communication-exchange-2013-help.md).

