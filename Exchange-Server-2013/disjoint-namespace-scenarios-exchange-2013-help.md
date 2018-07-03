---
title: 'Scenari di spazio dei nomi disgiunto: Exchange 2013 Help'
TOCTitle: Scenari di spazio dei nomi disgiunto
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 50481171
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Scenari di spazio dei nomi disgiunto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento vengono fornite informazioni sugli spazi dei nomi disgiunti e sugli scenari supportati per la distribuzione di Microsoft Exchange 2013 in un dominio con un nome di spazio disgiunto.

**Sommario**

DNS and NetBIOS domain names

Disjoint namespaces

Exchange 2013 and disjoint namespaces

Allow Exchange 2013 servers to access domain controllers that are disjoint

View DNS and NetBIOS name-related information of a computer running Windows Server 2008

## Nomi di dominio DNS e NetBIOS

Innanzitutto, qualche informazione generale. Ogni computer in Internet ha un nome DNS (Domain Name System), noto anche come *nome macchina* o *nome host*. Ogni computer con funzionalità di rete su cui è in esecuzione il sistema operativo Windows dispone anche di un nome NetBIOS.

Un computer in cui è in esecuzione Windows in un dominio di Active Directory dispone sia di un nome di dominio DNS sia di un nome di dominio NetBIOS, come indicato di seguito:

  - **Nome di dominio DNS**   Il nome di dominio DNS comprende uno o più sottodomini separati da un punto (**.**) e termina con un nome di dominio di primo livello. Ad esempio, nel nome di dominio DNS corp.contoso.com, i sottodomini sono corp e contoso e il nome di dominio di primo livello è com.

  - **Nome di dominio NetBIOS**   In genere, il nome di dominio NetBIOS è il sottodominio del nome di dominio DNS. Ad esempio, se il nome di dominio DNS è contoso.com, il nome di dominio NetBIOS è contoso. Se il nome di dominio DNS è corp.contoso.com, il nome di dominio NetBIOS è corp.


> [!NOTE]
> Per trovare le informazioni DNS e NetBIOS per i computer con sistema operativo Windows Server 2008, vedere View DNS and NetBIOS name-related information of a computer running Windows Server 2008.



Un computer in un dominio di Active Directory dispone anche di un suffisso DNS principale e può avere suffissi DNS aggiuntivi. Per impostazione predefinita, il suffisso DNS principale è lo stesso del nome di dominio DNS. Per istruzioni dettagliate su come modificare il suffisso DNS principale, vedere le procedure descritte di seguito.

