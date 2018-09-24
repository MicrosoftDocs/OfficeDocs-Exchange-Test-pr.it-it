---
title: "Configurare l'indirizzo postmaster esterno: Exchange 2013 Help"
TOCTitle: Configurare l'indirizzo postmaster esterno
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52063106
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare l'indirizzo postmaster esterno

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

L'indirizzo postmaster esterno viene utilizzato come mittente per i messaggi generati dal sistema e per le notifiche inviate ai mittenti esterni all'organizzazione di Microsoft Exchange Server 2013. Un mittente esterno è qualsiasi mittente con un indirizzo di posta elettronica in un dominio non configurato come dominio accettato nell'organizzazione.

Per impostazione predefinita, il valore dell'impostazione dell'indirizzo postmaster esterno è vuoto. Tale valore predefinito provoca il seguente comportamento nell'organizzazione di Exchange:

  - L'indirizzo postmaster esterno è postmaster@\<*Dominio accettato predefinito*\> per tutti i server Cassette postali e i server Trasporto Edge sottoscritti.

  - L'indirizzo postmaster esterno è postmaster@\<*Edge Transport server FQDN*\> per tutti i server Trasporto Edge non sottoscritti.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Configurazione di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Quando si configura un indirizzo postmaster esterno personalizzato, il valore si applica a tutti i Exchange 2013 server Cassette postali e Exchange 2010 ai server Trasporto Hub nell'organizzazione di Exchange. Tuttavia, il valore non viene replicato nei server Trasporto Edge. Se si specifica un valore personalizzato per l'indirizzo postmaster esterno, è necessario configurare manualmente il valore dell'indirizzo postmaster esterno in ogni server Trasporto Edge.

  - Se si dispone di un server Trasporto Hub Exchange 2007 o Trasporto Edge nell'organizzazione, è necessario configurare l'indirizzo postmaster esterno personalizzati in ognuno di questi server utilizzando il cmdlet **Set-TransportServer** . Per ulteriori informazioni, vedere [Gestione indirizzo Postmaster esterno](https://go.microsoft.com/fwlink/?linkid=279922).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Per saperne di più

## Utilizzare EAC per configurare l'indirizzo postmaster esterno

1.  Nell'interfaccia di amministrazione di Exchange, accedere alla scheda **Flusso di posta** \> **Connettori di ricezione** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **Impostazioni di trasporto nell'organizzazione** \> **Recapito**.

2.  Nel campo **Indirizzo postmaster esterno**, immettere l'indirizzo di posta elettronica SMTP, ad esempio, `postmaster@contoso.com`. Per reimpostare il valore predefinito dell'indirizzo postmaster esterno, eliminare tutti i valori esistenti affinché il campo sia vuoto.

3.  Al termine, scegliere **Salva**.

## Utilizzare Shell per configurare l'indirizzo postmaster esterno

Per configurare l'indirizzo postmaster esterno, utilizzare la sintassi seguente.

```powershell
Set-TransportConfig -ExternalPostmasterAddress <postmaster address>
```

Ad esempio, per impostare l'indirizzo postmaster esterno al valore `postmaster@contoso.com`, eseguire il seguente comando

```powershell
Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com
```

Per reimpostare il valore predefinito dell'indirizzo postmaster esterno, eseguire il comando seguente:

```powershell
Set-TransportConfig -ExternalPostmasterAddress $null
```

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta configurazione dell'indirizzo postmaster esterno, effettuare le seguenti operazioni:

1.  Eseguire il seguente comando su un server Cassette postali per verificare il valore dell'indirizzo postmaster esterno:
    
    ```powershell
    Get-TransportConfig | Format-List ExternalPostmasterAddress
    ```

2.  Da un account di posta elettronica esterno, inviare un messaggio all'organizzazione di Exchange che genererà una notifica sullo stato del recapito (DSN, Delivery Status Notification). Ad esempio, è possibile configurare una regola di trasporto per inviare un rapporto di mancato recapito per un messaggio contenente parole chiave specifiche. Verificare che l'indirizzo di posta elettronica del mittente nel DSN corrisponda al valore specificato.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

