---
title: Werkgebiedgroep Gezondheidszorgverlener
description: Dit document biedt een overzicht van de veldgroep met het schema van de zorgleverancier.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---

# [!UICONTROL Healthcare Provider] schemaveldgroep

[!UICONTROL Healthcare Provider] is een standaardschemagebiedgroep voor [[!UICONTROL Provider] class](../../classes/provider.md). Het biedt één veld van het objecttype `healthcareProvider` die eigenschappen vastlegt die verband houden met een individuele gezondheidswerker of een organisatie van een gezondheidsinstelling die een vergunning heeft om medische diagnoses en behandelingen te verrichten.

![](../../images/field-groups/healthcare-provider.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `addressDetails` | Array van objecten | Hier worden de adresgegevens van de provider weergegeven. Elk object bevat de volgende eigenschappen: <ul><li>`address`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)): Het postadres van de provider.</li><li>`addressType`: (String) Het type adres dat aangeeft waar de provider services levert.</li></ul> |
| `emailAddress` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Het e-mailadres van de provider. |
| `fax` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het faxnummer van de provider. |
| `phoneNumber` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het telefoonnummer van de provider. |
| `qualifications` | Array van objecten | Hier worden de certificeringen, licenties of opleidingen vermeld die betrekking hebben op het verlenen van zorg. Elk object bevat de volgende eigenschappen: <ul><li>`issuer`: ([[!UICONTROL Account details]](../../data-types/account-details.md)): De organisatie die de kwalificatie regelt en afgeeft.</li><li>`activePeriod`: (Geheel getal) Het jaar tot waar de kwalificatie geldig is.</li><li>`code`: (String) Een gecodeerde representatie van de kwalificatie.</li></ul> |
| `classification` | Tekenreeks | De classificatie van de dienstverlener gebaseerd op klasse of categorie (zoals patiëntenzorg, niet patiëntenzorg, etc.). |
| `isActive` | Boolean | Geeft aan of de provider actief is. |
| `languages` | Array van tekenreeksen | Een lijst met talen die de provider gebruikt. |
| `practiceGroupName` | Tekenreeks | De naam van de praktijkgroep voor de dienstverlener. |
| `practiceGroupType` | Tekenreeks | Het type van praktijkgroep voor de dienstverlener. |
| `practiceType` | Tekenreeks | Het praktijktype voor de dienstverlener. |
| `specialties` | Array van tekenreeksen | Een lijst van specialisaties die door deze leverancier worden aangeboden. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
