---
title: 'Note di configurazione per session border controller supportati: Exchange 2013 Help'
TOCTitle: Note di configurazione per session border controller supportati
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50555685
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Note di configurazione per session border controller supportati

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-07-25_

I controller SBC (session border controller) abilitano alla connessione della rete di telefonia locale in un datacenter Microsoft tramite una connessione WAN pubblica dedicata. Un SBC si colloca sul perimetro della rete IP locale e si connette a un secondo SBC in un datacenter Microsoft.

Gli SBC richiedono l'utilizzo di certificati digitali per crittografare tutto il traffico tra l'organizzazione on-premises e il datacenter Microsoft. È necessario ottenere un certificato digitale per l'elemento di limite della rete, ad esempio un session border controller, che si utilizza per comunicare con le distribuzioni di Exchange ibride e online. I certificati digitali consentono di stabilire l'attendibilità tra l'organizzazione on-premises e il datacenter Microsoft, nonché di abilitare la sicurezza reciproca a livello di trasporto (Mutual TLS o MTLS). Dopo avere stabilito questa attendibilità, gli elementi di limite della rete nell'organizzazione on-premises e nel datacenter Microsoft consentono di scambiare le chiavi di sessione e di utilizzare tali chiavi per crittografare il successivo traffico di dati.

Nelle distribuzioni ibride oppure online un gateway IP di messaggistica unificata rappresenta un SBC. Il nome comune dell'oggetto nel certificato deve essere uguale al nome di dominio completo presente nella casella Indirizzo del gateway IP di messaggistica unificata creato. Se ad esempio si specifica l'indirizzo per il nome di dominio completo sbcexternal.contoso.com nel gateway IP di messaggistica unificata, assicurarsi che il nome dell'oggetto e il nome alternativo dell'oggetto nel certificato contengano lo stesso valore: sbcexternal.contoso.com. Per il nome utilizzato si applica la distinzione tra maiuscole e minuscole, assicurarsi pertanto che la stessa distinzione venga applicata sia al certificato che al gateway IP di messaggistica unificata. Se si usa un Acme Packet SBC e il nome comune non corrisponde al nome FQDN del gateway IP di messaggistica unificata, la chiamata verrà respinta con un errore 403.


> [!NOTE]
> Poiché SBCs sono progettati per risiedono nel perimetro della rete, anche fungono da un firewall. Se si imposta un SBC dal firewall dell'organizzazione, può causare problemi di configurazione e non è supportata per la connessione a Office 365.



## SBC supportati

I session border controller (SBC) seguenti sono stati correttamente testati per l'interoperabilità con le distribuzioni di Exchange ibride e online. Notare che le funzionalità e le compatibilità dei controller SBC possono variare e la loro configurazione dipende dagli altri dispositivi sulla rete. Rivolgersi al produttore del controller SBC per verificare se sono presenti specifiche note di configurazione per la messaggistica unificata in una distribuzione ibrida oppure online.


> [!NOTE]
> Supporto in linea di messaggistica unificata di Exchange per i sistemi PBX di terze parti tramite connessioni dirette dal cliente utilizzati SBCs terminerà in 2018 luglio. Vedere blog del team di Exchange <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">cessazione del supporto per i session border controller in Exchange Online della messaggistica unificata</A> per ulteriori informazioni.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Fornitore</strong></p></td>
<td><p><strong>Modello</strong></p></td>
<td><p><strong>Note di configurazione</strong></p></td>
<td><p><strong>Commenti</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 oppure 4500</p></td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>Session border controller dedicato</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>Session border controller dedicato</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>SBC e IP gateway</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!NOTE]
> Deve disporre S3 IOS 15,4 (3) o versione successiva.


</td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>Session border controller dedicato</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>Dedicato SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>Opzione SBC per il prodotto gateway VoIP</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 o versione successiva</p></td>
<td><p><strong>Contattare il fornitore dell'hardware per aggiornati istruzioni su come impostare il dispositivo.</strong></p></td>
<td><p>Dedicato SBC</p></td>
</tr>
</tbody>
</table>

