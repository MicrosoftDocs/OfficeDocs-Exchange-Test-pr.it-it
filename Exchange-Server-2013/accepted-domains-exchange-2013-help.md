---
title: 'Domini accettati: Exchange 2013 Help'
TOCTitle: Domini accettati
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 50481588
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domini accettati

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-06-16_

Un dominio accettato è uno spazio dei nomi SMTP per conto del quale un'organizzazione di Microsoft Exchange Server 2013 invia o riceve posta elettronica. I domini accettati includono quei domini per i quali l'organizzazione di Exchange è autorevole. Un'organizzazione di Exchange è autorevole quando gestisce il recapito della posta elettronica per i destinatari nel dominio accettato. I domini accettati includono anche i domini per i quali l'organizzazione di Exchange riceve la posta e la inoltra a un server di posta elettronica esterno all'organizzazione per eseguirne il recapito al destinatario.

**Sommario**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## Configurazione dei domini accettati

I domini accettati sono configurati come impostazioni globali per l'organizzazione di Exchange. È necessario configurare ogni dominio per cui l'organizzazione di Exchange inoltra o recapita i messaggi come dominio accettato nell'organizzazione.

Sono disponibili tre tipi di domini accettati: autorevoli, di inoltro interno e di inoltro esterno. Questi tipi di dominio accettato sono descritti nelle sezioni seguenti.


> [!NOTE]
> Se si dispone di un server Trasporto Edge nella propria rete perimetrale, è necessario configurare i domini accettati su un server di cassette postali dell'organizzazione di Exchange. La configurazione dei domini accettati viene replicata nel server Trasporto Edge durante la sincronizzazione EdgeSync. Per ulteriori informazioni, vedere <A href="edge-subscriptions-exchange-2013-help.md">Sottoscrizioni Edge</A>.



## Domini autorevoli

Un'organizzazione può avere più domini SMTP. L'insieme dei domini di posta elettronica di un'organizzazione costituisce i domini autorevoli. In Exchange 2013, un dominio accettato viene considerato autorevole quando l'organizzazione di Exchange ospita cassette postali dei destinatari in questo dominio SMTP.

Per impostazione predefinita, quando viene installato il primo server Cassette postali di Exchange 2013, viene configurato un solo dominio accettato come autorevole per l'organizzazione di Exchange. Il dominio accettato predefinito corrisponde al nome di dominio completo (FQDN) per il dominio radice della foresta. Nella maggior parte dei casi, il nome di dominio interno è diverso dal nome di dominio esterno. Ad esempio, il nome di dominio interno può essere contoso.local, mentre il nome di dominio esterno è contoso.com. Il record MX DNS dell'organizzazione fa riferimento a contoso.com, che è lo spazio dei nomi SMTP assegnato agli utenti durante la creazione di un criterio degli indirizzi di posta elettronica. È necessario creare un dominio accettato da associare al nome di dominio esterno.

Per ulteriori informazioni, vedere:

  - [Configurare un dominio accettato nell'organizzazione di Exchange come autorevole](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [Configurare Exchange affinché accetti posta per più domini autorevoli](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## Domini di inoltro

In genere quasi tutti i server di messaggistica con accesso a Internet sono configurati per non consentire ad altri domini di essere inoltrati tramite essi. Esistono tuttavia scenari in cui potrebbe essere utile consentire a partner o filiali di inoltrare la posta elettronica tramite i server Exchange. In Exchange 2013, è possibile configurare i domini accettati come domini di inoltro. L'organizzazione riceve i messaggi di posta elettronica e li inoltra a un altro server di posta elettronica.

È possibile configurare un dominio di inoltro come dominio di inoltro interno o come dominio di inoltro esterno. Questi due tipi di dominio di inoltro sono descritti nelle sezioni seguenti.

## Dominio di inoltro interno

Quando si configura un dominio di inoltro interno, alcuni o tutti i destinatari del dominio non dispongono di cassette postali nell'organizzazione di Exchange. I messaggi di posta per il dominio provenienti da Internet vengono inoltrati tramite i server di trasporto nell'organizzazione di Exchange. Questa configurazione viene utilizzata negli scenari descritti in questa sezione.

È possibile che un'organizzazione debba condividere lo stesso spazio degli indirizzi SMTP tra due o più diversi sistemi di messaggistica. Ad esempio, potrebbe essere necessario condividere lo spazio degli indirizzi SMTP tra Exchange e un sistema di messaggistica di terze parti, oppure tra gli ambienti Exchange configurati in foreste di Active Directory diverse. In questi scenari, gli utenti di ogni sistema di posta elettronica utilizzano lo stesso suffisso di dominio come parte dei loro indirizzi di posta elettronica.

Per supportare tali scenari, è necessario creare un dominio accettato e configurato come dominio di inoltro interno. È inoltre necessario aggiungere un connettore di invio con origine sul server Cassette postali e configurato per inviare la posta elettronica allo spazio degli indirizzi condiviso. Se un dominio accettato viene configurato come autorevole e non viene trovato alcun destinatario in Active Directory, al mittente viene restituito un rapporto di mancato recapito (NDR). Il dominio accettato e configurato come dominio di inoltro interno tenta inizialmente di recapitare il messaggio a un destinatario all'interno dell'organizzazione di Exchange. Se non viene trovato alcun destinatario, il messaggio viene instradato al connettore di invio con lo spazio degli indirizzi più simile.

Se l'organizzazione contiene più foreste e dispone della sincronizzazione dell'elenco indirizzi globale, il dominio SMTP di una foresta può essere configurato come dominio di inoltro interno in una seconda foresta. I messaggi provenienti da Internet indirizzati ai destinatari dei domini di inoltro interno vengono inoltrati ai server Cassette postali della stessa organizzazione. I server Cassette postali di destinazione instradano i messaggi ai server Cassette postali nella foresta del destinatario. Configurare il dominio SMTP come dominio di inoltro interno per assicurarsi che la posta elettronica indirizzata al dominio sia accettata dall'organizzazione di Exchange. La configurazione dei connettori dell'organizzazione stabilisce come vengono instradati i messaggi.

Per ulteriori informazioni, vedere [Configurare un dominio accettato per una business unit con cassette postali all'esterno dell'organizzazione di Exchange](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md).

## Dominio di inoltro esterno

Quando si configura un dominio di inoltro esterno, i messaggi vengono inoltrati a un server di posta elettronica esterno dell'organizzazione di Exchange ed esterno al perimetro della rete dell'organizzazione.

Per ulteriori informazioni, vedere [Configurare un dominio accettato per una business unit indipendente](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md).

## Domini accettati e criteri degli indirizzi di posta elettronica

È necessario configurare un dominio accettato prima di tale spazio degli indirizzi SMTP può essere utilizzata in un criterio indirizzo di posta elettronica. Quando si crea un dominio accettato, è possibile utilizzare un carattere jolly (\*) nello spazio di indirizzi per indicare che tutti i sottodomini dello spazio degli indirizzi SMTP vengono accettati anche dall'organizzazione Exchange. Ad esempio, per configurare contoso.com e tutti i sottodomini come domini accettati, immettere **\*. contoso.com** come SMTP spazio degli indirizzi. Le voci di dominio accettato sono automaticamente disponibili per l'utilizzo di un criterio indirizzo di posta elettronica.

Se si elimina un dominio accettato utilizzato in un criterio degli indirizzi di posta elettronica, il criterio non è più valido e i destinatari con indirizzi di posta elettronica in quel dominio SMTP non saranno in grado di inviare o ricevere posta elettronica.

