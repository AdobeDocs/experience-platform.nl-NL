---
title: Integratie van auditlogboek voor query-service
description: De controlelogboeken van de Dienst van de vraag handhaven verslagen voor diverse gebruikersacties om een controletraject voor het oplossen van problemenkwesties te vormen of het naleven van het beleid van het collectieve gegevensbeheer en regelgevende vereisten. Dit leerprogramma verstrekt een overzicht van de eigenschappen van het controlelogboek specifiek voor de Dienst van de Vraag.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# [!DNL Query Service] integratie van controlelogboeken

De integratie van het Adobe Experience Platform [!DNL Query Service] -controlelogbestand biedt records met gebruikersacties die betrekking hebben op query. Auditlogboeken zijn een essentieel hulpmiddel voor het oplossen van problemen en het naleven van het beleid en de regelgevende vereisten van het bedrijfsgegevensbeheer. Het vermogen staat u toe om een actielogboek voor vele gebeurtenistypen en filter terug te keren en de verslagen uit te voeren. De logboeken kunnen of door Experience Platform UI of [ de Vraag API van de Controle van de Controle ](https://www.adobe.io/experience-platform-apis/references/audit-query/) worden betreden en in of CSV of JSON dossierformaten worden gedownload.

Meer over het gebruikersinterface van de controlelogboeken leren, verwijs naar het [ document van het controlelogboeken ](../../landing/governance-privacy-security/audit-logs/overview.md). Meer leren over het maken van vraag aan Experience Platform APIs, verwijs naar de [ handleiding van de controlelogboeken API ](../../landing/api-guide.md).

## Vereisten

U moet de machtiging [!DNL Data Governance] [!UICONTROL View User Activity Log] hebben ingeschakeld om het dashboard voor het auditlogboek weer te geven in de gebruikersinterface van Experience Platform. De toestemming wordt toegelaten door Adobe [ Admin Console ](https://adminconsole.adobe.com/). Neem contact op met de beheerder van uw organisatie als u geen beheerdersrechten hebt om deze machtiging in te schakelen. Zie de documentatie van de toegangscontrole voor [ volledige instructies bij het toevoegen van toestemmingen door Admin Console ](../../access-control/home.md).

## [!DNL Query Service] controlelogcategorieën {#audit-log-categories}

De categorieën van het controlelogboek die door [!DNL Query Service] worden verstrekt zijn als volgt.

| Categorie | Beschrijving |
|---|---|
| [!UICONTROL Query] | Met deze categorie kunt u query-uitvoeringen controleren. |
| [!UICONTROL Query template] | Met deze categorie kunt u de verschillende handelingen (maken, bijwerken en verwijderen) controleren die op een querysjabloon zijn uitgevoerd. |
| [!UICONTROL Scheduled query] | Met deze categorie kunt u de programma&#39;s controleren die zijn gemaakt, bijgewerkt of verwijderd in [!DNL Query Service] . |

## Een [!DNL Query Service] controlelogboek uitvoeren {#perform-an-audit-log}

Om een controle voor [!DNL Query Service] activiteiten uit te voeren, selecteer **[!UICONTROL Audits]** van de linkernavigatie, die door het kanaalpictogram wordt gevolgd (![ het filterpictogram van A.](/help/images/icons/filter.png)) om een lijst met filterbesturingselementen weer te geven om de resultaten te beperken.

![ het dashboard van het de controlelogboek van Experience Platform UI met &quot;Audits&quot;in de linkernavigatie en filtercontroles benadrukte.](../images/audit-log/filter-controls.png)

Vanuit het tabblad [!UICONTROL Audits] dashboard [!UICONTROL Activity log] kunt u alle opgenomen Experience Platform-handelingen filteren op een van de categorieën [!DNL Query Service] . De logboekresultaten kunnen verder worden gefiltreerd gebaseerd op de tijdsperiode zij werden uitgevoerd, de actie/de functie die, of de gebruiker werd genomen die de vraag uitvoerde. Zie de documentatie van het controlelogboek voor [ volledige instructies op hoe te om de logboeken te filtreren die op categorie, actie, gebruiker, en status ](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui) worden gebaseerd.

De teruggekeerde gegevens van het controlelogboek bevatten de volgende informatie over alle vragen die aan uw gekozen filtercriteria voldoen.

| Kolomnaam | Beschrijving |
|---|---|
| [!UICONTROL Timestamp] | De exacte datum en tijd van de actie die in een `month/day/year hour:minute AM/PM` -indeling wordt uitgevoerd. |
| [!UICONTROL Asset Name] | De waarde voor het veld [!UICONTROL Asset Name] is afhankelijk van de categorie die als filter is gekozen. Wanneer het gebruiken van de [!UICONTROL Scheduled query] categorie is dit de **planningsnaam**. Wanneer het gebruiken van de [!UICONTROL Query template] categorie, is dit de **malplaatjenaam**. Wanneer het gebruiken van de [!UICONTROL Query] categorie, is dit **zittingsidentiteitskaart** |
| [!UICONTROL Category] | Dit veld komt overeen met de categorie die u in de vervolgkeuzelijst met filters hebt geselecteerd. |
| [!UICONTROL Action] | Dit kan worden gemaakt, verwijderd, bijgewerkt of uitgevoerd. Welke acties beschikbaar zijn, is afhankelijk van de categorie die u als filter hebt gekozen. |
| [!UICONTROL User] | Dit veld bevat de gebruikersnaam die de query heeft uitgevoerd. |

![ het dashboard van Audits met het gefiltreerde benadrukte activiteitenlogboek.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Meer vraagdetails worden verstrekt door de logboekresultaten in of CSV of JSON dossierformaten te downloaden, dan door gebrek in het dashboard van het controlelogboek wordt getoond.

## Deelvenster Details

Selecteer een rij controlelogbestandresultaten om een deelvenster met details rechts van het scherm te openen.

![ het logboeklusje van de Activiteit van het dashboard van Audits met het benadrukte detailspaneel.](../images/audit-log/details-panel.png)

U kunt het deelvenster Details gebruiken om de [!UICONTROL Asset ID] en de [!UICONTROL Event status] te zoeken.

De waarde van de [!UICONTROL Asset ID] verandert afhankelijk van de categorie die in de controle wordt gebruikt.

* Wanneer het gebruiken van de [!UICONTROL Query] categorie, [!UICONTROL Asset ID] is **zittingsidentiteitskaart**.
* Wanneer het gebruiken van de [!UICONTROL Query template] categorie, [!UICONTROL Asset ID] is **malplaatje identiteitskaart** en met `[!UICONTROL templateID:]` vooraf bepaald.
* Wanneer het gebruiken van de [!UICONTROL Scheduled query] categorie, is [!UICONTROL Asset ID] **planningsidentiteitskaart** en met `[!UICONTROL scheduleID:]` vooraf bepaald.

De waarde van de [!UICONTROL Event status] verandert afhankelijk van de categorie die in de controle wordt gebruikt.

* Wanneer het gebruiken van de [!UICONTROL Query] categorie, verstrekt het [!UICONTROL Event status] gebied een lijst van alle **vraag IDs** die door de gebruiker binnen die zitting wordt uitgevoerd.
* Wanneer het gebruiken van de [!UICONTROL Query template] categorie, verstrekt het [!UICONTROL Event status] gebied de **malplaatjenaam** als prefix voor de gebeurtenisstatus.
* Wanneer het gebruiken van de [!UICONTROL Query schedule] categorie, verstrekt het [!UICONTROL Event status] gebied de **planningsnaam** als prefix voor de gebeurtenisstatus.

## Beschikbare filters voor [!DNL Query Service] controlelogcategorieën {#available-filters}

Welke filters beschikbaar zijn, is afhankelijk van de categorie die u in de vervolgkeuzelijst hebt geselecteerd. De volgende lijst specificeert de filters beschikbaar voor [[!DNL Query Service]  categorieën van het controlelogboek ](#audit-log-categories).

| Filter | Beschrijving |
|---|---|
| Categorie | Zie de [[!DNL Query Service]  sectie van het controlelogboek ](#audit-log-categories) voor een volledige lijst van beschikbare categorieën. |
| Actie | Wanneer het verwijzen naar [!DNL Query Service] controlecategorieën, is de update a **wijziging aan de bestaande vorm**, schrapt is de **verwijdering van het programma of het malplaatje**, creeer **creeert een nieuw programma of malplaatje**, en voert is **in werking stellend een vraag** uit. |
| Gebruiker | Voer de volledige gebruikersnaam in (bijvoorbeeld johndoe@acme.com) om te filteren op gebruiker. |
| Status | De [!UICONTROL Allow], [!UICONTROL Success], en [!UICONTROL Failure] opties filtreren de logboeken die op de &quot;Status&quot;of &quot;Status van de Gebeurtenis&quot;worden gebaseerd terwijl de [!UICONTROL Deny] optie **** logboeken zal filtreren. |
| Datum | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |

## Volgende stappen

Door dit document te lezen, hebt u een beter inzicht in de mogelijkheden van het [!DNL Query Service] controlelogboek en hoe het kan worden gebruikt om uw [!DNL Query Service] -gebruikersacties te filteren.

Als u het [!DNL Query Service] vermogen van het controlelogboek voor het oplossen van problemendoeleinden gebruikt, wordt u geadviseerd om de [ het oplossen van problemengids ](../troubleshooting-guide.md) te lezen.
