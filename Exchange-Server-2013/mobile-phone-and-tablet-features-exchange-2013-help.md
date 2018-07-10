---
title: 'Telefono cellulare e caratteristiche tablet: Exchange 2013 Help'
TOCTitle: Telefono cellulare e caratteristiche tablet
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50555661
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Telefono cellulare e caratteristiche tablet

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Gli utenti possono accedere loro posta elettronica, calendario, contatti e informazioni sull'attività nel telefoni cellulari, Tablet e altri dispositivi portatili tramite Microsoft Exchange ActiveSync. È inoltre possibile utilizzare per configurare le firme e le risposte automatiche. Un'ampia gamma di telefoni e dispositivi mobili funziona con Exchange ActiveSync.


> [!NOTE]
> Anche se si fa riferimento in modo coerente per dispositivi che accedono Exchange Server 2013 come telefoni cellulari, esistono molti dispositivi che possono accedere Exchange 2013 ma che non dispongono di funzionalità telefono cellulare. Il termine "telefono cellulare" nella presente documentazione fa riferimento a questi dispositivi.



## Dispositivi Exchange ActiveSync compatibile

Gli utenti possono sfruttare le funzionalità avanzate di Exchange ActiveSync selezionando telefoni cellulari, che sono compatibili con Exchange ActiveSync. Tali telefoni cellulari sono disponibili numerosi produttori e su molti gestori telefonici. Per ulteriori informazioni, vedere la documentazione di cellulare specifico.

Telefoni cellulari, che sono compatibili con Microsoft Exchange includono quanto segue:

  - **Apple**   Apple iPhone, iPod Touch e iPad supportano Exchange ActiveSync.

  - **Windows Phone**   Windows Phone 8, Windows Phone 7 e versioni precedenti supportano Exchange ActiveSync.

  - **Android**   Molti cellulari e Tablet con il sistema operativo Android supportano Exchange ActiveSync. Tuttavia, questi dispositivi mobili potrebbero non supportare tutti i criteri cassetta postale di dispositivo mobile disponibili. Per ulteriori informazioni, vedere [Criteri cassetta postale di dispositivo mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

## Caratteristiche del software di Windows Phone

Telefoni cellulari, che dispone di una versione di Windows software telefonica come il sistema operativo offre la massima funzionalità durante la sincronizzazione con Exchange 2013. Nella tabella seguente sono elencati i criteri cassetta postale di dispositivo mobile che sono disponibili con Windows Phone 8 e Windows Phone 7.

### Windows Phone 7 e 8 caratteristiche

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema operativo</th>
<th>Caratteristiche</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 supporta i seguenti criteri cassetta postale di dispositivo mobile:</p>
<ul>
<li><p>Consenti password semplice dispositivo</p></li>
<li><p>Password alfanumerica obbligatoria</p></li>
<li><p>Password del dispositivo abilitata</p></li>
<li><p>Scadenza password dispositivo</p></li>
<li><p>IRM abilitato</p></li>
<li><p>Password del dispositivo massimo tentativi non riusciti</p></li>
<li><p>Blocco per tempo di inattività massimo dispositivo</p></li>
<li><p>Numero minimo di caratteri complessi per password dispositivo</p></li>
<li><p>Lunghezza della password dispositivo minimo</p></li>
<li><p>Richiedi crittografia dispositivo</p></li>
<li><p>Cancellazione remota</p></li>
</ul>

> [!WARNING]
> Se l'organizzazione utilizza altre impostazioni dei criteri cassetta postale di dispositivo mobile, è necessario impostare il criterio <STRONG>Consenti dispositivi senza provisioning</STRONG> su true. Ciò può avere implicazioni di sicurezza per l'organizzazione, poiché saranno consentiti altri telefoni e dispositivi mobili che non soddisfano tutti i requisiti delle impostazioni dei criteri dispositivi mobili da sincronizzare. Per ulteriori informazioni, vedere <A href="mobile-device-mailbox-policies-exchange-2013-help.md">Criteri cassetta postale di dispositivo mobile</A>.


</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Telefoni cellulari Windows Phone 7 supporta solo un sottoinsieme di tutte le impostazioni dei criteri cassetta postale di Exchange ActiveSync:</p>
<ul>
<li><p>Uso di password</p></li>
<li><p>Lunghezza minima password</p></li>
<li><p>Tempo massimo di inattività prima del blocco</p></li>
<li><p>Password del dispositivo massimo tentativi non riusciti</p></li>
<li><p>Consenti password semplice</p></li>
<li><p>Scadenza password</p></li>
<li><p>Cronologia password</p></li>
<li><p>Disabilitare archiviazione rimovibile</p></li>
<li><p>Disabilitare IrDA</p></li>
<li><p>Disabilitare la sincronizzazione desktop</p></li>
<li><p>Desktop remoto blocco</p></li>
<li><p>Blocca la condivisione Internet</p></li>
</ul></td>
</tr>
</tbody>
</table>

