---
title: Overzicht van de extensie Meta Conversions API
description: Meer informatie over de API-extensie Meta Conversions voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# [!DNL Meta Conversions API] extensieoverzicht

De [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) staat u toe om uw server-kant marketing gegevens aan te sluiten [!DNL Meta] -technologieën om uw advertentie te optimaliseren, de kosten per actie te verlagen en de resultaten te meten. Gebeurtenissen zijn gekoppeld aan een [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID en worden op dezelfde manier verwerkt als gebeurtenissen aan de clientzijde.

Met de [!DNL Meta Conversions API] kunt u de API-mogelijkheden in uw [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) regels voor het verzenden van gegevens naar [!DNL Meta] van het Adobe Experience Platform Edge Network. In dit document wordt beschreven hoe u de extensie installeert en de mogelijkheden van de extensie gebruikt bij het doorsturen van gebeurtenissen [regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Als u gebeurtenissen wilt verzenden naar [!DNL Meta] van de client in plaats van van de server [[!DNL Meta Pixiel] tagextensie](../../client/meta/overview.md) in plaats daarvan.

## Vereisten

Als u de extensie wilt gebruiken, moet u toegang hebben tot het doorsturen van gebeurtenissen en een geldige waarde hebben [!DNL Meta] account met toegang tot [!DNL Ad Manager] en [!DNL Event Manager]. U moet met name de id van een bestaande id kopiëren [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (of [een nieuwe [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) in plaats daarvan), zodat de extensie kan worden geconfigureerd voor uw account.

## De extensie installeren

Als u het dialoogvenster [!DNL Meta Conversions API] de extensie, navigeert u naar de gebruikersinterface van de gegevensverzameling of het Experience Platform en selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie. Van hier, selecteer een bezit om de uitbreiding aan toe te voegen, of een nieuw bezit in plaats daarvan tot stand te brengen.

Als u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie, dan selecteer **[!UICONTROL Catalog]** tab. Zoeken naar [!UICONTROL Meta Conversions API] kaart, dan selecteren **[!UICONTROL Install]**.

![De [!UICONTROL Install] knop die wordt geselecteerd voor de [!UICONTROL Meta Conversions API] in de UI voor gegevensverzameling.](../../../images/extensions/server/meta/install.png)

In de configuratieweergave die wordt weergegeven, moet u de opdracht [!DNL Pixel] ID die u eerder hebt gekopieerd om de extensie te koppelen aan uw account. U kunt de id rechtstreeks in de invoer plakken, maar u kunt ook een gegevenselement gebruiken.

U moet ook een toegangstoken verstrekken om te gebruiken [!DNL Conversions API] specifiek. Zie de [!DNL Conversions API] documentatie over [toegangstoken genereren](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) voor stappen voor het verkrijgen van deze waarde.

Als u klaar bent, selecteert u **[!UICONTROL Save]**

![De [!DNL Pixel] ID verstrekt als gegevenselement in de mening van de uitbreidingsconfiguratie.](../../../images/extensions/server/meta/configure.png)

De extensie is geïnstalleerd en u kunt nu de mogelijkheden van de extensie gebruiken in de labelregels.

## Vorm een gebeurtenis door:sturen regel {#rule}

Begin creërend een nieuwe gebeurtenis door:sturen regel en vorm zijn voorwaarden zoals gewenst. Selecteer bij het selecteren van de handelingen voor de regel de optie **[!UICONTROL Meta Conversions API Extension]** voor de extensie selecteert u vervolgens **[!UICONTROL Send Conversions API Event]** voor het actietype.

![De [!UICONTROL Send Page View] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/meta/select-action.png)

De controles verschijnen die u toestaan om de gebeurtenisgegevens te vormen die zullen worden verzonden naar [!DNL Meta] via de [!DNL Conversions API]. Deze opties kunnen rechtstreeks in de verstrekte input worden ingevoerd, of u kunt bestaande gegevenselementen selecteren om de waarden te vertegenwoordigen. De configuratieopties worden verdeeld in vier hoofdsecties, zoals hieronder beschreven.

| Config-sectie | Beschrijving |
| --- | --- |
| [!UICONTROL Server Event Parameters] | Algemene informatie over de gebeurtenis, waaronder de tijd dat deze heeft plaatsgevonden en de bronactie die deze heeft geactiveerd. Zie de [[!DNL Conversions API] documentatie](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) voor meer informatie over deze parameters.<br><br>U kunt ook **[!UICONTROL Enable Limited Data Use]** om te helpen voldoen aan de opt-outs van klanten. Zie de [!DNL Conversions API] documentatie over [gegevensverwerkingsopties](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) voor meer informatie over deze functie. |
| [!UICONTROL Customer Information Parameters] | De identiteitsgegevens van de gebruiker die worden gebruikt om de gebeurtenis aan een klant toe te schrijven. Sommige van deze waarden moeten worden gehasht voordat ze naar de API kunnen worden verzonden. Zie de [[!DNL Conversions API] documentatie](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) voor meer informatie over deze parameters. |
| [!UICONTROL Custom Data] | Aanvullende gegevens die moeten worden gebruikt voor optimalisatie van levering voor advertenties, opgegeven in de vorm van een JSON-object. Zie de [[!DNL Conversions API] documentatie](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) voor meer informatie over de geaccepteerde eigenschappen voor dit object.<br><br>Als u een aankoopgebeurtenis verzendt, moet u deze sectie gebruiken om de vereiste kenmerken op te geven `currency` en `value`. |
| [!UICONTROL Test Event] | Deze optie wordt gebruikt om te verifiëren of uw configuratie servergebeurtenissen om veroorzaakt te ontvangen door [!DNL Meta] zoals verwacht. Als u deze functie wilt gebruiken, selecteert u de optie **[!UICONTROL Send as Test Event]** Schakel het selectievakje in en geef een gewenste testgebeurteniscode op in de onderstaande invoer. Zodra de gebeurtenis door:sturen regel wordt opgesteld, als u de uitbreiding en de actie correct vormde zou u activiteiten zien die binnen het **[!DNL Test Events]** weergeven in [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen.

![[!UICONTROL Keep Changes] geselecteerd voor de actieconfiguratie.](../../../images/extensions/server/meta/keep-changes.png)

Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**. Ten slotte publiceert u een nieuwe gebeurtenis die wordt doorgestuurd [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek mogelijk te maken.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gebeurtenisgegevens op de server kunt verzenden naar [!DNL Meta] met de [!DNL Meta Conversions API] extensie. Raadpleeg voor meer informatie over tags en het doorsturen van gebeurtenissen de [overzicht van tags](../../../home.md).
