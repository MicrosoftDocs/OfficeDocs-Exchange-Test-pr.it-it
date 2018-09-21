---
title: 'Pianificazione e distribuzione: Exchange 2013 Help'
TOCTitle: Pianificazione e distribuzione
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 50480870
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pianificazione e distribuzione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Sono necessarie indicazioni un'installazione di Exchange in corso. In questo articolo vengono fornite indicazioni per la pianificazione di una distribuzione di Microsoft Exchange Server 2013, nonché collegamenti ad articoli in cui è necessario durante la distribuzione.

Le sezioni seguenti contengono collegamenti a informazioni sulla pianificazione e la distribuzione di Microsoft Exchange Server 2013.


> [!IMPORTANT]
> Accertarsi di leggere l'argomento <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Note sulla versione di Exchange 2013</A> prima di iniziare la distribuzione. Le note sulla versione contengono informazioni importanti sui problemi che si possono verificare durante e dopo la distribuzione.



**Sommario**

Planning for Exchange 2013

Deploying Exchange 2013

Understanding Exchange 2013 Setup

For more information

## Pianificazione di Exchange 2013

Utilizzare i seguenti collegamenti per accedere a informazioni utili per la pianificazione della distribuzione di Exchange Server 2013 nell'organizzazione.


> [!IMPORTANT]
> Vedere Establish a Test Environment più avanti in questo argomento per informazioni sull'installazione di Exchange 2013 in un ambiente di prova.



  - [Server cassette postali e accesso Client](mailbox-and-client-access-servers-exchange-2013-help.md)  
    Informazioni sui ruoli del server Accesso client e Cassette postali inclusi in Exchange 2013.

<!-- end list -->

  - [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md)  
    Informazioni sui requisiti di sistema che devono essere soddisfatti nell'organizzazione prima di poter installare Exchange 2013.

<!-- end list -->

  - [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md)  
    Informazioni sulle funzionalità di Windows Server 2008 R2 Service Pack 1 (SP1) o Windows Server 2012 e sugli altri software che devono essere installati per effettuare una corretta installazione corretta di Exchange 2013.

<!-- end list -->

  - [Assistente per la distribuzione di Exchange Server](exchange-server-deployment-assistant-exchange-2013-help.md)  
    Utilizzare questo strumento per generare un elenco di controllo personalizzato per la pianificazione, l'installazione o l'aggiornamento a Exchange 2013. Sono disponibili informazioni aggiuntive per più scenari, inclusa la distribuzione locale, ibrida o cloud.

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    Leggere questo argomento per ottenere informazioni sull'utilizzo di Active Directory da parte di Exchange 2013 e sull'impatto di Active Directory in relazione alla distribuzione di Exchange.

<!-- end list -->

  - [Protezione antimalware](anti-malware-protection-exchange-2013-help.md)  
    Leggere questo argomento per comprendere le opzioni di protezione antimalware di Exchange 2013.

<!-- end list -->

  - [Distribuzioni ibride di Exchange Server](https://technet.microsoft.com/it-it/library/jj200581\(v=exchg.150\))  
    Leggere questo argomento per informazioni sulla pianificazione di una distribuzione ibrida con Microsoft Office 365 e l'organizzazione Exchange 2013 locale.

<!-- end list -->

  - [Pianificazione della disponibilità elevata e della resilienza del sito](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    Leggere questo argomento per informazione su come pianificare il raggiungimento di requisiti di disponibilità elevata e business continuity.

<!-- end list -->

  - [Integrazione con SharePoint e Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    Leggere questo argomento per informazioni sull'integrazione di Exchange 2013, Microsoft SharePoint 2013 e Microsoft Lync 2013 per abilitare funzionalità di archiviazione tra prodotti, conservazione ed eDiscovery; cassette postali del sito; autenticazione; presenza Lync e così via.

<!-- end list -->

  - [Pianificazione per la messaggistica unificata](planning-for-unified-messaging-exchange-2013-help.md)  
    Leggere questo argomento per ulteriori informazioni sulla pianificazione della Messaggistica unificata di Exchange 2013.

<!-- end list -->

  - [Opzioni di configurazione di archiviazione di Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    Leggere questo argomento per informazioni su architetture di archiviazione, tipi di dischi e configurazioni di archiviazione supportati dal ruolo del server Cassette postali di Exchange 2013.

<!-- end list -->

  - [Virtualizzazione di Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md)  
    Leggere questo argomento per sapere come è possibile distribuire Exchange 2013 in un ambiente virtualizzato.

<!-- end list -->

  - [Multi-tenancy in Exchange 2013](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    Leggere questo argomento per ulteriori informazioni su come configurare Exchange 2013 per ospitare più organizzazioni o business unit distinte che normalmente non condividono messaggi di posta elettronica, dati, utenti, elenchi indirizzi globali o altri oggetti di Exchange di uso comune.

<!-- end list -->

  - [Tecnologie di sviluppo di Exchange](https://go.microsoft.com/fwlink/p/?linkid=268448)  
    Questo argomento contiene informazioni importanti sulle interfacce API (Application Programming Interface) disponibili per le applicazioni che utilizzano Exchange 2013.

## Creazione di un ambiente di prova

Prima di installare Exchange 2013 per la prima volta, si consiglia di installarlo in un ambiente di prova isolato. In questo modo è possibile ridurre il rischio che gli utenti finali debbano affrontare prolungati tempi di inattività e che nell'ambiente di produzione si verifichino effetti negativi.

L'ambiente di prova agirà come "prova di installazione" per Exchange 2013 permettendo di ottimizzare le implementazioni prima della distribuzione nell'ambiente di produzione. Disporre di un ambiente di prova esclusivo per la convalida e la verifica permette di fare controlli prima dell'installazione negli ambienti di produzione. Iniziando con l'installazione in un ambiente di prova, l'organizzazione avrà maggiori probabilità di successo quando passerà all'implementazione completa.

Per molte organizzazioni, i costi legati alla creazione di un ambiente di prova possono risultare elevati a causa della necessità di duplicare l'ambiente di produzione. Per ridurre i costi dell'hardware associato a un ambiente di prova, si consiglia di ricorrere alla virtualizzazione tramite le tecnologie Windows Server 2008 R2 o Windows Server 2012 Hyper-V. Hyper-V consente di eseguire la virtualizzazione dei server perché consente l'esecuzione contemporanea di più sistemi operativi virtuali su un singolo computer fisico.

Per ulteriori informazioni su Hyper-V, vedere [Virtualizzazione Server](https://go.microsoft.com/fwlink/p/?linkid=117704). Per informazioni sul supporto tecnico Microsoft di Exchange 2013 nell'ambiente di produzione in software di virtualizzazione dell'hardware, vedere "La virtualizzazione dell'Hardware" in [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

## Distribuzione di un'installazione di Exchange 2013

La fase di distribuzione indica il periodo in cui Exchange 2013 viene installato nell'organizzazione. Prima di avviare la fase di distribuzione, è necessario pianificare l'organizzazione di Exchange. Per ulteriori informazioni, vedere la sezione Planning descritta precedentemente in questo argomento.

Utilizzare i seguenti collegamenti per accedere alle informazioni necessarie per la distribuzione di Exchange 2013.

  - [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md)  
    Informazioni sulla procedura da seguire per preparare la foresta Active Directory per Exchange 2013 e sulle modifiche apportate alla foresta da Exchange.

<!-- end list -->

  - [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    Attenersi alla procedura descritta in questo argomento per utilizzare l'installazione guidata di Exchange 2013 per installare Exchange 2013 in una nuova organizzazione Exchange.

<!-- end list -->

  - [Installare Exchange 2013 utilizzando la modalità automatica](ge-2013-using-unattended-mode-exchange-2013-help 
Redirect to URL: https://review.docs.microsoft.com/zh-cn/office/exchange-server-2013/exchange-2013-client-access-server-configuration-exchange-2013-help)  
    Attenersi alla procedura descritta in questo argomento per utilizzare l'installazione automatica di Exchange 2013 per installare Exchange 2013 in una nuova organizzazione Exchange.

<!-- end list -->

  - [Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    Attenersi alla procedura descritta in questo argomento per utilizzare l'installazione guidata di Exchange 2013 per installare il ruolo Trasporto Edge Exchange 2013 in una rete perimetrale.

<!-- end list -->

  - [Upgrade di Exchange 2013 all'aggiornamento cumulativo o Service Pack più recente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    Attenersi alla procedura riportata in questo argomento per applicare l'aggiornamento cumulativo o service pack più recente ai server Exchange 2013 nell'organizzazione.

<!-- end list -->

  - [Aggiornamento da Exchange 2007 a Exchange 2010](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    Attenersi alla procedura riportata in questo argomento per installare Exchange 2013 nell'organizzazione di Exchange 2010 esistente.

<!-- end list -->

  - [Aggiornamento da Exchange 2007 a Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    Attenersi alla procedura riportata in questo argomento per installare Exchange 2013 nell'organizzazione di Exchange 2007 esistente.

<!-- end list -->

  - [Distribuire più topologie a foresta di Exchange Server 2013](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    Leggere le informazioni in questo argomento per distribuire Exchange 2013 in un'organizzazione contenente più di una foresta di Active Directory.

<!-- end list -->

  - [Distribuzione di segreteria telefonica e messaggistica UNIFICATA](deploying-voice-mail-and-um-exchange-2013-help.md)  
    Leggere questo argomento per informazioni che consentiranno una visione più approfondita della distribuzione della messaggistica unificata di Exchange 2013, che si tratti di una nuova distribuzione o di un aggiornamento.

<!-- end list -->

  - [Procedure di distribuzione ibrida](https://technet.microsoft.com/it-it/library/jj200788\(v=exchg.150\))  
    Leggere questo argomento per informazioni che consentiranno di distribuire Exchange 2013 in una distribuzione ibrida esistente.

<!-- end list -->

  - [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    Informazioni sulle attività successive all'installazione necessarie per completare l'installazione di Exchange 2013.

## Informazioni sull'installazione di Exchange 2013

Per installare e gestire le varie edizioni e versioni di Exchange 2013, è possibile utilizzare diversi tipi e modalità di installazione di Exchange 2013.

## Edizioni e versioni di Exchange

Exchange 2013 è disponibile in due versioni server: standard ed Enterprise Edition. Queste licenze edizioni definito da un codice product key. Per ulteriori informazioni, vedere [Gestione delle licenze di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=237292).

## Tipi di installazione di Exchange

Per l'installazione di Exchange 2013, sono disponibili le seguenti opzioni:

  - **Interfaccia utente del programma di installazione di Exchange**   L'esecuzione di Setup.exe senza opzioni della riga di comando costituisce una modalità interattiva in cui l'utente viene assistito dall'installazione guidata di Exchange 2013.

  - **Installazione automatica di Exchange**   L'esecuzione di Setup.exe con opzioni della riga di comando consente l'installazione di Exchange da una riga di comando interattiva o tramite script.

Setup.exe è disponibile nel DVD di Exchange 2013 o nei file di origine scaricati.

## Modalità di installazione di Exchange

Il programma di installazione di Exchange 2013 include diverse modalità di installazione:

  - **Installa**   Utilizzare questa modalità quando si sta installando un nuovo ruolo del server o si sta aggiungendo un ruolo del server a un'installazione esistente (modalità di manutenzione). ﻿È possibile accedere a questa modalità sia dall'installazione guidata di Exchange che dall'installazione automatica.

  - **Disintallazione**   Utilizzare questa modalità quando viene rimossa l'installazione Exchange da un computer. ﻿È possibile accedere a questa modalità sia dall'installazione guidata di Exchange che dall'installazione automatica.

  - **Aggiornamento**   Selezionare questa modalità quando si desidera installare un service pack o un aggiornamento cumulativo di un'installazione di Exchange esistente. ﻿È possibile accedere a questa modalità sia dall'installazione guidata di Exchange che dall'installazione automatica.
    

    > [!NOTE]
    > Exchange 2013 non supporta aggiornamenti sul posto da versioni precedenti di Exchange. Questa modalità viene utilizzata solo per installare service pack o aggiornamenti cumulativi.



  - **RecoverServer**   Utilizzare questa modalità per recuperare i dati dopo che si è verificato un errore irreversibile del server. Il nuovo server deve essere installato utilizzando lo stesso nome di dominio completo server (FQDN) di quello che ha generato errore ed eseguire l'installazione con l'opzione **/m:RecoverServer**. Non specificare i ruoli da ripristinare. Il programma di installazione rileva l'oggetto Exchange Server in Active Directory e installa automaticamente file e configurazione corrispondenti. Dopo il recupero del server, è possibile ripristinare i database e riconfigurare le altre impostazioni. Per eseguire la modalità **RecoverServer**, non è possibile avere Exchange installato sul server. In Active Directory deve esistere l'oggetto Exchange Server. È possibile utilizzare questa modalità solo durante un'installazione automatica.


> [!NOTE]
> Per passare da una modalità di installazione all'altra, è necessario completare la modalità in uso.



## Ulteriori informazioni

[Supporto IPv6 in Exchange 2013](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Interfaccia di amministrazione di Exchange in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Lingue supportate per Exchange 2013](exchange-2013-language-support-exchange-2013-help.md)

[Controlli di conformità di Exchange 2013](exchange-2013-readiness-checks-exchange-2013-help.md)

