---
title: 'Identità: Exchange 2013 Help'
TOCTitle: Identità
ms:assetid: e90fae91-37e7-4fdc-9170-44f0dc965c66
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125042(v=EXCHG.150)
ms:contentKeyID: 50481914
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identità

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-04_

Il parametro *Identity* è un parametro speciale che può essere utilizzato con la maggior parte dei cmdlet. Il parametro *Identity* consente di accedere agli identificatori univoci che fanno riferimento a un particolare oggetto in Microsoft Exchange Server 2013. Questa capacità consente di eseguire azioni su un oggetto di Exchange 2013 specifico.

Nelle seguenti sezioni viene descritto il parametro Identity e vengono forniti esempi di utilizzo efficace dello stesso:

Characteristics of the Identity parameter

Wildcard characters in Identity

Examples of the Identity parameter

## Caratteristiche del parametro Identity

L'identificatore unico primario di un oggetto in Exchange 2013 è sempre un GUID. Un GUID è un identificatore a 128 bit, quale ad esempio `63d64005-42c5-4f8f-b310-14f6cb125bf3`. Questo GUID non si ripete mai, pertanto è sempre univoco. Tuttavia, non si desidera digitare i GUID regolarmente. Pertanto, il parametro *Identity* è composto in genere anche dai valori di altri parametri, o insiemi di valori combinati derivanti da vari parametri in un singolo oggetto. Viene garantita l'univocità di questi valori all'interno dell'insieme di oggetti. È possibile specificare i valori di questi parametri, ad esempio *Name* e *DistriguishedName*, oppure è possibile lasciare al sistema il compito di generarli. I parametri aggiuntivi utilizzati, se presenti, e le relative modalità di riempimento dipendono dall'oggetto a cui si fa riferimento.

Il parametro *Identity* è considerato anche un parametro posizionale. Nei casi in cui non viene specificata alcuna etichetta di parametro, si presuppone che il parametro *Identity* sia il primo argomento nel cmdlet. Questo riduce il numero delle pressioni di tasto durante la digitazione dei comandi. Per ulteriori informazioni sui parametri posizionali, vedere [Parametri](https://technet.microsoft.com/it-it/library/bb124388\(v=exchg.150\)).

Con il seguente esempio viene mostrato l'utilizzo del parametro *Identity* mediante il valore di parametro *Name* univoco del connettore di ricezione. Con questo esempio viene inoltre mostrato come sia possibile omettere il nome del parametro *Identity* poiché *Identity* è un parametro posizionale.
```powershell
    Get-ReceiveConnector -Identity "From the Internet"
    Get-ReceiveConnector "From the Internet"
```
Come tutti gli oggetti in Exchange 2013, è possibile fare riferimento al connettore di ricezione anche mediante il relativo GUID univoco. Ad esempio, se al connettore di ricezione denominato `"From the Internet"` viene assegnato anche il GUID `63d64005-42c5-4f8f-b310-14f6cb125bf3`, è possibile recuperare il connettore utilizzando il seguente comando:

```powershell
Get-ReceiveConnector 63d64005-42c5-4f8f-b310-14f6cb125bf3
```

Inizio pagina

## Caratteri jolly nel parametro Identity

Alcuni cmdlet **Get** possono accettare un carattere jolly (`*`) come parte del valore inviato a *Identity* durante l'esecuzione del cmdlet. Utilizzando un carattere jolly con il parametro *Identity*, è possibile specificare un nome parziale e recuperare un elenco di oggetti corrispondenti al nome parziale. È possibile inserire un carattere jolly all'inizio o alla fine del valore di *Identity*, ma non all'interno della stringa. Ad esempio, i comandi `Get-Mailbox David*` e `Get-Mailbox *anders*` sono validi, mentre `Get-Mailbox Reb*ca` non è un comando valido.

Alcuni cmdlet **Get** recuperano oggetti in Exchange 2013 organizzati in una relazione gerarchica o padre/figlio. In pratica, potrebbe esistere un insieme di oggetti padre che contiene anche i relativi oggetti figlio. Gli oggetti con una relazione padre/figlio possono avere un parametro *Identity* con la sintassi `<parent>\<child>`.

Se un parametro *Identity* presenta la sintassi `<parent>\<child>`, alcuni cmdlet consentono di utilizzare un carattere jolly (\*) per sostituire alcuni o tutti i nomi dei padri o dei figli. Ad esempio, se si desidera trovare tutti gli oggetti figlio denominati "Contoso" in tutti gli oggetti padre, è possibile utilizzare la sintassi `"*\Contoso"`. Analogamente, se si desidera trovare tutti gli oggetti figlio con nome parziale "Auth" esistenti nell'oggetto padre `"ServerA" `, è possibile utilizzare la sintassi `"ServerA\Auth*"`.

Alcuni cmdlet, ma non tutti, consentono di specificare solamente la parte relativa al figlio del parametro Identity durante l'esecuzione di un comando. In questo caso, i cmdlet utilizzano per impostazione predefinita l'oggetto padre corrente. Ad esempio, sia in MBX1 sia in MBX2 esistono due connettori di ricezione denominati "Contoso Receive Connector". Se si esegue il comando `Get-ReceiveConnector "Contoso Receive Connector"` su MBX2, viene restituito solo il connettore di ricezione del server MBX2.

Il comportamento specifico del parametro Identity e dei caratteri jolly dipende dal cmdlet in fase di esecuzione. Per ulteriori informazioni sul cmdlet in fase di esecuzione, vedere il contenuto specifico per quel cmdlet.

Inizio pagina

## Esempi del parametro Identity

Gli esempi descritti in questo argomento illustrano come il parametro *Identity* sia in grado di accettare valori univoci diversi per fare riferimento a oggetti specifici nell'organizzazione di Exchange 2013. Questi esempi illustrano inoltre come l'etichetta di parametro *Identity* possa essere omessa per ridurre il numero di pressioni di tasti durante la digitazione dei comandi.

## Messaggi DSN

Gli esempi di questa sezione fanno riferimento ai messaggi di notifica sullo stato del recapito (DSN, delivery status notification) che possono essere configurati in un'organizzazione di Exchange 2013. Il primo esempio mostra come recuperare DSN 5.4.1 mediante il cmdlet **Get-SystemMessage**. Nel cmdlet **Get-SystemMessage**, il parametro *Identity* è formato da diversi dati configurati su ciascun oggetto messaggio DSN. Questi dati includono il linguaggio di scrittura del DSN, l'ambito interno o esterno del DSN e il codice messaggio DSN, come nell'esempio che segue:

```powershell
Get-SystemMessage en\internal\5.4.1
```

È inoltre possibile recuperare il messaggio DSN utilizzando il relativo GUID come nell'esempio che segue, poiché tutti gli oggetti in Exchange 2013 possiedono un GUID:

```powershell
Get-SystemMessage 82ca7bde-1c2d-4aa1-97e1-f298a6f10222
```

Per ulteriori informazioni sulla composizione del parametro *Identity* quando viene utilizzato con i cmdlet **SystemMessage**, vedere [Identità del messaggio DSN](dsn-message-identity-exchange-2013-help.md).

## Voci del ruolo di gestione

Gli esempi in questa sezione fanno riferimento alle voci del ruolo di gestione che compongono i ruoli di gestione in Exchange 2013. I ruoli di gestione sono utilizzati per controllare le autorizzazioni concesse agli amministratori e agli utenti finali. Le voci del ruolo di gestione sono costituite da due parti: il ruolo di gestione a cui sono associate e un cmdlet. Il parametro Identity è anch'esso costituito dal nome del ruolo di gestione e dal nome del cmdlet. Ad esempio, di seguito è riportata la voce di ruolo per il cmdlet **Set-Mailbox** nel ruolo `Mail Recipients`.

```powershell
Mail Recipients\Set-Mailbox
```

La voce di ruolo `Mail Recipients\Set-Mailbox` è una delle varie voci nel ruolo `Mail Recipients`. Per visualizzare tutte le voci di ruolo nel ruolo `Mail Recipients`, utilizzare il seguente comando:
```powershell
    Get-ManagementRoleEntry "Mail Recipients\*"
```
Per visualizzare tutte le voci di ruolo nel ruolo `Mail Recipients` contenenti la stringa "`Mailbox`", utilizzare il seguente comando:
```powershell
    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*"
```
Per visualizzare tutti i ruoli di gestione che contengono **Set-Mailbox** come una delle voci di ruolo, utilizzare il seguente comando:
```powershell
    Get-ManagementRoleEntry *\Set-Mailbox
```
Con le voci di ruolo è possibile utilizzare il carattere jolly in diversi modi per recuperare da Exchange 2013 le informazioni desiderate.

Per ulteriori informazioni sui ruoli di gestione, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Inizio pagina

