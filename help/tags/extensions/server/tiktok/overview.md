---
title: Adobe TikTok webgebeurtenissen API-extensie Integratie
description: Met deze Adobe Experience Platform-API voor webgebeurtenissen kunt u interacties van websites rechtstreeks delen met TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
source-git-commit: d8b7006ade1dc82fdd79b7ed744c021bc304bca7
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 2%

---

# [!DNL TikTok] API-extensie voor webgebeurtenissen

De [!DNL TikTok] events API is beveiligd [Edge Network Server-API](/help/server-api/overview.md) interface die u toestaat om informatie met te delen [!DNL TikTok] rechtstreeks informatie over gebruikersacties op uw websites. U kunt de regels voor het doorsturen van gebeurtenissen gebruiken om gegevens te verzenden vanuit de [!DNL Adobe Experience Platform Edge Network] tot [!DNL TikTok] door de [!DNL TikTok] Web Events API-extensie.

## [!DNL TikTok] voorwaarden {#prerequisites}

Om te vormen [!DNL TikTok] webgebeurtenissen met de API [!DNL TikTok] gebeurtenissen-API, moet u een [!DNL TikTok] pixelcode en toegangstoken.

U moet een geldige [!DNL TikTok] voor zakelijke account om een [!DNL TikTok] pixel die de partneropstelling gebruiken. Ga naar de [[!DNL TikTok] voor de registratiepagina voor bedrijven](https://www.tiktok.com/business/en-US/solutions/business-account) als u nog geen account hebt, kunt u zich registreren en een account maken.

U moet zijn aangemeld bij uw zakelijke account om te kunnen worden ingesteld [!DNL TikTok] Pixel die partneropstelling gebruikt. Volg de onderstaande stappen om dit te doen:

1. Ga naar de **[!UICONTROL Assets]** en selecteert u **[!UICONTROL Event]**.
2. Selecteer onder Webgebeurtenissen de optie **[!UICONTROL Manage]**.
3. Selecteer **[!UICONTROL Set Up Web Events]**.
4. Selecteren **[!UICONTROL Partner Setup]** als verbindingsmethode.

Zie de [Aan de slag met pixels](https://ads.tiktok.com/help/article/get-started-pixel) voor meer informatie over het instellen van de [!DNL TikTok] pixel.

U kunt een toegangstoken genereren zodra de pixel is gemaakt. Navigeer hiertoe naar de pixel en selecteer de **[!UICONTROL Settings]** tab. Selecteer onder Gebeurtenissen-API **[!UICONTROL Generate Access Token]**.

Zie de [[!DNL TikTok] gids Aan de slag](https://business-api.tiktok.com/portal/docs?id=1739584855420929) voor meer informatie over het instellen van de pixelcode en het toegangstoken.

## Installeer en configureer de [!DNL TikTok] API-extensie voor webgebeurtenissen {#install}

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** selecteert u de **[!UICONTROL TikTok Web Events API Extension]** en selecteer vervolgens **[!UICONTROL Install]**.

![De extensiecatalogus die de [!DNL TikTok] installatie van markering voor extensiekaart.](../../../images/extensions/server/tiktok/install-extension.png)

Voer in het volgende scherm de volgende configuratiewaarden in die u eerder hebt gegenereerd [!DNL TikTok] Advertentiebeheer:

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

Selecteer **[!UICONTROL Save]**.

![[!DNL TikTok] configuratiescherm voor de [!DNL TikTok] API-extensie voor webgebeurtenissen.](../../../images/extensions/server/tiktok/configure.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen door:sturen regels die bepalen wanneer en hoe uw gebeurtenissen zullen worden verzonden naar [!DNL TikTok].

Een nieuwe [regel](../../../ui/managing-resources/rules.md) in uw gebeurtenis die bezit door:sturen. Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL TikTok Web Events API Extension]**. Edge Network-gebeurtenissen verzenden naar [!DNL TikTok], stelt u de **[!UICONTROL Action Type]** tot **[!UICONTROL Send TikTok Web Events API Event].**

![De [!UICONTROL Send TikTok Web Events API Event] handelingstype dat wordt geselecteerd voor een [!DNL TikTok] regel in de UI van de Inzameling van Gegevens.](../../../images/extensions/server/tiktok/select-action.png)

Na de selectie worden extra besturingselementen weergegeven om de gebeurtenis verder te configureren, zoals hieronder wordt beschreven. Selecteer **[!UICONTROL Keep Changes]** om de regel op te slaan.

**[!UICONTROL Web Events and Parameters]**

Webgebeurtenissen en -parameters bevatten algemene informatie over de gebeurtenis. Standaardgebeurtenissen worden ondersteund in alle [!DNL TikTok] de integratiehulpmiddelen en kunnen voor rapportering worden gebruikt, optimaliserend voor omzettingen, en bouwend publiek.

| Invoer | Beschrijving |
| --- | --- |
| Gebeurtenisnaam | De naam van de gebeurtenis. Dit zijn handelingen met vooraf gedefinieerde namen die zijn gemaakt door [!DNL TikTok] en is een verplicht veld. Zie de [[!DNL TikTok] Marketing-API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) documentatie voor meer informatie over ondersteunde gebeurtenissen. |
| Gebeurtenistijd | Datum-tijd als tekenreeks in ISO 8601 of in jjjj-MM-dd&#39;T&#39;HH:mm:ss:SSSZ-indeling. Dit is een verplicht veld. |
| Gebeurtenis-id | De unieke id die door adverteerders wordt gegenereerd om elke gebeurtenis aan te geven. Dit is een optioneel veld en wordt gebruikt voor deduplicatie. |

{style="table-layout:auto"}

![De [!DNL Web Events and Parameters] sectie met voorbeeldgegevens die in de velden worden ingevoerd.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

De parameters van de gebruikerscontext bevatten klanteninformatie die wordt gebruikt om de gebeurtenissen van de Webbezoeker met te passen [!DNL TikTok] gebruikers. Door meerdere typen overeenkomende gegevens op te nemen, kunt u de nauwkeurigheid van doelmodellen en optimalisatiemodellen verhogen.

| Invoer | Beschrijving |
| --- | --- |
| IP-adres | Niet-gehakt openbaar IP adres van browser. Er wordt ondersteuning geboden voor IPv4- en IPv6-adressen. Zowel worden de volledige als de samengeperste vormen van IPv6 adressen erkend. |
| User Agent | De niet-gehashte gebruikersagent van het apparaat van de gebruiker. |
| Email | E-mailadres van de contactpersoon die aan de conversiegebeurtenis is gekoppeld. |
| Telefoon | Het telefoonnummer moet de E164-notatie [+][landcode] hebben[netnummer][local phone number] voordat u gaat hashen. |
| Cookie-id | Als u de SDK van Pixel gebruikt, wordt automatisch een unieke id opgeslagen in het dialoogvenster `_ttp` cookie, als cookies zijn ingeschakeld. De `_ttp` Deze waarde kan voor dit veld worden geëxtraheerd en gebruikt. |
| Externe id | Om het even welk uniek herkenningsteken zoals gebruiker IDs, externe koekjesidentiteitskaarts etc. en moet met SHA256 worden gehakt. |
| TikTok Click ID | De `ttclid` Deze wordt toegevoegd aan de URL van de bestemmingspagina telkens wanneer een advertentie wordt geselecteerd op [!DNL TikTok]. |
| Pagina-URL | De pagina-URL op het moment van de gebeurtenis. |
| URL paginaverwijzing | De URL van de paginaverwijzing. |

{style="table-layout:auto"}

![De [!DNL User Context Parameters] sectie met voorbeeldgegevens die in de velden worden ingevoerd.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

Gebruik de parameters van eigenschappen om extra gesteunde eigenschappen te vormen.

| Invoer | Beschrijving |
| --- | --- |
| Prijs | De kosten van één object. |
| Aantal | Het aantal items dat in de gebeurtenis wordt aangeschaft. Dit moet een positief getal zijn dat groter is dan 0. |
| Inhoudstype | Een waarde van of `product` of `product_group` moet worden toegewezen aan de content_type objecteigenschap, afhankelijk van hoe u uw gegevensinvoer zult vormen wanneer u opstelling uw productcatalogus. |
| Inhoud-id | Een unieke id van het item. |
| Inhoudscategorie | Categorie van de pagina/het product. |
| Inhoudsnaam | Naam van de pagina/het product. |
| Valuta | De valuta van de items die in de gebeurtenis worden gekocht. Dit wordt uitgedrukt in ISO-4217. |
| Waarde | De totale prijs van de bestelling. Deze waarde is gelijk aan de prijs * hoeveelheid. |
| Beschrijving | Een beschrijving van het item of de pagina. |
| Query | De tekenreeks met tekst die is gebruikt om een product op te zoeken. |
| Status | De status van een bestelling, onderdeel of service. Bijvoorbeeld &quot;verzonden&quot;. |

{style="table-layout:auto"}

![De [!DNL Properties Parameters] sectie met voorbeeldgegevens die in de velden worden ingevoerd.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Gebeurtenisdeduplicatie {#deduplication}

[!DNL TikTok] pixel zal opstelling voor deduplicatie moeten zijn als u zowel [!DNL TikTok] pixel SDK en de [!DNL TikTok] webgebeurtenissen: API-extensie voor het verzenden van dezelfde gebeurtenissen naar [!DNL TikTok].

Deduplicatie is niet vereist als verschillende gebeurtenistypen zonder overlapping van de client en server worden verzonden. Om ervoor te zorgen dat uw rapport niet negatief wordt beïnvloed, moet u ervoor zorgen dat om het even welke enige gebeurtenis die door wordt gedeeld [!DNL TikTok] pixel SDK en de [!DNL TikTok] API-extensie voor webgebeurtenissen is gededupliceerd.

Wanneer u gedeelde gebeurtenissen verzendt, moet u ervoor zorgen dat elke gebeurtenis een pixel-id, gebeurtenis-id en naam bevat. Gedupliceerde gebeurtenissen die binnen vijf minuten na elkaar aankomen, worden samengevoegd. Als het gegevensveld niet aanwezig was in de eerste gebeurtenis, wordt dit gecombineerd met de volgende gebeurtenis. Eventuele dubbele gebeurtenissen die binnen 48 uur zijn ontvangen, worden verwijderd.

Zie de [!DNL TikTok] documentatie over [Gebeurtenis dedupliceren](https://ads.tiktok.com/help/article/event-deduplication) voor meer informatie over dit proces.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gebeurtenisgegevens op de server kunt verzenden naar [!DNL TikTok] met de [!DNL TikTok] API-extensie voor webgebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden door:sturen in [!DNL Adobe Experience Platform], verwijst u naar de [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).
