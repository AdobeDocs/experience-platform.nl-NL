---
keywords: Experience Platform;home;populaire onderwerpen;relationeel schema;relationele schema's;schema;Schema;xdm;ervaringsgegevensmodel;
solution: Experience Platform
title: Relationele schema's
description: Meer informatie over relationele schema's in Adobe Experience Platform, waaronder functies, vereiste velden, relaties en beperkingen.
badge: Beperkte beschikbaarheid
exl-id: 397e5937-b892-4fd3-b90e-29ed9229dc69
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 0%

---

# Relationele schema&#39;s

>[!AVAILABILITY]
>
>Data Mirror en relationele schema&#39;s zijn beschikbaar aan Adobe Journey Optimizer **Geordende campagnes** vergunninghouders. Zij zijn ook beschikbaar als a **beperkte versie** voor de gebruikers van Customer Journey Analytics, afhankelijk van uw vergunning en eigenschapenactivering. Neem contact op met uw Adobe-vertegenwoordiger voor toegang.

Relationele schema&#39;s verstrekken een flexibel, gecontroleerd modelleringspatroon voor het vertegenwoordigen van gestructureerde gegevens in het gegevensmeer van Adobe Experience Platform. Zij steunen afgedwongen primaire sleutels, schema-vlakke verhoudingen, en fijnkorrelige controle over verslagen-allen zonder zich het baseren op verenigingsschema&#39;s of volledige relationele gegevensbestandsystemen.

>[!IMPORTANT]
>
>De overwegingen van de schrapping van gegevens zijn op alle relationele schemaimplementaties van toepassing. Toepassingen die deze schema&#39;s gebruiken moeten begrijpen hoe schrappingen verwante datasets, nalevingsvereisten, en stroomafwaartse processen beïnvloeden. Plan voor schrappingsscenario&#39;s en herzie [ begeleiding van de gegevenshygiëne ](../../hygiene/ui/record-delete.md#relational-record-delete) vóór implementatie.

Relationele schema&#39;s gebruiken voor:

* Zorg voor gegevensintegriteit met afgedwongen primaire of enkelvoudige toetsen.
* Schakel nauwkeurige wijzigingen bijhouden in met versiebeheer voor invoegen, bijwerken en verwijderen.
* Bepaal herbruikbare schema-vlakke verhoudingen aan model echt-wereld entiteitverbindingen.
* Vermijd het dupliceren van schemastructuren over toepassingen door veelvoudige gegevensmodellen te steunen.
* Verbindingsschemabeperkingen omzeilen om het instappen te stroomlijnen, schemavlek te verminderen, en ongewenste schemaveranderingen te vermijden.

## Hoe relationele schema&#39;s van standaardXDM schema&#39;s verschillen

De standaard XDM- schema&#39;s in Experience Platform volgen één van drie gegevensgedrag: Verslag, tijdreeks, of ad hoc. Voor definities en details, zie [ XDM gegevensgedrag ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors).

In het traditionele model, nemen het verslag en de tijd-reeksen schema&#39;s aan [ verenigingsschema&#39;s ](../api/unions.md) deel (zie ook de [ gids UI van het unieschema ](../../profile/ui/union-schema.md)). Deze schema&#39;s evolueren automatisch als gedeelde [ gebiedsgroepen ](./composition.md#field-group) worden bijgewerkt en de douanegebieden moeten onder een huurdersnamespace worden genest. Hoewel dit model krachtig is, kan het instappen vertragen, overdreven complexe schema&#39;s met ongebruikte gebieden produceren, en extra gegevenstoewijzing of transformatie vereisen. Deze factoren verhogen de leercurve en de voortdurende onderhoudsinspanningen.

Relationele schema&#39;s verwijderen de gebiedsdelen van het unieschema, die automatische updates uit gedeelde gebiedsgroepen elimineren en directe gebiedsdefinities zonder huurdersnaamruimtebeperkingen toestaat. U krijgt expliciete controle over primaire sleutels, verhoudingen, en aanvankelijke schemaontwerp, die het gemakkelijker maken om gegevens te modelleren om uw behoeften in aanmaaktijd te passen.

## Functies van relationele schema&#39;s

Gebruik de volgende mogelijkheden om gestructureerde gegevens in het datumpeer te modelleren terwijl het handhaven van bestuur, integriteit, en interoperabiliteit.

* **de gedragssteun van het Schema**: Vorm met:
   * **gedrag van het Verslag**: Vangt de huidige staat van een entiteit, zoals een klant, een rekening, of een campagne.
   * **tijd-reeks gedrag**: Vangt gebeurtenissen en de tijd zij voorkomen, nuttig om opeenvolgingen of veranderingen in tijd te volgen.
