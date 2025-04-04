---
title: XDM Business Person Components-schemaveldgroep
description: Meer informatie over de XDM Business Person Components schemagroep.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!UICONTROL XDM Business Person Components] schemaveldgroep

[!UICONTROL XDM Business Person Components] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse ](../../classes/individual-profile.md) die veelvoudige bronverslagen voor een persoon vangt, en andere attributen die voor persoonsegmentatie worden vereist.

Wanneer een profiel voor een persoon door [ Real-Time Profiel van de Klant ](../../../profile/home.md) in B2B edition van Real-Time CDP wordt gecreeerd, kan de informatie die wordt gebruikt om dat profiel tot stand te brengen potentieel uit vele bronverslagen voortkomen. Bijvoorbeeld, als een persoon voor twee verschillende bedrijven werkt, zouden vele systemen van CRM tot een opzettelijk dubbel exemplaar van die persoon leiden zodat één exemplaar met Bedrijf A wordt verbonden, terwijl andere met Onderneming B wordt verbonden. Wanneer die gegevens naar Adobe Experience Platform worden overgebracht, wordt deze veldgroep gebruikt om die verschillende bronrecords samen te voegen tot één representatie.

De veldgroep biedt een veld op hoofdniveau `personComponents` . Dit is een array van objecten. Elk object in de array vertegenwoordigt een andere bronrecord.

>[!IMPORTANT]
>
>U moet de innamepatronen volgen zoals die in de [ documentatie van bronnen ](../../../rtcdp/sources/b2b.md) worden beschreven. Andere kaartmethoden in het veld werken niet gegarandeerd.
>
>Elk object van de array `personComponents` wordt bijvoorbeeld afzonderlijk verzonden tijdens standaard opname-patronen en vervolgens door Experience Platform aan de array toegevoegd. Als u handmatig een array met objecten toevoegt aan de Business Person Component, wordt een fout geretourneerd.
>U zou het auto-generatienut moeten gebruiken wanneer het creëren van schema&#39;s voor uw B2B gegevens. Zie de documentatie voor instructies op hoe te om [ B2B te gebruiken namespace en schema auto-generatienut ](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Als u niet het auto-generatienut gebruikt en van plan bent om uw gegevensmodel manueel in kaart te brengen, ben zeker om de documentatie over de [ Adobe Real-Time Customer Data Platform B2B edition XDM klassen ](../../../rtcdp/schemas/b2b.md) te lezen alvorens uw gegevens in kaart te brengen.
>
>Zie het [ leerprogramma van begin tot eind ](../../../rtcdp/b2b-tutorial.md) voor informatie over geadviseerde werkschema&#39;s voor B2B- gegevens.

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

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
