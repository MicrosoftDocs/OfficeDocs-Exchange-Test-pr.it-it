---
title: 'Cosa cercare i tipi di informazioni riservate in Exchange: Exchange 2013 Help'
TOCTitle: Tipi di informazioni riservate disponibili da cercare
ms:assetid: 98b81f9c-87bb-4905-8e53-04621c3ae74d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150541(v=EXCHG.150)
ms:contentKeyID: 50479844
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cosa cercare i tipi di informazioni riservate in Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-05-03_

Prevenzione perdita dati (DLP) in Exchange include 80 tipi di informazioni riservate che si desidera utilizzare i criteri DLP. In questo argomento vengono elencati tutti questi tipi di informazioni riservate di un criterio DLP aspetto quando viene rilevato ogni tipo. Da un criterio che può essere identificato in base a un'espressione regolare o una funzione viene definito un tipo di informazioni riservate. Inoltre, elemento avvalorante, ad esempio parole chiave e checksum utilizzabile per identificare il tipo di informazioni riservate. Livello di probabilità e prossimità vengono inoltre utilizzati nel processo di valutazione.

## Numero di registrazione ABA


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre formattate o meno</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Formattato:</p>
<ul>
<li><p>Quattro cifre che iniziano con 0, 1, 2, 3, 6, 7 o 8</p></li>
<li><p>Una lineetta</p></li>
<li><p>Quattro cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Una cifra</p></li>
</ul>
<p>Non formattato:</p>
<ul>
<li><p>9 cifre consecutive che iniziano con 0, 1, 2, 3, 6, 7 o 8</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_aba_routing</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_ABA_Routing</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- ABA Routing Number -->
<Entity id="cb353f78-2b72-4c3c-8827-92ebe4f69fdf" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_aba_routing" />
        <Match idRef="Keyword_ABA_Routing" />
      </Pattern>
 </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-1"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ABA_Routing</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>aba</p>
<p>aba #</p>
<p>aba routing #</p>
<p>aba routing number</p>
<p>aba #</p>
<p>abarouting#</p>
<p>aba number</p>
<p>abaroutingnumber</p>
<p>american bank association routing #</p>
<p>american bank association routing number</p>
<p>americanbankassociationrouting#</p>
<p>americanbankassociationroutingnumber</p>
<p>bank routing number</p>
<p>bankrouting#</p>
<p>bankroutingnumber</p>
<p>routing transit number</p>
<p>RTN</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Argentina - Numero di identità nazionale (DNI)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Otto cifre separate da spazi</p></td>
</tr>
<tr class="even">
<td><p>Motivo</p></td>
<td><p>Otto cifre</p>
<ul>
<li><p>Due cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_argentina_national_id</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_argentina_national_id</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Argentina National Identity (DNI) Number -->
<Entity id="eefbb00e-8282-433c-8620-8f1da3bffdb2" recommendedConfidence="75" patternsProximity="300">
   <Pattern confidenceLevel="75">
      <IdMatch idRef="Regex_argentina_national_id"/>
      <Match idRef="Keyword_argentina_national_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-3"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_argentina_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Argentina - Numero di identità nazionale</p>
<p>Identità</p>
<p>Identificazione Carta d’identità nazionale</p>
<p>DNI</p>
<p>Scheda di interfaccia di rete (NIC) Registro nazionale delle persone</p>
<p>Documento Nacional de Identidad</p>
<p>Registro Nacional de las Personas</p>
<p>Identidad</p>
<p>Identificación</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Australia - Numero di conto bancario


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>6-10 cifre con o senza un numero BSB (Bank/State/Branch)</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Il numero di conto comprende 6-10 cifre.</p>
<p>Numero BSB australiano:</p>
<ul>
<li><p>Tre cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Tre cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_australia_bank_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_australia_bank_account_number</code>.</p></li>
<li><p>L'espressione regolare <code>Regex_australia_bank_account_number_bsb</code> restituisce contenuti che corrispondono al modello.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_australia_bank_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_australia_bank_account_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Bank Account Number -->
<Entity id="74a54de9-2a30-4aa0-a8aa-3d9327fc07c7" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_australia_bank_account_number" />
        <Match idRef="Keyword_australia_bank_account_number" />
        <Match idRef="Regex_australia_bank_account_number_bsb" />
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_bank_account_number" />
        <Match idRef="Keyword_australia_bank_account_number" />
  </Pattern>
 </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-5"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_australia_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>swift bank code</p>
<p>correspondent bank</p>
<p>base currency</p>
<p>usa account</p>
<p>holder address</p>
<p>bank address</p>
<p>information account</p>
<p>fund transfers</p>
<p>bank charges</p>
<p>bank details</p>
<p>banking information</p>
<p>full names</p>
<p>iaea</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Australia - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Nove lettere e numeri</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Nove lettere e numeri:</p>
<ul>
<li><p>Due cifre o lettere (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>Due cifre</p></li>
<li><p>Cinque cifre o lettere (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>OPPURE</p></li>
<li><p>1-2 lettere facoltative (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>4-9 cifre</p></li>
<li><p>OPPURE</p></li>
<li><p>Nove cifre o lettere (senza distinzione tra maiuscole/minuscole)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_australia_drivers_license_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_australia_drivers_license_number</code>.</p></li>
<li><p>Non vengono trovate parole chiava da <code>Keyword_australia_drivers_license_number_exclusions</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Drivers License Number -->
<Entity id="1cbbc8f5-9216-4392-9eb5-5ac2298d1356" patternsProximity="300" recommendedConfidence="75">
   <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_drivers_license_number" />
        <Match idRef="Keyword_australia_drivers_license_number" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_australia_drivers_license_number_exclusions" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-7"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_australia_drivers_license_number</p></th>
<th><p>Keyword_australia_drivers_license_number_exclusions</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>international driving permits</p>
<p>australian automobile association</p>
<p>sydney nsw</p>
<p>international driving permit</p>
<p>DriverLicence</p>
<p>DriverLicences</p>
<p>Driver Lic</p>
<p>Driver Licence</p>
<p>Driver Licences</p>
<p>DriversLic</p>
<p>DriversLicence</p>
<p>DriversLicences</p>
<p>Drivers Lic</p>
<p>Drivers Lics</p>
<p>Drivers Licence</p>
<p>Drivers Licences</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver'Licence</p>
<p>Driver'Licences</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver'Licence</p>
<p>Driver' Licences</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicence</p>
<p>Driver'sLicences</p>
<p>Driver's Lic</p>
<p>Driver's Lics</p>
<p>Driver's Licence</p>
<p>Driver's Licences</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicence#</p>
<p>DriverLicences#</p>
<p>Driver Lic#</p>
<p>Driver Lics#</p>
<p>Driver Licence#</p>
<p>Driver Licences#</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicence#</p>
<p>DriversLicences#</p>
<p>Drivers Lic#</p>
<p>Drivers Lics#</p>
<p>Drivers Licence#</p>
<p>Drivers Licences#</p>
<p>Driver'Lic#</p>
<p>Driver'Lics#</p>
<p>Driver'Licence#</p>
<p>Driver'Licences#</p>
<p>Driver'Lic#</p>
<p>Driver'Lics#</p>
<p>Driver'Licence#</p>
<p>Driver'Licences#</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicence#</p>
<p>Driver'sLicences#</p>
<p>Driver's Lic#</p>
<p>Driver's Lics#</p>
<p>Driver's Licence#</p>
<p>Driver's Licences#</p></td>
<td><p>aaa</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Driver'License</p>
<p>Driver'Licenses</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>Driver License#</p>
<p>Driver Licenses#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>Drivers License#</p>
<p>Drivers Licenses#</p>
<p>Driver'License#</p>
<p>Driver'Licenses#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver's License#</p>
<p>Driver's Licenses#</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Australia - Numero di tessera sanitaria


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10-11 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10-11 cifre:</p>
<ul>
<li><p>La prima cifra è compresa nell'intervallo 2-6</p></li>
<li><p>La nona cifra è una cifra di controllo</p></li>
<li><p>La decima cifra è la cifra del problema</p></li>
<li><p>L'undicesima cifra (facoltativa) è il numero singolo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 95%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_australian_medical_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_Australia_Medical_Account_Number</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_australian_medical_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Medical Account Number -->
<Entity id="104a99a0-3d3b-4542-a40d-ab0b9e1efe63" recommendedConfidence="85" patternsProximity="300">
    <Pattern confidenceLevel="95">
     <IdMatch idRef="Func_australian_medical_account_number"/>
     <Any minMatches="1">
     <Match idRef="Keyword_Australia_Medical_Account_Number"/>
     </Any>
  </Pattern>
<Pattern confidenceLevel="85">
     <IdMatch idRef="Func_australian_medical_account_number"/>
     <Any minMatches="0" maxMatches="0">
  <Match idRef="Keyword_Australia_Medical_Account_Number"/>
     </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-9"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Australia_Medical_Account_Number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>bank account details</p>
<p>medicare payments</p>
<p>mortgage account</p>
<p>bank payments</p>
<p>information branch</p>
<p>credit card loan</p>
<p>department of human services</p>
<p>local service</p>
<p>medicare</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Australia - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Una lettera seguita da sette cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Una lettera (senza distinzione tra maiuscole/minuscole) seguita da sette cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_australia_passport_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_passport</code> o da <code>Keyword_australia_passport_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Passport Number -->
<Entity id="29869db6-602d-4853-ab93-3484f905df50" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_passport" />
          <Match idRef="Keyword_australia_passport_number" />
        </Any>
   </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-11"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
<th><p>Keyword_australia_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート ＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
<td><p>passport</p>
<p>passport details</p>
<p>immigration and citizenship</p>
<p>commonwealth of australia</p>
<p>department of immigration</p>
<p>residential address</p>
<p>department of immigration and citizenship</p>
<p>visa</p>
<p>national identity card</p>
<p>passport number</p>
<p>travel document</p>
<p>issuing authority</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Australia - Identificativo fiscale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>8-9 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>8-9 cifre in genere presentate con spazi, come mostrato di seguito:</p>
<ul>
<li><p>Tre cifre</p></li>
<li><p>Uno spazio facoltativo</p></li>
<li><p>Tre cifre</p></li>
<li><p>Uno spazio facoltativo</p></li>
<li><p>2-3 cifre e l'ultima è una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 95%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_australian_tax_file_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_Australia_Tax_File_Number</code>.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_number_exclusions</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_australian_tax_file_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_Australia_Tax_File_Number</code> o da <code>Keyword_number_exclusions</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Australia Tax File Number -->
<Entity id="e29bc95f-ff70-4a37-aa01-04d17360a4c5" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="95">
        <IdMatch idRef="Func_australian_tax_file_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_Australia_Tax_File_Number" />
        </Any>
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_number_exclusions" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_australian_tax_file_number" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_Australia_Tax_File_Number" />
          <Match idRef="Keyword_number_exclusions" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-13"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Australia_Tax_File_Number</p></th>
<th><p>Keyword_number_exclusions</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>australian business number</p>
<p>marginal tax rate</p>
<p>medicare levy</p>
<p>portfolio number</p>
<p>service veterans</p>
<p>withholding tax</p>
<p>individual tax return</p>
<p>tax file number</p></td>
<td><p>00000000</p>
<p>11111111</p>
<p>22222222</p>
<p>33333333</p>
<p>44444444</p>
<p>55555555</p>
<p>66666666</p>
<p>77777777</p>
<p>88888888</p>
<p>99999999</p>
<p>000000000</p>
<p>111111111</p>
<p>222222222</p>
<p>333333333</p>
<p>444444444</p>
<p>555555555</p>
<p>666666666</p>
<p>777777777</p>
<p>888888888</p>
<p>999999999</p>
<p>0000000000</p>
<p>1111111111</p>
<p>2222222222</p>
<p>3333333333</p>
<p>4444444444</p>
<p>5555555555</p>
<p>6666666666</p>
<p>7777777777</p>
<p>8888888888</p>
<p>9999999999</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Belgio - Numero nazionale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>11 cifre più delimitatori</p></td>
</tr>
<tr class="even">
<td><p>Motivo</p></td>
<td><p>11 cifre più delimitatori:</p>
<ul>
<li><p>Sei cifre e due punti nel formato AA.MM.GG per data di nascita</p></li>
<li><p>Una lineetta</p></li>
<li><p>Tre cifre sequenziali (dispari sia per uomini che per donne)</p></li>
<li><p>Un punto</p></li>
<li><p>Due cifre, ovvero una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_belgium_national_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_belgium_national_number</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Belgium National Number -->
  <Entity id="fb969c9e-0fd1-4b18-8091-a2123c5e6a54" recommendedConfidence="75" patternsProximity="300">
   <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_belgium_national_number"/>
     <Match idRef="Keyword_belgium_national_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-15"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_belgium_national_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identità</p>
<p>Registrazione</p>
<p>Identificazione</p>
<p>ID</p>
<p>Identiteitskaart</p>
<p>Registratie nummer</p>
<p>Identificatie nummer</p>
<p>Identiteit</p>
<p>Registratie</p>
<p>Identificatie</p>
<p>Carte d’identité</p>
<p>numéro d'immatriculation</p>
<p>numéro d'identification</p>
<p>identité</p>
<p>iscrizione</p>
<p>Identifikation</p>
<p>Identifizierung</p>
<p>Identifikationsnummer</p>
<p>Personalausweis</p>
<p>Registrierung</p>
<p>Registrationsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Brasile - Codice fiscale persone giuridiche (CNPJ)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>14 cifre che includono il numero di registrazione, il codice della filiale, le cifre di controllo e i delimitatori</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>14 cifre più delimitatori:</p>
<ul>
<li><p>Due cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre (le prime otto sono il numero di registrazione)</p></li>
<li><p>Una barra</p></li>
<li><p>Numero del ramo a quattro cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Due cifre, ovvero le cifre di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_brazil_cnpj</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_brazil_cnpj</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_brazil_cnpj</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Brazil Legal Entity Number (CNPJ) -->
<Entity id="9b58b5cd-5e90-4df6-b34f-1ebcc88ceae4" recommendedConfidence="85" patternsProximity="300">
   <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_cnpj"/>
     <Match idRef="Keyword_brazil_cnpj"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_cnpj"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-17"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_cnpj</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNPJ</p>
<p>CNPJ/MF</p>
<p>CNPJ-MF</p>
<p>Codice fiscale persone giuridiche</p>
<p>Registro contribuenti</p>
<p>Persona giuridica</p>
<p>Persone giuridiche</p>
<p>Stato della registrazione</p>
<p>Ufficio</p>
<p>Società</p>
<p>CNPJ</p>
<p>Cadastro Nacional da Pessoa Jurídica</p>
<p>Cadastro Geral de Contribuintes</p>
<p>CGC</p>
<p>Pessoa jurídica</p>
<p>Pessoas jurídicas</p>
<p>Situação cadastral</p>
<p>Inscrição</p>
<p>Empresa</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero CPF Brasile


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>11 cifre che includono una cifra di controllo e possono essere formattate o non formattate</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Formattato:</p>
<ul>
<li><p>Tre cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Due cifre, ovvero le cifre di controllo</p></li>
</ul>
<p>Non formattate:</p>
<ul>
<li><p>11 cifre dove le ultime due sono cifre di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_brazil_cpf</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_brazil_cpf</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_brazil_cpf</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Brazil CPF Number -->
<Entity id="78e09124-f2c3-4656-b32a-c1a132cd2711" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_cpf"/>
     <Match idRef="Keyword_brazil_cpf"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_cpf"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-19"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_cpf</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPF</p>
<p>Identificazione</p>
<p>Registrazione</p>
<p>Ricavi</p>
<p>Cadastro de Pessoas Físicas</p>
<p>Imposto</p>
<p>Identificação</p>
<p>Inscrição</p>
<p>Receita</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carta d'identità (Brasile) (RG)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Registro Geral (formato precedente)</p>
<dl>
<dd><p>9 cifre</p>
</dd>
</dl>
<p>Registro de Identidade (RIC) (nuovo formato)</p>
<dl>
<dd><p>11 cifre</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Registro Geral (formato precedente):</p>
<ul>
<li><p>Due cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Una cifra, ovvero una cifra di controllo</p></li>
</ul>
<p>Registro de Identidade (RIC) (nuovo formato)</p>
<ul>
<li><p>10 cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Una cifra, ovvero una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_brazil_rg</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_brazil_rg</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_brazil_rg</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Brazil National ID Card (RG) -->
<Entity id="486de900-db70-41b3-a886-abdf25af119c" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_rg"/>
     <Match idRef="Keyword_brazil_rg"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_rg"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-21"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_rg</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cédula de identidade</p>
<p>carta di identità</p>
<p>national id</p>
<p>número de rregistro</p>
<p>registro de Iidentidade</p>
<p>registro geral</p>
<p>RG (per questa parola chiave viene fatta distinzione tra maiuscole e minuscole)</p>
<p>RIC (per questa parola chiave viene fatta distinzione tra maiuscole e minuscole)</p>
<p></p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Canada - Numero di conto bancario


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>7 o 12 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Un numero di conto corrente canadese comprende 7 o 12 cifre.</p>
<p>Un numero di transito bancario canadese comprende:</p>
<ul>
<li><p>Cinque cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Tre cifre</p>
<p>OPPURE</p></li>
<li><p>Uno zero &quot;0&quot;</p>
<p>Otto cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_canada_bank_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_canada_bank_account_number</code>.</p></li>
<li><p>L'espressione regolare <code>Regex_canada_bank_account_transit_number</code> restituisce contenuti che corrispondono al modello.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_canada_bank_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_canada_bank_account_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Bank Account Number -->
<Entity id="552e814c-cb50-4d94-bbaa-bb1d1ffb34de" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_canada_bank_account_number" />
        <Match idRef="Keyword_canada_bank_account_number" />
        <Match idRef="Regex_canada_bank_account_transit_number" />
   </Pattern>
   <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_bank_account_number" />
        <Match idRef="Keyword_canada_bank_account_number" />
   </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-23"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>canada savings bonds</p>
<p>canada revenue agency</p>
<p>canadian financial institution</p>
<p>direct deposit form</p>
<p>canadian citizen</p>
<p>legal representative</p>
<p>notary public</p>
<p>commissioner for oaths</p>
<p>child care benefit</p>
<p>universal child care</p>
<p>canada child tax benefit</p>
<p>income tax benefit</p>
<p>harmonized sales tax</p>
<p>social insurance number</p>
<p>income tax refund</p>
<p>child tax benefit</p>
<p>territorial payments</p>
<p>institution number</p>
<p>deposit request</p>
<p>banking information</p>
<p>direct deposit</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Canada - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Varia in base alla provincia</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Vari modelli per Alberta, Columbia Britannica, Manitoba, Nuovo Brunswick, Terranova e Labrador, Nuova Scozia, Ontario, Isola del Principe Edoardo, Quebec e Saskatchewan</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_[province_name]_drivers_license_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_[province_name]_drivers_license_name</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_canada_drivers_license</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Driver&#39;s License Number -->
    <Entity id="37186abb-8e48-4800-ad3c-e3d1610b3db0" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_alberta_drivers_license_number" />
        <Match idRef="Keyword_alberta_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_british_columbia_drivers_license_number" />
        <Match idRef="Keyword_british_columbia_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_manitoba_drivers_license_number" />
        <Match idRef="Keyword_manitoba_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_new_brunswick_drivers_license_number" />
        <Match idRef="Keyword_new_brunswick_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_newfoundland_labrador_drivers_license_number" />
        <Match idRef="Keyword_newfoundland_labrador_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_nova_scotia_drivers_license_number" />
        <Match idRef="Keyword_nova_scotia_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_ontario_drivers_license_number" />
        <Match idRef="Keyword_ontario_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_prince_edward_island_drivers_license_number" />
        <Match idRef="Keyword_prince_edward_island_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_quebec_drivers_license_number" />
        <Match idRef="Keyword_quebec_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_saskatchewan_drivers_license_number" />
        <Match idRef="Keyword_saskatchewan_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-25"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_[province_name]_drivers_license_name</p></th>
<th><p>Keyword_canada_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>L'abbreviazione della provincia, ad esempio, AB</p>
<p>Il nome della provincia, ad esempio, Alberta</p></td>
<td><p>DL</p>
<p>DLS</p>
<p>CDL</p>
<p>CDLS</p>
<p>DriverLic</p>
<p>DriverLics</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>DriverLicence</p>
<p>DriverLicences</p>
<p>Driver Lic</p>
<p>Driver Lics</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>Driver Licence</p>
<p>Driver Licences</p>
<p>DriversLic</p>
<p>DriversLics</p>
<p>DriversLicence</p>
<p>DriversLicences</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Drivers Lic</p>
<p>Drivers Lics</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Drivers Licence</p>
<p>Drivers Licences</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver'Licence</p>
<p>Driver'Licences</p>
<p>Driver'Lic</p>
<p>Driver' Lics</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver' Licence</p>
<p>Driver' Licences</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver'sLicence</p>
<p>Driver'sLicences</p>
<p>Driver's Lic</p>
<p>Driver's Lics</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>Driver's Licence</p>
<p>Driver's Licences</p>
<p>Permis de Conduire</p>
<p>id</p>
<p>ids</p>
<p>idcard number</p>
<p>idcard numbers</p>
<p>idcard #</p>
<p>idcard #s</p>
<p>idcard card</p>
<p>idcard cards</p>
<p>idcard</p>
<p>identification number</p>
<p>identification numbers</p>
<p>identification #</p>
<p>identification #s</p>
<p>identification card</p>
<p>identification cards</p>
<p>identification</p>
<p>DL#</p>
<p>DLS#</p>
<p>CDL#</p>
<p>CDLS#</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>DriverLicence#</p>
<p>DriverLicences#</p>
<p>Driver Lic#</p>
<p>Driver Lics#</p>
<p>Driver License#</p>
<p>Driver Licenses#</p>
<p>Driver License#</p>
<p>Driver Licences#</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>DriversLicence#</p>
<p>DriversLicences#</p>
<p>Drivers Lic#</p>
<p>Drivers Lics#</p>
<p>Drivers License#</p>
<p>Drivers Licenses#</p>
<p>Drivers Licence#</p>
<p>Drivers Licences#</p>
<p>Driver'Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' License#</p>
<p>Driver'Licenses#</p>
<p>Driver'Licence#</p>
<p>Driver'Licences#</p>
<p>Driver' Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver' Licence#</p>
<p>Driver' Licences#</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver'sLicence#</p>
<p>Driver'sLicences#</p>
<p>Driver's Lic#</p>
<p>Driver's Lics#</p>
<p>Driver's License#</p>
<p>Driver's Licenses#</p>
<p>Driver's Licence#</p>
<p>Driver's Licences#</p>
<p>Permis de Conduire#</p>
<p>id#</p>
<p>ids#</p>
<p>idcard card#</p>
<p>idcard cards#</p>
<p>idcard#</p>
<p>identification card#</p>
<p>identification cards#</p>
<p>identification#</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Canada - Codice del servizio sanitario


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_canada_health_service_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_canada_health_service_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Health Service Number -->
<Entity id="59c0bf39-7fab-482c-af25-00faa4384c94" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_health_service_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_canada_health_service_number" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-27"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_health_service_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>personal health number</p>
<p>patient information</p>
<p>health services</p>
<p>speciality services</p>
<p>automobile accident</p>
<p>patient hospital</p>
<p>psychiatrist</p>
<p>workers compensation</p>
<p>disability</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Canada - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Due lettere maiuscole seguite da 6 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Due lettere maiuscole seguite da 6 cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_canada_passport_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_canada_passport_number</code> o da <code>Keyword_passport</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Passport Number -->
<Entity id="14d0db8b-498a-43ed-9fca-f6097ae687eb" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_canada_passport_number" />
          <Match idRef="Keyword_passport" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-29"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_passport_number</p></th>
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>canadian citizenship</p>
<p>canadian passport</p>
<p>passport application</p>
<p>passport photos</p>
<p>certified translator</p>
<p>canadian citizens</p>
<p>processing times</p>
<p>renewal application</p></td>
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Canada - Numero di identificazione sanitaria personale (PHIN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>9 cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_canada_phin</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Vengono trovate almeno due parole chiave da <code>Keyword_canada_phin</code> o da <code>Keyword_canada_provinces</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada PHIN -->
<Entity id="722e12ac-c89a-4ec8-a1b7-fea3469f89db" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_phin" />
        <Any minMatches="2">
          <Match idRef="Keyword_canada_phin" />
          <Match idRef="Keyword_canada_provinces" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-31"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_phin</p></th>
<th><p>Keyword_canada_provinces</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>social insurance number</p>
<p>health information act</p>
<p>income tax information</p>
<p>manitoba health</p>
<p>health registration</p>
<p>prescription purchases</p>
<p>benefit eligibility</p>
<p>personal health</p>
<p>power of attorney</p>
<p>registration number</p>
<p>personal health number</p>
<p>practitioner referral</p>
<p>wellness professional</p>
<p>patient referral</p>
<p>health and wellness</p></td>
<td><p>Nunavut</p>
<p>Quebec</p>
<p>Northwest Territories</p>
<p>Ontario</p>
<p>British Columbia</p>
<p>Alberta</p>
<p>Saskatchewan</p>
<p>Manitoba</p>
<p>Yukon</p>
<p>Newfoundland and Labrador</p>
<p>New Brunswick</p>
<p>Nova Scotia</p>
<p>Prince Edward Island</p>
<p>Canada</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Canada - Numero di assicurazione sociale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre con spazi o lineette facoltativi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Formattato:</p>
<ul>
<li><p>Tre cifre</p></li>
<li><p>Una lineetta o uno spazio</p></li>
<li><p>Tre cifre</p></li>
<li><p>Una lineetta o uno spazio</p></li>
<li><p>Tre cifre</p></li>
</ul>
<p>Non formattato:</p>
<ul>
<li><p>9 cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_canadian_sin</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Almeno due delle seguenti combinazioni:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_sin</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_sin_collaborative</code>.</p></li>
<li><p>La funzione <code>Func_eu_date</code> rileva una data nel formato corretto.</p></li>
</ul></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_unformatted_canadian_sin</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_sin</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Canada Social Insurance Number -->
<Entity id="a2f29c85-ecb8-4514-a610-364790c0773e" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_canadian_sin" />
        <Any minMatches="2">
          <Match idRef="Keyword_sin" />
          <Match idRef="Keyword_sin_collaborative" />
          <Match idRef="Func_eu_date" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_canadian_sin" />
        <Match idRef="Keyword_sin" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-33"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_sin</p></th>
<th><p>Keyword_sin_collaborative</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>sin</p>
<p>social insurance</p>
<p>numero d'assurance sociale</p>
<p>sins</p>
<p>ssn</p>
<p>ssns</p>
<p>social security</p>
<p>numero d'assurance social</p>
<p>national identification number</p>
<p>national id</p>
<p>sin#</p>
<p>soc ins</p>
<p>social ins</p></td>
<td><p>driver's license</p>
<p>drivers license</p>
<p>driver's licence</p>
<p>drivers licence</p>
<p>DOB</p>
<p>Birthdate</p>
<p>Birthday</p>
<p>Date of Birth</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Cile - Numero di carta di identità


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>7-8 cifre più delimitatori, una cifra di controllo o una lettera</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>7-8 cifre più delimitatori:</p>
<ul>
<li><p>1-2 cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un punto</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un trattino</p></li>
<li><p>Una cifra o una lettera (senza distinzione tra maiuscole e minuscole) che corrisponde a una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_chile_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_chile_id_card</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_chile_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Chile Identity Card Number -->
<Entity id="4e979794-49a0-407e-a0b9-2c536937b925" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_chile_id_card"/>
     <Match idRef="Keyword_chile_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_chile_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-35"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_chile_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero di carta d’identità</p>
<p>Carta di identità</p>
<p>ID</p>
<p>Identificazione</p>
<p>Rol Único Nacional</p>
<p>RUN</p>
<p>Rol Único Tributario</p>
<p>RUT</p>
<p>Cédula de Identidad</p>
<p>Número De Identificación Nacional</p>
<p>Tarjeta de identificación</p>
<p>Identificación</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero carta di identità per residenti in Cina (RPC)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>18 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>18 cifre:</p>
<ul>
<li><p>Sei cifre, ovvero un codice indirizzo</p></li>
<li><p>Otto cifre nel formato AAAAMMGG, ovvero la data di nascita</p></li>
<li><p>Tre cifre, ovvero un codice di ordine</p></li>
<li><p>Una cifra, ovvero una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_china_resident_id</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_china_resident_id</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_china_resident_id</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- China Resident Identity Card (PRC) Number -->
<Entity id="c92daa86-2d16-4871-901f-816b3f554fc1" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_china_resident_id"/>
     <Match idRef="Keyword_china_resident_id"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_china_resident_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-37"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_china_resident_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta d’identità per residenti</p>
<p>RPC</p>
<p>Carta d’identità</p>
<p>身份证</p>
<p>居民 身份证</p>
<p>居民身份证</p>
<p>鉴定</p>
<p>身分證</p>
<p>居民 身份證</p>
<p>鑑定</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Credit Card Number


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>16 cifre che possono essere formattate o non formattato (dddddddddddddddd) e deve superare la verifica Luhn.</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Modello molto complesso e solido che rileva carte di credito dei maggiori circuiti del mondo, ad esempio, Visa, MasterCard, Discover Card, JCB, American Express, nonché carte regalo e ticket restaurant.</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Yes, il checksum Luhn</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_credit_card</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_cc_verification</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_cc_name</code>.</p></li>
<li><p>La funzione <code>Func_expiration_date</code> rileva una data nel formato corretto.</p></li>
</ul></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_credit_card</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Credit Card Number -->
<Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_credit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_cc_verification" />
          <Match idRef="Keyword_cc_name" />
          <Match idRef="Func_expiration_date" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_credit_card" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-39"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_cc_verification</p></th>
<th><p>Keyword_cc_name</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>card verification</p>
<p>card identification number</p>
<p>cvn</p>
<p>cid</p>
<p>cvc2</p>
<p>cvv2</p>
<p>pin block</p>
<p>security code</p>
<p>security number</p>
<p>security no</p>
<p>issue number</p>
<p>issue no</p>
<p>cryptogramme</p>
<p>numéro de sécurité</p>
<p>numero de securite</p>
<p>kreditkartenprüfnummer</p>
<p>kreditkartenprufnummer</p>
<p>prüfziffer</p>
<p>prufziffer</p>
<p>sicherheits Kode</p>
<p>sicherheitscode</p>
<p>sicherheitsnummer</p>
<p>verfalldatum</p>
<p>codice di verifica</p>
<p>cod. sicurezza</p>
<p>cod sicurezza</p>
<p>n autorizzazione</p>
<p>código</p>
<p>codigo</p>
<p>cod. seg</p>
<p>cod seg</p>
<p>código de segurança</p>
<p>codigo de seguranca</p>
<p>codigo de segurança</p>
<p>código de seguranca</p>
<p>cód. segurança</p>
<p>cod. seguranca cod. segurança</p>
<p>cód. seguranca</p>
<p>cód segurança</p>
<p>cod seguranca cod segurança</p>
<p>cód seguranca</p>
<p>número de verificação</p>
<p>numero de verificacao</p>
<p>ablauf</p>
<p>gültig bis</p>
<p>gültigkeitsdatum</p>
<p>gultig bis</p>
<p>gultigkeitsdatum</p>
<p>scadenza</p>
<p>data scad</p>
<p>fecha de expiracion</p>
<p>fecha de venc</p>
<p>vencimiento</p>
<p>válido hasta</p>
<p>valido hasta</p>
<p>vto</p>
<p>data de expiração</p>
<p>data de expiracao</p>
<p>data em que expira</p>
<p>validade</p>
<p>valor</p>
<p>vencimento</p>
<p>Venc</p></td>
<td><p>amex</p>
<p>american express</p>
<p>americanexpress</p>
<p>Visa</p>
<p>mastercard</p>
<p>master card</p>
<p>mc</p>
<p>mastercards</p>
<p>master cards</p>
<p>diner's Club</p>
<p>diners club</p>
<p>dinersclub</p>
<p>discover card</p>
<p>discovercard</p>
<p>discover cards</p>
<p>JCB</p>
<p>japanese card bureau</p>
<p>carte blanche</p>
<p>carteblanche</p>
<p>credit card</p>
<p>cc#</p>
<p>cc#:</p>
<p>expiration date</p>
<p>exp date</p>
<p>expiry date</p>
<p>date d’expiration</p>
<p>date d'exp</p>
<p>date expiration</p>
<p>bank card</p>
<p>bankcard</p>
<p>card number</p>
<p>card num</p>
<p>cardnumber</p>
<p>cardnumbers</p>
<p>card numbers</p>
<p>creditcard</p>
<p>credit cards</p>
<p>creditcards</p>
<p>ccn</p>
<p>card holder</p>
<p>cardholder</p>
<p>card holders</p>
<p>cardholders</p>
<p>check card</p>
<p>checkcard</p>
<p>check cards</p>
<p>checkcards</p>
<p>debit card</p>
<p>debitcard</p>
<p>debit cards</p>
<p>debitcards</p>
<p>atm card</p>
<p>atmcard</p>
<p>atm cards</p>
<p>atmcards</p>
<p>enroute</p>
<p>en route</p>
<p>card type</p>
<p>carte bancaire</p>
<p>carte de crédit</p>
<p>carte de credit</p>
<p>numéro de carte</p>
<p>numero de carte</p>
<p>nº de la carte</p>
<p>nº de carte</p>
<p>kreditkarte</p>
<p>karte</p>
<p>karteninhaber</p>
<p>karteninhabers</p>
<p>kreditkarteninhaber</p>
<p>kreditkarteninstitut</p>
<p>kreditkartentyp</p>
<p>eigentümername</p>
<p>kartennr</p>
<p>kartennummer</p>
<p>kreditkartennummer</p>
<p>kreditkarten-nummer</p>
<p>carta di credito</p>
<p>carta credito</p>
<p>n. carta</p>
<p>n carta</p>
<p>nr. carta</p>
<p>nr carta</p>
<p>numero carta</p>
<p>numero della carta</p>
<p>numero di carta</p>
<p>tarjeta credito</p>
<p>tarjeta de credito</p>
<p>tarjeta crédito</p>
<p>tarjeta de crédito</p>
<p>tarjeta de atm</p>
<p>tarjeta atm</p>
<p>tarjeta debito</p>
<p>tarjeta de debito</p>
<p>tarjeta débito</p>
<p>tarjeta de débito</p>
<p>nº de tarjeta</p>
<p>no. de tarjeta</p>
<p>no de tarjeta</p>
<p>numero de tarjeta</p>
<p>número de tarjeta</p>
<p>tarjeta no</p>
<p>tarjetahabiente</p>
<p>cartão de crédito</p>
<p>cartão de credito</p>
<p>cartao de crédito</p>
<p>cartao de credito</p>
<p>cartão de débito</p>
<p>cartao de débito</p>
<p>cartão de debito</p>
<p>cartao de debito</p>
<p>débito automático</p>
<p>debito automatico</p>
<p>número do cartão</p>
<p>numero do cartão</p>
<p>número do cartao</p>
<p>numero do cartao</p>
<p>número de cartão</p>
<p>numero de cartão</p>
<p>número de cartao</p>
<p>numero de cartao</p>
<p>nº do cartão</p>
<p>nº do cartao</p>
<p>nº. do cartão</p>
<p>no do cartão</p>
<p>no do cartao</p>
<p>no. do cartão</p>
<p>no. do cartao</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero di carta di identità della Croazia


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>9 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_croatia_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_croatia_id_card</code> .</p></li>
</ul>

```Command&nbsp;Line
<!--Croatia Identity Card Number-->
<Entity id="ff12f884-c20a-4189-b185-34c8e7258d47" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_croatia_id_card"/>
     <Match idRef="Keyword_croatia_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-41"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_croatia_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta d’identità croata</p>
<p>Osobna iskaznica</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero di identificazione personale (OIB) - Croazia


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 cifre:</p>
<ul>
<li><p>Sei cifre nel formato GGMMAA, ovvero la data di nascita</p></li>
<li><p>Quattro cifre, dove l'ultima è una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_croatia_oib_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_croatia_oib_number</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_croatia_oib_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Croatia Personal Identification (OIB) Number -->
<Entity id="31983b6d-db95-4eb2-a630-b44bd091968d" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_croatia_oib_number"/>
     <Match idRef="Keyword_croatia_oib_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_croatia_oib_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-43"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_croatia_oib_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Codice PIN</p>
<p>Osobni identifikacijski broj</p>
<p>OIB</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero carta d’identità (Repubblica Ceca)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 cifre contenenti una barra</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 cifre:</p>
<ul>
<li><p>Sei cifre, ovvero la data di nascita</p></li>
<li><p>Una barra</p></li>
<li><p>Quattro cifre, dove l'ultima è una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_czech_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_czech_id_card</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Czech National Identity Card Number -->
<Entity id="60c0725a-4eb6-455b-9dda-05d8a7396497" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_czech_id_card"/>
     <Match idRef="Keyword_czech_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-45"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_czech_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta d’identità (Repubblica ceca)</p>
<p>Občanský průka</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Codice PIN - Danimarca


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 cifre contenenti una lineetta</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 cifre:</p>
<ul>
<li><p>Sei cifre nel formato GGMMAA, ovvero la data di nascita</p></li>
<li><p>Una lineetta</p></li>
<li><p>Quattro cifre, dove l'ultima è una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_denmark_id</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_denmark_id</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Denmark Personal Identification Number -->
<Entity id="6c4f2fef-56e1-4c00-8093-88d7a01cf460" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_denmark_id"/>
     <Match idRef="Keyword_denmark_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-47"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_denmark_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Codice PIN</p>
<p>CPR</p>
<p>Det Centrale Personregister</p>
<p>Personnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero della Drug Enforcement Agency (DEA)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Due lettere seguite da 7 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Il modello deve includere tutti gli elementi seguenti:</p>
<ul>
<li><p>Una lettera (senza distinzione tra maiuscole/minuscole) da questo gruppo di lettere: abcdefghjklmnprstux, ovvero un codice registrante</p></li>
<li><p>Una lettera (senza distinzione tra maiuscole/minuscole), ovvero la prima lettera del cognome del registrante</p></li>
<li><p>7 cifre e l'ultima è quella di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_dea_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- DEA Number -->
<Entity id="9a5445ad-406e-43eb-8bd7-cac17ab6d0e4" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_dea_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>None</p></td>
</tr>
</tbody>
</table>


## Unione Europea - Numero di carta di debito


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>16 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Modello molto complesso e solido</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_eu_debit_card</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica almeno una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_eu_debit_card</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_card_terms_dict</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_card_security_terms_dict</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_card_expiration_terms_dict</code>.</p></li>
<li><p>La funzione <code>Func_expiration_date</code> rileva una data nel formato corretto.</p></li>
</ul></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- EU Debit Card Number -->
    <Entity id="0e9b3178-9678-47dd-a509-37222ca96b42" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_eu_debit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_eu_debit_card" />
          <Match idRef="Keyword_card_terms_dict" />
          <Match idRef="Keyword_card_security_terms_dict" />
          <Match idRef="Keyword_card_expiration_terms_dict" />
          <Match idRef="Func_expiration_date" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-50"> </h3>
<div>
<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_eu_debit_card</p></th>
<th> </th>
<th><p>Keyword_card_terms_dict</p></th>
<th><p>Keyword_card_security_terms_dict</p></th>
<th><p>Keyword_card_expiration_terms_dict</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>account number</p>
<p>card number</p>
<p>card no.</p>
<p>security number</p>
<p>cc#</p></td>
<td> </td>
<td><p>acct nbr</p>
<p>acct num</p>
<p>acct no</p>
<p>american express</p>
<p>americanexpress</p>
<p>americano espresso</p>
<p>amex</p>
<p>atm card</p>
<p>atm cards</p>
<p>atm kaart</p>
<p>atmcard</p>
<p>atmcards</p>
<p>atmkaart</p>
<p>atmkaarten</p>
<p>bancontact</p>
<p>bank card</p>
<p>bankkaart</p>
<p>card holder</p>
<p>card holders</p>
<p>card num</p>
<p>card number</p>
<p>card numbers</p>
<p>card type</p>
<p>cardano numerico</p>
<p>cardholder</p>
<p>cardholders</p>
<p>cardnumber</p>
<p>cardnumbers</p>
<p>carta bianca</p>
<p>carta credito</p>
<p>carta di credito</p>
<p>cartao de credito</p>
<p>cartao de crédito</p>
<p>cartao de debito</p>
<p>○cartao de débito</p>
<p>carte bancaire</p>
<p>carte blanche</p>
<p>carte bleue</p>
<p>carte de credit</p>
<p>carte de crédit</p>
<p>carte di credito</p>
<p>carteblanche</p>
<p>cartão de credito</p>
<p>cartão de crédito</p>
<p>cartão de debito</p>
<p>cartão de débito</p>
<p>cb</p>
<p>ccn</p>
<p>check card</p>
<p>check cards</p>
<p>checkcard</p>
<p>checkcards</p>
<p>chequekaart</p>
<p>cirrus</p>
<p>cirrus-edc-maestro</p>
<p>controlekaart</p>
<p>controlekaarten</p>
<p>credit card</p>
<p>credit cards</p>
<p>creditcard</p>
<p>creditcards</p>
<p>debetkaart</p>
<p>debetkaarten</p>
<p>debit card</p>
<p>debit cards</p>
<p>debitcard</p>
<p>debitcards</p>
<p>debito automatico</p>
<p>diners club</p>
<p>dinersclub</p>
<p>discover</p>
<p>discover card</p>
<p>discover cards</p>
<p>discovercard</p>
<p>discovercards</p>
<p>débito automático</p>
<p>edc</p>
<p>eigentümername</p>
<p>european debit card</p>
<p>hoofdkaart</p>
<p>hoofdkaarten</p>
<p>in viaggio</p>
<p>japanese card bureau</p>
<p>japanse kaartdienst</p>
<p>jcb</p>
<p>kaart</p>
<p>kaart num</p>
<p>kaartaantal</p>
<p>kaartaantallen</p>
<p>kaarthouder</p>
<p>kaarthouders</p>
<p>karte</p>
<p>karteninhaber</p>
<p>karteninhabers</p>
<p>kartennr</p>
<p>kartennummer</p>
<p>kreditkarte</p>
<p>kreditkarten-nummer</p>
<p>kreditkarteninhaber</p>
<p>kreditkarteninstitut</p>
<p>kreditkartennummer</p>
<p>kreditkartentyp</p>
<p>maestro</p>
<p>master card</p>
<p>master cards</p>
<p>mastercard</p>
<p>mastercards</p>
<p>mc</p>
<p>mister cash</p>
<p>n carta</p>
<p>n. carta</p>
<p>no de tarjeta</p>
<p>no do cartao</p>
<p>no do cartão</p>
<p>no. de tarjeta</p>
<p>no. do cartao</p>
<p>no. do cartão</p>
<p>nr carta</p>
<p>nr. carta</p>
<p>numeri di scheda</p>
<p>numero carta</p>
<p>numero de cartao</p>
<p>numero de carte</p>
<p>numero de cartão</p>
<p>numero de tarjeta</p>
<p>numero della carta</p>
<p>numero di carta</p>
<p>numero di scheda</p>
<p>numero do cartao</p>
<p>numero do cartão</p>
<p>numéro de carte</p>
<p>nº carta</p>
<p>nº de carte</p>
<p>nº de la carte</p>
<p>nº de tarjeta</p>
<p>nº do cartao</p>
<p>nº do cartão</p>
<p>nº. do cartão</p>
<p>número de cartao</p>
<p>número de cartão</p>
<p>número de tarjeta</p>
<p>número do cartao</p>
<p>scheda dell'assegno</p>
<p>scheda dell'atmosfera</p>
<p>scheda dell'atmosfera</p>
<p>scheda della banca</p>
<p>scheda di controllo</p>
<p>scheda di debito</p>
<p>scheda matrice</p>
<p>schede dell'atmosfera</p>
<p>schede di controllo</p>
<p>schede di debito</p>
<p>schede matrici</p>
<p>scoprono la scheda</p>
<p>scoprono le schede</p>
<p>solo</p>
<p>supporti di scheda</p>
<p>supporto di scheda</p>
<p>switch</p>
<p>tarjeta atm</p>
<p>tarjeta credito</p>
<p>tarjeta de atm</p>
<p>tarjeta de credito</p>
<p>tarjeta de debito</p>
<p>tarjeta debito</p>
<p>tarjeta no</p>
<p>tarjetahabiente</p>
<p>tipo della scheda</p>
<p>ufficio giapponese della</p>
<p>scheda</p>
<p>v pay</p>
<p>v-pay</p>
<p>visa</p>
<p>visa plus</p>
<p>visa electron</p>
<p>visto</p>
<p>visum</p>
<p>vpay</p></td>
<td><p>card identification number</p>
<p>card verification</p>
<p>cardi la verifica</p>
<p>cid</p>
<p>cod seg</p>
<p>cod seguranca</p>
<p>cod segurança</p>
<p>cod sicurezza</p>
<p>cod. seg</p>
<p>cod. seguranca</p>
<p>cod. segurança</p>
<p>cod. sicurezza</p>
<p>codice di sicurezza</p>
<p>codice di verifica</p>
<p>codigo</p>
<p>codigo de seguranca</p>
<p>codigo de segurança</p>
<p>crittogramma</p>
<p>cryptogram</p>
<p>cryptogramme</p>
<p>cv2</p>
<p>cvc</p>
<p>cvc2</p>
<p>cvn</p>
<p>cvv</p>
<p>cvv2</p>
<p>cód seguranca</p>
<p>cód segurança</p>
<p>cód. seguranca</p>
<p>cód. segurança</p>
<p>código</p>
<p>código de seguranca</p>
<p>código de segurança</p>
<p>de kaart controle</p>
<p>geeft nr uit</p>
<p>issue no</p>
<p>issue number</p>
<p>kaartidentificatienummer</p>
<p>kreditkartenprufnummer</p>
<p>kreditkartenprüfnummer</p>
<p>kwestieaantal</p>
<p>no. dell'edizione</p>
<p>no. di sicurezza</p>
<p>numero de securite</p>
<p>numero de verificacao</p>
<p>numero dell'edizione</p>
<p>numero di identificazione della</p>
<p>scheda</p>
<p>numero di sicurezza</p>
<p>numero van veiligheid</p>
<p>numéro de sécurité</p>
<p>nº autorizzazione</p>
<p>número de verificação</p>
<p>perno il blocco</p>
<p>pin block</p>
<p>prufziffer</p>
<p>prüfziffer</p>
<p>security code</p>
<p>security no</p>
<p>security number</p>
<p>sicherheits kode</p>
<p>sicherheitscode</p>
<p>sicherheitsnummer</p>
<p>speldblok</p>
<p>veiligheid nr</p>
<p>veiligheidsaantal</p>
<p>veiligheidscode</p>
<p>veiligheidsnummer</p>
<p>verfalldatum</p></td>
<td><p>ablauf</p>
<p>data de expiracao</p>
<p>data de expiração</p>
<p>data del exp</p>
<p>data di exp</p>
<p>data di scadenza</p>
<p>data em que expira</p>
<p>data scad</p>
<p>data scadenza</p>
<p>date de validité</p>
<p>datum afloop</p>
<p>datum van exp</p>
<p>de afloop</p>
<p>espira</p>
<p>espira</p>
<p>exp date</p>
<p>exp datum</p>
<p>expiration</p>
<p>expire</p>
<p>expires</p>
<p>expiry</p>
<p>fecha de expiracion</p>
<p>fecha de venc</p>
<p>gultig bis</p>
<p>gultigkeitsdatum</p>
<p>gültig bis</p>
<p>gültigkeitsdatum</p>
<p>la scadenza</p>
<p>scadenza</p>
<p>valable</p>
<p>validade</p>
<p>valido hasta</p>
<p>valor</p>
<p>venc</p>
<p>vencimento</p>
<p>vencimiento</p>
<p>verloopt</p>
<p>vervaldag</p>
<p>vervaldatum</p>
<p>vto</p>
<p>válido hasta</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Finland National ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>6 cifre, un carattere di indicazione del secolo, tre cifre più una cifra di controllo</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Il modello deve includere tutti gli elementi seguenti:</p>
<ul>
<li><p>Sei cifre nel formato DDMMYY che corrisponde alla data di nascita</p></li>
<li><p>Indicatore del secolo (&quot;-&quot;, &quot;+&quot; o &quot;a&quot;)</p></li>
<li><p>Codice PIN di 3 cifre</p></li>
<li><p>Una cifra o una lettera (con distinzione tra maiuscole/minuscole) che corrisponde a una cifra di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_finnish_national_id</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_finnish_national_id</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Finnish National ID-->
<Entity id="338FD995-4CB5-4F87-AD35-79BD1DD926C1" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_finnish_national_id" />
          <Match idRef="Keyword_finnish_national_id" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-52"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_finnish_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sosiaaliturvatunnus</p>
<p>SOTU Henkilötunnus HETU</p>
<p>Personbeteckning</p>
<p>Personnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Finlandia - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Una combinazione di nove lettere e cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Una combinazione di nove lettere e cifre:</p>
<ul>
<li><p>Due lettere (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>Sette cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_finland_passport_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_finland_passport_number</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Finland Passport Number -->
<Entity id="d1685ac3-1d3a-40f8-8198-32ef5669c7a5" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_finland_passport_number"/>
     <Match idRef="Keyword_finland_passport_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-54"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_finland_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passaporto</p>
<p>Passi</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Francia - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>12 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>12 cifre con convalida per scontare modelli analoghi, ad esempio, quello dei numeri telefonici francesi</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_french_drivers_license</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica almeno una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_french_drivers_license</code>.</p></li>
<li><p>La funzione <code>Func_eu_date</code> rileva una data nel formato corretto.</p></li>
</ul></li>
</ul>

```Command&nbsp;Line
<!-- France Driver's License Number -->
<Entity id="18e55a36-a01b-4b0f-943d-dc10282a1824" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_french_drivers_license" />
        <Any minMatches="1">
          <Match idRef="Keyword_french_drivers_license" />
          <Match idRef="Func_eu_date" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-56"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_french_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>drivers licence</p>
<p>drivers license</p>
<p>driving licence</p>
<p>driving license</p>
<p>permis de conduire</p>
<p>licence number</p>
<p>license number</p>
<p>licence numbers</p>
<p>license numbers</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Francia - Carta d'identità nazionale (CNI)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>12 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>12 cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_france_cni</code> restituisce contenuti che corrispondono al modello.</p></li>
</ul>

```Command&nbsp;Line
<!-- France CNI -->
<Entity id="f741ac74-1bc0-4665-b69b-f0c7f927c0c4" patternsProximity="300" recommendedConfidence="65">
  <Pattern confidenceLevel="65">
        <IdMatch idRef="Regex_france_cni" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>None</p></td>
</tr>
</tbody>
</table>


## Francia - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Nove cifre e lettere</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Nove cifre e lettere:</p>
<ul>
<li><p>Due cifre</p></li>
<li><p>Due lettere (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>Cinque cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_fr_passport</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_passport</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- France Passport Number -->
<Entity id="3008b884-8c8c-4cd8-a289-99f34fc7ff5d" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_fr_passport" />
        <Match idRef="Keyword_passport" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-59"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート ＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Francia - Numero di previdenza sociale (INSEE)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>15 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Deve corrispondere a uno di questi due modelli:</p>
<ul>
<li><p>13 cifre seguite da uno spazio e da due cifre oppure</p></li>
<li><p>15 cifre consecutive</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 95%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_french_insee</code> o <code>Func_fr_insee</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_fr_insee</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_french_insee</code> o <code>Func_fr_insee</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_fr_insee</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- France INSEE -->
<Entity id="71f62b97-efe0-4aa1-aa49-e14de253619d" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="95">
        <IdMatch idRef="Func_french_insee" />
        <Match idRef="Func_fr_insee" />
        <Any minMatches="1">
          <Match idRef="Keyword_fr_insee" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_french_insee" />
        <Match idRef="Func_fr_insee" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_fr_insee" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-61"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_fr_insee</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>insee</p>
<p>securité sociale</p>
<p>securite sociale</p>
<p>national id</p>
<p>national identification</p>
<p>numéro d'identité</p>
<p>no d'identité</p>
<p>no. d'identité</p>
<p>numero d'identite</p>
<p>no d'identite</p>
<p>no. d'identite</p>
<p>social security number</p>
<p>social security code</p>
<p>social insurance number</p>
<p>le numéro d'identification nationale</p>
<p>d'identité nationale</p>
<p>numéro de sécurité sociale</p>
<p>le code de la sécurité sociale</p>
<p>numéro d'assurance sociale</p>
<p>numéro de sécu</p>
<p>code sécu</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Germania - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Combinazione di 11 cifre e lettere</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>11 cifre e lettere (senza distinzione tra maiuscole/minuscole):</p>
<ul>
<li><p>Una cifra o una lettera</p></li>
<li><p>Due cifre</p></li>
<li><p>Sei cifre o lettere</p></li>
<li><p>Una cifra</p></li>
<li><p>Una cifra o una lettera</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_german_drivers_license</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica almeno una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_german_drivers_license_number</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_german_drivers_license_collaborative</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_german_drivers_license</code>.</p></li>
</ul></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- German Driver's License Number -->
<Entity id="91da9335-1edb-45b7-a95f-5fe41a16c63c" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_german_drivers_license" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_drivers_license_number" />
          <Match idRef="Keyword_german_drivers_license_collaborative" />
          <Match idRef="Keyword_german_drivers_license" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-63"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_german_drivers_license_number</p></th>
<th> </th>
<th><p>Keyword_german_drivers_license_collaborative</p></th>
<th><p>Keyword_german_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Führerschein</p>
<p>Fuhrerschein</p>
<p>Fuehrerschein</p>
<p>Führerscheinnummer</p>
<p>Fuhrerscheinnummer</p>
<p>Fuehrerscheinnummer</p>
<p>Führerschein-</p>
<p>Fuhrerschein-</p>
<p>Fuehrerschein-</p>
<p>FührerscheinnummerNr</p>
<p>FuhrerscheinnummerNr</p>
<p>FuehrerscheinnummerNr</p>
<p>FührerscheinnummerKlasse</p>
<p>FuhrerscheinnummerKlasse</p>
<p>FuehrerscheinnummerKlasse</p>
<p>Führerschein- Nr</p>
<p>Fuhrerschein- Nr</p>
<p>Fuehrerschein- Nr</p>
<p>Führerschein- Klasse</p>
<p>Fuhrerschein- Klasse</p>
<p>Fuehrerschein- Klasse</p>
<p>FührerscheinnummerNr</p>
<p>FuhrerscheinnummerNr</p>
<p>FuehrerscheinnummerNr</p>
<p>FührerscheinnummerKlasse</p>
<p>FuhrerscheinnummerKlasse</p>
<p>FuehrerscheinnummerKlasse</p>
<p>Führerschein- Nr</p>
<p>Fuhrerschein- Nr</p>
<p>Fuehrerschein- Nr</p>
<p>Führerschein- Klasse</p>
<p>Fuhrerschein- Klasse</p>
<p>Fuehrerschein- Klasse</p>
<p>DL</p>
<p>DLS</p>
<p>Driv Lic</p>
<p>Driv Licen</p>
<p>Driv License</p>
<p>Driv Licenses</p>
<p>Driv Licence</p>
<p>Driv Licences</p>
<p>Driv Lic</p>
<p>Driver Licen</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>Driver Licence</p>
<p>Driver Licences</p>
<p>Drivers Lic</p>
<p>Drivers Licen</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Drivers Licence</p>
<p>Drivers Licences</p>
<p>Driver's Lic</p>
<p>Driver's Licen</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>Driver's Licence</p>
<p>Driver's Licences</p>
<p>Driving Lic</p>
<p>Driving Licen</p>
<p>Driving License</p>
<p>Driving Licenses</p>
<p>Driving Licence</p>
<p>Driving Licences</p></td>
<td> </td>
<td><p>Nr-Führerschein</p>
<p>Nr-Fuhrerschein</p>
<p>Nr-Fuehrerschein</p>
<p>No-Führerschein</p>
<p>No-Fuhrerschein</p>
<p>No-Fuehrerschein</p>
<p>N-Führerschein</p>
<p>N-Fuhrerschein</p>
<p>N-Fuehrerschein</p>
<p>Nr-Führerschein</p>
<p>Nr-Fuhrerschein</p>
<p>Nr-Fuehrerschein</p>
<p>No-Führerschein</p>
<p>No-Fuhrerschein</p>
<p>No-Fuehrerschein</p>
<p>N-Führerschein</p>
<p>N-Fuhrerschein</p>
<p>N-Fuehrerschein</p></td>
<td><p>ausstellungsdatum</p>
<p>ausstellungsort</p>
<p>ausstellende behöde</p>
<p>ausstellende behorde</p>
<p>ausstellende behoerde</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero di carta di identità (Germania)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>A partire dal 1° novembre 2010</p>
<dl>
<dd><p>Nove lettere e numeri</p>
</dd>
</dl>
<p>Dal 1° aprile 1987 fino al 31 ottobre 2010</p>
<dl>
<dd><p>10 cifre</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>A partire dal 1° novembre 2010:</p>
<ul>
<li><p>Una lettera (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>Otto cifre</p></li>
</ul>
<p>Dal 1° aprile 1987 fino al 31 ottobre 2010</p>
<ul>
<li><p>10 cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_germany_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_germany_id_card</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Germany Identity Card Number -->
<Entity id="e577372f-c42e-47a0-9d85-bebed1c237d4" recommendedConfidence="65" patternsProximity="300">
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Regex_germany_id_card"/>
     <Match idRef="Keyword_germany_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-65"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_germany_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta di identità</p>
<p>ID</p>
<p>Identificazione</p>
<p>Personalausweis</p>
<p>Identifizierungsnummer</p>
<p>Ausweis</p>
<p>Identifikation</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Germania - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 cifre o lettere</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Il modello deve includere tutti gli elementi seguenti:</p>
<ul>
<li><p>Il primo carattere è una cifra o una lettera del gruppo seguente: C, F, G, H, J, K</p></li>
<li><p>Tre cifre</p></li>
<li><p>Cinque cifre o lettere del gruppo seguente: C, -H, J-N, P, R, T, V-Z</p></li>
<li><p>Una cifra</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_german_passport</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave fra le cinque elencate.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_german_passport_data</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave fra le cinque elencate.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- German Passport Number -->
<Entity id="2e3da144-d42b-47ed-b123-fbf78604e52c" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_german_passport" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_passport" />
          <Match idRef="Keyword_german_passport_collaborative" />
          <Match idRef="Keyword_german_passport_number" />
          <Match idRef="Keyword_german_passport1" />
          <Match idRef="Keyword_german_passport2" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_german_passport_data" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_passport" />
          <Match idRef="Keyword_german_passport_collaborative" />
          <Match idRef="Keyword_german_passport_number" />
          <Match idRef="Keyword_german_passport1" />
          <Match idRef="Keyword_german_passport2" />
        </Any>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-67"> </h3>
<div>
<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_german_passport</p></th>
<th> </th>
<th><p>Keyword_german_passport_collaborative</p></th>
<th><p>Keyword_german_passport_number</p></th>
<th><p>Keyword_german_passport1</p></th>
<th><p>Keyword_german_passport2</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>reisepass</p>
<p>reisepasse</p>
<p>reisepassnummer</p>
<p>passport</p>
<p>passports</p></td>
<td> </td>
<td><p>geburtsdatum</p>
<p>ausstellungsdatum</p>
<p>ausstellungsort</p></td>
<td><p>No-Reisepass</p>
<p>Nr-Reisepass</p></td>
<td><p>Reisepass-Nr</p></td>
<td><p>bnationalit.t</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carta d'identità (Grecia)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Combinazione di 7-8 lettere e numeri, oltre a un trattino</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Sette lettere e numeri (formato precedente):</p>
<ul>
<li><p>Una lettera (qualsiasi lettera dell'alfabeto greco)</p></li>
<li><p>Un trattino</p></li>
<li><p>Sei cifre</p></li>
</ul>
<p>Otto lettere e numeri (nuovo formato):</p>
<ul>
<li><p>Due lettere in maiuscolo sia in alfabeto latino che greco (ABEZHIKMNOPTYX)</p></li>
<li><p>Un trattino</p></li>
<li><p>Sei cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_greece_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_greece_id_card</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Greece National ID Card -->
<Entity id="82568215-1da1-46d3-874a-d2294d81b5ac" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_greece_id_card"/>
     <Match idRef="Keyword_greece_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-69"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_greece_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta d’identità greca</p>
<p>Tautotita</p>
<p>Δελτίο αστυνομικής ταυτότητας</p>
<p>Ταυτότητα</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Hong Kong - Numero di carta di identità (HKID)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Combinazione di 8-9 lettere e numeri. Facoltativamente, l’ultimo carattere può essere racchiuso tra parentesi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Combinazione di 8-9 lettere:</p>
<ul>
<li><p>1-2 lettere (senza distinzione tra maiuscole e minuscole)</p></li>
<li><p>Sei cifre</p></li>
<li><p>L'ultimo carattere (qualsiasi cifra o la lettera A), è rappresentato dal numero di controllo. Facoltativamente, può essere racchiuso tra parentesi.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_hong_kong_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_hong_kong_id_card</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_hong_kong_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Hong Kong Identity Card (HKID) number -->
<Entity id="e63c28a7-ad29-4c17-a41a-3d2a0b70fd9c" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_hong_kong_id_card"/>
     <Match idRef="Keyword_hong_kong_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Func_hong_kong_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-71"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_hong_kong_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta d’identità (Hong Kong)</p>
<p>HKID</p>
<p>Carta di identità</p>
<p>香港身份證</p>
<p>香港永久性居民身份證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## India - Numero di conto permanente (PAN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 lettere o cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 lettere o cifre:</p>
<ul>
<li><p>Cinque lettere (senza distinzione tra maiuscole e minuscole)</p></li>
<li><p>Quattro cifre</p></li>
<li><p>Una lettera, ovvero una cifra di controllo alfabetica</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_india_permanent_account_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_india_permanent_account_number</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- India Permanent Account Number -->
<Entity id="2602bfee-9bb0-47a5-a7a6-2bf3053e2804" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_india_permanent_account_number"/>
     <Match idRef="Keyword_india_permanent_account_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-73"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_india_permanent_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Permanent Account Number</p>
<p>PAN</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## India - Numero di identificazione univoco (Aadhaar)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>12 cifre contenenti spazi o trattini facoltativi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>12 cifre:</p>
<ul>
<li><p>Quattro cifre</p></li>
<li><p>Uno spazio o un trattino facoltativo</p></li>
<li><p>Quattro cifre</p></li>
<li><p>Uno spazio o un trattino facoltativo</p></li>
<li><p>L'ultimo carattere, ovvero il numero di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_india_aadhaar</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_india_aadhar</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_india_aadhaar</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- India Unique Identification (Aadhaar) number -->
<Entity id="1ca46b29-76f5-4f46-9383-cfa15e91048f" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_india_aadhaar"/>
     <Match idRef="Keyword_india_aadhar"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_india_aadhaar"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-75"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_india_aadhar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aadhar</p>
<p>Aadhaar</p>
<p>UID</p>
<p>आधार</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Indonesia - Numero di carta di identità (KTP)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>16 cifre contenenti punti facoltativi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>16 cifre:</p>
<ul>
<li><p>Codice provincia a due cifre</p></li>
<li><p>Un punto (facoltativo)</p></li>
<li><p>Codice città o area a due cifre</p></li>
<li><p>Codice sotto-distretto a due cifre</p></li>
<li><p>Un punto (facoltativo)</p></li>
<li><p>Sei cifre nel formato GGMMAA, ovvero la data di nascita</p></li>
<li><p>Un punto (facoltativo)</p></li>
<li><p>Quattro cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_indonesia_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_indonesia_id_card</code> .</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_indonesia_id_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
</ul>

```Command&nbsp;Line
<!-- Indonesia Identity Card (KTP) Number -->
<Entity id="da68fdb0-f383-4981-8c86-82689d3b7d55" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_indonesia_id_card"/>
     <Match idRef="Keyword_indonesia_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_indonesia_id_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-77"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_indonesia_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KTP</p>
<p>Kartu Tanda Penduduk</p>
<p>Nomor Induk Kependudukan</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Numero di conto bancario internazionale (IBAN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Codice paese, due lettere, nonché controllare cifre (due cifre) plus bban numero (fino a 30 caratteri)</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Il modello deve includere tutti gli elementi seguenti:</p>
<ul>
<li><p>Codice di due lettere del paese</p></li>
<li><p>Due cifre di controllo (seguite da uno spazio facoltativo)</p></li>
<li><p>1 a 7 gruppi di quattro lettere o cifre (possono essere separati da spazi)</p></li>
<li><p>1-3 lettere o cifre</p></li>
</ul>
<p>Il formato per ogni paese è leggermente diverso. Il tipo di informazioni riservate IBAN vengono trattati questi 60 paesi:</p>
<dl>
<dd><p>Active Directory, ae, all'az, ba, essere, bg, orario di ufficio, ch, cr, cy, cz, de, dk, eseguire, ee, es, fi, fo, fr, gb, ge, gi, contabilità generale, gr, risorse umane, hu, vale a dire il, è, viene, kw, kz, kg, li, lt, lu, lv mc, md, me, mk, mr, mt, mu , nl, no pl, pt, RU, rs, sa, se, si, sk, sm, tn, tr, vg</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_iban</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<Entity id="e7dc4711-11b7-4cb0-b88b-2c394a771f0e" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_iban" />
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>None</p></td>
</tr>
</tbody>
</table>


## Indirizzo IP


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>IPv4:</p>
<ul>
<li><p>Modello complesso che rappresenta le versioni formattate (punti) e quelle non formattate (senza punti) degli indirizzi IPv4</p></li>
</ul>
<p>IPv6:</p>
<ul>
<li><p>Modello complesso che rappresenta i numeri dell'indirizzo IPv6 non formattati (include i due punti)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Nel caso di IPv6, un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_ipv6_address</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_ipaddress</code>.</p></li>
</ul>
<p>Nel caso di IPv4, un criterio DLP rileva questo tipo di informazioni con una probabilità del 95%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_ipv4_address</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_ipaddress</code>.</p></li>
</ul>
<p>Nel caso di IPv6, un criterio DLP rileva questo tipo di informazioni con una probabilità del 95%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_ipv6_address</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_ipaddress</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- IP Address -->
    <Entity id="1daa4ad5-e2dd-4ca4-a788-54722c09efb2" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_ipv6_address" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="95">
        <IdMatch idRef="Regex_ipv4_address" />
        <Any minMatches="1">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="95">
        <IdMatch idRef="Regex_ipv6_address" />
        <Any minMatches="1">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-80"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ipaddress</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP (per questa parola chiave viene fatta distinzione tra maiuscole e minuscole)</p>
<p>ip address</p>
<p>Indirizzi IP</p>
<p>internet protocol</p>
<p>IP-כתובת ה</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Irlanda - Numero personale di servizio pubblico (PPS)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Formato precedente (fino al 31 dicembre 2012)</p>
<dl>
<dd><p>Sette cifre seguite da 1-2 lettere</p>
</dd>
</dl>
<p>Nuovo formato (dal 1° gennaio 2013 in poi)</p>
<dl>
<dd><p>Sette cifre seguite da due lettere</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Formato precedente (fino al 31 dicembre 2012)</p>
<ul>
<li><p>Sette cifre</p></li>
<li><p>1-2 lettere (senza distinzione tra maiuscole e minuscole)</p></li>
</ul>
<p>Nuovo formato (dal 1° gennaio 2013 in poi)</p>
<ul>
<li><p>Sette cifre</p></li>
<li><p>Una lettera (senza distinzione tra maiuscole e minuscole) che corrisponde a una cifra di controllo alfabetica</p></li>
<li><p>La lettera &quot;A&quot; o &quot;H&quot; (senza distinzione tra maiuscole e minuscole)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_ireland_pps</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Si verifica una delle situazioni seguenti:</p>
<ul>
<li><p>È possibile trovare una parola chiave da <code>Keyword_ireland_pps</code> .</p></li>
<li><p>La funzione <code>Func_eu_date</code> rileva una data nel formato corretto.</p></li>
</ul></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_ireland_pps</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Ireland Personal Public Service (PPS) Number -->
<Entity id="1cdb674d-c19a-4fcf-9f4b-7f56cc87345a" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_ireland_pps"/>
     <Any minMatches="1">
  <Match idRef="Keyword_ireland_pps"/>
  <Match idRef="Func_eu_date"/>
     </Any>
  </Pattern>
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Func_ireland_pps"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-82"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ireland_pps</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero personale di servizio pubblico</p>
<p>Numero PPS</p>
<p>Num. PPS</p>
<p>N° PPS</p>
<p>PPS #</p>
<p>PPS#</p>
<p>PPSN</p>
<p>Scheda servizi pubblici</p>
<p>Uimhir Phearsanta Seirbhíse Poiblí</p>
<p>Uimh. PSP</p>
<p>PSP</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Israele - Numero di conto bancario


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>13 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Formattato:</p>
<ul>
<li><p>Due cifre</p></li>
<li><p>Un trattino</p></li>
<li><p>Tre cifre</p></li>
<li><p>Un trattino</p></li>
<li><p>Otto cifre</p></li>
</ul>
<p>Non formattato:</p>
<ul>
<li><p>13 cifre consecutive</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_israel_bank_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_israel_bank_account_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Israel Bank Account Number -->
<Entity id="7d08b2ff-a0b9-437f-957c-aeddbf9b2b25" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_israel_bank_account_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_israel_bank_account_number" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-84"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_israel_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bank Account Number</p>
<p>Bank Account</p>
<p>Account Number</p>
<p>מספר חשבון בנק</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carta di identità (Israele)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>9 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_israeli_national_id_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_Israel_National_ID</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Israel National ID Number -->
<Entity id="e05881f5-1db1-418c-89aa-a3ac5c5277ee" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_israeli_national_id_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_Israel_National_id" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-86"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Israel_National_ID</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>מספר זהות</p>
<p>National ID Number</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Italia - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Una combinazione di 10 lettere e cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Una combinazione di 10 lettere e cifre:</p>
<ul>
<li><p>Una lettera (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>La lettera &quot;A&quot; o &quot;V&quot; (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>7 lettere (senza distinzione tra maiuscole/minuscole), cifre o carattere di sottolineatura</p></li>
<li><p>Una lettera (senza distinzione tra maiuscole/minuscole)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_italy_drivers_license_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_italy_drivers_license_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Italy Driver's license Number -->
<Entity id="97d6244f-9157-41bd-8e0c-9d669a5c4d71" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_italy_drivers_license_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_italy_drivers_license_number" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-88"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_italy_drivers_license_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numero di patente di guida</p>
<p>patente di guida</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Giappone - Numero di conto bancario


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Sette o otto cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Numero di conto corrente:</p>
<ul>
<li><p>Sette o otto cifre</p></li>
</ul>
<p>Codice della filiale del conto corrente:</p>
<ul>
<li><p>Quattro cifre</p></li>
<li><p>Uno spazio o un trattino (facoltativo)</p></li>
<li><p>Tre cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_bank_account</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_bank_account</code>.</p></li>
<li><p>Si verifica una delle situazioni seguenti:</p>
<ul>
<li><p>La funzione <code>Func_jp_bank_account_branch_code</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_bank_branch_code</code>.</p></li>
</ul></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_bank_account</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_bank_account</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Bank Account Number -->
<Entity id="d354f95b-96ee-4b80-80bc-4377312b55bc" patternsProximity="300" recommendedConfidence="75">
  <Version minEngineVersion="15.01.0131.000">
    <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_jp_bank_account" />
          <Match idRef="Keyword_jp_bank_account" />
          <Any minMatches="1">
            <Match idRef="Func_jp_bank_account_branch_code" />
            <Match idRef="Keyword_jp_bank_branch_code" />
          </Any>
      </Pattern>
  </Version>    
     <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_bank_account" />
        <Match idRef="Keyword_jp_bank_account" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-90"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_bank_account</p></th>
<th> </th>
<th><p>Keyword_jp_bank_branch_code</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Checking Account Number</p>
<p>Checking Account</p>
<p>Checking Account #</p>
<p>Checking Acct Number</p>
<p>Checking Acct #</p>
<p>Checking Acct No.</p>
<p>Checking Account No.</p>
<p>Bank Account Number</p>
<p>Bank Account</p>
<p>Bank Account #</p>
<p>Bank Acct Number</p>
<p>Bank Acct #</p>
<p>Bank Acct No.</p>
<p>Bank Account No.</p>
<p>Savings Account Number</p>
<p>Savings Account</p>
<p>Savings Account #</p>
<p>Savings Acct Number</p>
<p>Savings Acct #</p>
<p>Savings Acct No.</p>
<p>Savings Account No.</p>
<p>Debit Account Number</p>
<p>Debit Account</p>
<p>Debit Account #</p>
<p>Debit Acct Number</p>
<p>Debit Acct #</p>
<p>Debit Acct No.</p>
<p>Debit Account No.</p>
<p>口座番号を当座預金口座の確認</p>
<p>＃アカウントの確認、勘定番号の確認</p>
<p>＃勘定の確認</p>
<p>勘定番号の確認</p>
<p>口座番号の確認</p>
<p>銀行口座番号</p>
<p>銀行口座</p>
<p>銀行口座＃</p>
<p>銀行の勘定番号</p>
<p>銀行のacct＃</p>
<p>銀行の勘定いいえ</p>
<p>銀行口座番号</p>
<p>普通預金口座番号</p>
<p>預金口座</p>
<p>貯蓄口座＃</p>
<p>貯蓄勘定の数</p>
<p>貯蓄勘定＃</p>
<p>貯蓄勘定番号</p>
<p>普通預金口座番号</p>
<p>引き落とし口座番号</p>
<p>口座番号</p>
<p>口座番号＃</p>
<p>デビットのacct番号</p>
<p>デビット勘定＃</p>
<p>デビットACCTの番号</p>
<p>デビット口座番号</p></td>
<td> </td>
<td><p>Otemachi</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Giappone - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>12 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>12 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_drivers_license_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_drivers_license_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Driver's License Number -->
<Entity id="c6011143-d087-451c-8313-7f6d4aed2270" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_drivers_license_number" />
        <Match idRef ="Keyword_jp_drivers_license_number" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-92"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_drivers_license_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>patente</p>
<p>patente di Guida</p>
<p>patente</p>
<p>licenze di driver</p>
<p>licenze della patente di Guida</p>
<p>licenze di driver</p>
<p>DL #</p>
<p>le liste di distribuzione #</p>
<p>LIC #</p>
<p>conglomerati #</p>
<p>運転免許証</p>
<p>運転免許</p>
<p>免許証</p>
<p>免許</p>
<p>運転免許証番号</p>
<p>運転免許番号</p>
<p>免許証番号</p>
<p>免許番号</p>
<p>運転免許証ナンバー</p>
<p>運転免許ナンバー</p>
<p>免許証ナンバー</p>
<p>運転免許証No.</p>
<p>運転免許No.</p>
<p>免許証No.</p>
<p>免許No.</p>
<p>運転免許証 #</p>
<p>運転免許 #</p>
<p>免許証 #</p>
<p>免許 #</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Giappone - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Due lettere seguite da 7 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Due lettere (senza distinzione tra maiuscole/minuscole) seguite da sette cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_passport</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_passport</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Passport Number -->
<Entity id="75177310-1a09-4613-bf6d-833aae3743f8" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_passport" />
        <Match idRef="Keyword_jp_passport" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-94"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Giappone - Numero di registrazione dei residenti


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>11 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>11 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_resident_registration_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_resident_registration_number</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Resident Registration Number -->
<Entity id="01c1209b-6389-4faf-a5f8-3f7e13899652" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_resident_registration_number" />
        <Match idRef ="Keyword_jp_resident_registration_number" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-96"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_resident_registration_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Resident Registration Number</p>
<p>Resident Register Number</p>
<p>Residents Basic Registry Number</p>
<p>Resident Registration No.</p>
<p>Resident Register No.</p>
<p>Residents Basic Registry No.</p>
<p>Basic Resident Register No.</p>
<p>住民登録番号、登録番号をレジデント</p>
<p>住民基本登録番号、登録番号</p>
<p>住民基本レジストリ番号を常駐</p>
<p>登録番号を常駐住民基本台帳登録番号</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Giappone - Numero di assicurazione sociale (SIN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>7-12 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>7-12 cifre:</p>
<ul>
<li><p>Quattro cifre</p></li>
<li><p>Una lineetta (facoltativa)</p></li>
<li><p>Sei cifre</p></li>
<li><p>OPPURE</p></li>
<li><p>7-12 cifre consecutive</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_sin</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_sin</code>.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_jp_sin_pre_1997</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_jp_sin</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Japan Social Insurance Number -->
<Entity id="c840e719-0896-45bb-84fd-1ed5c95e45ff" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_jp_sin" />
        <Match idRef="Keyword_jp_sin" />
    </Pattern>
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_sin_pre_1997" />
        <Match idRef="Keyword_jp_sin" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-98"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_sin</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Social Insurance No.</p>
<p>Social Insurance Num</p>
<p>Social Insurance Number</p>
<p>社会保険のテンキー</p>
<p>社会保険番号</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Malesia - Numero di carta d’identità


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>12 cifre contenenti lineette facoltative</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>12 cifre:</p>
<ul>
<li><p>Sei cifre nel formato AAMMGG, ovvero la data di nascita</p></li>
<li><p>Un trattino (facoltativo)</p></li>
<li><p>Codice luogo di nascita a due lettere</p></li>
<li><p>Un trattino (facoltativo)</p></li>
<li><p>Tre cifre casuali</p></li>
<li><p>Codice genere a una cifra singola</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_malaysia_id_card_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_malaysia_id_card_number</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Malaysia ID Card Number -->
</Entity>
      <Entity id="7f0e921c-9677-435b-aba2-bb8f1013c749" patternsProximity="300" recommendedConfidence="85">
        <Pattern confidenceLevel="85">
            <IdMatch idRef="Regex_malaysia_id_card_number" />
            <Match idRef="Keyword_malaysia_id_card_number" />
        </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-100"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_malaysia_id_card_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyKad</p>
<p>Carta di identità</p>
<p>Carta di identità</p>
<p>Identification Card</p>
<p>Scheda applicazione digitale</p>
<p>Kad Akuan Diri</p>
<p>Kad Aplikasi Digital</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Paesi Bassi - Numero di servizio cittadino (BSN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>8-9 cifre contenenti spazi facoltativi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>8-9 cifre:</p>
<ul>
<li><p>Tre cifre</p></li>
<li><p>Uno spazio (facoltativo)</p></li>
<li><p>Tre cifre</p></li>
<li><p>Uno spazio (facoltativo)</p></li>
<li><p>2-3 cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_netherlands_bsn</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_netherlands_bsn</code> .</p></li>
<li><p>La funzione <code>Func_eu_date2</code> rileva una data nel formato corretto.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Netherlands Citizen's Service (BSN) Number -->
<Entity id="c5f54253-ef7e-44f6-a578-440ed67e946d" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
       <IdMatch idRef="Func_netherlands_bsn" /> 
       <Match idRef="Keyword_netherlands_bsn" /> 
       <Match idRef="Func_eu_date2" /> 
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-102"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_netherlands_bsn</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero di servizio cittadino</p>
<p>BSN</p>
<p>Burgerservicenummer</p>
<p>Sofinummer</p>
<p>Persoonsgebonden nummer</p>
<p>Persoonsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Nuova Zelanda - Numero del Ministero della Sanità


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Tre lettere, uno spazio (facoltativo) e quattro cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Tre lettere (senza distinzione tra maiuscole/minuscole), uno spazio (facoltativo) e 4 cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_new_zealand_ministry_of_health_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_nz_terms</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- New Zealand Health Number -->
<Entity id="2b71c1c8-d14e-4430-82dc-fd1ed6bf05c7" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_new_zealand_ministry_of_health_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_nz_terms" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-104"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_nz_terms</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NHI</p>
<p>New Zealand</p>
<p>Health</p>
<p>treatment</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Norvegia - Numero di identificazione


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>11 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>11 cifre:</p>
<ul>
<li><p>Sei cifre nel formato GGMMAA, ovvero la data di nascita</p></li>
<li><p>Numero individuale composto da tre cifre</p></li>
<li><p>Due cifre di controllo</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_norway_id_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_norway_id_number</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_norway_id_numbe</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Norway Identification Number -->
<Entity id="d4c8a798-e9f2-4bd3-9652-500d24080fc3" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_norway_id_number"/>
     <Match idRef="Keyword_norway_id_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_norway_id_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-106"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_norway_id_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Codice PIN</p>
<p>Numero ID norvegese</p>
<p>Numero ID</p>
<p>Identificazione</p>
<p>Personnummer</p>
<p>Fødselsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Filippine - Numero ID multifunzione unificato


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>12 cifre separate da dei segni meno</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>12 cifre:</p>
<ul>
<li><p>Quattro cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Sette cifre</p></li>
<li><p>Una lineetta</p></li>
<li><p>Una cifra</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_philippines_unified_id</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_philippines_id</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Philippines Unified Multi-Purpose ID number -->
<Entity id="019b39dd-8c25-4765-91a3-d9c6baf3c3b3" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_philippines_unified_id"/>
     <Match idRef="Keyword_philippines_id"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-108"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_philippines_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID multifunzione unificato</p>
<p>UMID</p>
<p>Carta di identità</p>
<p>Pinag-isang Multi-Layunin ID</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Carta di identita - Polonia


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Tre lettere e sei cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Tre lettere (senza distinzione tra maiuscole/minuscole) seguite da sei cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_polish_national_id</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_polish_national_id_passport_number</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Poland Identity Card-->
<Entity id="25E64989-ED5D-40CA-A939-6C14183BB7BF" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_polish_national_id" />
          <Match idRef="Keyword_polish_national_id_passport_number" />
      </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-110"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_polish_national_id_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nazwa i nr dowodu tożsamości</p>
<p>Dowód Tożsamości</p>
<p>dow. os.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## ID nazionale Polonia (PESEL)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>11 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>11 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_pesel_identification_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_pesel_identification_number</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Poland National ID (PESEL) -->      
<Entity id="E3AAF206-4297-412F-9E06-BA8487E22456" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_pesel_identification_number" />
          <Match idRef="Keyword_pesel_identification_number" />
      </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-112"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_pesel_identification_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nr PESEL</p>
<p>PESEL</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Passaporto Polonia


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Due lettere e sette cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Due lettere (senza distinzione tra maiuscole/minuscole) seguite da sette cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_polish_passport_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_polish_national_id_passport_number</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Poland Passport Number -->
<Entity id="03937FB5-D2B6-4487-B61F-0F8BFF7C3517" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_polish_passport_number" />
          <Match idRef="Keyword_polish_national_id_passport_number" />
      </Pattern>
</Entity>
</Version>

```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-114"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_polish_national_id_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nazwa i nr dowodu tożsamości</p>
<p>Dowód Tożsamości</p>
<p>dow. os.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Portogallo - Numero di carta del cittadino


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Otto cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Otto cifre</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_portugal_citizen_card</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_portugal_citizen_card</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Portugal Citizen Card Number -->
<Entity id="91a7ece2-add4-4986-9a15-c84544d81ecd" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_portugal_citizen_card"/>
     <Match idRef="Keyword_portugal_citizen_card"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-116"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_portugal_citizen_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Scheda cittadino</p>
<p>Carta ID</p>
<p>CC</p>
<p>Cartão de Cidadão</p>
<p>Bilhete de Identidade</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Arabia Saudita - Identificativo nazionale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_saudi_arabia_national_id</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_saudi_arabia_national_id</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- Saudi Arabia National ID -->
<Entity id="8c5a0ba8-404a-41a3-8871-746aa21ee6c0" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_saudi_arabia_national_id" />
        <Any minMatches="1">
          <Match idRef="Keyword_saudi_arabia_national_id" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-118"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_saudi_arabia_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identification Card</p>
<p>I card number</p>
<p>ID number</p>
<p>الوطنية الهوية بطاقة رقم</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Singapore - Numero di carta di identità di registrazione nazionale (NRIC)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Nove lettere e numeri</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Nove lettere e numeri:</p>
<ul>
<li><p>La lettera &quot;F&quot;, &quot;G&quot;, &quot;S&quot; o &quot;T&quot; (senza distinzione tra maiuscole e minuscole)</p></li>
<li><p>Sette cifre</p></li>
<li><p>Una cifra di controllo alfabetica</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_singapore_nric</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_singapore_nric</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_singapore_nric</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Singapore National Registration Identity Card (NRIC) Number -->
<Entity id="cead390a-dd83-4856-9751-fb6dc98c34da" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_singapore_nric"/>
     <Match idRef="Keyword_singapore_nric"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_singapore_nric"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-120"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_singapore_nric</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta di identità di registrazione nazionale</p>
<p>Numero di carta di identità</p>
<p>NRIC</p>
<p>IC</p>
<p>Numero di identificazione per stranieri</p>
<p>FIN</p>
<p>身份证</p>
<p>身份證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Sudafrica - Numero di identificazione


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>13 cifre che possono contenere spazi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>13 cifre:</p>
<ul>
<li><p>Sei cifre nel formato AAMMGG, ovvero la data di nascita</p></li>
<li><p>Quattro cifre</p></li>
<li><p>Un indicatore di cittadinanza a una cifra</p></li>
<li><p>La cifra &quot;8&quot; o &quot;9&quot;</p></li>
<li><p>Una cifra, ovvero una cifra di checksum</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_south_africa_identification_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_south_africa_identification_number</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- South Africa Identification Number -->
<Entity id="e2adf7cb-8ea6-4048-a2ed-d89eb65f2780" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_south_africa_identification_number"/>
     <Match idRef="Keyword_south_africa_identification_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-122"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_south_africa_identification_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta di identità</p>
<p>ID</p>
<p>Identificazione</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Corea del Sud - Numero di registrazione dei residenti


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>13 cifre contenenti un segno meno</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>13 cifre:</p>
<ul>
<li><p>Sei cifre nel formato AAMMGG, ovvero la data di nascita</p></li>
<li><p>Una lineetta</p></li>
<li><p>Una cifra determinata dal secolo e dal sesso</p></li>
<li><p>Codice di quattro cifre dell’area geografica di nascita</p></li>
<li><p>Una cifra utilizzata per distinguere persone i cui numeri precedenti sono uguali</p></li>
<li><p>Una cifra di controllo.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_south_korea_resident_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_south_korea_resident_number</code> .</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_south_korea_resident_number</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- South Korea Resident Registration Number -->
<Entity id="5b802e18-ba80-44c4-bc83-bf2ad36ae36a" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_south_korea_resident_number"/>
     <Match idRef="Keyword_south_korea_resident_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_south_korea_resident_number"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-124"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_south_korea_resident_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carta di identità</p>
<p>Numero di registrazione del cittadino</p>
<p>Jumin deungnok beonho</p>
<p>RRN</p>
<p>주민등록번호</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Spagna - Numero di previdenza sociale (SSN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>11-12 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>11-12 cifre:</p>
<ul>
<li><p>Due cifre</p></li>
<li><p>Una barra (facoltativa)</p></li>
<li><p>7-8 cifre</p></li>
<li><p>Una barra (facoltativa)</p></li>
<li><p>Due cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_spanish_social_security_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Spain SSN -->
<Entity id="5df987c0-8eae-4bce-ace7-b316347f3070" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_spanish_social_security_number" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>None</p></td>
</tr>
</tbody>
</table>


## Svezia - Identificativo nazionale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 o 12 cifre e un delimitatore facoltativo</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 o 12 cifre e un delimitatore facoltativo:</p>
<ul>
<li><p>2-4 cifre (facoltative)</p></li>
<li><p>Sei cifre nel formato data AAMMGG</p></li>
<li><p>Delimitatore di &quot;-&quot; o &quot;+&quot; (facoltativo) più</p></li>
<li><p>Quattro cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_swedish_national_identifier</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Sweden National ID -->
<Entity id="f69aaf40-79be-4fac-8f05-fd1910d272c8" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_swedish_national_identifier" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Svezia - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Otto cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Otto cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_sweden_passport_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_passport</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_sweden_passport</code>.</p></li>
</ul></li>
</ul>

```Command&nbsp;Line
<!-- Sweden Passport Number -->
<Entity id="ba4e7456-55a9-4d89-9140-c33673553526" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_sweden_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_passport" />
          <Match idRef="Keyword_sweden_passport" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-128"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_sweden_passport</p></th>
<th> </th>
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>visa requirements</p>
<p>Alien Registration Card</p>
<p>Schengen visas</p>
<p>Schengen visa</p>
<p>Visa Processing</p>
<p>Visa Type</p>
<p>Single Entry</p>
<p>Multiple Entry</p>
<p>G3 Processing Fees</p></td>
<td> </td>
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport#</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport#</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Codice SWIFT


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Quattro lettere seguite da 5-31 lettere o cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Quattro lettere seguite da 5-31 lettere o cifre:</p>
<ul>
<li><p>Codice ABI di quattro cifre (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>Uno spazio facoltativo</p></li>
<li><p>4-28 lettere o cifre (BBAN)</p></li>
<li><p>Uno spazio facoltativo</p></li>
<li><p>1-3 lettere o cifre (resto del BBAN)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_swift</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_swift</code>.</p></li>
</ul>

```Command&nbsp;Line
<Entity id="cb2ab58c-9cb8-4c81-baf8-a4e106791df4" patternsProximity="300" recommendedConfidence="75">
<Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_swift" />
        <Match idRef="Keyword_swift" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-130"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_swift</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>international organization for standardization 9362</p>
<p>iso 9362</p>
<p>iso9362</p>
<p>swift#</p>
<p>swiftcode</p>
<p>swiftnumber</p>
<p>swiftroutingnumber</p>
<p>swift code</p>
<p>swift number #</p>
<p>swift routing number</p>
<p>bic number</p>
<p>bic code</p>
<p>bic #</p>
<p>bic#</p>
<p>bank identifier code</p>
<p>標準化9362</p>
<p>迅速＃</p>
<p>SWIFTコード</p>
<p>SWIFT番号</p>
<p>迅速なルーティング番号</p>
<p>BIC番号</p>
<p>BICコード</p>
<p>銀行識別コードのための国際組織</p>
<p>Organisation internationale de normalisation 9362</p>
<p>rapide #</p>
<p>code SWIFT</p>
<p>le numéro de swift</p>
<p>swift numéro d'acheminement</p>
<p>le numéro BIC</p>
<p># BIC</p>
<p>code identificateur de banque</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Taiwan National ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Una lettera (in lingua inglese) seguita da nove cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Una lettera (in lingua inglese) seguita da nove cifre:</p>
<ul>
<li><p>Una lettera (in inglese, senza distinzione tra tra maiuscole/minuscole)</p></li>
<li><p>La cifra &quot;1&quot; o &quot;2&quot;</p></li>
<li><p>Otto cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_taiwanese_national_id</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_taiwanese_national_id</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- Taiwanese National ID -->
<Entity id="4C7BFC34-8DD1-421D-8FB7-6C6182C2AF03" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_taiwanese_national_id" />
          <Match idRef="Keyword_taiwanese_national_id" />
      </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-132"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwanese_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>身份證字號</p>
<p>身份證</p>
<p>身份證號碼</p>
<p>身份證號</p>
<p>身分證字號</p>
<p>身分證</p>
<p>身分證號碼</p>
<p>身份證號</p>
<p>身分證統一編號</p>
<p>國民身分證統一編號</p>
<p>簽名</p>
<p>蓋章</p>
<p>簽名或蓋章</p>
<p>簽章</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Taiwan - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Numero di passaporto biometrico</p>
<dl>
<dd><p>9 cifre</p>
</dd>
</dl>
<p>Numero di passaporto non biometrico</p>
<dl>
<dd><p>9 cifre</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Numero di passaporto biometrico</p>
<ul>
<li><p>La cifra &quot;3&quot;</p></li>
<li><p>Otto cifre</p></li>
</ul>
<p>Numero di passaporto non biometrico</p>
<ul>
<li><p>9 cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_taiwan_passport</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_taiwan_passport</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Taiwan Passport Number -->
<Entity id="e7251cb4-4c2c-41df-963e-924eb3dae04a" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_taiwan_passport"/>
     <Match idRef="Keyword_taiwan_passport"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-134"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwan_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero passaporto ROC</p>
<p>Numero passaporto</p>
<p>N° passaporto</p>
<p>Num. passaporto</p>
<p>Passport #</p>
<p>护照</p>
<p>中華民國護照</p>
<p>Zhōnghuá Mínguó hùzhào</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Taiwan - Numero certificato di residenza (ARC/TARC)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10 lettere e cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10 lettere e cifre:</p>
<ul>
<li><p>Due lettere (senza distinzione tra maiuscole/minuscole)</p></li>
<li><p>Otto cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L' espressione regolare <code>Regex_taiwan_resident_certificate</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_taiwan_resident_certificate</code> .</p></li>
</ul>

```Command&nbsp;Line
<!-- Taiwan Resident Certificate (ARC/TARC) -->
<Entity id="48269fec-05ea-46ea-b326-f5623a58c6e9" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_taiwan_resident_certificate"/>
     <Match idRef="Keyword_taiwan_resident_certificate"/>
  </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-136"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwan_resident_certificate</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Certificato di residenza</p>
<p>Cert. di resid</p>
<p>Cert. di resid.</p>
<p>Carta d’identità</p>
<p>Certificato residente straniero</p>
<p>ARC</p>
<p>Certificato residente nell’area di Taiwan</p>
<p>TARC</p>
<p>居留證</p>
<p>外僑居留證</p>
<p>台灣地區居留證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Regno Unito - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Combinazione di 18 lettere e numeri nel formato specificato</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>18 lettere e cifre:</p>
<ul>
<li><p>Cinque lettere (senza distinzione fra maiuscole/minuscole) o la cifra 9 al posto di una lettera</p></li>
<li><p>Una cifra</p></li>
<li><p>5 cifre nel formato data GGMMA relativo alla data di nascita</p></li>
<li><p>Due lettere (senza distinzione fra maiuscole/minuscole) o la cifra 9 al posto di una lettera</p></li>
<li><p>Cinque cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_uk_drivers_license</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_uk_drivers_license</code>.</p></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. Driver's License Number -->
<Entity id="f93de4be-d94c-40df-a8be-461738047551" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_uk_drivers_license" />
        <Match idRef="Keyword_uk_drivers_license" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-138"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DVLA</p>
<p>light vans</p>
<p>quadbikes</p>
<p>motor cars</p>
<p>125cc</p>
<p>sidecar</p>
<p>tricycles</p>
<p>motorcycles</p>
<p>photocard licence</p>
<p>learner drivers</p>
<p>licence holder</p>
<p>licence holders</p>
<p>driving licences</p>
<p>driving licence</p>
<p>dual control car</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Regno Unito - Numero di iscrizione alle liste elettorali


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Due lettere seguite da 1-4 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Due lettere (senza distinzione fra maiuscole/minuscole) seguite da 1-4 numeri</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_uk_electoral</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_uk_electoral</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. Electoral Number -->
<Entity id="a3eea206-dc0c-4f06-9e22-aa1be3059963" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_uk_electoral" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_electoral" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-140"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_electoral</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>council nomination</p>
<p>nomination form</p>
<p>electoral register</p>
<p>electoral roll</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Regno Unito - Codice del servizio sanitario nazionale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>10-17 cifre separate da spazi</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>10-17 cifre:</p>
<ul>
<li><p>3 o 10 cifre</p></li>
<li><p>Uno spazio</p></li>
<li><p>Tre cifre</p></li>
<li><p>Uno spazio</p></li>
<li><p>Quattro cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_uk_nhs_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_uk_nhs_number</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_uk_nhs_number1</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_uk_nhs_number_dob</code>.</p></li>
</ul></li>
<li><p>Il checksum ha esito positivo.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. NHS Number -->
<Entity id="3192014e-2a16-44e9-aa69-4b20375c9a78" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_uk_nhs_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_nhs_number" />
          <Match idRef="Keyword_uk_nhs_number1" />
          <Match idRef="Keyword_uk_nhs_number_dob" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-142"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_nhs_number</p></th>
<th> </th>
<th><p>Keyword_uk_nhs_number1</p></th>
<th><p>Keyword_uk_nhs_number_dob</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>national health service</p>
<p>nhs</p>
<p>health services authority</p>
<p>health authority</p></td>
<td> </td>
<td><p>patient id</p>
<p>patient identification</p>
<p>patient no</p>
<p>patient number</p></td>
<td><p>GP</p>
<p>DOB</p>
<p>D.O.B</p>
<p>Date of Birth</p>
<p>Birth Date</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Regno Unito - Numero di assicurazione nazionale (NINO)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>7 cifre o 9 caratteri separati da spazi o trattini</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Due possibili motivi:</p>
<ul>
<li><p>Due lettere (NINOs valido utilizzare solo alcuni caratteri in questo prefisso, questo modello consente di convalidare; non maiuscole/minuscole)</p></li>
<li><p>Sei cifre</p></li>
<li><p>Entrambi '', &quot;B&quot;, &quot;C&quot;, oppure con ' (ad esempio il prefisso solo alcuni caratteri sono consentiti in suffisso; non distinzione tra maiuscole e minuscole)</p></li>
</ul>
<p>OPPURE</p>
<ul>
<li><p>Due lettere</p></li>
<li><p>Uno spazio o un trattino</p></li>
<li><p>Due cifre</p></li>
<li><p>Uno spazio o un trattino</p></li>
<li><p>Due cifre</p></li>
<li><p>Uno spazio o un trattino</p></li>
<li><p>Due cifre</p></li>
<li><p>Uno spazio o un trattino</p></li>
<li><p>Entrambi 'A', &quot;B&quot;, &quot;C&quot;, oppure con '</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_uk_nino</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_uk_nino</code>.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_uk_nino</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_uk_nino</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.K. NINO -->
<Entity id="16c07343-c26f-49d2-a987-3daf717e94cc" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_uk_nino" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_nino" />
        </Any>
    </Pattern>    
     <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_uk_nino" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_uk_nino" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-144"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_nino</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>national insurance number</p>
<p>national insurance contributions</p>
<p>protection act</p>
<p>insurance</p>
<p>social security number</p>
<p>insurance application</p>
<p>medical application</p>
<p>social insurance</p>
<p>medical attention</p>
<p>social security</p>
<p>great britain</p>
<p>insurance</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Stati Uniti/Regno Unito - Numero di passaporto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>9 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_usa_uk_passport</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_passport</code>.</p></li>
</ul>

```Command&nbsp;Line
<Entity id="178ec42a-18b4-47cc-85c7-d62c92fd67f8" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_usa_uk_passport" />
        <Match idRef="Keyword_passport" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-146"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport#</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport#</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Stati Uniti - Numero di conto bancario


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>8-17 cifre</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>8-17 cifre consecutive</p></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>L'espressione regolare <code>Regex_usa_bank_account_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_usa_Bank_Account</code>.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.S. Bank Account Number -->
<Entity id="a2ce32a8-f935-4bb6-8e96-2a5157672e2c" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_usa_bank_account_number" />
        <Match idRef="Keyword_usa_Bank_Account" />
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-148"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_usa_Bank_Account</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Checking Account Number</p>
<p>Checking Account</p>
<p>Checking Account #</p>
<p>Checking Acct Number</p>
<p>Checking Acct #</p>
<p>Checking Acct No.</p>
<p>Checking Account No.</p>
<p>Bank Account Number</p>
<p>Bank Account #</p>
<p>Bank Acct Number</p>
<p>Bank Acct #</p>
<p>Bank Acct No.</p>
<p>Bank Account No.</p>
<p>Savings Account Number</p>
<p>Savings Account.</p>
<p>Savings Account #</p>
<p>Savings Acct Number</p>
<p>Savings Acct #</p>
<p>Savings Acct No.</p>
<p>Savings Account No.</p>
<p>Debit Account Number</p>
<p>Debit Account</p>
<p>Debit Account #</p>
<p>Debit Acct Number</p>
<p>Debit Acct #</p>
<p>Debit Acct No.</p>
<p>Debit Account No.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Stati Uniti - Numero della patente di guida


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Varia in base allo stato</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Varia in base allo stato. Ad esempio, per New York:</p>
<ul>
<li><p>Nove cifre formattato come ggg ggg ggg corrispondenti.</p></li>
<li><p>Nove cifre come ddddddddd non corrispondono.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_new_york_drivers_license_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_[state_name]_drivers_license_name</code>.</p></li>
<li><p>È possibile trovare una parola chiave da <code>Keyword_us_drivers_license</code> .</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_new_york_drivers_license_number</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_[state_name]_drivers_license_name</code>.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_us_drivers_license_abbreviations</code>.</p></li>
<li><p>Non vengono trovate parole chiave da <code>Keyword_us_drivers_license</code>.</p></li>
</ul>

```Command&nbsp;Line
<Pattern confidenceLevel="75">
        <IdMatch idRef="Func_new_york_drivers_license_number" />
        <Match idRef="Keyword_new_york_drivers_license_name" />
        <Match idRef="Keyword_us_drivers_license" />
    </Pattern>
    <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_new_york_drivers_license_number" />
        <Match idRef="Keyword_new_york_drivers_license_name" />
        <Match idRef="Keyword_us_drivers_license_abbreviations" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_us_drivers_license" />
        </Any>
    </Pattern>

```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-150"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_us_drivers_license_abbreviations</p></th>
<th> </th>
<th><p>Keyword_us_drivers_license</p></th>
<th><p>Keyword_[state_name]_drivers_license_name</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DL</p>
<p>DLS</p>
<p>CDL</p>
<p>CDLS</p>
<p>ID</p>
<p>IDs</p>
<p>DL#</p>
<p>DLS#</p>
<p>CDL#</p>
<p>CDLS#</p>
<p>ID#</p>
<p>IDs#</p>
<p>ID number</p>
<p>ID numbers</p>
<p>LIC</p>
<p>LIC#</p></td>
<td> </td>
<td><p>DriverLic</p>
<p>DriverLics</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>Driver Lic</p>
<p>Driver Lics</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>DriversLic</p>
<p>DriversLics</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Drivers Lic</p>
<p>Drivers Lics</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Driver'Lic</p>
<p>Driver' Lics</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver'Lic</p>
<p>Driver' Lics</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver's Lic</p>
<p>Driver's Lics</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>identification number</p>
<p>identification numbers</p>
<p>identification#</p>
<p>id card</p>
<p>id cards</p>
<p>identification card</p>
<p>identification cards</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>Driver Lic#</p>
<p>Driver Lics#</p>
<p>Driver License#</p>
<p>Driver Licenses#</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>Drivers Lic#</p>
<p>Drivers Lics#</p>
<p>Drivers License#</p>
<p>Drivers Licenses#</p>
<p>Driver' Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver' Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver's Lic#</p>
<p>Driver's Lics#</p>
<p>Driver's License#</p>
<p>Driver's Licenses#</p>
<p>id card#</p>
<p>id cards#</p>
<p>identification card#</p>
<p>identification cards#</p></td>
<td><p>Abbreviazione dello stato (ad esempio, &quot;NY&quot;)</p>
<p>Nome dello stato (ad esempio, &quot;New York&quot;)</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Stati Uniti - Codice identificativo del contribuente individuale (ITIN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>Nove cifre che iniziano con &quot;9&quot; e contengono un &quot;7&quot; o un &quot;8&quot; come quarta cifra. Può essere formattato con spazi e trattini (facoltativo)</p></td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Formattato:</p>
<ul>
<li><p>La cifra &quot;9&quot;</p></li>
<li><p>Due cifre</p></li>
<li><p>Uno spazio o un trattino</p></li>
<li><p>Un &quot;7&quot; o un &quot;8&quot;</p></li>
<li><p>Una cifra</p></li>
<li><p>Uno spazio o un trattino</p></li>
<li><p>Quattro cifre</p></li>
</ul>
<p>Non formattato:</p>
<ul>
<li><p>La cifra &quot;9&quot;</p></li>
<li><p>Due cifre</p></li>
<li><p>Un &quot;7&quot; o un &quot;8&quot;</p></li>
<li><p>Cinque cifre</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_formatted_itin</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica almeno una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_itin</code>.</p></li>
<li><p>La funzione <code>Func_us_address</code> rileva un indirizzo nel formato di data corretto.</p></li>
<li><p>La funzione <code>Func_us_date</code> rileva una data nel formato corretto.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_itin_collaborative</code>.</p></li>
</ul></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_unformatted_itin</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Si verifica almeno una delle situazioni seguenti:</p>
<ul>
<li><p>Viene trovata una parola chiave da <code>Keyword_itin_collaborative</code>.</p></li>
<li><p>La funzione <code>Func_us_address</code> rileva un indirizzo nel formato di data corretto.</p></li>
<li><p>La funzione <code>Func_us_date</code> rileva una data nel formato corretto.</p></li>
</ul></li>
</ul>

```Command&nbsp;Line
<!-- U.S. Individual Taxpayer Identification Number (ITIN) -->
<Entity id="e55e2a32-f92d-4985-a35d-a0b269eb687b" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_formatted_itin" />
        <Any minMatches="1">
          <Match idRef="Keyword_itin" />
          <Match idRef="Func_us_address" />
          <Match idRef="Func_us_date" />
          <Match idRef="Keyword_itin_collaborative" />
        </Any>
    </Pattern>
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_itin" />
        <Match idRef="Keyword_itin" />
        <Any minMatches="1">
          <Match idRef="Keyword_itin_collaborative" />
          <Match idRef="Func_us_address" />
          <Match idRef="Func_us_date" />
        </Any>
    </Pattern>
</Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-152"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_itin</p></th>
<th> </th>
<th><p>Keyword_itin_collaborative</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>taxpayer</p>
<p>tax id</p>
<p>tax identification</p>
<p>itin</p>
<p>ssn</p>
<p>tin</p>
<p>social security</p>
<p>tax payer</p>
<p>itins</p>
<p>taxid</p>
<p>individual taxpayer</p></td>
<td> </td>
<td><p>License</p>
<p>DL</p>
<p>DOB</p>
<p>Birthdate</p>
<p>Birthday</p>
<p>Date of Birth</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Stati Uniti - Numero di previdenza sociale (SSN)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Formato</p></td>
<td><p>9 cifre formattate o meno</p>

> [!NOTE]
> Se eseguita prima funzione mid 2011, un SSN è sicuro formattazione cui devono essere compreso alcuni intervalli è valido in alcune parti del numero (ma non esiste alcun checksum).


</td>
</tr>
<tr class="even">
<td><p>Modello</p></td>
<td><p>Quattro funzioni cercare SSNs in quattro formati diversi:</p>
<ul>
<li><p><code>Func_ssn</code> trova SSNs di pre-2011 sicuro formattazione formattati con trattini o spazi (ggg-gg-gggg OR ggg gg gggg)</p></li>
<li><p><code>Func_unformatted_ssn</code> trova SSNs di pre-2011 sicuro la formattazione viene formattato come nove cifre consecutive (ddddddddd)</p></li>
<li><p><code>Func_randomized_formatted_ssn</code> trova SSNs post 2011 formattati con trattini o spazi (ggg-gg-gggg OR ggg gg gggg)</p></li>
<li><p><code>Func_randomized_unformatted_ssn</code> trova SSNs post 2011 che viene formattato come nove cifre consecutive (ddddddddd)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Checksum</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Definizione</p></td>
<td><p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 85%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_ssn</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_ssn</code>.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 75%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_unformatted_ssn</code> consente di trovare contenuto corrispondente al formato.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_ssn</code>.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 65%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_randomized_formatted_ssn</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_ssn</code>.</p></li>
<li><p>La funzione <code>Func_ssn</code> non trovare contenuti che corrispondono al modello.</p></li>
</ul>
<p>Un criterio DLP rileva questo tipo di informazioni con una probabilità del 55%, entro 300 caratteri, se:</p>
<ul>
<li><p>La funzione <code>Func_randomized_unformatted_ssn</code> restituisce contenuti che corrispondono al modello.</p></li>
<li><p>Viene trovata una parola chiave da <code>Keyword_ssn</code>.</p></li>
<li><p>La funzione <code>Func_unformatted_ssn</code> non trovare contenuti che corrispondono al modello.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.S. Social Security Number (SSN) -->
    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_ssn" />
        <Match idRef="Keyword_ssn" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_ssn" />
        <Match idRef="Keyword_ssn" />
      </Pattern>
      <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_randomized_formatted_ssn" />
        <Match idRef="Keyword_ssn" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Func_ssn" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="55">
        <IdMatch idRef="Func_randomized_unformatted_ssn" />
        <Match idRef="Keyword_ssn" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Func_unformatted_ssn" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><h3 id="section-154"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ssn</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Social Security</p>
<p>Social Security#</p>
<p>Soc Sec</p>
<p>SSN</p>
<p>SSNS</p>
<p>SSN#</p>
<p>SS#</p>
<p>SSID</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>

