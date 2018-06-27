---
title: 'Attività di gestione directory virtuale di Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Attività di gestione directory virtuale di Exchange ActiveSync
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 50482024
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attività di gestione directory virtuale di Exchange ActiveSync

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-05_

Alcune impostazioni delle applicazioni Exchange ActiveSync possono essere gestite in Exchange Server 2013 tramite la directory virtuale di Exchange ActiveSync. La directory virtuale viene utilizzata da Internet Information Services (IIS) per consentire l'accesso all'applicazione Web Exchange ActiveSync. È possibile gestire alcune impostazioni della directory virtuale affinché in Exchange ActiveSync sia inclusa autenticazione, sicurezza e reporting.

## Impostazioni della directory virtuale di Exchange ActiveSync

Nella directory virtuale di Exchange ActiveSync è possibile modificare le seguenti proprietà e impostazioni:

  - **URL interno** L'URL interno è l'URL utilizzabile dai client interni per accedere alla directory virtuale. In genere è in formato https://servername/Microsoft-Server-ActiveSync. A d esempio, se il nome NetBIOS del servere è Sequoia, l'URL interno sarà https://sequoia/Microsoft-Server-ActiveSync.

  - **URL esterno** L'URL esterno è l'URL utilizzabile dai client esterni per accedere alla directory virtuale. Questo URL deve essere accessibile all'esterno della rete interna. Ad esempio, l'URL esterno potrebbe essere https://www.contoso.com/.

  - **Impostazioni di autenticazione** I due metodi di autenticazione configurabili per la directory virtuale di Exchange ActiveSync sono Autenticazione di base e Autenticazione certificato client.