* **Primaire zeer belangrijke handhaving**: Bepaal een primaire sleutel om elk verslag uniek te identificeren en duplicaten tijdens opname te verhinderen.
* **controle van de Versie**: Gebruik het herkenningsteken van de a **versie** (een beschrijver) om updates te verzekeren in de correcte orde worden toegepast, zelfs als de verslagen uit opeenvolging aankomen.
* **afbeelding van de Verhouding**: Creeer één-aan-één of vele-aan-één verhouding tussen relationele schema&#39;s of tussen relationele en standaardschema&#39;s. Relatiedefinities worden opgeslagen als beschrijvingen om efficiënte verbindingen mogelijk te maken.
* **Vereenvoudigde evolutie**: De relationele schema&#39;s nemen niet deel aan verenigingsmeningen en worden niet bijgewerkt wanneer de gedeelde gebiedsgroepen veranderen, verhinderend onverwachte stroomafwaartse veranderingen.
* **Flexibele gebiedsdefinitie**: Voeg direct gebieden zonder huurder-id namespacing toe. Relationele schema&#39;s ondersteunen geen XDM-veldgroepen.
* **geen afhankelijkheid van verenigingsschema&#39;s**: Verbetert vraagprestaties en vermindert operationele overheadkosten van het beheren van globale schemameningen.
* **gebeurtenis-tijd die** opdracht geven: Voor tijdreeksschema&#39;s, gebruik a **timestamp herkenningsteken** om gebeurtenissen door voorvaltijd in plaats van innametijd tot stand te brengen.

## Vereiste velden

Relationele schema&#39;s vereisen bepaalde beschrijver-meta-gegevens in de schemadefinitie die zeer belangrijk gedrag en beperkingen controleert. Voeg de volgende beschrijvingen als deel van uw schemadefinitie toe.

### Descriptor primaire sleutel

Gebruik een descriptor van de primaire sleutel om ervoor te zorgen dat elke record uniek kan worden geïdentificeerd. De ondersteunde configuraties zijn:

* **Enig-gebied primaire sleutel**: Gebruik één gebied met een unieke waarde voor elk verslag.
* **Samengestelde primaire sleutel**: Gebruik veelvoudige gebieden om een uniek herkenningsteken te vormen. Voor tijdreeksschema&#39;s moet de samengestelde sleutel het tijdstempelveld bevatten dat door de tijdstempelbeschrijving wordt geïdentificeerd.

>[!NOTE]
>
>In de Redacteur van het Schema UI, verschijnen de versiedescriptor en timestamp beschrijvers als &quot;[!UICONTROL Version identifier]&quot;en &quot;[!UICONTROL Timestamp identifier]&quot; respectievelijk.

**Voorbeeld (enig-gebied):**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Voorbeeld (samenstelling voor tijd-reeks)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Versiebeschrijving (id)

Definieer een versiedescriptor (id) om de juiste recordstatus te behouden en ervoor te zorgen dat de laatste update wordt toegepast. Wanneer meerdere records dezelfde primaire sleutel delen, wordt de record met de hoogste versiewaarde als de meest recente record beschouwd.

**Voorbeeld:**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Tijdstempelbeschrijving (id)

Voor tijdreeksschema&#39;s, bepaal een timestamp beschrijver (herkenningsteken) om de gebeurtenistijd voor het opdracht geven te plaatsen.

**Voorbeeld:**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>Descriptors maken deel uit van de metagegevens van de schemadefinitie en worden niet opgeslagen in gegevensrijen.

Voor instructies bij het creëren van beschrijvers in de Redacteur van het Schema, zie [ beschrijvers in de Redacteur van het Schema ](../tutorials/relationship-ui.md) creëren. Voor op API-Gebaseerde verwezenlijking, zie [ beschrijvers creëren gebruikend API ](../tutorials/relationship-api.md).

## Relatieondersteuning {#relationship-support}

Relationele gegevensmodellering is een primair gebruik van relationele regelingen. In gevallen waarin toepassingen worden gebruikt, kan zelfs naar deze schema&#39;s worden verwezen als &#39;relationele schema&#39;s&#39;. De beschrijvers van de verhouding laten deze verbindingen toe door datasets over schema&#39;s te verbinden zonder buitenlandse sleutels in gegevensrijen in te bedden. Zij verbeteren referentiële integriteit, laten herbruikbare modelleringspatronen, en steunen verbonden vragen over toepassingen toe.

