---
title: LinkIn Conversions API-gebeurtenis die extensie doorsturen
description: Deze Adobe Experience Platform gebeurtenis die uitbreiding door:sturen staat u toe om de prestaties van uw LinkedIn marketing campagne te meten.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 0d6ade1a0b6c00a4f87395d476dd7e7915489ea5
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# [!DNL LinkedIn] conversie-API-extensie

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) is een hulpmiddel voor het bijhouden van conversies dat een directe verbinding maakt tussen marketinggegevens van de server van een adverteerder en [!DNL LinkedIn]. Hierdoor kunnen adverteerders de doeltreffendheid van hun [!DNL LinkedIn] marketingcampagnes, ongeacht de locatie van de conversie, en gebruik deze informatie om de campagne te optimaliseren. De [!DNL LinkedIn Conversions API] de uitbreiding kan de prestaties verbeteren en de kosten per actie verlagen met een vollediger toewijzing, verbeterde betrouwbaarheid van de gegevens en een beter geoptimaliseerde levering.

## Vereisten {#prerequisites}

U moet [een conversieregel maken](https://www.linkedin.com/help/lms/answer/a1657171) in uw [!DNL LinkedIn Campaign Manager] account. [!DNL Adobe] adviseert met inbegrip van &quot;CAPI&quot;aan het begin van de naam van de gespreksregel om het van andere types van omzettingsregel los te plaatsen u zou kunnen gevormd hebben.

### Een geheim en een gegevenselement maken

Een nieuwe [!DNL LinkedIn] [gebeurtenis die geheim door:sturen](../../../ui/event-forwarding/secrets.md) en geef deze een unieke naam die het authenticerende lid aangeeft. Dit wordt gebruikt om de verbinding met uw account te verifiëren en de waarde veilig te houden.

Volgende, [een gegevenselement maken](../../../ui/managing-resources/data-elements.md#create-a-data-element) met de [!UICONTROL Core] en [!UICONTROL Secret] het elementtype van gegevens om naar `LinkedIn` geheim dat je zojuist hebt gemaakt.

## Installeer en configureer de [!DNL LinkedIn] extension {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of selecteer een bestaande eigenschap die u wilt bewerken.

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** selecteert u de **[!UICONTROL LinkedIn]** en selecteer vervolgens **[!UICONTROL Install]**.

![De extensiecatalogus die de [!DNL LinkedIn] installatie van markering voor extensiekaart.](../../../images/extensions/server/linkedin/install-extension.png)

Op het volgende scherm, ga het geheim van het gegevenselement in u vroeger in het `Access Token` veld. Het gegevenselement-geheim bevat uw [!DNL LinkedIn] OAuth 2 token. Selecteren **[!UICONTROL Save]** wanneer gereed.

![De [!DNL LinkedIn] extensieconfiguratiepagina met de [!UICONTROL Access Token] veld en [!UICONTROL Save] gemarkeerd.](../../../images/extensions/server/linkedin/configure-extension.png)

## Een [!DNL Send Conversion] regel {#tracking-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen door:sturen regels die bepalen wanneer en hoe uw gebeurtenissen zullen worden verzonden naar [!DNL LinkedIn].

Een nieuwe gebeurtenis maken door:sturen [regel](../../../ui/managing-resources/rules.md) in uw gebeurtenis die bezit door:sturen. Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL LinkedIn]**. Selecteer vervolgens **[!UICONTROL Send Conversion]** voor de **[!UICONTROL Action Type]**.

![De gebeurtenis die de mening van de Regels van het Bezit door:sturen, met de gebieden die worden vereist om een gebeurtenis toe te voegen die de benadrukte configuratie van de regelactie door:sturen.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Na selectie, schijnen de extra controles om de gebeurtenis verder te vormen. Selecteren **[!UICONTROL Keep Changes]** om de regel op te slaan.

**[!UICONTROL User Data]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Email] | E-mailadres van de contactpersoon die aan de conversiegebeurtenis is gekoppeld. De e-mailwaarde wordt gecodeerd door de extensiecode in SHA256, tenzij de opgegeven waarde al een SHA256-tekenreeks is. |
| [!UICONTROL LinkedIn First Party Ads Tracking UUID] | Dit is een eerste cookie-id. Adverteerders moeten het bijhouden van conversies inschakelen [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) om cookies van eerste bedrijven te activeren die een parameter click-id toevoegen `li_fat_id` klikt u op URL&#39;s. |
| [!UICONTROL Customer Information Data] | Dit veld bevat een JSON-object met extra kenmerken die samen met het bericht worden verzonden.<br><br>Onder de **[!UICONTROL Raw]** kunt u het JSON-object rechtstreeks in het opgegeven tekstveld plakken of het pictogram voor het gegevenselement selecteren (![Dataset-pictogram](../../../images/extensions/server/aws/data-element-icon.png)) om de gegevens te selecteren in een lijst met bestaande gegevenselementen.<br><br>U kunt ook de opdracht **[!UICONTROL JSON Key-Value Pairs Editor]** optie om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar in plaats daarvan kan ook een gegevenselement worden geselecteerd. De geaccepteerde sleutelwaarden zijn: `firstName`, `lastName`, `companyName`, `title` en `country`. |

{style="table-layout:auto"}

![De [!DNL User Data] sectie met voorbeeldgegevens die in de velden worden ingevoerd.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Conversion Data]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Conversion] | De id van de omzettingsregel die is gemaakt in [LinkedIn Campagne Manager](https://www.linkedin.com/help/lms/answer/a1657171). Selecteer de omzettingsregel om identiteitskaart te verkrijgen, dan kopieer identiteitskaart van browser URL (bijvoorbeeld `/campaignmanager/accounts/508111232/conversions/15588877`) als `/conversions/<id>`. |
| [!UICONTROL Conversion Time] | Elke tijdstempel in milliseconden waarop de conversiegebeurtenis heeft plaatsgevonden. <br><br> Opmerking: als uw bron de tijdstempel van de conversie in seconden opneemt, voegt u aan het einde 000 in om deze om te zetten in milliseconden. |
| [!UICONTROL Currency] | Valutacode in ISO-indeling. |
| [!UICONTROL Amount] | Waarde van de conversie in decimale tekenreeks (bijvoorbeeld &quot;100.05&quot;). |
| [!UICONTROL Event ID] | De unieke id die door adverteerders wordt gegenereerd om elke gebeurtenis aan te geven. Dit is een optioneel veld en wordt gebruikt voor [deduplicatie](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![De [!DNL Conversion Data] sectie met voorbeeldgegevens in de velden.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Configuration Overrides]**

>OPMERKING
>
>De [!UICONTROL Configuration Overrides] veld stelt een gebruiker in staat een andere instelling te kiezen [!DNL LinkedIn] toegangstoken op elke regel, die elke regel toestaat om een toegangstoken te gebruiken die toegang tot verschillende kan hebben [!DNL LinkedIn] advertentierekeningen.

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Access Token] | De [!DNL LinkedIn] toegangstoken. |

![De [!DNL Configuration Overrides] sectie met voorbeeldgegevens in het veld.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe gegevens worden verzonden naar [!DNL LinkedIn] met de [!DNL LinkedIn Conversions API] gebeurtenis die uitbreiding door:sturen. Voor meer informatie over gebeurtenis die mogelijkheden door:sturen in [!DNL Adobe Experience Platform], lees de [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).

Voor details over hoe te om uw implementatie te zuiveren gebruikend het hulpmiddel van de Controle van Foutopsporing van het Experience Platform en van de Gebeurtenis door:sturen, lees [Overzicht van Adobe Experience Platform Debugger](../../../../debugger/home.md) en [Activiteiten controleren bij het doorsturen van gebeurtenissen](../../../ui/event-forwarding/monitoring.md).
