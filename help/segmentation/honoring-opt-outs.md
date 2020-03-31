---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Optie-outs respecteren
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Naleving van &quot;opt-out&quot;-verzoeken in segmenten

Met het Experience Platform kunnen uw klanten weigeren-aanvragen betreffende het gebruik en de opslag van hun gegevens verzenden binnen het Real-time Klantprofiel. Deze &quot;opt-out&quot;-verzoeken maken deel uit van de California Consumer Privacy Act (CCPA), die de inwoners van Californië het recht geeft toegang te krijgen tot hun persoonsgegevens en deze te verwijderen en te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie).

Zodra een klant heeft gekozen-uit, is het belangrijk dat uw organisatie die opt-outs respecteert wanneer het produceren van publiek voor marketing activiteiten. In dit document worden belangrijke details beschreven met betrekking tot het naleven van de &quot;opt-out&quot;-verzoeken.

## Aan de slag

Voor het uitvoeren van de optie om te weigeren is een goed begrip vereist van de verschillende services van het Adobe Experience Platform die u wilt gebruiken. Lees de documentatie voor de volgende services voordat u gaat werken met opt-out-verzoeken:

- [Klantprofiel](../profile/home.md)in realtime: Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Adobe Experience Platform Segmentation Service](./home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [XDM (Experience Data Model)](../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
- [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Helpt organisaties om naleving van gegevensprivacyverordeningen te automatiseren die klantengegevens binnen Platform impliceren. Deze verordeningen omvatten:
   - California Consumer Privacy Act (CCPA): Rechten op privacy van gegevens voor inwoners van Californië, met inbegrip van het recht op toegang tot en verwijdering van persoonsgegevens en om te weten of persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie).
   - Algemene gegevensbeschermingsverordening (GDPR): Rechten op privacy van gegevens voor leden van de Europese Unie, waaronder het &quot;recht op toegang&quot; en het &quot;recht om te worden vergeten&quot;.

## Opt-out-mixen

Om uit CCPA te respecteren opt-out verzoeken, moet één van de schema&#39;s die een deel van het unieschema uitmaken de noodzakelijke gebieden van de Optie van Gegevens van de Ervaring van het Model (XDM) bevatten. Er zijn twee combinaties die kunnen worden gebruikt om opt-outvelden toe te voegen aan een schema. Elk van deze combinaties wordt nader beschreven in de volgende secties:

- [Profielprivacy](#profile-privacy): Wordt gebruikt om verschillende soorten opt-out vast te leggen (algemeen of verkoop/delen).
- [Profielvoorkeuren — Details](#profile-preferences-details): Wordt gebruikt voor het vastleggen van optieverzoeken voor specifieke XDM-kanalen.

Voor geleidelijke instructies op hoe te om een mengeling aan een schema toe te voegen, gelieve te verwijzen naar de &quot;Add a mixin&quot;sectie in de volgende XDM documentatie:
- [Zelfstudie](../xdm/api/getting-started.md)voor schema Registry API.: Een schema maken met de API voor schemaregistratie.
- [Zelfstudie](../xdm/tutorials/create-schema-ui.md)Schema-editor: Een schema maken met de gebruikersinterface van Platform.

Hier ziet u een voorbeeld van de mix van de optie Weigeren die in de gebruikersinterface aan een schema wordt toegevoegd:

![](images/opt-outs/opt-out-mixins-user-interface.png)

De structuur van elke mix en een beschrijving van de velden die deze bijdragen aan het schema worden in de volgende secties nader beschreven.

### Profielprivacy

Met het mixin Profile Privacy kunt u twee soorten CCPA-verzoeken om te weigeren van klanten vastleggen:

1. Algemene opt-out
2. Optie voor verkopen/delen

![](images/opt-outs/profile-privacy.png)

De mix van de Privacy van het Profiel bevat de volgende gebieden:

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

Om de volledige structuur van de mix van de Privacy van het Profiel te bekijken, gelieve te verwijzen naar de openbare bewaarplaats [van GitHub van](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) XDM of voorproef de mixin gebruikend Platform UI.

### Details van profielvoorkeuren

De mix Profielvoorkeuren > Details bevat verschillende velden die voorkeuren voor klantprofielen vertegenwoordigen (zoals e-mailindeling, voorkeurstaal en tijdzone). In een van de velden in deze mix, OptInOut (`optInOut`), kunnen de waarden voor de optie om te weigeren worden ingesteld voor afzonderlijke kanalen.

![](images/opt-outs/profile-preferences-details.png)

De mix Details van de Voorkeur van het Profiel bevat de volgende gebieden met betrekking tot opt-outs:

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

Als u de volledige structuur van de mix met profielvoorkeuren wilt bekijken, gaat u naar de openbare GitHub-opslagruimte [van](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) XDM of bekijkt u een voorvertoning van de mix met behulp van de Platform-interface.

## Afhandeling van opt-outs in segmentatie

Om ervoor te zorgen dat profielen die zijn gemarkeerd met de optievlaggen voor de CCPA-indeling, niet in segmenten worden opgenomen, moeten speciale velden worden toegevoegd aan bestaande segmenten of worden opgenomen tijdens het maken van segmenten.

In de volgende secties ziet u hoe u de juiste velden toevoegt voor de twee typen optievlaggen:
1. Algemene opt-out
2. Optie voor verkopen/delen

### Algemene opt-out

De segmentatie houdt automatisch rekening met alle profielen die de vlag &quot;Algemene Opt-Out&quot;bevatten, die betekent dat die profielen niet in publiek of de uitvoer door gebrek zullen worden omvat. Het is echter aan te raden de juiste velden toe te voegen om ervoor te zorgen dat opted-out-profielen niet worden opgenomen in publiek- en marketingactiviteiten.

Dit kan worden gedaan gebruikend het gebruikersinterface van de Bouwer van het Segment door de **Gevoelige** attributen van de Privacy toe te voegen. In dit geval wordt het segment zo ingesteld dat het alleen diegenen omvat die hebben gekozen (wat betekent dat ze geen algemene &quot;opt-out&quot;-vlag hebben op hun profiel. Dit wordt gedaan door te verklaren dat het &quot;Opt-Out Type&quot;&quot;Algemene Opt-out&quot;en de &quot;Opt-uit Waarde&quot;&quot;Opt-in&quot;evenaart.

![](images/opt-outs/segment-general-opt-out.png)

### Optie voor verkopen/delen

Als een gebruiker een verkoop/het delen opt-out vlag op hun profiel heeft wordt geplaatst, zou dit profiel niet meer voor om het even welke segmentverwezenlijking of marketing activiteiten moeten worden gebruikt. Om ervoor te zorgen dat deze markering wordt toegepast, moet het &quot;Uitschakelen Type&quot; gelijk zijn aan &quot;Uitschakelen van verkoop&quot; en moet de &quot;Uitschakelen waarde&quot; gelijk zijn aan &quot;Opt-In&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Volgende stappen

Voor meer informatie over segmentatie, zoals het werken met segmentdefinities en publiek via de API en gebruikersinterface, gelieve te beginnen door het [segmentatieoverzicht](./home.md)te lezen.

Raadpleeg de documentatie [bij de](../privacy-service/home.md)privacyservice voor meer informatie over de privacy van gegevens binnen het platform, waaronder de manier waarop de privacyservice de automatische naleving van wettelijke en organisatorische privacyregels vergemakkelijkt.
