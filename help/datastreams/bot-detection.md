---
title: Beide detectie configureren voor gegevensstromen
description: Leer hoe te om botopsporing voor gegevensstromen te vormen, om menselijk en onmenselijk verkeer te onderscheiden.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: 0787876d80e308c1687304ace7538a51d9a754ff
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 0%

---

# Beide detectie configureren voor gegevensstromen

Het onmenselijke verkeer van geautomatiseerde programma&#39;s, Webschrapers, spinnen, en scripted scanners kan het moeilijk maken om gebeurtenissen van menselijke bezoekers te identificeren. Dit type van verkeer kan belangrijke bedrijfsmetriek negatief beïnvloeden, die tot onjuist verkeer leiden meldend.

Beide opsporing staat u toe om gebeurtenissen te identificeren die door [ SDK van het Web ](/help/collection/js/js-overview.md), [ Mobiele SDK ](https://developer.adobe.com/client-sdks/home/) en [[!DNL Edge Network API] ](https://developer.adobe.com/data-collection-apis/docs/api/) worden geproduceerd als door bekende spinnen en bots.

>[!NOTE]
>
>Gebruik [!DNL Bot Detection Service] om niet-menselijk (bot) verkeer van uw gegevens te identificeren en te filtreren. Dit vermindert ruis in de verzamelde datasets en helpt ervoor te zorgen dat uw analyses en rapportering echte gebruikersinteractie weerspiegelen.

Door beide opsporing voor uw gegevensstromen te vormen, kunt u specifieke IP adressen, IP waaiers, en verzoekkopballen identificeren om als beide gebeurtenissen te classificeren. Zo kunt u de gebruikersactiviteit op uw site of mobiele toepassing nauwkeuriger meten.

Wanneer een verzoek aan de Edge Network om het even welke beide ontdekkingsregels aanpast, wordt het schema XDM bijgewerkt met een beide score (altijd geplaatst aan 1), zoals hieronder getoond:

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Deze beide het scoren helpt de oplossingen die het verzoek ontvangen beide verkeer correct identificeren.

>[!IMPORTANT]
>
>Boot detection slaat beide aanvragen niet neer. Het werkt slechts het schema XDM met beide het scoren bij, en door:sturen de gebeurtenis aan de [ datastream dienst ](configure.md) die u vormde.
>
>Adobe-oplossingen kunnen beide scoren op verschillende manieren verwerken. Bijvoorbeeld, gebruikt Adobe Analytics zijn eigen [ bot filtrerende dienst ](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) en gebruikt niet de score die door Edge Network wordt geplaatst. De twee diensten gebruiken de zelfde [ IAB beide lijst ](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), zodat is het beide het scoren identiek.

## Technische overwegingen {#technical-considerations}

Before enabling bot detection on your datastreams, here are a few key points to keep in mind to ensure accurate results and a smooth implementation:

* Bot detection applies only to unauthenticated requests sent to `edge.adobedc.net`.
* Authenticated requests sent to `server.adobedc.net` are not evaluated for bot traffic, as authenticated traffic is considered trustworthy.
* Bot detection rules can take up to 15 minutes to propagate across the Edge Network after being created.

## Vereisten {#prerequisites}

For bot detection to work on your datastream, you must add the **[!UICONTROL [Bot Detection Information]](../xdm/field-groups/event/bot-detection-information.md)** field group to your schema. See the [XDM schema](../xdm/ui/resources/schemas.md#add-field-groups) documentation to learn how to add field groups to a schema.

## Beide detectie configureren voor gegevensstromen {#configure}

You can configure bot detection after creating a datastream configuration. See the documentation on how to [create and configure a datastream](configure.md), then follow the instructions below to add bot detection capabilities to your datastream.

Go to the datastreams list and select the datastream to which you want to add bot detection.

![Datastreams user interface showing the list of datastreams.](assets/bot-detection/datastream-list.png)

In the datastream details page, select the **[!UICONTROL Bot Detection]** option on the right rail.

![Bot detection option highlighted in the datastreams user interface.](assets/bot-detection/bot-detection.png)

The **[!UICONTROL Bot Detection Rules]** page is shown.

![Bot detection settings in the datastream settings page.](assets/bot-detection/bot-detection-page.png)

From the Bot Detection Rules page, you can configure bot detection by using the following functionalities:

* Using the [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Creating your own bot detection rules.

### Use the IAB/ABC International Spiders and Bots List {#iab-list}

The [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) is a third-party, industry-standard list of internet spiders and bots. This list helps you identify automated traffic such as search engine crawlers, monitoring tools, and other nonhuman traffic that you may not want to include in your analytics counts.

To configure your datastream to use the IAB/ABC International Spiders and Bots List:

1. Toggle the **[!UICONTROL Use IAB/ABC International Spiders and Bots List for bot detection on this datastream]** option.
2. Select **[!UICONTROL Save]** to apply the bot detection settings to your datastream.

![IAB spiders and bot list enabled.](assets/bot-detection/bot-detection-list.png)

### Baandetectieregels maken {#rules}

Naast het gebruiken van de [ IAB/ABC Internationale Spinnen en Bots Lijst ](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), kunt u uw eigen regels van de botopsporing voor elke gegevensstroom bepalen.

U kunt beide opsporingsregels tot stand brengen die op **IP adressen** en **IP adreswaaiers** worden gebaseerd.

Als u meer regels voor korrelige botdetectie nodig hebt, kunt u de IP-voorwaarden combineren met de voorwaarden van de aanvraagkoptekst. De regels van de Bot opsporing kunnen de volgende kopballen gebruiken:

| HTTP-header | Beschrijving |
| --- | --- |
| `user-agent` | Een koptekst waarmee servers en netwerkpeers de toepassing, het besturingssysteem, de leverancier en/of de versie van de aanvragende gebruikersagent kunnen identificeren. |
| `content-type` | Geeft het oorspronkelijke mediatype van de bron aan (vóór eventuele inhoudcodering die is toegepast voor verzending). |
| `referer` | Identificeert het adres van de Web-pagina waarvan het middel is gevraagd. |
| `sec-ch-ua` | Biedt het merk en de significante versie voor elk merk verbonden aan browser in een komma-gescheiden lijst. |
| `sec-ch-ua-mobile` | Geeft aan of de browser zich op een mobiel apparaat bevindt. Deze kan ook door een desktopbrowser worden gebruikt om een voorkeur voor een mobiele gebruikerservaring aan te geven. |
| `sec-ch-ua-platform` | Verstrekt het platform of het werkende systeem waarop de gebruikersagent loopt. Bijvoorbeeld: &quot;Windows&quot; of &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | Verstrekt de versie van het werkende systeem waarop de gebruikersagent loopt. |
| `sec-ch-ua-arch` | Verstrekt de onderliggende architectuur van CPU van de gebruiker-agent, zoals ARM of x86. |
| `sec-ch-ua-model` | Geeft het apparaatmodel aan waarop de browser wordt uitgevoerd. |
| `sec-ch-ua-bitness` | Verstrekt de &quot;bitness&quot;van de onderliggende architectuur van CPU van de gebruiker-agent. Dit is de grootte in beetjes van een geheel of geheugenadres-typisch 64 of 32 beetjes. |
| `sec-ch-ua-wow64` | Geeft aan of een binaire gebruikersagent wordt uitgevoerd in de 32-bits modus van 64-bits Windows. |

Volg onderstaande stappen om een regel voor botdetectie te maken:

1. Selecteer **[!UICONTROL Add New Rule]** .

   ![ de montages van de Bot opsporing met Add Nieuwe benadrukte knoop van de Regel.](assets/bot-detection/bot-detection-new-rule.png)

2. Typ een naam voor de regel in het veld **[!UICONTROL Rule Name]** .

   ![ Bot ontdekkingsregelscherm met de benadrukte regelnaam.](assets/bot-detection/rule-name.png)

3. Selecteer **[!UICONTROL Add new IP condition]** om een nieuwe op IP gebaseerde regel toe te voegen. U kunt de regel door IP adres of door IP adreswaaier bepalen.

   ![ Bot ontdekkingsregel scherm met het IP benadrukte adresgebied.](assets/bot-detection/ip-address-rule.png)

   ![ Bot ontdekkingsregel scherm met het IP benadrukte waaiergebied.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >De IP-voorwaarden zijn gebaseerd op een logische `OR` -bewerking. Een verzoek wordt gemarkeerd als afkomstig van beide als het overeenkomt met een van de door u gedefinieerde IP-voorwaarden.

4. Als u kopbalvoorwaarden aan uw regel wilt toevoegen, selecteert u **[!UICONTROL Add header conditions group]**, en selecteert u vervolgens de kopballen die u de regel wilt gebruiken.

   ![ Bot ontdekkingsregel scherm met de benadrukt kopbalvoorwaarden.](assets/bot-detection/header-conditions.png)

   Voeg vervolgens de voorwaarden toe die voor de geselecteerde koptekst moeten worden gebruikt.

   ![ Bot ontdekkingsregel scherm met de benadrukt kopbalvoorwaarden.](assets/bot-detection/header-condition-rule.png)

5. Nadat u de gewenste regels voor beide detectie hebt geconfigureerd, selecteert u **[!UICONTROL Save]** om de regels toe te passen op uw gegevensstroom.

   ![ Bot ontdekkingsregel scherm met de benadrukt kopbalvoorwaarden.](assets/bot-detection/bot-detection-save.png)


## Voorbeelden van binddetectieregel {#examples}

Om u te helpen aan de slag te gaan met beide detectie, kunt u de onderstaande voorbeelden gebruiken om beide detectieregels te maken.

### Bot-detectie op basis van één IP-adres {#one-ip}

Om alle verzoeken te merken die uit een specifiek IP adres als allebei verkeer voortkomen, creeer een nieuwe beide opsporingsregel die één enkel IP adres evalueert, zoals aangetoond in het hieronder beeld.

![ Bot ontdekkingsregel die op één IP adres wordt gebaseerd.](assets/bot-detection/bot-detection-one-ip.png)

### Bot-detectie op basis van twee IP-adressen {#two-ip}

Om alle verzoeken te merken die uit één van beiden van twee specifieke IP adressen als allebei verkeer voortkomen, creeer een nieuwe regel van de botopsporing die twee IP adressen evalueert, zoals aangetoond in het hieronder beeld.

![ Bot ontdekkingsregel die op twee IP adressen wordt gebaseerd.](assets/bot-detection/bot-detection-two-ips.png)

### Bot-detectie op basis van een reeks IP-adressen {#range}

Om alle verzoeken te merken die uit om het even welk IP adres in een specifieke waaier als beide verkeer voortkomen, creeer een nieuwe de detectieregel van de bot die een volledige IP adreswaaier evalueert, zoals aangetoond in het hieronder beeld.

![ Bot ontdekkingsregel die op IP waaier wordt gebaseerd.](assets/bot-detection/bot-detection-range.png)

### Bot-detectie op basis van een IP-adres en een aanvraagheader {#ip-header}

Om alle verzoeken te merken die uit een specifiek IP adres voortkomen en een specifieke verzoekkopbal als allebei verkeer bevatten, creeer een nieuwe de detectieregel van de bot zoals aangetoond in het hieronder beeld.

Deze regel controleert of de aanvraag afkomstig is van een specifiek IP-adres en of de aanvraagheader `referer` begint met `www.adobe.com` .

![ Bot ontdekkingsregel die op IP adres en verzoekkopbal wordt gebaseerd.](assets/bot-detection/bot-detection-header-ip.png)

### Bot-detectie op basis van meerdere omstandigheden {#multiple-conditions}

U kunt beide detectieregels maken op basis van:

* **Veelvoudige verschillende voorwaarden**: De verschillende voorwaarden worden geëvalueerd als logische `AND` verrichting, betekenend dat de voorwaarden gelijktijdig moeten worden vervuld opdat het verzoek als voortkomend van een beide worden geïdentificeerd.
* **Veelvoudige voorwaarden van het zelfde type**: De voorwaarden van het zelfde type worden geëvalueerd als logische `OR` verrichting, betekenend dat als om het even welke voorwaarden worden vervuld, wordt het verzoek geïdentificeerd als voortkomend van een beide.

De regel in onderstaande afbeelding geeft een verzoek aan dat van oorsprong is als aan de volgende voorwaarden is voldaan:

De aanvraag is afkomstig van een van de twee IP-adressen, de `referer` header begint met `www.adobe.com` en de `sec-ch-ua-mobile` header geeft aan dat de aanvraag afkomstig is van een desktopbrowser.

![ Bot ontdekkingsregel die op veelvoudige voorwaarden wordt gebaseerd.](assets/bot-detection/bot-detection-multiple.png)
