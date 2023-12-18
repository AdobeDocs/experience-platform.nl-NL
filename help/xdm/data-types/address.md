---
title: Gegevenstype postadres
description: Leer over het de gegevenstype van de Gegevens van de Ervaring van het Postadres Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# [!UICONTROL Postal Address] gegevenstype

[!UICONTROL Postal Address] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat adresdetails verstrekt.

![Een schema van de [!UICONTROL Postal Address] gegevenstype.](../images/data-types/postal-address.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primary] | `primary` | boolean | Primaire adresindicator. Een profiel kan slechts één profiel hebben `primary` adres op een bepaald tijdstip. |
| [!UICONTROL Label] | `label` | string | Vrije-vormnaam van het adres. |
| [!UICONTROL Street 1] | `street1` | string | Primaire straatinformatie, appartementnummer, straatnummer en straatnaam. |
| [!UICONTROL Street 2] | `street2` | string | Optionele straatinformatie, tweede regel. |
| [!UICONTROL Street 3] | `street3` | string | Optionele straatinformatie, derde regel. |
| [!UICONTROL Street 4] | `street4` | string | Optionele straatinformatie, vierde regel. |
| [!UICONTROL Region] | `region` | string | Het gebied, het graafschap, of het districtsgedeelte van het adres. |
| [!UICONTROL Post office box] | `postOfficeBox` | string | Postkantoor van het adres. |
| [!UICONTROL Country] | `country` | string | De naam van het door de overheid bestuurde gebied. andere dan ``countryCode``Dit is een veld met vrije vorm dat de naam van het land in elke taal kan hebben. |
| [!UICONTROL State] | `state` | string | De naam van de staat. Dit is een veld met vrije vorm. |
| [!UICONTROL Status] | `status` | string | Een indicatie van de mogelijkheid om het adres te gebruiken. |
| [!UICONTROL Status reason] | `statusReason` | string | Een beschrijving van de huidige status. |
| [!UICONTROL Last verified date] | `lastVerifiedDate` | string | De datum dat het adres het laatst als nog verbonden met de persoon werd geverifieerd. |

{style="table-layout:auto"}

Voor meer details over het gegevenstype raadpleegt u de [volledig schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) in de openbare XDM-opslagplaats:
