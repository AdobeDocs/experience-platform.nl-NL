---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;emailAddress;xdm:emailAddress;email;email adres;datatype;data-type;data-type; data-type;
solution: Experience Platform
title: Gegevenstype e-mailadres
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor e-mailadressen.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: fe6abe468025ab3373f802954aedceeb1af625fe
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# [!UICONTROL Email address] gegevenstype

[!UICONTROL Email address] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de details van een e-mailadres beschrijft.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `address` | Het technische adres van e-mail zoals algemeen bepaald in RFC2822 en verdere normen (bijvoorbeeld, `name@domain.com`).<br><br>In XDM moeten e-mailadressen een geldig domein op hoofdniveau bevatten om validatie te kunnen doorstaan. Raadpleeg het volgende: [document](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) voor een volledige lijst van geldige top-level domeinen zoals die door Internet wordt bepaald Toegewezen Instantie van Aantallen (IANA). |
| `label` | Aanvullende weergavegegevens die beschikbaar kunnen zijn. Als een e-mailbericht bijvoorbeeld een uitgebreide adresweergave van Microsoft Outlook heeft van `John Smith smithjr@company.uk`, `John Smith` wordt in dit veld geplaatst. |
| `primary` | Geeft aan of dit het primaire e-mailadres van de betrokkene is. Een profiel kan slechts één profiel hebben `primary` e-mailadres op een bepaald tijdstip. |
| `status` | Geeft aan of het e-mailadres momenteel kan worden gebruikt |
| `statusReason` | Een beschrijving van de huidige `status`. |
| `type` | De wijze waarop de rekening op de persoon betrekking heeft (zoals `work` of `personal`). |

{style=&quot;table-layout:auto&quot;}


Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het e-mailadres:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
