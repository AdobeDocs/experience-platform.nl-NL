---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;field;
solution: Experience Platform
title: XDM-velden definiëren in de UI
description: Leer hoe u XDM-velden definieert in de gebruikersinterface van het Experience Platform.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 89519918aa830dc09365fa80449099229dc475d5
workflow-type: tm+mt
source-wordcount: '1636'
ht-degree: 0%

---

# XDM-velden definiëren in de UI

De [!DNL Schema Editor] in de gebruikersinterface van Adobe Experience Platform kunt u uw eigen velden definiëren binnen de klassen van het aangepaste Experience Data Model (XDM) en de schemaveldgroepen. In deze handleiding worden de stappen beschreven voor het definiëren van XDM-velden in de gebruikersinterface, inclusief de beschikbare configuratieopties voor elk veldtype.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) om te leren hoe de klassen en de gebiedsgroepen gebieden aan schema&#39;s XDM bijdragen.

Hoewel dit niet nodig is voor deze handleiding, wordt u aangeraden de zelfstudie ook op te volgen [samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) om vertrouwd te maken met de verschillende mogelijkheden van de [!DNL Schema Editor].

## Selecteer een bron waaraan u velden wilt toevoegen {#select-resource}

Als u nieuwe XDM-velden in de gebruikersinterface wilt definiëren, moet u eerst een schema openen in het dialoogvenster [!DNL Schema Editor]. Afhankelijk van welke schema&#39;s momenteel beschikbaar zijn in de [!DNL Schema Library], kunt u [een nieuw schema maken](../resources/schemas.md#create) of [een bestaand schema selecteren om te bewerken](../resources/schemas.md#edit).

Als u eenmaal [!DNL Schema Editor] openen, worden besturingselementen voor het toevoegen van velden weergegeven op het canvas. Deze besturingselementen worden naast de naam van het schema weergegeven, evenals alle velden van het objecttype die zijn gedefinieerd onder de geselecteerde klasse of veldgroep.

![De Schema-editor met de gemarkeerde pictogrammen voor toevoegen.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Als u een veld probeert toe te voegen aan een object dat wordt geleverd door een standaardveldgroep, wordt die veldgroep geconverteerd naar een aangepaste veldgroep en is de oorspronkelijke veldgroep niet meer beschikbaar. Zie de sectie over [velden toevoegen aan standaardveldgroepen](../resources/schemas.md#custom-fields-for-standard-groups) in de gids van schema&#39;s UI voor meer informatie.

Als u een nieuw veld aan de bron wilt toevoegen, selecteert u de optie **plus (+)** naast de naam van het schema op het canvas of naast het veld voor het objecttype dat u wilt definiëren onder.

![De Schema-editor met een pictogram voor toevoegen gemarkeerd.](../../images/ui/fields/overview/plus-icon.png)

Afhankelijk van het feit of u een veld rechtstreeks aan een schema of aan de deel-klasse en -veldgroepen toevoegt, variëren de vereiste stappen voor het toevoegen van het veld. De rest van dit document richt zich op hoe te om de eigenschappen van een gebied ongeacht te vormen waar dat gebied in het schema verschijnt. Voor meer informatie over de verschillende manieren dat de gebieden aan een schema kunnen worden toegevoegd, verwijs naar de volgende secties in de gids van schema&#39;s UI:

* [Velden toevoegen aan veldgroepen](../resources/schemas.md#add-fields)
* [Velden rechtstreeks aan een schema toevoegen](../resources/schemas.md#add-individual-fields)

## De eigenschappen van een veld definiëren {#define}

Na het selecteren van **plus (+)** pictogram, an **[!UICONTROL Untitled field]** wordt weergegeven in het canvas.

![De Schema-editor heeft een nieuw naamloos veld gemarkeerd.](../../images/ui/fields/overview/new-field.png)

In de rechterspoorlijn onder **[!UICONTROL Field properties]** kunt u de details van het nieuwe veld configureren. Voor elk veld is de volgende informatie vereist:

| Field, eigenschap | Beschrijving |
| --- | --- |
| [!UICONTROL Field name] | Een unieke, beschrijvende naam voor het veld. De naam van het veld kan niet worden gewijzigd nadat het schema is opgeslagen. Deze waarde wordt gebruikt om het veld in code en in andere downstreamtoepassingen te identificeren en ernaar te verwijzen<br><br>De naam moet idealiter in camelCase worden geschreven. Het kan alfanumerieke, streepje- of onderstrepingstekens bevatten, maar het kan **mag** begint met een onderstrepingsteken.<ul><li>**Juist**: `fieldName`</li><li>**Aanvaardbaar:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Onjuist**: `_fieldName`</li></ul> |
| [!UICONTROL Display name] | Een weergavenaam voor het veld. Dit is de naam die wordt gebruikt om het veld in het canvas van de Schema-editor weer te geven. U kunt de veldnaam wijzigen in de weergavenaam met de [weergavenaam](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Type] | Het type gegevens dat het veld zal bevatten. In dit vervolgkeuzemenu kunt u een van de [standaard scalaire typen](../../schema/field-constraints.md) ondersteund door XDM of een van de velden met meerdere velden [gegevenstypen](../resources/data-types.md) die eerder zijn gedefinieerd in de [!DNL Schema Registry].<br>Opmerking: als u het gegevenstype Kaart selecteert, [!UICONTROL Map value type] wordt weergegeven.<br><br>U kunt ook **[!UICONTROL Advanced type search]** om bestaande gegevenstypen te zoeken en te filteren en het gewenste type gemakkelijker te vinden. |
| [!UICONTROL Map value type] | Deze waarde is vereist als u [!UICONTROL Map] als het gegevenstype voor het veld. Beschikbare waarden voor de kaart zijn: [!UICONTROL String] en [!UICONTROL Integer]. Selecteer een waarde in de vervolgkeuzelijst met beschikbare opties.<br>Meer informatie over [type-specifieke veldeigenschappen](#type-specific-properties)Zie het overzicht met gedefinieerde velden. |

{style="table-layout:auto"}

U kunt ook een beschrijving en notities opgeven voor elk veld. Gebruik de **[!UICONTROL Description]** veld om context toe te voegen en de functionaliteit van het gegevenstype map te beschrijven. Dit draagt bij tot het onderhoud en de leesbaarheid van de implementatie. U kunt ook notities toevoegen als aanvulling op de oorspronkelijke beschrijving. Dit zou korrelige en specifieke informatie moeten aanbieden om ontwikkelaars te helpen bij het begrijpen, onderhouden en effectief gebruiken van de kaart binnen de context van codebase. |


>[!NOTE]
>
>Afhankelijk van de **[!UICONTROL Type]** Als u voor het veld hebt geselecteerd, worden mogelijk extra besturingselementen voor de configuratie weergegeven in de rechterrail. Zie de sectie over [type-specifieke veldeigenschappen](#type-specific-properties) voor meer informatie over deze controles.
>
>De rechterrail biedt ook selectievakjes voor het aanwijzen van speciale veldtypen. Zie de sectie over [speciale veldtypen](#special) voor meer informatie .

Nadat u het veld hebt geconfigureerd, selecteert u **[!UICONTROL Apply]**.

![De [!UICONTROL Field properties] wordt gemarkeerd.](../../images/ui/fields/overview/field-details.png)

Het canvas wordt bijgewerkt om het nieuwe toegevoegde veld weer te geven dat zich binnen een object bevindt dat een naamruimte heeft naar uw unieke huurder-id (weergegeven als `_tenantId` in het onderstaande voorbeeld). Alle aangepaste velden die aan een schema worden toegevoegd, worden automatisch binnen deze naamruimte geplaatst om conflicten met andere velden van door de Adobe verschafte klassen en veldgroepen te voorkomen. Het rechterspoor geeft nu naast de andere eigenschappen ook het pad van het veld weer.

![Een nieuw veld in het schema en het bijbehorende pad in het schema [!UICONTROL Field properties] wordt gemarkeerd.](../../images/ui/fields/overview/field-added.png)

U kunt de bovenstaande stappen blijven volgen om meer velden aan het schema toe te voegen. Zodra het schema wordt bewaard, worden zijn basisklasse en gebiedsgroepen ook bewaard als om het even welke veranderingen in hen zijn aangebracht.

>[!NOTE]
>
>Om het even welke veranderingen u aan de gebiedsgroepen of de klasse van één schema aanbrengt zullen in alle andere schema&#39;s worden weerspiegeld die hen aanwenden.

## Eigenschappen van specifieke velden {#type-specific-properties}

Wanneer u een nieuw veld definieert, kunnen er aanvullende configuratieopties worden weergegeven in de rechterraster, afhankelijk van de **[!UICONTROL Type]** kiest u voor het veld. In de volgende tabel worden deze extra veldeigenschappen in combinatie met de compatibele typen weergegeven:

| Field, eigenschap | Compatibele typen | Beschrijving |
| --- | --- | --- |
| [!UICONTROL Map value type] | [!UICONTROL Map] | De [!UICONTROL Map value type] wordt alleen in de gebruikersinterface weergegeven als u de waarde Kaart in het menu [!UICONTROL Type] vervolgkeuzemogelijkheden. U kunt kiezen tussen de waarden voor Tekenreeks en Geheel getal voor Kaart.<br>![De Schema-editor met de velden Type- en Kaartwaardetype gemarkeerd.](../../images/ui/fields/overview/map-type.png "De Schema-editor met de velden Type- en Kaartwaardetype gemarkeerd."){width="100" zoomable="yes"}<br>Opmerking: alle gegevenstypen die via de API zijn gemaakt en die geen tekenreeks of geheel getal zijn, worden weergegeven als een &#39;[!UICONTROL Complex]&#39; gegevenstype. U kunt geen &#39;[!UICONTROL Complex]&#39;gegevenstypen via de gebruikersinterface. |
| [!UICONTROL Default value] | [!UICONTROL String], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Integer], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolean] | A default value that is assigned to this field if no other value is provided during ingestion. Deze waarde moet overeenkomen met het geselecteerde veldtype.<br><br>De standaardwaarden worden niet opgeslagen in de gegevensset op het moment van inname, omdat ze in de loop der tijd kunnen veranderen. De standaardwaarden die in het schema worden geplaatst worden afgeleid door de stroomafwaartse diensten en de toepassingen van het Platform wanneer zij de gegevens van de dataset lezen. Bijvoorbeeld, wanneer het vragen van de gegevens gebruikend de Dienst van de Vraag, als de attributen een ONGELDIGE waarde hebben, maar het gebrek wordt geplaatst aan `5` op het schemaniveau, wordt verwacht dat de Dienst van de Vraag zal terugkeren `5` in plaats van NULL. Dit gedrag is momenteel niet uniform voor alle AEP-services. |
| [!UICONTROL Pattern] | [!UICONTROL String] | A [reguliere expressie](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) dat de waarde voor dit veld in overeenstemming moet zijn om tijdens de inname te worden geaccepteerd. |
| [!UICONTROL Format] | [!UICONTROL String] | Selecteer een optie in een lijst met vooraf gedefinieerde indelingen voor tekenreeksen die de waarde moet bevatten. Beschikbare indelingen zijn: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | Het minimale aantal tekens dat de tekenreeks moet bevatten voordat de waarde wordt geaccepteerd tijdens de opname. |
| [!UICONTROL Maximum length] | [!UICONTROL String] | Het maximum aantal tekens dat de tekenreeks moet bevatten voordat de waarde wordt geaccepteerd tijdens de invoer. |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | De minimumwaarde voor het Dubbele die tijdens inname moet worden goedgekeurd. Als de ingevoerde waarde precies overeenkomt met de waarde die hier is ingevoerd, wordt de waarde geaccepteerd. Wanneer u deze beperking gebruikt, wordt &quot;[!UICONTROL Exclusive minimum value]&quot; beperking moet leeg blijven. |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | De maximumwaarde voor het dubbel dat tijdens inname moet worden geaccepteerd. Als de ingevoerde waarde precies overeenkomt met de waarde die hier is ingevoerd, wordt de waarde geaccepteerd. Wanneer u deze beperking gebruikt, wordt &quot;[!UICONTROL Exclusive maximum value]&quot; beperking moet leeg blijven. |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | De maximumwaarde voor het dubbel dat tijdens inname moet worden geaccepteerd. Als de ingevoerde waarde precies overeenkomt met de waarde die hier is ingevoerd, wordt de waarde afgewezen. Wanneer u deze beperking gebruikt, wordt &quot;[!UICONTROL Minimum value]&quot;(niet-exclusieve) beperking moet leeg worden gelaten. |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | De maximumwaarde voor het dubbel dat tijdens inname moet worden geaccepteerd. Als de ingevoerde waarde precies overeenkomt met de waarde die hier is ingevoerd, wordt de waarde afgewezen. Wanneer u deze beperking gebruikt, wordt &quot;[!UICONTROL Maximum value]&quot;(niet-exclusieve) beperking moet leeg worden gelaten. |

{style="table-layout:auto"}

## Speciale veldtypen {#special}

Het rechterspoor biedt verschillende selectievakjes voor het aanwijzen van speciale rollen voor het geselecteerde veld. De gebruiksgevallen voor sommige van deze opties vereisen belangrijke overwegingen met betrekking tot uw strategie voor het modelleren van gegevens en hoe u de downstream services van het Platform wilt gebruiken.

Raadpleeg de volgende documentatie voor meer informatie over deze speciale typen:

* [Kaart](./map.md)
* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) (Alleen beschikbaar voor tekenreeksvelden)
* [[!UICONTROL Relationship]](./relationship.md) (Alleen beschikbaar voor tekenreeksvelden)

Technisch gezien is dit geen speciaal veldtype, maar u kunt het beste de handleiding raadplegen op [definiëren, van objecttype](./object.md) voor meer informatie over het definiëren van geneste subvelden als uw schema is gestructureerd.

## Volgende stappen

Deze handleiding gaf een overzicht van hoe u XDM-velden in de gebruikersinterface kunt definiëren. Vergeet niet dat velden alleen aan schema&#39;s kunnen worden toegevoegd met behulp van klassen en veldgroepen. Raadpleeg de handleidingen bij het maken en bewerken van deze bronnen voor meer informatie over het beheren van deze bronnen in de gebruikersinterface [klassen](../resources/classes.md) en [veldgroepen](../resources/field-groups.md).

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie de [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).
