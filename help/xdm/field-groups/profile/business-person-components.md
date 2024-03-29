---
title: XDM Business Person Components-schemaveldgroep
description: Meer informatie over de XDM Business Person Components schemagroep.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# [!UICONTROL XDM Business Person Components] schemaveldgroep

[!UICONTROL XDM Business Person Components] is een standaardschemagebiedgroep voor [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) die veelvoudige bronverslagen voor een persoon, en andere eigenschappen vangen die voor persoonsegmentatie worden vereist.

Wanneer een profiel voor een persoon via [Klantprofiel in realtime](../../../profile/home.md) In de B2B-editie van Real-Time CDP kan de informatie die voor het maken van dat profiel wordt gebruikt, mogelijk afkomstig zijn van veel bronrecords. Bijvoorbeeld, als een persoon voor twee verschillende bedrijven werkt, zouden vele systemen van CRM tot een opzettelijk dubbel exemplaar van die persoon leiden zodat één exemplaar met Bedrijf A wordt verbonden, terwijl andere met Onderneming B wordt verbonden. Wanneer die gegevens naar Adobe Experience Platform worden overgebracht, wordt deze veldgroep gebruikt om die verschillende bronrecords samen te voegen tot één representatie.

De veldgroep biedt een basisniveau `personComponents` field, een array van objecten. Elk object in de array vertegenwoordigt een andere bronrecord.

>[!IMPORTANT]
>
>U dient de inname-patronen te volgen zoals beschreven in het dialoogvenster [documentatie bronnen](../../../rtcdp/sources/b2b.md). Andere kaartmethoden in het veld werken niet gegarandeerd.
>
>Elk object van de `personComponents` array wordt afzonderlijk verzonden tijdens standaard innamepatronen en vervolgens aan de array toegevoegd door Platform. Als u handmatig een array met objecten toevoegt aan de Business Person Component, wordt een fout geretourneerd.
>U zou het auto-generatienut moeten gebruiken wanneer het creëren van schema&#39;s voor uw B2B gegevens. Zie de documentatie voor instructies over het gebruik van de [B2B-naamruimte en hulpprogramma voor automatisch genereren van schema](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Als u het hulpprogramma voor automatisch genereren niet gebruikt en van plan bent het gegevensmodel handmatig toe te wijzen, moet u de documentatie op het tabblad [Adobe Real-time Customer Data Platform B2B Edition XDM-klassen](../../../rtcdp/schemas/b2b.md) voordat u uw gegevens toewijst.
>
>Zie de [end-to-end zelfstudie](../../../rtcdp/b2b-tutorial.md) voor informatie over aanbevolen workflows voor B2B-gegevens.

![](../../images/field-groups/business-person-components.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de account die aan de persoon is gekoppeld. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de gerelateerde contactpersoon als deze lead is omgezet. |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor het bronsysteem waaruit de gegevens van de persoon afkomstig zijn. |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon. |
| `workEmail` | [[!UICONTROL Email address]](../../data-types/b2b-source.md) | De werkmail-id van de persoon. |
| `personGroupID` | String | Een groepsidentificatie voor de persoon. |
| `personScore` | String | Een score die door een CRM-systeem voor de persoon wordt gegenereerd. |
| `personSource` | String | Een unieke op tekenreeks gebaseerde id voor het bronsysteem waaruit de gegevens van de persoon afkomstig zijn. |
| `personStatus` | String | De huidige handels- of verkoopstatus van de persoon. |
| `personType` | String | Het type persoon in een B2B-context. |
| `sourceAccountID` | String | Een unieke op tekenreeks gebaseerde id voor de account in het bronsysteem dat aan de persoon is gekoppeld. Dit veld wordt door het systeem gebruikt als een buitenlandse sleutel om de verschillende bedrijven op te zoeken waar deze persoon voor werkt. |
| `sourceConvertedContactID` | String | Een unieke op tekenreeks gebaseerde id voor de gerelateerde contactpersoon als deze lead is omgezet. |
| `sourceExternalID` | String | Een unieke op tekenreeks gebaseerde id voor het bronsysteem waaruit de gegevens van de persoon afkomstig zijn. |
| `sourcePersonID` | String | Een unieke op tekenreeks gebaseerde id voor de persoon. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