Definire il nome di dominio DNS e nome NetBIOS del dominio di un dominio Active Directory quando si configura il primo controller di dominio nel dominio. Per ulteriori informazioni sulla configurazione del controller di dominio, vedere [Ruoli del Controller di dominio](https://go.microsoft.com/fwlink/p/?linkid=268367) e [Active Directory Domain Services Overview](https://go.microsoft.com/fwlink/p/?linkid=268366).

## Spazi dei nomi disgiunti

Nella maggior parte delle topologie di dominio il suffisso DNS primario dei computer nel dominio è uguale al nome di dominio DNS.

In alcuni casi può essere necessario che questi spazi dei nomi siano differenti. In tal caso si parla di *spazio dei nomi disgiunto*. Ad esempio, dopo una fusione o un'acquisizione si può avere una topologia con uno spazio dei nomi disgiunto. Inoltre, se la gestione del DNS nell'azienda è divisa tra amministratori che gestiscono Active Directory e amministratori che gestiscono le reti, può essere necessaria una topologia con uno spazio dei nomi disgiunto.

Uno spazio dei nomi disgiunto corrisponde a uno scenario in cui il suffisso DNS primario di un computer non corrisponde al nome di dominio DNS in cui risiede il computer. Il computer con il suffisso DNS primario che non corrisponde è definito *disgiunto*. Un altro scenario dello spazio dei nomi disgiunto si verifica se il nome di dominio NetBIOS di un controller di dominio non corrisponde al nome di dominio DNS.

## Exchange 2013 e spazi dei nomi disgiunti

Exchange 2013 supporta i tre scenari riportati di seguito per la distribuzione di Exchange in un dominio con uno spazio dei nomi disgiunto:

  - **Suffisso DNS primario e nome di dominio DNS diversi**   Il suffisso DNS primario del controller di dominio non corrisponde al nome di dominio DNS. I computer membri del dominio possono essere disgiunti oppure non disgiunti.

  - **Computer membro disgiunto**   Un computer membro di un dominio di Active Directory è disgiunto, anche se il controller di dominio non lo è.

  - **Nome NetBIOS del controller di dominio diverso dal sottodominio del nome di dominio DNS**   Il nome di dominio NetBIOS del controller di dominio non corrisponde al sottodominio del nome di dominio DNS di tale controller di dominio.

Questi scenari vengono descritti in modo dettagliato nelle sezioni seguenti.


> [!NOTE]
> È supportata per eseguire Exchange 2013 negli scenari spazio dei nomi disgiunto descritti in questo argomento. Tuttavia, se si dispone di uno scenario di spazio dei nomi disgiunto uno degli scenari descritti in questo argomento, è necessario utilizzare Microsoft Services per distribuire Exchange 2013. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=94845">Servizi Microsoft</A>.



## Scenario: Suffisso DNS primario e nome di dominio DNS diversi

In questo scenario il suffisso DNS principale del controller di dominio non è uguale al nome di dominio DNS. Il controller di dominio in questo scenario è disgiunto. I computer che sono membri del dominio, inclusi i server Exchange e i computer client Microsoft Outlook, possono avere un suffisso DNS principale corrispondente al suffisso DNS principale del controller di dominio oppure al nome di dominio DNS.

## Scenario: Il computer membro è disgiunto

In questo scenario il suffisso DNS principale di un computer membro in cui è installato Exchange 2013 non è uguale al nome di dominio DNS, anche se lo è il suffisso DNS principale del controller di dominio. In questo scenario sono presenti un controller di dominio che non è disgiunto e un computer membro che lo è. I computer membro su cui è in esecuzione Outlook possono avere un suffisso DNS principale che corrisponde al suffisso DNS principale del server Exchange disgiunto oppure che corrisponde al nome di dominio DNS.

## Scenario: Nome di dominio NetBIOS diverso dal sottodominio del nome di dominio DNS

In questo scenario il nome di dominio NetBIOS del controller di dominio non è uguale al nome di dominio DNS dello stesso controller di dominio.

**Il nome di dominio NetBIOS non corrisponde al nome di dominio DNS**

![Il nome di dominio NetBIOS non corrisponde al nome di domino DNS](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "Il nome di dominio NetBIOS non corrisponde al nome di domino DNS")

## Come consentire ai server Exchange 2013 di accedere ai controller di dominio disgiunti

Per consentire ai server Exchange 2013 di accedere ai controller di dominio sono disgiunti, è necessario modificare l'attributoActive Directory**msDS-AllowedDNSSuffixes**nel contenitore oggetti di dominio. È necessario aggiungere entrambi i suffissi DNS per l'attributo. Per ulteriori informazioni su come modificare l'attributo, vedere [suffisso DNS primario del computer non corrisponde il nome di dominio COMPLETO del dominio in cui si trova](https://go.microsoft.com/fwlink/p/?linkid=98848).

Inoltre, per assicurarsi che l'elenco di ricerca suffissi DNS contenga tutti gli spazi dei nomi DNS distribuiti nell'organizzazione, è necessario configurare tale elenco per ogni computer nel dominio disgiunto. L'elenco degli spazi dei nomi deve includere non solo il suffisso DNS principale del controller di dominio e il nome di dominio DNS, ma anche altri eventuali spazi dei nomi aggiuntivi per altri server con cui Exchange può interagire (quali server di monitoraggio o server per applicazioni di terze parti). Per eseguire l'operazione è possibile impostare Criteri di gruppo per il dominio. Per ulteriori informazioni sui Criteri di gruppo, vedere i seguenti argomenti:

  - [Domande frequenti (FAQ) dei criteri di gruppo](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [Nuovi criteri di gruppo per DNS in Windows Server 2003](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=294785)

  - [Criteri di gruppo](https://go.microsoft.com/fwlink/p/?linkid=268043)

Per la procedura dettagliata relativa alla configurazione di Criteri di gruppo per l'elenco di ricerca suffissi DNS, vedere [Configurare l'elenco ricerca suffissi DNS per un spazio dei nomi disgiunto](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md).

## Visualizzare le informazioni sui nomi DNS e NetBIOS di un computer con sistema operativo Windows Server 2008

1.  Fare clic su **Start**, fare clic con il pulsante destro del mouse su **Computer** e scegliere **Proprietà**.

2.  In **Sistema** il nome host DNS e il suffisso DNS primario sono visualizzati nella sezione **Impostazioni relative a nome computer, dominio e gruppo di lavoro**, accanto a **Nome completo computer**. Il nome di dominio DNS è visualizzato accanto a **Dominio**.

3.  Fare clic su **Cambia impostazioni**.

4.  In **Proprietà di sistema**, nella scheda **Nome computer** scegliere **Cambia**.

5.  Nella pagina **Cambiamenti dominio/nome computer** fare clic su **Altro**. Il suffisso DNS primario è visualizzato sotto **Suffisso DNS primario del computer**. Il nome NetBIOS del computer è visualizzato sotto **Nome NetBIOS del computer**.
    
    Per modificare il suffisso DNS principale, digitare il nuovo suffisso DNS principale in **Suffisso DNS primario del computer**, quindi fare clic su **OK**.

6.  Da una finestra del prompt dei comandi digitare **set**. La variabile USERDNSDOMAIN visualizza il nome di dominio DNS. La variabile USERDOMAIN visualizza il nome di dominio NetBIOS.

