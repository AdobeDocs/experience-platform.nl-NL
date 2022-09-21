---
title: Aan de slag met het doorsturen van gebeurtenissen
description: Volg deze stapsgewijze zelfstudie om te beginnen met het doorsturen van gebeurtenissen in Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# Aan de slag met het doorsturen van gebeurtenissen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Als u gebeurtenissen wilt doorsturen in Adobe Experience Platform, moeten gegevens naar Adobe Experience Platform Edge Network worden verzonden met een of meer van de volgende drie opties:

* [Adobe Experience Platform Web SDK](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Server-naar-server-API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>De SDK van het Web SDK van het Platform en van het Platform Mobiele SDK vereisen geen plaatsing door markeringen in Adobe Experience Platform. Het gebruik van labels voor de implementatie van deze SDK&#39;s wordt echter aanbevolen.

Nadat u gegevens naar het Edge-netwerk hebt verzonden, kunt u Adobe-oplossingen inschakelen om gegevens naar dat netwerk te verzenden. Om gegevens naar een niet-Adobe oplossing te verzenden, plaats die opstelling in gebeurtenis door:sturen.

## Vereisten

* Adobe Experience Platform Collection Enterprise (neem contact op met uw accountmanager voor prijzen)
* Gebeurtenis doorsturen in Adobe Experience Platform
* Adobe Experience Platform Web of Mobile SDK, die wordt gevormd om gegevens naar het Netwerk van Edge te verzenden
* Gegevens toewijzen aan XDM (Experience Data Model) (voor deze toewijzing kunt u codes gebruiken)

## Een XDM-schema maken

Maak uw schema in Adobe Experience Platform.

1. Een schema maken door **[!UICONTROL Schemas]**>**[!UICONTROL Create Schema]** en kiest u de **[!UICONTROL XDM ExperienceEvent]** optie.

1. Geef het schema een naam en een korte beschrijving.

1. U kunt de veldgroep &quot;ExperienceEvent-webdetails&quot; toevoegen door **[!UICONTROL Add]** naast **[!UICONTROL Field Groups]**.

   >[!NOTE]
   >
   >U kunt desgewenst meerdere veldgroepen toevoegen.

1. Sla het schema op en noteer de naam die u het hebt gegeven.

Voor meer informatie over schema&#39;s, zie [Help-systeem voor Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl).

## Een eigenschap voor het doorsturen van gebeurtenissen maken

In de **[!UICONTROL Tags]** werkruimte, een eigenschap van het type maken **[!UICONTROL Edge]**.

1. Selecteer **[!UICONTROL New Property]**.

1. Geef de eigenschap een naam.

1. Kies het platformtype &quot;Edge&quot;.

1. Selecteer **[!UICONTROL Save]**.

Nadat u de eigenschap hebt gemaakt, gaat u naar de **[!UICONTROL Environments]** voor de nieuwe eigenschap en noteer de milieu-id&#39;s. Als de in de gegevensstroom gebruikte Adobe Org verschilt van de Adobe Org die in gebeurtenis door:sturen wordt gebruikt, kunt u milieu-id van kopiëren **[!UICONTROL Environments]** en plakt deze bij het maken van een gegevensstroom. Anders kunt u de omgeving selecteren in een vervolgkeuzemenu.

## Een gegevensstroom maken

Om uw gegevensstroom in Adobe Experience Platform tot stand te brengen, gebruik identiteitskaart van het Milieu die wanneer u de gebeurtenis creeerde door:sturen bezit wordt geproduceerd.

1. Selecteren **[!UICONTROL Datastreams]** in de linkernavigatie.

1. Geef de configuratie een naam en geef een optionele beschrijving op.
De beschrijving helpt om configuraties in een lijst van verscheidene configuraties te identificeren.

1. Selecteer **[!UICONTROL Save]**.

## Gebeurtenis doorsturen inschakelen

Daarna, vorm het Netwerk van de Rand om gegevens naar gebeurtenis door:sturen, en naar andere producten van Adobe te verzenden.

1. In de **[!UICONTROL Datastreams]** selecteert u de eigenschap die u hebt gemaakt.

1. Selecteer de ontwikkelings-, productie- of staging-omgeving.

   Of, om gegevens naar een gebeurtenis te verzenden die milieu buiten Adobe org door:sturen, selecteer **[!UICONTROL Switch to Advanced Mode]** en plak in een id. ID wordt verstrekt wanneer u een gebeurtenis creeert die bezit door:sturen.

1. Schakel de benodigde gereedschappen in en configureer deze naar wens.

   * Adobe Analytics heeft een rapportsuite-id nodig.

   * Voor het doorsturen van gebeurtenissen in Adobe Experience Platform is een eigenschap-id en een omgeving-id vereist. Dit is de publicatiepad voor de eigenschap voor het doorsturen van gebeurtenissen.

Na het vormen, neem nota van milieu IDs voor het nieuwe bezit.

## Vorm de uitbreiding van SDK van het Web van het Platform om gegevens naar de eerder gemaakte gegevensstroom te verzenden

Maak uw eigenschap in het dialoogvenster **[!UICONTROL Tags]** werkruimte, navigeer vervolgens naar **[!UICONTROL Extensions]** en selecteer de uitbreiding van SDK van het Web van het Experience Platform van de catalogus om het te vormen en te installeren.

Zie de [Web SDK-uitbreidingsdocumentatie](../../extensions/web/sdk/overview.md) voor meer informatie over configuratieopties.

## Creeer een markeringsregel om gegevens naar het Web SDK van het Platform te verzenden

Nadat het bovenstaande op zijn plaats is, bouwt gegevensdefinities, regels, etc., die gebeurtenis het door:sturen en markeringen gebruiken, maar die slechts één enkel verzoek van de pagina vereisen.

Creeer een regel van de paginading gebruikend de uitbreiding van SDK van het Web van het Platform en het &quot;Send Event&quot;actietype:

1. Open de **[!UICONTROL Rules]** tab, dan selecteren **[!UICONTROL Create New Rule]**.

1. Geef de regel een naam.

1. Selecteer **[!UICONTROL Events Add]**.

1. Voeg een gebeurtenis toe door een extensie en een van de gebeurtenistypen te kiezen die beschikbaar zijn voor die extensie, en configureer vervolgens de instellingen voor de gebeurtenis. Selecteer bijvoorbeeld **[!UICONTROL Core - Window Loaded]**.

1. Voeg een actie toe gebruikend de uitbreiding van SDK van het Web van het Platform. Selecteren **[!UICONTROL Send Event]** van de **[!UICONTROL Action Type]** Selecteer de gewenste instantie (Alloy-instantie die eerder is geconfigureerd) en selecteer vervolgens een gegevenselement dat u wilt toevoegen aan het XDM-gegevensblok in de Alloy-hit.

1. Laat de overige instellingen als standaard voor dit voorbeeld staan en selecteer **[!UICONTROL Save]**.

In een ander voorbeeld kunt u een regel maken die de gegevenslaag naar Edge verzendt wanneer de gebruiker de cursor op een opgegeven knop plaatst.

## Samenvatting

Met het volgende op zijn plaats, kunt u gebeurtenis nu tot stand brengen die regels door:sturen om gegevens aan niet-Adobe bestemmingen door:sturen.

* Het Model van de Gegevens van de ervaring schema (Noteer de naam die u het gaf.)
* Een gebeurtenis die bezit door:sturen (houd spoor van bezitsidentiteitskaart en milieu IDs.)
* Een gegevensstroom (Noteer de milieu-id, niet te verwarren met de milieu-id door gebeurtenis te verzenden.)
* A tag, eigenschap
