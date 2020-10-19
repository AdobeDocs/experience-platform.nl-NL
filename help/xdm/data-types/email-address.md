---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype e-mailadres
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor e-mailadressen.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# [!UICONTROL Gegevenstype e-mailadres]

[!UICONTROL Het e-mailadres] is een standaard XDM gegevenstype dat de details van een e-mailadres beschrijft.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `address` | Het technische adres van e-mail zoals algemeen bepaald in RFC2822 en verdere normen (bijvoorbeeld, `name@domain.com`). |
| `label` | Aanvullende weergavegegevens die beschikbaar kunnen zijn. Bijvoorbeeld, als een e-mail een rijke adresvertoning van Microsoft Outlook heeft `John Smith smithjr@company.uk`, zou `John Smith` op dit gebied worden geplaatst. |
| `primary` | Geeft aan of dit het primaire e-mailadres van de betrokkene is. Een profiel kan slechts één `primary` e-mailadres op een bepaald tijdstip hebben. |
| `status` | Geeft aan of het e-mailadres momenteel kan worden gebruikt |
| `statusReason` | Een beschrijving van de huidige `status`. |
| `type` | De wijze waarop de rekening op de persoon betrekking heeft (zoals `work` of `personal`). |


Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het e-mailadres:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)