---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;emailAddress;xdm:emailAddress;email;email adres;datatype;data-type;data-type; data-type;
solution: Experience Platform
title: Gegevenstype e-mailadres
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor e-mailadressen.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# [!UICONTROL Email address] gegevenstype

[!UICONTROL Email address] is een standaard XDM gegevenstype dat de details van een e-mailadres beschrijft.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `address` | Het technische adres van e-mail zoals algemeen bepaald in RFC2822 en verdere normen (bijvoorbeeld, `name@domain.com`). |
| `label` | Aanvullende weergavegegevens die beschikbaar kunnen zijn. Als een e-mailbericht bijvoorbeeld een uitgebreide adresweergave van Microsoft Outlook van `John Smith smithjr@company.uk` heeft, wordt `John Smith` in dit veld geplaatst. |
| `primary` | Geeft aan of dit het primaire e-mailadres van de betrokkene is. Een profiel kan slechts één `primary` e-mailadres op een bepaald tijdstip hebben. |
| `status` | Geeft aan of het e-mailadres momenteel kan worden gebruikt |
| `statusReason` | Een beschrijving van de huidige `status`. |
| `type` | De manier waarop de account betrekking heeft op de persoon (zoals `work` of `personal`). |


Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het e-mailadres:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
