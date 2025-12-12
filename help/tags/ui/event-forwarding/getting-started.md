---
title: Aan de slag met het doorsturen van gebeurtenissen
description: Volg deze stapsgewijze zelfstudie om te beginnen met het doorsturen van gebeurtenissen in Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# Aan de slag met het doorsturen van gebeurtenissen

>[!NOTE]
>
>Het door:sturen van gebeurtenissen is een betaalde eigenschap die als deel van het aanbod van de Verbindingen van Adobe Real-Time Customer Data Platform, Prime, of Ultimate inbegrepen is.

Als u gebeurtenissen wilt doorsturen in Adobe Experience Platform, moeten gegevens naar Adobe Experience Platform Edge Network worden verzonden met een of meer van de volgende drie opties:

* [Adobe Experience Platform Web SDK](../../extensions/client/web-sdk/overview.md)
* [ Adobe Experience Platform Mobile SDK ](https://sdkdocs.com)
* [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/)

>[!NOTE]
>Experience Platform Web SDK en Experience Platform Mobile SDK vereisen geen implementatie via tags in Adobe Experience Platform. Het gebruik van labels voor de implementatie van deze SDK&#39;s wordt echter aanbevolen.

Nadat u gegevens naar het Edge-netwerk hebt verzonden, kunt u Adobe-oplossingen in- en uitschakelen om gegevens naar dat netwerk te verzenden. Om gegevens naar een niet-Adobe oplossing te verzenden, plaats die opstelling in gebeurtenis door:sturen.

## Vereisten

* Adobe Real-Time CDP Connections, Prime of Ultimate (Neem contact op met uw Adobe-accountteam voor prijzen)
* Gebeurtenis doorsturen in Adobe Experience Platform
* Adobe Experience Platform Web SDK, Mobile SDK of Edge Network API geconfigureerd voor het verzenden van gegevens naar Edge Network
* Gegevens toewijzen aan XDM (Experience Data Model) (voor deze toewijzing kunt u codes gebruiken)

## Een XDM-schema maken

Maak uw schema in Adobe Experience Platform.

1. Creeer een schema door **[!UICONTROL Schemas]** te selecteren > **[!UICONTROL Create Schema]** en de **[!UICONTROL XDM ExperienceEvent]** optie te kiezen.

1. Geef het schema een naam en een korte beschrijving.

1. U kunt de veldgroep ‘ExperienceEvent-webdetails’ toevoegen door **[!UICONTROL Add]** naast **[!UICONTROL Field Groups]** te selecteren.

   >[!NOTE]
   >
   >U kunt desgewenst meerdere veldgroepen toevoegen.

1. Sla het schema op en noteer de naam die u het hebt gegeven.

Voor meer informatie over schema&#39;s, zie [ de ModelHulp van de Gegevens van de Ervaring (XDM) van het Systeem ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl).

## Een eigenschap voor het doorsturen van gebeurtenissen maken

Maak in de werkruimte **[!UICONTROL Tags]** een eigenschap van het type **[!UICONTROL Edge]** .

1. Selecteer **[!UICONTROL New Property]**.

1. Geef de eigenschap een naam.

1. Kies het platformtype &quot;Edge&quot;.

1. Selecteer **[!UICONTROL Save]**.

Nadat u de eigenschap hebt gemaakt, gaat u naar het tabblad **[!UICONTROL Environments]** voor de nieuwe eigenschap en maakt u
nota van milieu-IDs. Als de Adobe-organisatie die in de gegevensstroom wordt gebruikt afwijkt van de Adobe-organisatie die wordt gebruikt bij het doorsturen van gebeurtenissen, kunt u de milieu-id kopiëren vanaf het tabblad **[!UICONTROL Environments]** en deze plakken bij het maken van een gegevensstroom. Anders kunt u de omgeving selecteren in een vervolgkeuzemenu.

## Een gegevensstroom maken

Om uw gegevensstroom in Adobe Experience Platform tot stand te brengen, gebruik identiteitskaart van het Milieu die wanneer u de gebeurtenis creeerde door:sturen bezit wordt geproduceerd.

1. Selecteer **[!UICONTROL Datastreams]** in de linkernavigatie.

1. Geef de configuratie een naam en geef een optionele beschrijving op.
De beschrijving helpt om configuraties in een lijst van verscheidene configuraties te identificeren.

1. Selecteer **[!UICONTROL Save]**.

## Gebeurtenis doorsturen inschakelen {#enable-event-forwarding}

Configureer vervolgens Edge Network om gegevens naar gebeurtenissen door:sturen en naar andere Adobe-producten te verzenden.

1. Selecteer in de werkruimte **[!UICONTROL Datastreams]** de eigenschap die u hebt gemaakt.

1. Selecteer de ontwikkelings-, productie- of testomgeving.

   Of selecteer **[!UICONTROL Switch to Advanced Mode]** en plak in een id als u gegevens naar een door:sturen-gebeurtenisomgeving buiten de Adobe-org wilt verzenden. ID wordt verstrekt wanneer u een gebeurtenis creeert die bezit door:sturen.

1. Schakel de benodigde gereedschappen in en configureer deze naar wens.

   * Adobe Analytics heeft een rapportsuite-id nodig.

   * Voor het doorsturen van gebeurtenissen in Adobe Experience Platform is een eigenschap-id en een omgeving-id vereist. Dit is de publicatiepad voor de eigenschap voor het doorsturen van gebeurtenissen.

Na het vormen, neem nota van milieu IDs voor het nieuwe bezit.

## Configureer de Experience Platform Web SDK-extensie voor het verzenden van gegevens naar de eerder gemaakte gegevensstroom

Maak uw eigenschap in de **[!UICONTROL Tags]** -werkruimte en navigeer naar **[!UICONTROL Extensions]** en selecteer de Experience Platform Web SDK-extensie in de catalogus om deze te configureren en installeren.

Zie de [ de uitbreidingsdocumentatie van SDK van het Web ](../../extensions/client/web-sdk/overview.md) voor details op configuratieopties.

## Een labelregel maken om gegevens naar Experience Platform Web SDK te verzenden

Nadat het bovenstaande op zijn plaats is, bouwt gegevensdefinities, regels, etc., die gebeurtenis het door:sturen en markeringen gebruiken, maar die slechts één enkel verzoek van de pagina vereisen.

Maak een regel voor het laden van pagina&#39;s met de Experience Platform Web SDK-extensie en het actietype &quot;Send Event&quot;:

1. Open het tabblad **[!UICONTROL Rules]** en selecteer vervolgens **[!UICONTROL Create New Rule]** .

1. Geef de regel een naam.

1. Selecteer **[!UICONTROL Events Add]**.

1. Voeg een gebeurtenis toe door een extensie en een van de gebeurtenistypen te kiezen die beschikbaar zijn voor die extensie, en configureer vervolgens de instellingen voor de gebeurtenis. Selecteer bijvoorbeeld **[!UICONTROL Core - Window Loaded]** .

1. Voeg een handeling toe met de extensie Experience Platform Web SDK. Selecteer **[!UICONTROL Send Event]** in de lijst **[!UICONTROL Action Type]** de gewenste instantie (Alloy-instantie die eerder is geconfigureerd) en selecteer vervolgens een gegevenselement dat u wilt toevoegen aan het XDM-gegevensblok in de Alloy-hit.

1. Laat de rest van de instellingen als standaard voor dit voorbeeld staan en selecteer **[!UICONTROL Save]** .

In een ander voorbeeld kunt u een regel maken die de gegevenslaag naar Edge verzendt wanneer de gebruiker de cursor op een opgegeven knop plaatst.

## Samenvatting

Met het volgende op zijn plaats, kunt u gebeurtenis nu tot stand brengen die regels door:sturen om gegevens aan bestemmingen door:sturen niet-Adobe.

* Het Model van de Gegevens van de ervaring schema (Noteer de naam die u het gaf.)
* Een gebeurtenis die bezit door:sturen (houd spoor van bezitsidentiteitskaart en milieu IDs.)
* Een gegevensstroom (Noteer de milieu-id, niet te verwarren met de milieu-id door gebeurtenis te verzenden.)
* A tag, eigenschap
