---
title: Werkgebiedgroep Gezondheidszorgverlener
description: Leer over de het schemagebiedgroep van de Leverancier van de Gezondheid.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!UICONTROL Healthcare Provider] schemaveldgroep

[!UICONTROL Healthcare Provider] is een standaardgroep van het schemagebied voor de [[!UICONTROL Provider] klasse ](../../classes/provider.md). Het biedt één objecttype veld `healthcareProvider` waarin eigenschappen worden vastgelegd die gerelateerd zijn aan een individuele gezondheidswerker of een organisatie van een gezondheidszorginstelling die een vergunning heeft om medische diagnoses en behandelingsdiensten te verrichten.

![](../../images/field-groups/healthcare-provider.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `addressDetails` | Array van objecten | Hier worden de adresgegevens van de provider weergegeven. Elk object bevat de volgende eigenschappen: <ul><li>`address`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)): Het postadres voor de leverancier.</li><li>`addressType`: (Tekenreeks) Het type adres dat aangeeft waar de provider services levert.</li></ul> |
| `emailAddress` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Het e-mailadres van de provider. |
| `fax` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het faxnummer van de provider. |
| `phoneNumber` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het telefoonnummer van de provider. |
| `qualifications` | Array van objecten | Hier worden de certificeringen, licenties of opleidingen vermeld die betrekking hebben op het verlenen van zorg. Elk object bevat de volgende eigenschappen: <ul><li>`issuer`: ([[!UICONTROL Account details]](../../data-types/account-details.md)): De organisatie die de kwalificatie regelt en uitgeeft.</li><li>`activePeriod`: (Geheel getal) Het jaar tot waar de kwalificatie geldig is.</li><li>`code`: (String) Een gecodeerde representatie van de kwalificatie.</li></ul> |
| `classification` | String | De classificatie van de dienstverlener gebaseerd op klasse of categorie (zoals patiëntenzorg, niet patiëntenzorg, etc.). |
| `isActive` | Boolean | Geeft aan of de provider actief is. |
| `languages` | Array van tekenreeksen | Een lijst met talen die de provider gebruikt. |
| `practiceGroupName` | String | De naam van de praktijkgroep voor de dienstverlener. |
| `practiceGroupType` | String | Het type van praktijkgroep voor de dienstverlener. |
| `practiceType` | String | Het praktijktype voor de dienstverlener. |
| `specialties` | Array van tekenreeksen | Een lijst van specialisaties die door deze leverancier worden aangeboden. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
