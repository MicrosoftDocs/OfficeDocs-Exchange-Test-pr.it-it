---
title: 'Supportato criteri cassetta postale di dispositivo mobile per Windows Phone e dispositivi: Exchange 2013 Help'
TOCTitle: Supportato criteri cassetta postale di dispositivo mobile per Windows Phone e dispositivi
ms:assetid: d76b1d4c-d1f6-4501-a7c9-854327aceda5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ983805(v=EXCHG.150)
ms:contentKeyID: 52063136
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supportato criteri cassetta postale di dispositivo mobile per Windows Phone e dispositivi

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Con il rilascio di Windows Phone 8, Windows 8 e Windows RT esistono diversi dispositivi che supportano Exchange ActiveSync e i criteri cassetta postale dei dispositivi mobili. Ogni sistema operativo del dispositivo supporta uno specifico set di impostazioni dei criteri cassetta postale dei dispositivi mobili.

## Matrice di compatibilità tra il client Windows e Exchange Server

Nella tabella seguente viene fornito in elenco di parametri di criteri cassetta postale dei dispositivi mobili compatibili per le diverse versioni di Windows Phone, Windows 8, Windows RT e Exchange Server.

## Parametri dei criteri supportati per Windows Phone 7

Nella seguente tabella sono elencate le impostazioni dei criteri cassetta postale dei dispositivi mobili per Windows 7.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
</tr>
<tr class="even">
<td><p>MinPasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>PasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
<tr class="even">
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
</tr>
<tr class="even">
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
</tr>
<tr class="odd">
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
</tr>
<tr class="even">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
</tbody>
</table>


## Parametri dei criteri supportati per Windows Phone 8

Nella seguente tabella sono elencate le impostazioni dei criteri cassetta postale dei dispositivi mobili per Windows 8.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="even">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>N/D</p></td>
<td><p>IRMEnabled</p></td>
<td><p>IRMEnabled</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>


## Parametri dei criteri cassetta postale supportati per Windows 8 e Windows RT

Nella seguente tabella sono elencate le impostazioni dei criteri cassetta postale dei dispositivi mobili per Windows 8 e Windows RT.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="odd">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="even">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="odd">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>

