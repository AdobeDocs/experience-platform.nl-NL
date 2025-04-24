---
title: Adobe TikTok Web events API-extensie Integratie
description: Met deze Adobe Experience Platform-API voor webgebeurtenissen kunt u interacties van websites rechtstreeks delen met TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 1%

---

# [!DNL TikTok] API-extensieoverzicht van webgebeurtenissen

De [!DNL TikTok] gebeurtenissen API is een veilige [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/) interface die u toestaat om informatie met [!DNL TikTok] direct over gebruikersacties op uw websites te delen. U kunt de regels voor het doorsturen van gebeurtenissen gebruiken om gegevens van [!DNL Adobe Experience Platform Edge Network] naar [!DNL TikTok] te verzenden met de API-extensie [!DNL TikTok] Webgebeurtenissen.

## [!DNL TikTok] voorwaarden {#prerequisites}

Als u de API voor webgebeurtenissen van [!DNL TikTok] wilt configureren voor het gebruik van de API voor [!DNL TikTok] events, moet u een [!DNL TikTok] pixelcode en toegangstoken genereren.

U moet een geldige [!DNL TikTok] voor een zakelijke account hebben om een [!DNL TikTok] pixel te kunnen maken met behulp van de partnerinstellingen. Ga naar [[!DNL TikTok]  voor bedrijfs registratiepagina ](https://www.tiktok.com/business/en-US/solutions/business-account) om een rekening te registreren en tot stand te brengen als u niet reeds hebt.

U moet in uw bedrijfsrekening worden geregistreerd aan opstelling [!DNL TikTok] Pixel gebruikend partneropstelling. Hiervoor voert u de volgende stappen uit:

1. Navigeer naar de tab **[!UICONTROL Assets]** en selecteer **[!UICONTROL Event]** .
2. Selecteer onder Webgebeurtenissen de optie **[!UICONTROL Manage]** .
3. Selecteer **[!UICONTROL Set Up Web Events]**.
4. Selecteer **[!UICONTROL Partner Setup]** als verbindingsmethode.

Zie [ Begonnen met Pixel ](https://ads.tiktok.com/help/article/get-started-pixel) gids voor meer informatie over hoe te opstelling het [!DNL TikTok] pixel.

U kunt een toegangstoken genereren zodra de pixel is gemaakt. Navigeer hiertoe naar de pixel en selecteer de tab **[!UICONTROL Settings]** . Selecteer onder Gebeurtenissen-API **[!UICONTROL Generate Access Token]** .

Zie [[!DNL TikTok]  begonnen gids ](https://business-api.tiktok.com/portal/docs?id=1739584855420929) voor meer informatie over hoe te opstelling de pixelcode en toegangstoken.

## De API-extensie voor [!DNL TikTok] webgebeurtenissen installeren en configureren {#install}

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie als u de extensie wilt installeren. Selecteer op het tabblad **[!UICONTROL Catalog]** de **[!UICONTROL TikTok Web Events API Extension]** en selecteer vervolgens **[!UICONTROL Install]** .

![ de uitbreidingscatalogus die [!DNL TikTok] uitbreidingskaart tonen die installeert benadrukt.](../../../images/extensions/server/tiktok/install-extension.png)

Voer in het volgende scherm de volgende configuratiewaarden in die u eerder hebt gegenereerd via [!DNL TikTok] Advertentiebeheer:

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

Selecteer **[!UICONTROL Save]** als u klaar bent.

![[!DNL TikTok] configuratiescherm voor de [!DNL TikTok] API-extensie voor webgebeurtenissen. ](../../../images/extensions/server/tiktok/configure.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen die regels bepaalt wanneer en hoe uw gebeurtenissen naar [!DNL TikTok] zullen worden verzonden.

Creeer een nieuwe [ regel ](../../../ui/managing-resources/rules.md) in uw gebeurtenis door:sturen bezit. Voeg onder **[!UICONTROL Actions]** een nieuwe handeling toe en stel de extensie in op **[!UICONTROL TikTok Web Events API Extension]** . Als u Edge Network-gebeurtenissen naar [!DNL TikTok] wilt verzenden, stelt u de eigenschap **[!UICONTROL Action Type]** to **[!UICONTROL Send TikTok Web Events API Event]in.**

![ het [!UICONTROL Send TikTok Web Events API Event] actietype dat voor een [!DNL TikTok] regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/tiktok/select-action.png)

Na de selectie worden extra besturingselementen weergegeven om de gebeurtenis verder te configureren, zoals hieronder wordt beschreven. Nadat de regel is voltooid, selecteert u **[!UICONTROL Keep Changes]** om deze op te slaan.

**[!UICONTROL Web Events and Parameters]**

Webgebeurtenissen en -parameters bevatten algemene informatie over de gebeurtenis. Standaardgebeurtenissen worden ondersteund door alle [!DNL TikTok] -integratieprogramma&#39;s en kunnen worden gebruikt voor rapportage, optimalisatie voor conversies en het opbouwen van doelgroepen.

| Invoer | Beschrijving |
| --- | --- |
| Gebeurtenisnaam | De naam van de gebeurtenis. Dit zijn handelingen met vooraf gedefinieerde namen die door [!DNL TikTok] zijn gemaakt en die een verplicht veld zijn. Verwijs naar de [[!DNL TikTok]  Marketing API ](https://business-api.tiktok.com/portal/docs?id=1741601162187777) documentatie voor meer informatie over gesteunde gebeurtenissen. |
| Gebeurtenistijd | Datum en tijd als tekenreeks in ISO 8601 of in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` indeling. Dit is een verplicht veld. |
| Gebeurtenis-id | De unieke id die door adverteerders wordt gegenereerd om elke gebeurtenis aan te geven. Dit is een optioneel veld en wordt gebruikt voor deduplicatie. |

{style="table-layout:auto"}

![ de [!DNL Web Events and Parameters] sectie die voorbeeldgegevensinput in de gebieden toont.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

De parameters van de gebruikerscontext bevatten klantinformatie die wordt gebruikt om de gebeurtenissen van de Webbezoeker met [!DNL TikTok] gebruikers aan te passen. Door meerdere typen overeenkomende gegevens op te nemen, kunt u de nauwkeurigheid van doelmodellen en optimalisatiemodellen verhogen.

| Invoer | Beschrijving |
| --- | --- |
| IP-adres | Niet-gehakt openbaar IP adres van browser. Er wordt ondersteuning geboden voor IPv4- en IPv6-adressen. Zowel worden de volledige als de samengeperste vormen van IPv6 adressen erkend. |
| Gebruikersagent | De niet-gehashte gebruikersagent van het apparaat van de gebruiker. |
| Email | E-mailadres van de contactpersoon die aan de conversiegebeurtenis is gekoppeld. |
| Telefoon | Het telefoonaantal moet in formaat E164 zijn [+] [landcode] [ gebiedscode ][local phone number] alvorens het hakken. |
| Cookie-id | Als u Pixel gebruikt, slaat SDK automatisch een unieke id op in het cookie `_ttp` als cookies zijn ingeschakeld. De waarde `_ttp` kan voor dit veld worden geëxtraheerd en gebruikt. |
| Externe id | Om het even welk uniek herkenningsteken zoals gebruiker IDs, externe koekjesidentiteitskaarts etc. en moet met SHA256 worden gehakt. |
| TikTok Click ID | De `ttclid` die aan de URL van de bestemmingspagina wordt toegevoegd telkens als een advertentie op [!DNL TikTok] wordt geselecteerd. |
| Pagina-URL | De pagina-URL op het moment van de gebeurtenis. |
| URL paginaverwijzing | De URL van de paginaverwijzing. |

{style="table-layout:auto"}

![ de [!DNL User Context Parameters] sectie die voorbeeldgegevensinput in de gebieden toont.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

Gebruik de parameters van eigenschappen om extra gesteunde eigenschappen te vormen.

| Invoer | Beschrijving |
| --- | --- |
| Prijs | De kosten van één object. |
| Aantal | Het aantal items dat in de gebeurtenis wordt aangeschaft. Dit moet een positief getal zijn dat groter is dan 0. |
| Inhoudstype | De waarde `product` of `product_group` moet worden toegewezen aan de eigenschap content_type object, afhankelijk van de manier waarop u de gegevensinvoer configureert wanneer u de productcatalogus instelt. |
| Inhoud-id | Een unieke id van het item. |
| Inhoudscategorie | Categorie van de pagina/het product. |
| Inhoudsnaam | Naam van de pagina/het product. |
| Valuta | De valuta van de items die in de gebeurtenis worden gekocht. Dit wordt uitgedrukt in ISO-4217. |
| Waarde | De totale prijs van de bestelling. Deze waarde is gelijk aan de prijs * hoeveelheid. |
| Beschrijving | Een beschrijving van het item of de pagina. |
| Query | De tekenreeks met tekst die is gebruikt om een product op te zoeken. |
| Status | De status van een bestelling, onderdeel of service. Bijvoorbeeld &quot;verzonden&quot;. |

{style="table-layout:auto"}

![ de [!DNL Properties Parameters] sectie die voorbeeldgegevensinput in de gebieden toont.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Gebeurtenisdeduplicatie {#deduplication}

[!DNL TikTok] -pixel moet worden ingesteld voor deduplicatie als u zowel de [!DNL TikTok] pixel SDK- als de [!DNL TikTok] web events API-extensie gebruikt om dezelfde gebeurtenissen naar [!DNL TikTok] te verzenden.

Deduplicatie is niet vereist als verschillende gebeurtenistypen zonder overlapping van de client en server worden verzonden. Om ervoor te zorgen dat uw rapportage geen negatieve gevolgen heeft, moet u ervoor zorgen dat elke afzonderlijke gebeurtenis die wordt gedeeld door de extensie [!DNL TikTok] pixel SDK en de [!DNL TikTok] web events API, wordt gededupliceerd.

Wanneer u gedeelde gebeurtenissen verzendt, moet u ervoor zorgen dat elke gebeurtenis een pixel-id, gebeurtenis-id en naam bevat. Gedupliceerde gebeurtenissen die binnen vijf minuten na elkaar aankomen, worden samengevoegd. Als het gegevensveld niet aanwezig was in de eerste gebeurtenis, wordt dit gecombineerd met de volgende gebeurtenis. Eventuele dubbele gebeurtenissen die binnen 48 uur zijn ontvangen, worden verwijderd.

Zie de [!DNL TikTok] documentatie over [ de Deduplicatie van de Gebeurtenis ](https://ads.tiktok.com/help/article/event-deduplication) voor meer details over dit proces.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gebeurtenisgegevens aan de serverzijde naar [!DNL TikTok] kunt verzenden met de API-extensie voor [!DNL TikTok] webgebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden in [!DNL Adobe Experience Platform] door:sturen, verwijs naar de [ gebeurtenis die overzicht ](../../../ui/event-forwarding/overview.md) door:sturen.
