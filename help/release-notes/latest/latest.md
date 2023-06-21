---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van juni 2023 staat Adobe Experience Platform vermeld.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b9d78cd726430b0c7690fdb814d0888aaad832f6
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 21 juni 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Query-service](#query-service)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensie | [!DNL Google Cloud Platform] extensie voor doorsturen van gebeurtenissen | De [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) Met de extensie voor het doorsturen van gebeurtenissen kunt u gebeurtenisgegevens doorsturen naar Google voor activering via [!DNL Google Pub/Sub]. |
| Extensie | [!DNL Cloud connector for Google Analytics 4 (ga4)] extension | De [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) gebeurtenis die uitbreiding door:sturen staat u toe om analyses via nieuwe te volgen [!DNL Google Analytics 4 (ga4)] standaard. |
| Geheim | OAuth 2 JWT Secret | De [OAuth 2 JWT Secret](../../tags/ui/event-forwarding/secrets.md) staat u toe om Adobe te gebruiken en [!DNL Google] De tokens van de dienst om server-server interactie in gebeurtenis te steunen die door:sturen. |
| Tags en doorsturen van gebeurtenissen | Toewijzing gebruiker | De attributie van de gebruiker levert zeer belangrijke activiteitsgegevens over over [Tags](../../tags/home.md) en [Gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) UI.<br><br>De gegevens bevatten wie welke wijzigingen heeft aangebracht en op welk tijdstip. Deze gegevens zijn in de volgende schermen zichtbaar in de gebruikersinterface Tags en Event Forwarding:<br><ul><li> Overzicht van eigenschappen</li><li> Geïnstalleerde extensies</li><li>Regels vergelijken en herzien</li><li>Gegevenselementen vergelijken overzicht</li><li>Extensies vergelijken revisie</li><li>Wijzigingen in bibliotheekbron</li><li>Bibliotheek laatst samenstellen en gepubliceerd</li></ul> |

{style="table-layout:auto"}

Voor meer informatie over gegevensverzameling leest u de [overzicht van gegevensverzameling](../../tags/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL te gebruiken om gegevens in het gegevenspeer van Adobe Experience Platform te vragen. U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time. &#x200B;
**Bijgewerkte functies**
&#x200B; | Functie | Beschrijving | | — | — | | Inline-sjablonen &#x200B; | De Dienst van de vraag steunt nu het gebruik van malplaatjes die andere malplaatjes binnen uw SQL van verwijzingen voorzien. Verminder uw werkbelasting en vermijd fouten door inlinesjablonen in uw query&#39;s te gebruiken. U kunt instructies of voorwaarden opnieuw gebruiken en verwijzen naar geneste sjablonen voor meer flexibiliteit in uw SQL. Er is geen grens in de grootte van vragen die als malplaatjes kunnen worden opgeslagen, of het aantal malplaatjes die van uw originele vraag kunnen worden van verwijzingen voorzien. Lees voor meer informatie de [inline sjabloonhandleiding](../../query-service/essential-concepts/inline-templates.md). | | Geplande UI-updates voor query | U kunt alle geplande query&#39;s vanaf één locatie in de gebruikersinterface beheren met de [[!UICONTROL Scheduled Queries tab]](../../query-service/ui/monitor-queries.md#inline-actions). De [!UICONTROL Scheduled Queries] UI is verbeterd met de toevoeging van gealigneerde vraagacties en de nieuwe kolom van de vraagstatus. De recente toevoegingen omvatten de capaciteit om, een programma toe te laten onbruikbaar te maken en te schrappen, of aan alarm voor komende vraaglooppas direct van te abonneren [!UICONTROL Scheduled Queries] weergeven. <p>![Inline-handelingen gemarkeerd in het dialoogvenster [!UICONTROL Scheduled Queries] weergeven.](../../query-service/images/ui/monitor-queries/disable-inline.png "Inline-handelingen gemarkeerd in het dialoogvenster [!UICONTROL Scheduled Queries] weergeven."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
&#x200B; Voor meer informatie over de Dienst van de Vraag, verwijs naar [Overzicht van Query Service](../../query-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens uit verschillende bronnen invoeren, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Adobe Analytics-indelingsbron met gegevensstroom voor verwijderen | U kunt nu brongegevens verwijderen die gebruikmaken van Adobe Analytics-classificaties als bron. Onder **[!UICONTROL Sources]** > **[!UICONTROL Dataflows]**, selecteert u de gewenste gegevensstroom en selecteert u Verwijderen. Lees voor meer informatie de handleiding op [een bronverbinding maken voor Adobe Analytics-classificatiegegevens](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| Ondersteuning voor filteren van [!DNL Microsoft Dynamics] API gebruiken | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) bron. Lees voor meer informatie de handleiding op [gegevens filteren voor een bron met behulp van de API](../../sources/tutorials/api/filter.md). |
| [!BADGE Beta]{type=Informative}[!DNL RainFocus] | U kunt nu de opdracht [!DNL RainFocus] bronnen integratie om gebeurtenisbeheer en analysegegevens van uw [!DNL RainFocus] aan Experience Platform. Lees voor meer informatie de [[!DNL RainFocus] bronoverzicht](../../sources/connectors/analytics/rainfocus.md). |
| Ondersteuning voor Adobe Commerce | U kunt nu de integratie met Adobe Commerce-bronnen gebruiken om gegevens van uw Adobe Commerce-account naar Experience Platform te brengen. Lees voor meer informatie de [Adobe Commerce-bronoverzicht](../../sources/connectors/adobe-applications/commerce.md). |
| Ondersteuning voor [!DNL Mixpanel] | U kunt nu de opdracht [!DNL Mixpanel] bronnen integratie om analysegegevens van uw [!DNL Mixpanel] account aan Experience Platform met behulp van API&#39;s of de gebruikersinterface. Lees voor meer informatie de [[!DNL Mixpanel] bronoverzicht](../../sources/connectors/analytics/mixpanel.md). |
| Ondersteuning voor [!DNL Zendesk] | U kunt nu de opdracht [!DNL Zendesk] bronnen integratie om gegevens van uw klanten over succes te brengen [!DNL Zendesk] account aan Experience Platform met behulp van API&#39;s of de gebruikersinterface. Lees voor meer informatie de [[!DNL Zendesk] bronoverzicht](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
