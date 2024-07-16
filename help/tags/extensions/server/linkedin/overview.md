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

# [!DNL LinkedIn] conversies-API-extensie

[[!DNL LinkedIn Conversions API] ](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) is een hulpmiddel van de omzetcontrole dat tot een directe verbinding tussen marketing gegevens van de server van een adverteerder en [!DNL LinkedIn] leidt. Hierdoor kunnen adverteerders de doeltreffendheid van hun [!DNL LinkedIn] -marketingcampagnes evalueren, ongeacht de locatie van de conversie, en deze informatie gebruiken om de campagne te optimaliseren. De extensie [!DNL LinkedIn Conversions API] kan u helpen de prestaties te verbeteren en de kosten per actie te verlagen met een vollediger toewijzing, verbeterde betrouwbaarheid van gegevens en een betere geoptimaliseerde levering.

## Vereisten {#prerequisites}

U moet [ een omzettingsregel ](https://www.linkedin.com/help/lms/answer/a1657171) in uw [!DNL LinkedIn Campaign Manager] rekening tot stand brengen. [!DNL Adobe] adviseert met inbegrip van &quot;CAPI&quot;aan het begin van de naam van de gespreksregel om het van andere types van omzettingsregel te plaatsen u zou kunnen gevormd hebben.

### Een geheim en een gegevenselement maken

Creeer een nieuwe [!DNL LinkedIn] [ gebeurtenis door:sturen geheim ](../../../ui/event-forwarding/secrets.md) en verstrek het van een unieke naam die het voor authentiek verklaren lid aanduidt. Dit wordt gebruikt om de verbinding met uw account te verifiëren en de waarde veilig te houden.

Daarna, [ creeer een gegevenselement ](../../../ui/managing-resources/data-elements.md#create-a-data-element) gebruikend de [!UICONTROL Core] uitbreiding en een [!UICONTROL Secret] type van gegevenselement om naar het `LinkedIn` geheim te verwijzen u enkel creeerde.

## De extensie [!DNL LinkedIn] installeren en configureren {#install}

Om de uitbreiding te installeren, [ creeer een gebeurtenis door:sturen bezit ](../../../ui/event-forwarding/overview.md#properties) of selecteer een bestaand bezit om uit te geven.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer op het tabblad **[!UICONTROL Catalog]** de extensie **[!UICONTROL LinkedIn]** en selecteer vervolgens **[!UICONTROL Install]** .

![ de uitbreidingscatalogus die [!DNL LinkedIn] uitbreidingskaart tonen die installeert benadrukt.](../../../images/extensions/server/linkedin/install-extension.png)

Voer in het volgende scherm het geheim voor het gegevenselement dat u eerder hebt gemaakt in het veld `Access Token` in. Het gegevenselement-geheim bevat uw [!DNL LinkedIn] OAuth 2-token. Selecteer **[!UICONTROL Save]** wanneer u klaar bent.

![ de [!DNL LinkedIn] pagina van de uitbreidingsconfiguratie met het [!UICONTROL Access Token] gebied en [!UICONTROL Save] benadrukte.](../../../images/extensions/server/linkedin/configure-extension.png)

## Een [!DNL Send Conversion] -regel maken {#tracking-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen die regels bepaalt wanneer en hoe uw gebeurtenissen naar [!DNL LinkedIn] zullen worden verzonden.

Creeer een nieuwe gebeurtenis door:sturen [ regel ](../../../ui/managing-resources/rules.md) in uw gebeurtenis door:sturen bezit. Voeg onder **[!UICONTROL Actions]** een nieuwe handeling toe en stel de extensie in op **[!UICONTROL LinkedIn]** . Selecteer vervolgens **[!UICONTROL Send Conversion]** voor **[!UICONTROL Action Type]** .

![ de Gebeurtenis die de mening van de Regels van het Bezit door:sturen, met de gebieden die worden vereist om een gebeurtenis toe te voegen die de benadrukte configuratie van de regelactie door:sturen.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Na selectie, schijnen de extra controles om de gebeurtenis verder te vormen. Selecteer **[!UICONTROL Keep Changes]** om de regel op te slaan.

**[!UICONTROL User Data]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Email] | E-mailadres van de contactpersoon die aan de conversiegebeurtenis is gekoppeld. De e-mailwaarde wordt gecodeerd door de extensiecode in SHA256, tenzij de opgegeven waarde al een SHA256-tekenreeks is. |
| [!UICONTROL LinkedIn First Party Ads Tracking UUID] | Dit is een eerste cookie-id. Adverteerders moeten de verbeterde omzetting het volgen van [[!DNL LinkedIn Campaign Manager] ](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) toelaten om eerste partijkoekjes te activeren die een klikparameter van identiteitskaart `li_fat_id` aan klikURLs toevoegen. |
| [!UICONTROL Customer Information Data] | Dit veld bevat een JSON-object met extra kenmerken die samen met het bericht worden verzonden.<br><br> onder de **[!UICONTROL Raw]** optie, kunt u het voorwerp JSON in het verstrekte tekstgebied direct kleven, of u kunt het pictogram van het gegevenselement (![ pictogram Dataset ](../../../images/extensions/server/aws/data-element-icon.png)) selecteren uit een lijst van bestaande gegevenselementen om de gegevens te vertegenwoordigen.<br><br> u kunt de **[!UICONTROL JSON Key-Value Pairs Editor]** optie ook gebruiken om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar in plaats daarvan kan ook een gegevenselement worden geselecteerd. De toegestane toetswaarden zijn: `firstName`, `lastName`, `companyName`, `title` en `country` . |

{style="table-layout:auto"}

![ de [!DNL User Data] sectie die voorbeeldgegevensinput in de gebieden toont.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Conversion Data]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Conversion] | Identiteitskaart van de omzettingsregel die in [ wordt gecreeerd de Manager van de Campagne van LinkedIn ](https://www.linkedin.com/help/lms/answer/a1657171). Selecteer de omzettingsregel om identiteitskaart te verkrijgen, dan kopieer identiteitskaart van browser URL (bijvoorbeeld, `/campaignmanager/accounts/508111232/conversions/15588877`) als `/conversions/<id>`. |
| [!UICONTROL Conversion Time] | Elke tijdstempel in milliseconden waarop de conversiegebeurtenis heeft plaatsgevonden. <br><br> Opmerking: als uw bron de tijdstempel van de conversie in seconden opneemt, voegt u aan het einde 000 in om deze om te zetten in milliseconden. |
| [!UICONTROL Currency] | Valutacode in ISO-indeling. |
| [!UICONTROL Amount] | Waarde van de conversie in decimale tekenreeks (bijvoorbeeld &quot;100.05&quot;). |
| [!UICONTROL Event ID] | De unieke id die door adverteerders wordt gegenereerd om elke gebeurtenis aan te geven. Dit is een facultatief gebied en wordt gebruikt voor [ deduplicatie ](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![ de [!DNL Conversion Data] sectie die voorbeeldgegevens op de gebieden tonen.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Configuration Overrides]**

>OPMERKING
>
>Met het veld [!UICONTROL Configuration Overrides] kan een gebruiker op elke regel een ander [!DNL LinkedIn] -toegangstoken instellen, zodat elke regel een toegangstoken kan gebruiken dat toegang kan hebben tot verschillende [!DNL LinkedIn] -advertentierekeningen.

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Access Token] | Het toegangstoken van [!DNL LinkedIn]. |

![ de [!DNL Configuration Overrides] sectie die voorbeeldgegevensinput op het gebied tonen.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u gegevens naar [!DNL LinkedIn] kunt verzenden met de extensie [!DNL LinkedIn Conversions API] voor het doorsturen van gebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden in [!DNL Adobe Experience Platform] door:sturen, lees de [ gebeurtenis die overzicht ](../../../ui/event-forwarding/overview.md) door:sturen.

Voor details op hoe te om uw implementatie te zuiveren gebruikend het Experience Platform Debugger en het Door:sturen van de Gebeurtenis hulpmiddel van de Controle, lees het [ overzicht van het Adobe Experience Platform Debugger ](../../../../debugger/home.md) en [ de activiteiten van de Monitor in gebeurtenis door:sturen ](../../../ui/event-forwarding/monitoring.md).
