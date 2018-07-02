---
title: 'Modificare i criteri di archiviazione: Exchange 2013 Help'
TOCTitle: Modificare i criteri di archiviazione
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 50480131
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare i criteri di archiviazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-02-01_

In Exchange Server 2013 e Exchange Online, è possibile utilizzare i criteri di archiviazione per spostare automaticamente gli elementi della cassetta postale personale (locale) o archivi basata su cloud. I criteri di archiviazione sono i tag di conservazione che utilizzano l'azione di conservazione **Sposta nell'archivio**.

Il programma di installazione di Exchange crea un criterio di conservazione denominato **Criterio di gestione record di messaggistica predefinito**. A questo criterio è assegnato un tag criterio predefinito (DPT) che dopo due anni sposta gli elementi nella cassetta postale di archiviazione. Questo criterio include un certo numero di tag personali che gli utenti possono applicare agli elementi delle cassette postali o delle cartelle per spostare o eliminare automaticamente i messaggi. Se a una cassetta postale abilitata per l'archivio non è associato un criterio di conservazione, Exchange le applica automaticamente il **Criterio di gestione record di messaggistica predefinito**. È comunque possibile creare criteri di archiviazione e conservazione personalizzati e applicarli agli utenti delle cassette postali. Per ulteriori informazioni, vedere [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md).

È possibile modificare i tag di conservazione inclusi nel criterio predefinito in base ai requisiti aziendali. Ad esempio, è possibile modificare il tag criterio predefinito di archiviazione in modo che gli elementi vengano spostati nell'archivio dopo tre anni invece che dopo due. È, inoltre, possibile creare altri tag personali e aggiungerli a un criterio di conservazione (incluso il **Criterio di gestione record di messaggistica predefinito**) o consentire agli utenti di aggiungere tag personali alle relative cassette postali dalle opzioni di Outlook Web App.

Per altre attività di gestione relative agli archivi, vedere:

  - **Exchange Server 2013:**  [Gestione degli archivi In Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:**  [Abilitare o disabilitare una cassetta postale di archiviazione in Exchange Online.](https://technet.microsoft.com/it-it/library/jj984357\(v=exchg.150\))


> [!NOTE]
> In una distribuzione ibrida Exchange, è possibile abilitare una cassetta postale di archiviazione basate su cloud per una cassetta postale principale in locale. Se si assegna un criterio di archiviazione in una cassetta postale locale, vengono spostati gli elementi nell'archivio basato su cloud. Se un elemento viene spostato la cassetta postale di archiviazione, una copia non viene mantenuta nella cassetta postale locale. Se la cassetta postale locale viene messa in attesa, criteri di archiviazione verranno comunque di spostare gli elementi per la cassetta postale di archiviazione basata sul cloud dove vengono conservate per la durata specificata per la sospensione.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Modifica del criterio di archiviazione predefinito tramite l'interfaccia di amministrazione di Exchange

1.  Passare a **Gestione della conformità** \> **Tag di conservazione**.

2.  Quindi, selezionare, nella visualizzazione elenco, il tag **Sposta elementi predefiniti in archivio dopo 2 anni** e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    

    > [!TIP]
    > È possibile fare clic sulla colonna <STRONG>TIPO</STRONG> per ordinare le tag di conservazione per tipo. Il criterio di archiviazione predefinito viene visualizzato come tipo <STRONG>Predefinito</STRONG> con l'azione di conservazione <STRONG>Archivia</STRONG> attivata. In alternativa, fare clic su <STRONG>NOME</STRONG> per ordinare i tag di conservazione per nome.



3.  
    
    In **Tag di conservazione**, visualizzare o modificare le seguenti impostazioni, quindi fare clic su **Salva**:
    
      - **Nome**   Utilizzare questa casella nella parte superiore della pagina per visualizzare o modificare il nome del tag.
    
      - **Tipo di tag di conservazione**   Questo campo di sola lettura visualizza il tipo di tag.
    
      - **Azione di conservazione**   Non modificare questo campo per i criteri di conservazione.
    
      - **Periodo di conservazione**Selezionare una delle seguenti opzioni:
        
          - **Mai**   Fare clic su questo pulsante per disattivare il tag. Se viene disabilitato il DPT, il tag non verrà più applicato alla cassetta postale.
            

            > [!IMPORTANT]
            > Gli elementi con un tag di conservazione disabilitato non vengono elaborati dall'Assistente cassette postali. Se si desidera impedire l'applicazione di un tag ad alcuni elementi, è consigliabile disabilitare il tag anziché eliminarlo. Quando si elimina un tag, la configurazione del tag viene eliminata da Active Directory e l'Assistente cassette postali elabora tutti i messaggi per la rimozione del tag eliminato.

            

            > [!NOTE]
            > Se un utente applica un tag a un elemento convinto che comunque questo non verrà mai spostato, l'abilitazione successiva del tag potrebbe provocare lo spostamento degli elementi che l'utente desiderava conservare nella cassetta postale principale.

        
          - **Quando l'elemento raggiunge la seguente età (in giorni)**   Fare clic su questo pulsante per specificare che gli elementi devono essere spostati nell'archivio dopo un determinato periodo di tempo. Per impostazione predefinita, questa opzione è impostata in modo che gli elementi vengano spostati nell'archivio dopo due anni (730 giorni). Per modificare questa impostazione, nella casella di testo corrispondente, digitare il numero di giorni per il periodo di conservazione. Il valore deve essere compreso nell'intervallo 1-24.855 giorni.
    
      - **Commento**   Utilizzare questa casella per digitare un commento che verrà visualizzato dagli utenti Outlook e Outlook Web App.

## Modifica dei criteri di archiviazione tramite Shell

In questo esempio, il tag `Default 2 year move to archive` viene modificato in modo che gli elementi vengano spostati dopo 1.095 giorni (3 anni).

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

In questo esempio, il tag `Default 2 year move to archive` viene disabilitato.

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

In questo esempio, tutti i tag personali e i tag criteri predefiniti di archiviazione vengono recuperati e disabilitati.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd298042\(v=exchg.150\)) e [Get-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd298009\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Utilizzare il cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd298009\(v=exchg.150\)) per recuperare le impostazioni del tag di conservazione.

Questo comando consente di recuperare le proprietà del tag di conservazione `Default 2 year move to archive` e di eseguire il pipelining dell'output all'attivazione del cmdlet **Format-List** per visualizzare tutte le proprietà in un formato elenco.

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