Creeer relatiebeschrijvers op het schemaniveau voor dynamische resolutie bij vraagtijd. De waarden van de kardinaliteit (1 :1, veel-aan-één) verstrekken begeleiding maar dwingen geen beperkingen tijdens opname af, ondersteunend flexibele gegevensmodellering over verbonden datasets.

Voordat u relatiebeschrijvingen toevoegt, bepaalt u het juiste type en doel:

* **één-aan-één** - elk verslag in het bronschema beantwoordt aan hoogstens één verslag in het bestemmingsschema.
* **vele-aan-één** - de veelvoudige verslagen in het bronschema kunnen het zelfde verslag in het bestemmingsschema van verwijzingen voorzien.

>[!NOTE]
>
>U kunt relaties definiëren tussen twee relationele schema&#39;s of tussen een relationeel schema en een standaardschema. Relaties met ad-hocschema&#39;s worden niet ondersteund.

**Voorbeeld: Één-aan-één verhouding**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

**Voorbeeld: Vele-aan-één verhouding**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

Voor een lijst van de types en syntaxis van relatiebeschrijver, zie de [ beschrijvers API verwijzing ](../api/descriptors.md).Leren hoe te om deze concepten in praktijk toe te passen, de leerprogramma&#39;s volgen om [ een verhouding in API ](../tutorials/relationship-api.md) te bepalen of [ een verhouding in UI ](../tutorials/relationship-ui.md) tot stand te brengen.

>[!NOTE]
>
>Aangezien de verhoudingen op het schemaniveau worden bepaald, zorg ervoor om zich uitdrukkelijk bij verwante datasets in uw vragen aan te sluiten. Gebruik een hulpmiddel zoals Gegevens Distiller om deze verhoudingen tijdens vraagtijd op te lossen.

>[!IMPORTANT]
>
>Relationship cardinality is informational en wordt niet afgedwongen tijdens inname. Het wordt toegepast slechts wanneer het oplossen van verhoudingen tijdens vraag of analyse. Vertrouw niet op standaardinstellingen om uw gegevens tijdens de inname te valideren. Controleer en schoonmaak uw gegevens zelf, en zorg ervoor de relatieregels u bepaalt aanpassen de manier u van plan bent om de gegevens te vragen of te analyseren.

>[!NOTE]
>
>Relationele schema&#39;s kunnen aan standaardschema&#39;s worden gekoppeld, maar kunnen niet aan ad-hocschema&#39;s worden gekoppeld.

## Gegevensverwijdering en hygiëne {#data-hygiene-support}

Relationele schema&#39;s maken nauwkeurige schrappingen op recordniveau mogelijk die universele implicaties voor alle toepassingen en gebruiksgevallen hebben. Primaire sleutel-, versie- en tijdstempelbeschrijvingen vormen de basis voor nauwkeurige identificatie van records tijdens verwijderingsbewerkingen.

### Algemene verwijderingseffecten

Alle toepassingen die relationele schema&#39;s gebruiken moeten nadenken:

* **Referentiële integriteit**: De schrappingen kunnen verwante verslagen over verbonden datasets beïnvloeden
* **vereisten van de Naleving**: Sommige industrieën vereisen specifiek schrappingsgedrag en controletrails
* **het gedrag van de Toepassing**: De stroomafwaartse systemen kunnen de gebeurtenissen van de handvat geschikt
* **consistentie van Gegevens**: De verwante datasets moeten consistentie tijdens schrappingsverrichtingen handhaven
* **planning van de Schrapping**: Rekening voor stroomafwaartse gevolgen over alle verbonden datasets en toepassingen tijdens de ontwerpfase

Voor implementatierichtlijnen, zie [ het Schrappen van verslagen van datasets die op relationele schema&#39;s ](../../hygiene/ui/record-delete.md#relational-record-delete) worden gebaseerd.

## Beperkingen en overwegingen {#limitations}

Controleer de volgende beperkingen voordat u relationele schema&#39;s gebruikt:

* Relationele schema&#39;s nemen niet deel aan unieschema&#39;s.
* De evolutie van het schema is manueel; zij niet auto-update wanneer de gebiedsgroepen veranderen.

>[!IMPORTANT]
>
>De evolutie van het schema wordt beperkt nadat een dataset gebruikend het schema wordt geïnitialiseerd. Namen en typen van velden vooraf zorgvuldig plannen, aangezien velden niet kunnen worden verwijderd of gewijzigd nadat gegevens zijn ingevoerd.

* De relaties zijn beperkt tot één-op-één en veel-op-één.
* Beschikbaarheid is afhankelijk van uw licentie of functionaliteit.
* Samengestelde primaire sleutels zijn vereist voor tijdreeksschema&#39;s.
