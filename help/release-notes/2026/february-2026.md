---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2026
description: Aanvullende informatie voor Adobe Experience Platform van februari 2026.
exl-id: a677026f-e07e-4e69-bd6c-5ddcb13e8e38
source-git-commit: a11c00c218ffbbd5618616f401613a604c35859a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 54%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 17 februari 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Bestemmingen](#destinations)
- [Bronnen](#sources)
- [Experience Data Model (XDM)](#xdm)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Slack] integratie voor klantgerichte waarschuwingen | U kunt nu klantgerichte waarschuwingen naar [!DNL Slack] verzenden. Volg het [&#x200B; geleidelijke leerprogramma &#x200B;](../../observability/alerts/slack-integration.md) aan opstelling de [!DNL Slack] integratie en ontvang direct waakzame berichten in uw [!DNL Slack] werkruimte. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [[!DNL Observability Insights] overzicht](../../observability/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [[!DNL Snowflake]  Partij &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md) algemeen beschikbaar | De [!DNL Snowflake] Batch-bestemming is nu over het algemeen beschikbaar. Real-Time CDP-klanten overal ter wereld kunnen deze connector nu gebruiken om gegevens in hun Snowflake-accounts te activeren zonder dat ze de gegevens fysiek hoeven te kopiëren. Alle beperkingen van de beperkte release zijn opgeheven (beschikbaarheid voor klanten in de VS, ondersteuning voor publiek dat alleen tot het standaardsamenvoegbeleid behoort). |

{style="table-layout:auto"}

**Bevestigingen en verbeteringen**

| Repareren | Beschrijving |
| --- | --- |
| Activeringsfrequentie overschreden waarschuwing | Het mislukte Tarief van de Activering Te boven ging bestemmingsalarm gebruikt nu correct de drempel u wanneer het evalueren van en het verzenden van het alarm vormt. Eerder, teweeggebracht de alarm bij een 1% mislukkingstarief ongeacht het percentage u vormde. Zie [&#x200B; standaard waakzame regels &#x200B;](../../observability/alerts/rules.md#destinations) voor meer details over dit alarm. |
| Rapportering van uitgesloten identiteiten volgens Google Customer Match | Probleem verholpen in de logica voor het tellen van overgeslagen records die ertoe leidde dat het aantal opgepompte uitgesloten profielen werd weergegeven voor Google Customer Match-bestemmingen. De activering en het exportgedrag werden niet beïnvloed; alleen de gerapporteerde nummers waren onjuist. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| Ondersteuning voor Unity Catalog in [!DNL Databricks] bronconnector | De [!DNL Databricks] bronaansluiting ondersteunt nu de catalogus Eenheid. Lees de bijgewerkte [[!DNL Databricks]](../../sources/connectors/databases/databricks.md) documentatie om te leren hoe te om de Catalogus van de Eenheid te gebruiken wanneer u uw bronverbinding vormt. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).


## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Beperkt bewerken voor schema&#39;s met gegevenssets | Het uitgeven verrichtingen die in het breken van veranderingen resulteren worden nu beperkt zodra een dataset voor een schema bestaat. Wanneer een dataset wordt geassocieerd, kunt u niet meer gebieden anders noemen of schrappen, de types of formaten van gebiedsgegevens veranderen, identiteitsbeschrijvers wijzigen, verwante gebieden beheren om bestaande gebieden te verwijderen, of de toegewezen klasse veranderen; de additieve veranderingen en gebiedsafstand blijven gesteund. |

Voor meer informatie raadpleegt u het [overzicht van XDM](../../xdm/home.md).
