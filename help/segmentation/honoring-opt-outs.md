---
keywords: Experience Platform;home;popular topics;opt-out;Segmentation;Segmentation service;segmentation service;honor opt-outs;opt-outs;opt out;opt outs;
solution: Experience Platform
title: Optie-outs respecteren
topic: overview
description: 'Met Experience Platform kunnen uw klanten weigeren-aanvragen betreffende het gebruik en de opslag van hun gegevens verzenden binnen het realtime profiel van de klant]. Deze "opt-out"-verzoeken maken deel uit van de California Consumer Privacy Act (CCPA), die de inwoners van Californië het recht geeft toegang te krijgen tot hun persoonsgegevens en deze te verwijderen en te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie). '
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---


# Naleving van &quot;opt-out&quot;-verzoeken in segmenten

[!DNL Experience Platform] kunnen uw klanten aanvragen om te weigeren verzenden met betrekking tot het gebruik en de opslag van hun gegevens binnen [!DNL Real-time Customer Profile]. Deze &quot;opt-out&quot;-verzoeken maken deel uit van de [!DNL California Consumer Privacy Act] (CCPA), die de inwoners van Californië het recht geven hun persoonsgegevens te raadplegen en te verwijderen en te weten te komen of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie).

Zodra een klant heeft gekozen-uit, is het belangrijk dat uw organisatie die opt-outs respecteert wanneer het produceren van publiek voor marketing activiteiten. In dit document worden belangrijke details beschreven met betrekking tot het naleven van de &quot;opt-out&quot;-verzoeken.

## Aan de slag

Voor het naleven van de &quot;opt-out&quot;-verzoeken moet inzicht worden verkregen in de verschillende betrokken [!DNL Adobe Experience Platform] diensten. Lees de documentatie voor de volgende services voordat u gaat werken met opt-out-verzoeken:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Staat u toe om publiekssegmenten van [!DNL Real-time Customer Profile] gegevens te bouwen.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Helpt organisaties om naleving van de regels van de gegevensprivacy te automatiseren die klantengegevens binnen impliceren [!DNL Platform].

## Opt-out-mixen

Om de optieverzoeken CCPA te respecteren moet een van de schema&#39;s die deel uitmaken van het unieschema de noodzakelijke (XDM) opt-out gebieden bevatten. [!DNL Experience Data Model] Er zijn twee combinaties die kunnen worden gebruikt om opt-outvelden toe te voegen aan een schema. Elk van deze combinaties wordt nader beschreven in de volgende secties:

- [Profielprivacy](#profile-privacy): Wordt gebruikt om verschillende soorten opt-out vast te leggen (algemeen of verkoop/delen).
- [Profielvoorkeuren — Details](#profile-preferences-details): Wordt gebruikt voor het vastleggen van optieverzoeken voor specifieke XDM-kanalen.

Voor geleidelijke instructies op hoe te om een mengeling aan een schema toe te voegen, gelieve te verwijzen naar de &quot;Add a mixin&quot;sectie in de volgende XDM documentatie:
- [Zelfstudie](../xdm/api/getting-started.md)voor schema Registry API.: Een schema maken met de API voor schemaregistratie.
- [Zelfstudie](../xdm/tutorials/create-schema-ui.md)Schema-editor: Een schema maken met behulp van de gebruikersinterface van het Platform.

Hier ziet u een voorbeeld van de mix van de optie Weigeren die in de gebruikersinterface aan een schema wordt toegevoegd:

![](images/opt-outs/opt-out-mixins-user-interface.png)

De structuur van elke mix en een beschrijving van de velden die deze bijdragen aan het schema worden in de volgende secties nader beschreven.

### [!DNL Profile Privacy] {#profile-privacy}

Het [!DNL Profile Privacy] mengen staat u toe om twee soorten opt-outverzoeken CCPA van klanten te vangen:

1. Algemene opt-out
2. Optie voor verkopen/delen

![](images/opt-outs/profile-privacy.png)

De [!DNL Profile Privacy] mix bevat de volgende velden:

- Privacy opt-Outs (`privacyOptOuts`): Een array met een lijst met opt-out-objecten.
- Type optie (`optOutType`): Het type opt-out. Dit veld is een opsomming met twee mogelijke waarden:
   - Algemene optie-uit (`general_opt_out`)
   - Afmelden bij verkoop delen (`sales_sharing_opt_out`)
- Uitgaande waarde (`optOutValue`): De actieve status van de opt-out, ook wel de waarde van het opt-out-signaal genoemd, op basis van het opgegeven opt-out-type. Dit veld is een opsomming met vier mogelijke waarden:
   - Niet verstrekt (`not_provided`): Er is geen aanvraag voor een opt-out ingediend.
   - Verificatie in behandeling (`pending`): Het verzoek om te weigeren is in afwachting van verificatie.
   - Uitschakelen (`out`): De klant heeft zich afgemeld.
   - Inschakelen (`in`): De klant heeft zich aangemeld.
- Tijdstempel uitschakelen (`timestamp`): Tijdstempel van het ontvangen opt-out-signaal.

Om de volledige structuur van de [!DNL Profile Privacy] mix te bekijken, gelieve te verwijzen naar de [XDM openbare bewaarplaats](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) GitHub of voorproef de mixin gebruikend het Platform UI.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

De [!DNL Profile Preferences Details] mix bevat verschillende velden die voorkeuren voor klantprofielen vertegenwoordigen (zoals e-mailindeling, voorkeurstaal en tijdzone). In een van de velden in deze mix, OptInOut (`optInOut`), kunnen de waarden voor de optie om te weigeren worden ingesteld voor afzonderlijke kanalen.

![](images/opt-outs/profile-preferences-details.png)

De [!DNL Profile Preferences Details] mix bevat de volgende velden met betrekking tot opt-outs:

- OptInOut (`optInOut`): Een object waarbij elke sleutel een geldige en bekende URI voor een communicatiekanaal vertegenwoordigt en de actieve status van de opt-out voor elk kanaal. Elk kanaal kan een van vier mogelijke waarden hebben:
   - Niet verstrekt (`not_provided`): Er is geen verzoek om te weigeren ingediend voor dit kanaal.
   - Verificatie in behandeling (`pending`): De aanvraag om te weigeren voor dit kanaal is in afwachting van verificatie.
   - Uitschakelen (`out`): De klant heeft dit kanaal uitgeschakeld.
   - Inschakelen (`in`): De klant heeft voor dit kanaal gekozen.
- Global Opt-out (`globalOptout`): Een Booleaanse waarde die, indien ingesteld op true, een algemene uitschakeloverschrijving voor het profiel instelt. De standaardwaarde voor dit veld is false.

In het onderstaande voorbeeld ziet u hoe het OptInOut-object meerdere optiesignalen voor verschillende communicatiekanalen kan vastleggen:

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

Om de volledige structuur van de de Details van de Voorkeur van het Profiel te bekijken mengen, te bezoeken gelieve de openbare bewaarplaats [van GitHub van](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) XDM of voorproef de mixin gebruikend [!DNL Platform] UI.

## Afhandeling van opt-outs in segmentatie

Om ervoor te zorgen dat profielen die zijn gemarkeerd met de optievlaggen voor de CCPA-indeling, niet in segmenten worden opgenomen, moeten speciale velden worden toegevoegd aan bestaande segmenten of worden opgenomen tijdens het maken van segmenten.

In de volgende secties ziet u hoe u de juiste velden toevoegt voor de twee typen optievlaggen:
1. Algemene opt-out
2. Optie voor verkopen/delen

### Algemene opt-out

[!DNL Segmentation] Hiermee worden automatisch alle profielen geaccepteerd die de markering &quot;[!UICONTROL Algemeen uitschakelen]&quot; bevatten. Dit betekent dat deze profielen niet standaard worden opgenomen in het publiek of de exportbewerking. Het is echter aan te raden de juiste velden toe te voegen om ervoor te zorgen dat opted-out-profielen niet worden opgenomen in publiek- en marketingactiviteiten.

Dit kan worden gedaan gebruikend het gebruikersinterface door de **[!UICONTROL attributen van de Privacy toe te voegen Opt-Outs]** . In dit geval wordt het segment zo ingesteld dat het alleen diegenen omvat die ervoor hebben gekozen (wat betekent dat ze geen algemene &quot;opt-out&quot;-vlag hebben op hun profiel. Dit wordt gedaan door te verklaren dat het &quot;Type[!UICONTROL van]Opt-uit&quot;&quot;[!UICONTROL Algemene Opt-uit]&quot;en de &quot;[!UICONTROL Opt-uit Waarde]&quot;gelijke &quot;[!UICONTROL Opt-in]&quot; is.

![](images/opt-outs/segment-general-opt-out.png)

### Optie voor verkopen/delen

Als een gebruiker een verkoop/het delen opt-out vlag op hun profiel heeft wordt geplaatst, zou dit profiel niet meer voor om het even welke segmentverwezenlijking of marketing activiteiten moeten worden gebruikt. Om ervoor te zorgen dat deze markering wordt toegepast, moet het &quot;[!UICONTROL Opt-Out Type]&quot; gelijk zijn aan &quot;[!UICONTROL Sales Sharing Opt-Out]&quot; en moet de &quot;[!UICONTROL Opt-Out Waarde]&quot; gelijk zijn aan &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Volgende stappen

Voor meer informatie over segmentatie, zoals het werken met segmentdefinities en publiek via de API en gebruikersinterface, gelieve te beginnen door het [segmentatieoverzicht](./home.md)te lezen.

Raadpleeg de documentatie op voor meer informatie over de privacy van gegevens binnen [!DNL Platform]en over hoe u de automatische naleving van wettelijke en organisatorische privacyregels [!DNL Privacy Service] kunt vergemakkelijken. [[!DNL Privacy Service]](../privacy-service/home.md).
