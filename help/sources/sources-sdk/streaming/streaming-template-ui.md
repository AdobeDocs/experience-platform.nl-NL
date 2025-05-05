---
title: Zelfservicesjabloon voor documentatie voor streaming SDK UI
description: Leer hoe u streaminggegevens van een bron naar Adobe Experience Platform kunt overbrengen via de gebruikersinterface.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Creeer een bronverbinding en dataflow aan stroom *JUURSOURCE* gegevens gebruikend UI

*aangezien u door dit malplaatje gaat, vervang of schrap alle paragrafen in cursief (beginnend met dit).*

*Begin door de meta-gegevens (titel en beschrijving) bij te werken bij de bovenkant van de pagina. Negeer alle exemplaren van UICONTROL op deze pagina. Dit is een label waarmee de pagina in de verschillende talen die wij ondersteunen correct wordt vertaald in onze computervertaalprocessen. Wij zullen markeringen aan uw documentatie toevoegen nadat u het voorlegt.*

Dit leerprogramma verstrekt stappen voor het creëren van a ** bronschakelaar van de JONGE bron gebruikend het gebruikersinterface van Experience Platform.

## Overzicht

*verstrek een kort overzicht van uw bedrijf, met inbegrip van de waarde het aan klanten verstrekt. Neem een koppeling op naar de startpagina van de productdocumentatie voor meer informatie.*

>[!IMPORTANT]
>
>Deze bronschakelaar en documentatiepagina worden gecreeerd en door het ** team van de JONGE &lbrace;gehandhaafd. Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct bij *verbinding of e-mailadres van het Tussenvoegsel te contacteren waar u voor updates* kunt worden bereikt.

## Vereisten

*voegt informatie in deze sectie over om het even wat toe dat de klanten zich van bewust moeten zijn alvorens aan opstelling de bron in het gebruikersinterface van Adobe Experience Platform te beginnen. Dit kan over zijn:*

* *moet aan een lijst van gewenste personen worden toegevoegd*
* *vereisten voor e-mailhashing*
* *om het even welke rekeningsspecificaties op uw kant*
* *hoe te om de authentificatiegeloofsbrieven te verkrijgen om met uw platform te verbinden*

### Vereiste referenties verzamelen

Om *UURSOURCE* aan Experience Platform te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| *referentie één* | *Gelieve te voegen een korte beschrijving aan de authentificatiereferentie van uw bron hier* toe | *gelieve een voorbeeld van de authentificatiereferentie van uw bron hier toe te voegen* |
| *referentie twee* | *Gelieve te voegen een korte beschrijving aan de authentificatiereferentie van uw bron hier* toe | *gelieve een voorbeeld van de authentificatiereferentie van uw bron hier toe te voegen* |
| *referentie drie* | *Gelieve te voegen een korte beschrijving aan de authentificatiereferentie van uw bron hier* toe | *gelieve een voorbeeld van de authentificatiereferentie van uw bron hier toe te voegen* |

Voor meer informatie over deze geloofsbrieven, zie *JONGE* authentificatiedocumentatie. *gelieve verbinding aan de authentificatiedocumentatie van uw platform toe te voegen hier*.

### Integreer *JUURSOURCE* met uw webhaak

*het stromen SDK vereist uw bron om webhaken te kunnen steunen om met Experience Platform te communiceren. In deze sectie, moet u de stappen verstrekken die uw gebruikers zullen moeten volgen om Uw BRON met een webhaak te integreren.*

## Verbind uw ** rekening van de JUURBRON

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **Streaming** categorie, selecteer *JUURSOURCE*, en selecteer dan **[!UICONTROL Add data]**.

>[!TIP]
>
>De onderstaande schermafbeeldingen zijn voorbeelden. Vervang de afbeeldingen bij het maken van de documentatie door schermafbeeldingen van de werkelijke bron. U kunt hetzelfde patroon en dezelfde kleur en dezelfde bestandsnamen gebruiken. Zorg ervoor dat uw schermafbeelding het volledige Experience Platform UI-scherm vastlegt. Voor informatie over hoe te om uw screenshots te uploaden, zie de gids bij [ het voorleggen van uw documentatie voor overzicht ](../documentation/github.md).

![ de Experience Platform broncatalogus ](../assets/streaming/catalog.png)

## Gegevens selecteren

De stap **[!UICONTROL Select data]** wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar Experience Platform verzendt.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteer **[!UICONTROL Upload files]** om een JSON-bestand van uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden naar het deelvenster [!UICONTROL Drag and drop files] slepen.

![ voegt gegevensstap van het bronwerkschema toe.](../assets/streaming/add-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het hulpprogramma [!UICONTROL Search field] ook gebruiken om toegang te krijgen tot specifieke items binnen uw schema.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de voorproefstap van het bronwerkschema.](../assets/streaming/preview.png)

## Gegevens

De **Dataflow detailstap** verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw dataflow te vestigen, evenals een kans om een naam en een beschrijving voor uw dataflow te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ dataflow-detail stap van het bronwerkschema.](../assets/streaming/dataflow-detail.png)

## Toewijzing

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [ gids UI van de Prep van Gegevens ](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![ de afbeeldingsstap van het bronwerkschema.](../assets/streaming/mapping.png)

## Controleren

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, klikt u op **[!UICONTROL Finish]** en laat u enige tijd over tot de gegevensstroom.

![ de overzichtsstap van het bronwerkschema.](../assets/streaming/review.png)

## Uw URL voor het streamingeindpunt ophalen

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt wordt gebruikt om een abonnement te nemen op uw webhaak, zodat uw streamingbron kan communiceren met Experience Platform.

Als u het streamingeindpunt wilt ophalen, gaat u naar de [!UICONTROL Dataflow activity] -pagina van de gegevensstroom die u net hebt gemaakt en kopieert u het eindpunt van de onderkant van het deelvenster [!UICONTROL Properties] .

![ het stromen eindpunt in dataflow activiteit.](../assets/testing/endpoint-test.png)

## Volgende stappen

*de Werkschema&#39;s voor de resterende stappen van het creëren van een dataflow worden gemoduleerd. Als er om het even welke specifieke vraag-outs zijn u betreffende uw bron wilt maken, gelieve de extra middelensectie hieronder te zien.*

Door dit leerprogramma te volgen, hebt u een verbinding aan uw ** rekening van UUR &lbrace;gevestigd. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Experience Platform ](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html) te brengen.

## Aanvullende bronnen

*dit is een facultatieve sectie waar u verdere verbindingen aan uw productdocumentatie of om het even welke andere stappen, screenshots, nuances kunt verstrekken u belangrijk voor de klant om vindt succesvol te zijn. U kunt deze sectie gebruiken om informatie over of uiteinden op het volledige werkschema van uw bron toe te voegen, vooral als er bijzondere &quot;gotchas&quot;zijn die een eindgebruiker zou kunnen ontmoeten.*
