---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schemaontwerp;mixin;mixin;het werkdetails;het profielwerk;
solution: Experience Platform
title: Werkgroep Contactgegevens-schema
description: Leer over de het schemagebiedgroep van de Details van het Contact van het Werk.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# [!UICONTROL Work Contact Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [&#x200B; de naamupdates van de gebiedsgroep &#x200B;](../name-updates.md) voor meer informatie.

[!UICONTROL Work Contact Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../classes/individual-profile.md). De veldgroep bevat verschillende velden waarin beroepsinformatie over een individuele persoon wordt vastgelegd, zoals het werkadres, e-mail over het werk, het telefoonnummer van de werkplek en de organisaties waartoe de persoon behoort.

![](../../images/field-groups/work-contact-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `workAddress` | [&#x200B; Postadres &#x200B;](../../data-types/postal-address.md) | Beschrijft het het werkadres van de persoon. |
| `workEmail` | [&#x200B; E-mailadres &#x200B;](../../data-types/email-address.md) | Beschrijft het het werk e-mailadres van de persoon. |
| `workPhone` | [&#x200B; Aantal van de Telefoon &#x200B;](../../data-types/phone-number.md) | Beschrijft het het het werktelefoonnummer van de persoon. |
| `organizations` | String (Array) | Een array van vrije-vormreeksen die de organisaties vertegenwoordigen waarvan de persoon lid is. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
