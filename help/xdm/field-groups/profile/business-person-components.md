---
title: XDM Business Person Components-schemaveldgroep
description: Dit document biedt een overzicht van de XDM Business Person Components schema-veldgroep.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# [!UICONTROL XDM Business Person Components] schemaveldgroep (bèta)

>[!IMPORTANT]
>
>Deze veldgroep is beschikbaar als onderdeel van Customer Data Platform B2B Edition in realtime, dat momenteel in bèta wordt weergegeven. De documentatie en functionaliteit kunnen worden gewijzigd.

[!UICONTROL XDM Business Person Components] is een standaardgroep van het schemagebied voor de  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klasse die veelvoudige bronverslagen voor een persoon, en andere attributen vangt die voor persoonsegmentatie worden vereist.

Wanneer een profiel voor een persoon door [Real-time Profiel van de Klant ](../../../profile/home.md) in de B2B uitgave van CDP in real time wordt gecreeerd, kan de informatie die wordt gebruikt om dat profiel tot stand te brengen potentieel uit vele bronverslagen voortkomen. Bijvoorbeeld, als een persoon voor twee verschillende bedrijven werkt, zouden vele systemen van CRM tot een opzettelijk dubbel exemplaar van die persoon leiden zodat één exemplaar met Bedrijf A wordt verbonden, terwijl andere met Onderneming B wordt verbonden. Wanneer die gegevens naar Adobe Experience Platform worden overgebracht, wordt deze veldgroep gebruikt om die verschillende bronrecords samen te voegen tot één representatie.

De veldgroep bevat een `personComponents`-veld op hoofdniveau. Dit is een array van objecten. Elk object in de array vertegenwoordigt een andere bronrecord.

![](../../images/field-groups/business-person-components.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de account die aan de persoon is gekoppeld. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de gerelateerde contactpersoon als deze lead is omgezet. |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor het bronsysteem waaruit de gegevens van de persoon afkomstig zijn. |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon. |
| `workEmail` | [[!UICONTROL Email address]](../../data-types/b2b-source.md) | De werk-e-mailid van de persoon. |
| `personGroupID` | Tekenreeks | Een groepsidentificatie voor de persoon. |
| `personScore` | Tekenreeks | Een score die door een CRM-systeem voor de persoon wordt gegenereerd. |
| `personSource` | Tekenreeks | Een unieke op tekenreeks gebaseerde id voor het bronsysteem waaruit de gegevens van de persoon afkomstig zijn. |
| `personStatus` | Tekenreeks | De huidige handels- of verkoopstatus van de persoon. |
| `personType` | Tekenreeks | Het type persoon in een B2B-context. |
| `sourceAccountID` | Tekenreeks | Een unieke op tekenreeks gebaseerde id voor de account in het bronsysteem dat aan de persoon is gekoppeld. Dit veld wordt door het systeem gebruikt als een buitenlandse sleutel om de verschillende bedrijven op te zoeken waar deze persoon voor werkt. |
| `sourceConvertedContactID` | Tekenreeks | Een unieke op tekenreeks gebaseerde id voor de gerelateerde contactpersoon als deze lead is omgezet. |
| `sourceExternalID` | Tekenreeks | Een unieke op tekenreeks gebaseerde id voor het bronsysteem waaruit de gegevens van de persoon afkomstig zijn. |
| `sourcePersonID` | Tekenreeks | Een unieke op tekenreeks gebaseerde id voor de persoon. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
