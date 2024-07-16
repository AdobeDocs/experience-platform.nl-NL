---
title: Gegevenstype postadres
description: Leer over het de gegevenstype van de Gegevens van de Ervaring van het Postadres Model (XDM).
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# [!UICONTROL Postal Address] gegevenstype

[!UICONTROL Postal Address] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat adresdetails verstrekt.

![ een diagram van het [!UICONTROL Postal Address] gegevenstype.](../images/data-types/postal-address.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primary] | `primary` | boolean | Primaire adresindicator. Een profiel kan slechts één `primary` -adres op een bepaald tijdstip hebben. |
| [!UICONTROL Label] | `label` | string | Vrije-vormnaam van het adres. |
| [!UICONTROL Street 1] | `street1` | string | Primaire straatinformatie, appartementnummer, straatnummer en straatnaam. |
| [!UICONTROL Street 2] | `street2` | string | Optionele straatinformatie, tweede regel. |
| [!UICONTROL Street 3] | `street3` | string | Optionele straatinformatie, derde regel. |
| [!UICONTROL Street 4] | `street4` | string | Optionele straatinformatie, vierde regel. |
| [!UICONTROL Region] | `region` | string | Het gebied, het graafschap, of het districtsgedeelte van het adres. |
| [!UICONTROL Post office box] | `postOfficeBox` | string | Post Office box of the address. |
| [!UICONTROL Country] | `country` | string | De naam van het door de overheid bestuurde gebied. Met uitzondering van ``countryCode`` is dit een veld met vrije vorm dat de landnaam in elke taal kan hebben. |
| [!UICONTROL State] | `state` | string | De naam van de staat. Dit is een veld met vrije vorm. |
| [!UICONTROL Status] | `status` | string | Een indicatie van de mogelijkheid om het adres te gebruiken. |
| [!UICONTROL Status reason] | `statusReason` | string | Een beschrijving van de huidige status. |
| [!UICONTROL Last verified date] | `lastVerifiedDate` | string | De datum dat het adres het laatst als nog verbonden met de persoon werd geverifieerd. |

{style="table-layout:auto"}

Voor meer details op het gegevenstype, verwijs naar het [ volledige schema ](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) op de openbare bewaarplaats XDM:
