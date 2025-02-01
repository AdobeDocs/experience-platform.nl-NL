---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;emailAddress;xdm:emailAddress;email;email adres;datatype;data-type;data-type; data-type;
solution: Experience Platform
title: Gegevenstype e-mailadres
description: Leer over het E-mailadres XDM gegevenstype.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# [!UICONTROL Email address] gegevenstype

[!UICONTROL Email address] is een standaard XDM-gegevenstype (Experience Data Model) waarmee de details van een e-mailadres worden beschreven.

![](../images/data-types/email-address.png){width=450}

| Eigenschap | Beschrijving |
| --- | --- |
| `address` | Het technische adres van e-mail zoals algemeen bepaald in RFC2822 en verdere normen (bijvoorbeeld, `name@domain.com`).<br><br> in XDM, moeten de e-mailadressen een geldig top-level domein bevatten om bevestiging over te gaan. Verwijs naar het volgende [ document ](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) voor een volledige lijst van geldige top-level domeinen zoals die door Internet worden bepaald Toegewezen Instantie van Aantallen (IANA). |
| `label` | Aanvullende weergavegegevens die beschikbaar kunnen zijn. Als een e-mailbericht bijvoorbeeld een uitgebreide adresweergave van `John Smith smithjr@company.uk` in Microsoft Outlook heeft, wordt `John Smith` in dit veld geplaatst. |
| `primary` | Geeft aan of dit het primaire e-mailadres van de betrokkene is. Een profiel kan slechts één `primary` e-mailadres op een bepaald tijdstip hebben. |
| `status` | Geeft aan of het e-mailadres momenteel kan worden gebruikt |
| `statusReason` | Een beschrijving van de huidige `status` . |
| `type` | De manier waarop de account betrekking heeft op de persoon (bijvoorbeeld `work` of `personal` ). |

{style="table-layout:auto"}


Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het e-mailadres:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
