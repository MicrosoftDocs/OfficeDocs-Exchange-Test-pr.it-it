---
title: 'Distribuzione di Exchange 2013 in topologia più foreste: Exchange 2013 Help'
TOCTitle: Distribuzione di Exchange 2013 in una topologia a più foreste
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51407380
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione di Exchange 2013 in una topologia a più foreste

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento viene illustrato come distribuire Exchange 2013 in una topologia con più foreste, tramite Microsoft Forefront Identity Manager 2010 R2 SP1. Per distribuire Exchange 2013 in una topologia con più foreste, è necessario innanzitutto installare Exchange 2013 in ogni foresta, quindi connettere le foreste affinché sia possibile visualizzare l'indirizzo e i dati di disponibilità tra le stesse.

Nella figura seguente viene mostrata la sincronizzazione di un utente tra due foreste di Exchange 2013.

**Esempio di una sincronizzazione tra più foreste di Exchange 2013**

![Esempio di foresta multipla di Exchange 2010](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Esempio di foresta multipla di Exchange 2010")

In questo argomento *non viene descritto* come distribuire Exchange 2013 in una topologia di foreste dedicata (o foresta di risorse) di Exchange. Per ulteriori informazioni su come distribuire Exchange 2013 in una topologia con foresta di risorse, vedere [Distribuzione di Exchange 2013 in una topologia a foresta risorsa Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## Informazioni necessarie per iniziare

Per eseguire la procedura seguente in Exchange 2013, accertarsi che siano soddisfatte le seguenti condizioni:

  - Il DSN per la risoluzione dei nomi nelle foreste dell'organizzazione è stato configurato correttamente. Per verificare che il DNS sia configurato correttamente, utilizzare lo strumento Ping per verificare la connettività di ogni foresta dalle altre foreste nell'organizzazione e dal server sul quale si eseguirà l'agente GALSync.

  - L'agente di gestione GALSync comunica con la foresta di Exchange 2013 tramite Windows PowerShell V2.0 RTM. Verificare che Windows PowerShell v1.0 non sia installato sul computer selezionando Pannello di controllo e facendo clic su Programmi e funzionalità.

  - Verificare che la Gestione remota Windows non sia stata installata da Windows Update.

  - Installare Windows PowerShell e Gestione remota Windows. Per informazioni dettagliate, vedere l'articolo 968930 della Microsoft Knowledge Base, [Pacchetto di Windows Management Framework Core (Windows PowerShell 2.0 e Gestione remota Windows 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Download di Forefront Identity Manager 2010 R2 SP1. Vedere [Download di Microsoft Forefront Identity Manager 2010 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=279868).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Distribuzione di Exchange 2013 in una topologia con più foreste tramite Forefront Identity Manager 2010 R2 SP1

1.  Installare separatamente Exchange 2013 in ciascuna foresta. Per installare Exchange 2013, eseguire la stessa procedura che si utilizza per l'installazione di Exchange 2013 in una singola foresta. Per la procedura dettagliata, vedere uno dei seguenti argomenti:
    
      - [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        

        > [!NOTE]
        > In questo argomento si presuppone che non è un esistente Exchange&nbsp;2007 o Exchange&nbsp;2010 topologia. Se si dispone di una topologia Exchange esistente e si desidera aggiornare, vedere <A href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Aggiornamento da Exchange&nbsp;2007 a Exchange&nbsp;2010</A> o <A href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Aggiornamento da Exchange&nbsp;2007 a Exchange&nbsp;2013</A>.



2.  In ciascuna foresta, utilizzare Utenti e computer di Active Directory per creare un contenitore in cui, tramite Forefront Identity Manager 2010 R2 SP1, vengono inseriti i contatti per ciascuna cassetta postale dall'altra foresta. È consigliabile denominare il contenitore **FromMIIS**. Per la creazione del contenitore, selezionare il dominio in cui si desidera eseguire questa operazione, fare clic con il pulsante destro del mouse sul dominio, quindi scegliere **Nuovo** \> **Unità organizzativa**. In **Nuovo oggetto - Unità organizzativa** digitare **FromILM**, quindi fare clic su **OK**.

3.  Creare un agente di gestione GALSync per ogni foresta tramite Forefront Identify Manager. In questo modo è possibile sincronizzare gli utenti in ogni foresta e creare un comune elenco indirizzi globale. Per la procedura dettagliata, vedere le seguenti risorse:
    
      - [La configurazione della sincronizzazione elenco indirizzi globale con Forefront Identity Manager (FIM) 2010](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [Utilizzare gli agenti di gestione](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Struttura della documentazione Forefront Identity Manager 2010 R2](https://go.microsoft.com/fwlink/p/?linkid=279871)
    

    > [!IMPORTANT]
    > Le risorse discutere Exchange&nbsp;2010, Exchange 2013 è supportato per FIM 2010 R2 SP1. Assicurarsi di configurare <STRONG>le estensioni</STRONG> di FIM 2010 R2 SP1 per Exchange 2013.

    
    1.  Nella pagina **Configura estensioni**, in **Configura partizione dei nomi di visualizzazione**, accanto a **Effettua il provisioning per**, selezionare **Exchange 2013**. Viene visualizzato il campo **URI RPS Exchange 2013**. Immettere l'URI di un server Accesso client di Exchange 2013 per verificare che la connessione di Remote PowerShell sia in funzione correttamente. È necessario che **URI RPS Exchange 2013** sia nel seguente formato: http://CAS\_Server\_FQDN/Powershell. Scegliere **OK**.
        

        > [!NOTE]
        > Verificare che le credenziali di amministratore utilizzate per connettersi alla foresta di Exchange 2013, funzionino anche per connetterla a Remote PowerShell.<BR>Nella figura seguente viene illustrato come selezionare il provisioning per Exchange 2013.

        
        **Provisioning dell'agente di gestione GalSync per Exchange 2013**
        
        ![Provisioning dell'agente di gestione di Exchange 2010](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Provisioning dell'agente di gestione di Exchange 2010")  

4.  Creare un connettore di invio SMTP in ciascuna foresta. Per la procedura dettagliata, vedere [Configurare un connettore di invio tra foreste](configure-a-cross-forest-send-connector-exchange-2013-help.md).

5.  In ciascuna foresta abilitare il Servizio Disponibilità affinché gli utenti in ciascuna foresta possano visualizzare i dati sulla disponibilità relativi agli utenti nell'altra foresta. Per ulteriori informazioni, vedere [Servizio disponibilità in Exchange 2013](availability-service-in-exchange-2013-exchange-2013-help.md).

6.  Per inoltrare la posta in qualsiasi foresta dell'organizzazione, è necessario configurare un dominio autorevole nella foresta. Per la procedura dettagliata, vedere [Configurare Exchange affinché accetti posta per più domini autorevoli](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md).

