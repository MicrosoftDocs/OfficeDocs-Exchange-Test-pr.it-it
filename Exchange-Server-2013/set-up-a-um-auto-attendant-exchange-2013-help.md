---
title: 'Configura operatore automatico messaggistica unificata: Exchange 2013 Help'
TOCTitle: Configurare un operatore automatico di messaggistica unificata
ms:assetid: 0a3492f8-8aba-4904-96fd-6e023175012a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673508(v=EXCHG.150)
ms:contentKeyID: 50479970
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un operatore automatico di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-03-09_

Oltre a consentire l'accesso utente ai messaggi vocali, Messaggistica unificata consente di creare uno o più operatori automatici di messaggistica unificata, in base alle necessità dell'organizzazione. Gli operatori automatici di messaggistica unificata possono essere utilizzati per creare un sistema di menu vocali per un'organizzazione, consentendo in tal modo ai chiamanti interni ed esterni di individuare, eseguire o trasferire chiamate agli utenti dell'azienda o ai reparti dell'organizzazione.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Operatori automatici

In ambienti di telefonia o di messaggistica unificata, un operatore automatico o un sistema di menu con operatori automatici trasferisce i chiamanti al numero di interno di un utente o di un reparto senza l'intervento di un centralinista o di un operatore. In molti sistemi con operatore automatico il centralinista o l'operatore può essere raggiunto premendo o pronunciando lo zero. Alcuni sistemi con operatori automatici utilizzano menu informativi di soli messaggi e menu vocali che consentono all'organizzazione di fornire informazioni sugli orari di ufficio, sul raggiungimento delle sedi dell'azienda, sulle opportunità di lavoro e risposte ad altre domande frequenti. Dopo la riproduzione del messaggio, i chiamanti vengono inoltrati al centralinista o all'operatore oppure possono tornare al menu principale.

Gli operatori automatici sono indubbiamente di grande utilità, tuttavia se non vengono progettati e configurati correttamente possono disorientare e ostacolare i chiamanti. Ad esempio, soprattutto nelle organizzazioni di grandi dimensioni, se gli operatori automatici non sono progettati correttamente i chiamanti passano in genere attraverso una lunga serie di domande e di prompt di menu prima di essere finalmente trasferiti alla persona in grado di rispondere alle loro domande.

## Come configurare un operatore automatico

Nell'interfaccia di amministrazione di Exchange, è possibile configurare e gestire operatori automatici di messaggistica unificata per rispondere automaticamente alle chiamate effettuate all'organizzazione e consentire ai chiamanti di selezionare in modo automatico diverse opzioni tramite i tasti del telefono. È possibile configurare un solo operatore di messaggistica unificata per fornire funzionalità di spostamento di base nei menu ai chiamanti dell'organizzazione o più operatori automatici nidificati e con più diramazioni per offrire ai chiamanti funzionalità più avanzate. Tuttavia, in entrambi i casi, è necessario pianificare e configurare gli operatori automatici con molta attenzione.

Per pianificare e creare una nuova struttura di operatori automatici di messaggistica unificata, è necessario effettuare le seguenti operazioni:

1.  Decidere se si desidera consentire agli utenti di interagire con l'operatore automatico utilizzando input vocali.

2.  Decidere quale lingua si desidera utilizzare per l'operatore automatico principale e se bisogna creare altri operatori automatici per supportare più lingue.

3.  Decidere l'orario di ufficio e non di ufficio per l'operatore automatico e impostare l'orario d'ufficio utilizzando **Orario di ufficio**. Sebbene non sia richiesto, è possibile decidere anche la pianificazione dei periodi di vacanza per questo operatore automatico.
    

    > [!NOTE]
    > È necessario impostare anche il fuso orario sull'operatore.



4.  Decidere se si desidera utilizzare messaggi di saluto standard generati dal sistema per gli orari di ufficio e non di ufficio o creare registrazioni personalizzate.
    
    Se si desidera utilizzare messaggi di saluto personalizzati, pianificare e registrare i propri messaggi di saluto per l'orario di ufficio e non di ufficio da inoltrare ai chiamanti durante l'orario di ufficio e non di ufficio. Se necessario, è possibile creare anche un messaggio di saluto informativo personalizzato. Ad esempio, per il messaggio di saluto nell'orario di ufficio, si potrebbe utilizzare "Benvenuti in Contoso. Premere o dire 1 per l'inglese, premere o dire 2 per lo spagnolo." Per un messaggio di saluto da riprodurre durante l'orario non di ufficio, è possibile registrare il testo seguente: "Benvenuti in Contoso. I nostri uffici sono chiusi. Saremo aperti lunedì alle 08:00."

