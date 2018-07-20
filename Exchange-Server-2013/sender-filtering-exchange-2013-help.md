---
title: 'Filtro mittente: Exchange 2013 Help'
TOCTitle: Filtro mittente
ms:assetid: b833f864-ff10-46a0-a653-28fb9ba30896
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124354(v=EXCHG.150)
ms:contentKeyID: 50481528
ms.date: 01/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Filtro mittente

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-12_

Il filtro mittente si basa sull'intestazione MAIL FROM: Intestazione SMTP per determinare l'eventuale azione da intraprendere per un messaggio di posta elettronica in ingresso. Il filtro mittente viene fornito dall'agente filtro mittente.

L'agente Filtro mittente agisce sui messaggi provenienti da mittenti specifici esterni all'organizzazione. Gli amministratori gestiscono un elenco di mittenti bloccati ai quali non è consentito inviare messaggi all'organizzazione. In qualità di amministratore, è possibile bloccare mittenti singoli (kim@contoso.com), interi domini (contoso.com) o domini con tutti i sottodomini (\*.contoso.com). È possibile inoltre configurare l'azione che l'agente Filtro mittente deve intraprendere quando viene rilevato un messaggio proveniente da un mittente bloccato. È possibile configurare le seguenti azioni:

  - L'agente filtro mittente rifiuta la richiesta SMTP con un errore di sessione SMTP `554 5.1.0 Sender Denied` e chiude la connessione.

  - L'agente Filtro mittente accetta il messaggio e lo aggiorna per indicare che proviene da un mittente bloccato. Poiché il messaggio proviene da un mittente bloccato ed è contrassegnato come tale, l'agente Filtro contenuto utilizzerà queste informazioni per calcolare il livello di probabilità di posta indesiderata.

È possibile designare i mittenti bloccati e definire la modalità di azione dell'agente filtro mittente sui messaggi provenienti dai mittenti bloccati. Per ulteriori informazioni su come configurare l'agente Filtro mittente, vedere [Gestire il filtro mittente](manage-sender-filtering-exchange-2013-help.md).


> [!IMPORTANT]
> Le intestazioni MAIL FROM: SMTP possono essere falsificate. Si consiglia pertanto di non basarsi esclusivamente sull'agente Filtro mittente, ma di utilizzare contemporaneamente l'agente Filtro mittente e l'agente ID mittente. L'agente ID mittente utilizza l'indirizzo IP di origine del server mittente per verificare che il dominio nell'intestazione MAIL FROM: L'intestazione SMTP corrisponde al dominio registrato. Per ulteriori informazioni sull'agente ID mittente, vedere <A href="sender-id-exchange-2013-help.md">ID mittente</A>.



## Utilizzo dell'agente filtro mittente per bloccare i messaggi

Quando l'agente filtro mittente è abilitato su un server Exchange, il filtro mittente blocca i messaggi in entrata provenienti da Internet ma che non sono autenticati. Questi messaggi vengono gestiti come messaggi esterni. È possibile disabilitare l'agente filtro mittente in configurazioni di singoli computer. Per ulteriori informazioni, vedere [Gestire il filtro mittente](manage-sender-filtering-exchange-2013-help.md).

Quando si abilita l'agente filtro mittente su un server Exchange, vengono filtrati tutti i messaggi che passano attraverso i connettori di ricezione di quel computer. Come indicato in precedenza, vengono filtrati solo i messaggi provenienti da origini esterne. Le *origini esterne* vengono definite come origini non autenticate. Sono considerate origini Internet anonime.

Si consiglia di non filtrare i messaggi di posta elettronica provenienti da partner attendibili o dall'interno dell'organizzazione. Quando si eseguono i filtri protezione da posta indesiderata, è sempre possibile che vengano individuati falsi positivi. È necessario configurare gli agenti di protezione dalla posta indesiderata affinché vengano eseguiti solo sui messaggi provenienti da fonti sconosciute o potenzialmente non attendibili, riducendo in tal modo la possibilità che i filtri gestiscano in modo errato i messaggi di posta elettronica legittimi. È possibile abilitare e disabilitare l'esecuzione dell'agente filtro mittente per i messaggi provenienti da qualsiasi fonte. Per ulteriori informazioni, vedere [Gestire il filtro mittente](manage-sender-filtering-exchange-2013-help.md).

È possibile configurare l'agente Filtro mittente per bloccare i messaggi in arrivo in cui non viene specificato il mittente e il dominio nell'intestazione MAIL: SMTP. Tale funzione può essere utilizzata per impedire gli attacchi basati sul rapporto di mancato recapito (NDR, Non-Delivery Report) al server Exchange. La maggior parte dei messaggi SMTP legittimi proviene da server SMTP che indicano il mittente e il dominio nel comando MAIL FROM: .

## Specifica dell'azione di blocco

Dopo aver indicato i mittenti e i domini bloccati, è necessario specificare come l'agente Filtro mittente deve comportarsi rispetto ai messaggi provenienti da tali mittenti e domini. È consigliabile rifiutare i messaggi. Quando si utilizza l'agente filtro mittente per bloccare tutti gli indirizzi di posta elettronica e i domini specificati dall'amministratore di Exchange, la probabilità di falsi positivi è relativamente più bassa di quando si utilizzano altri agenti di protezione dalla posta indesiderata. Ad esempio, l'agente Filtro contenuti è un agente di protezione dalla posta indesiderata che si basa su molte variabili per determinare se un messaggio è indesiderato o meno.

Esistono solo due scenari in cui i messaggi legittimi possono essere rifiutati dall'agente Filtro mittente:

  - Se si digita in modo errato un indirizzo di posta elettronica o un nome di dominio, probabilmente verrà bloccato il mittente errato.

  - Se un nome di dominio viene registrato di nuovo come legittimo dopo avere aggiunto il dominio all'elenco dei mittenti bloccati, verranno involontariamente bloccati i messaggi legittimi.

In entrambi i casi può comunque essere opportuno rifiutare i messaggi.

