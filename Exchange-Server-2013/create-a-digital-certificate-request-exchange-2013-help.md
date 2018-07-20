---
title: 'Creare una richiesta di certificato digitale: Exchange 2013 Help'
TOCTitle: Creare una richiesta di certificato digitale
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52063117
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una richiesta di certificato digitale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-21_

In Exchange Server 2013,è possibile gestire i certificati tramite EAC o Shell. EAC include una nuova interfaccia utente per la gestione dei certificati. Tramite questa nuova interfaccia è possibile creare un nuovo certificato, modificarne uno esistente o rimuovere un certificato.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti più il tempo per cui si attende la risposta dell'autorità di certificazione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione del server Accesso client" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di una nuova richiesta di certificato tramite EAC

1.  In EAC, andare a **Server** \> **Certificati**.

2.  Nell'elenco **Seleziona server**, selezionare il server per cui si desidera creare un certificato e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella procedura guidata **Nuovo certificato di Exchange**, scegliere **Crea la richiesta per un certificato emesso da un'autorità di certificazione** o **Crea un certificato autofirmato** e selezionare **Avanti**.

4.  Immettere un nome significativo per il certificato e selezionare **Avanti**.

5.  Se non è stato scelto un certificato autofirmato e si desidera un certificato con caratteri jolly, selezionare la casella **Richiedi un certificato con caratteri jolly**, immettere il dominio radice, ad esempio \*.contoso.com, e selezionare **Avanti**. Se è stato scelto un certificato autofirmato, ignorare questo passaggio.

6.  Selezionare i server a cui applicare il certificato e selezionare **Avanti**.

7.  Specificare i domini da includere nel certificato e selezionare **Avanti**.

8.  Verificare che i domini inclusi siano corretti. Se è stato scelto un certificato autofirmato, selezionare **Fine**. Altrimenti selezionare **Avanti**.

9.  Immettere il nome dell'organizzazione, il nome del reparto, la città o località, lo stato, il paese e selezionare **Avanti**.

10. Immettere un percorso in cui salvare la richiesta di certificato e selezionare **Fine**.

Se non è stato selezionato un certificato autofirmato, sarà necessario inviare il file della richiesta di certificato all'autorità di certificazione per l'elaborazione.

## Creazione di una nuova richiesta di certificato tramite Shell

Eseguire i comandi riportati di seguito.
  ```
  $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true
  ```
  ```
  $reqfile | out-file c:\certreq.txt
  ```

## Come verificare se l'operazione ha avuto esito positivo

Se è stato creato un certificato autofirmato, il certificato appena creato apparirà nell'interfaccia utente per la gestione dei certificati. Se è stata creata una richiesta di certificato da un'autorità di certificazione, il file della richiesta di certificato si troverà nel percorso specificato. Inviare il file all'autorità di certificazione.