5.  Pianificare la struttura dell'operatore automatico in base alle esigenze aziendali. Ad esempio, un'organizzazione potrebbe essere un'azienda multinazionale con uffici sia in Germania sia nel Regno Unito e, pertanto, avrebbe bisogno di una struttura per l'operatore automatico basata su più lingue. Un'altra organizzazione potrebbe avere il proprio ufficio aziendale in un sito, l'Ufficio Vendite in un altro sito e il Servizio clienti in un terzo sito e, pertanto avrebbe bisogno di un operatore automatico che si relazioni direttamente con la struttura dell'organizzazione.

6.  Decidere se si avrà bisogno di operatori automatici per il fallback del segnale multifrequenza (DTMF) o di altri operatori automatici da utilizzare quando i comandi vocali dell'operatore automatico non funzionano.

7.  Pianificare lo spostamento nei menu per l'orario di ufficio e non di ufficio. Per ciascun operatore automatico, inclusi quelli DTMF, sarà necessario pianificare e configurare prompt del menu e le voci per lo spostamento nei menu. Sarà necessario fare ciò sia per l'orario di ufficio sia per quello non di ufficio.

8.  Di seguito viene fornito un foglio di lavoro di esempio che è possibile utilizzare per pianificare lo spostamento nei menu per l'orario non di ufficio.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><strong>Tasto</strong></th>
    <th><strong>Nome della voce del menu di navigazione/prompt</strong></th>
    <th><strong>Risposta da registrare</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1</p></td>
    <td><p>Selezione della lingua per utilizzare l'inglese.</p></td>
    <td><p>&quot;Premere o dire 1 per utilizzare l'inglese.&quot;</p></td>
    </tr>
    <tr class="even">
    <td><p>2</p></td>
    <td><p>Saldo conto</p></td>
    <td><p>&quot;Premere o dire 2 per ottenere il saldo del conto.&quot;</p></td>
    </tr>
    <tr class="odd">
    <td><p>3</p></td>
    <td><p>Trasferimento all'Ufficio Vendite</p></td>
    <td><p>&quot;Premere o dire 3 per essere trasferiti al reparto vendite.&quot;</p></td>
    </tr>
    <tr class="even">
    <td><p>4</p></td>
    <td><p>Trasferimento al servizio clienti</p></td>
    <td><p>&quot;Premere o dire 4 per essere trasferiti al prossimo rappresentante del servizio clienti.&quot;</p></td>
    </tr>
    <tr class="odd">
    <td><p>5</p></td>
    <td><p>Orario di ufficio</p></td>
    <td><p>Non è necessaria una risposta.</p></td>
    </tr>
    <tr class="even">
    <td><p>6</p></td>
    <td><p>Sede aziendale</p></td>
    <td><p>Non è necessaria una risposta.</p></td>
    </tr>
    </tbody>
    </table>


9.  Utilizzando il piano di spostamento nei menu, registrare prompt per i chiamanti, indicanti le azioni disponibili. Ad esempio. a seconda della struttura dell'operatore automatico, è possibile registrare il seguente script per lo spostamento nei menu durante l'orario non di ufficio illustrato nella tabella. Per lo spostamento nei menu durante l'orario non di ufficio illustrato nella tabella, ad esempio, è possibile registrare lo script seguente: "Per lasciare un messaggio per il reparto vendite, premere uno. Per conoscere l'orario di ufficio, premere due. Per conoscere l'indirizzo, premere tre."

10. Determinare la modalità di accesso dei chiamanti all'organizzazione. Considerare la modalità di ricerca e contatto degli utenti da parte dei chiamanti all'interno dell'organizzazione. Considerare anche la modalità di trasferimento dei chiamanti, incluso il modo in cui verranno indirizzati su una persona o un rappresentante dell'organizzazione, e se i chiamanti avranno accesso a un operatore durante l'orario di ufficio e non di ufficio.

11. Determinare quali chiamate potranno effettuare i chiamanti quando utilizzano un determinato operatore automatico. Ad esempio, se si desidera consentire ai chiamanti di effettuare chiamate a utenti in un singolo dial plan, a qualsiasi estensione, o se sarà consentito loro di effettuare chiamate al di fuori dell'organizzazione.

12. Una volta pianificate le impostazioni dell'operatore automatico, i messaggi di saluto e lo spostamento nei menu e aver creato file audio contenenti i messaggi di saluto registrati, i prompt per lo spostamento nei menu e le risposte per lo spostamento nei menu, è possibile creare e configurare l'operatore automatico. A tale scopo, attenersi alla procedura seguente:
    
      - [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md)
    
      - [Gestire un operatore automatico di messaggistica unificata](manage-a-um-auto-attendant-exchange-2013-help.md)

13. Se si sono create le impostazioni e la struttura dell'operatore automatico, abilitare l'operatore automatico di messaggistica unificata in modo da poter avviare l'accettazione delle chiamate.

