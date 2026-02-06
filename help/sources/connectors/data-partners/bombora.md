---
title: Bombora-intentie
description: Meer informatie over de Bombora Intent-bron op Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 04af34d439ba76b0d0053ba9de45ca962458d3e8
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 0%

---

# [!DNL Bombora Intent]

[!DNL Bombora] is een uitgebreide publieksoplossing die zich in B2B intentgegevens specialiseert. [!DNL Bombora Intent] is een Adobe Experience Platform-bron die u kunt gebruiken om uw [!DNL Bombora] -account te verbinden met Experience Platform en uw gegevens over uw accountintenties te integreren.

Met de [!DNL Bombora Intent] -bron kunt u [!DNL Bombora's] -bedrijfsgegevens integreren om accounts te identificeren die actief onderzoek naar uw producten of services uitvoeren. Gebruik [!DNL Bombora] om prioriteit toe te kennen aan accounts op de markt om precieze segmenten te maken en ABM-campagnes met hyperlinks uit te voeren, zodat uw marketinginspanningen zich richten op die accounts die het meest converteren. Bovendien kunt u met behulp van intentgestuurde strategieën optimaliseren en uitgeven, de betrokkenheid verhogen en het investeringsrendement maximaliseren.

Lees dit document voor noodzakelijke informatie over de [!DNL Bombora] bron.

## Gebruiksscenario’s {#use-cases}

Lees de volgende voorbeelden van gebruiksscenario&#39;s die u kunt toepassen op de [!DNL Bombora] -bron.

### Integratie van Demand-Side Platform (DSP)

Als een B2B-markeerteken kunt u een accountlijst in Real-Time CDP maken, bedrijven identificeren die hoge intenties voor uw producten tonen en deze lijst vervolgens activeren in [!DNL Bombora] , die rechtstreeks met DSP&#39;s integreert, zodat u gerichte programmatische advertentiecampagnes kunt uitvoeren met [!DNL Bombora's] -gegevens. Zo weet u zeker dat uw advertentie-uitgaven zijn gericht op bedrijven die zich het meest waarschijnlijk zullen omzetten.

### Account-Based Marketing (ABM) Capabilities

Als B2B-markeerteken kunt u een accountlijst maken op basis van de eerste en derde intentsignalen. U kunt deze lijst vervolgens activeren in [!DNL Bombora] , waar u met ABM-functies werknemers op deze accounts specifiek kunt richten, zodat uw advertenties besluitvormers bereiken in plaats van een breed publiek.

### ABM-activering via meerdere kanalen

Als een B2B-markeerteken kunt u een accountlijst in Real-Time CDP maken, bedrijven met een hoge intentie identificeren en deze activeren in [!DNL Bombora] om gerichte campagnes op meerdere kanalen uit te voeren. Op betaalde sociale media kunt u persoonlijke advertenties leveren aan professionals op doelaccounts op platforms als [!DNL Linkedin] en [!DNL Facebook] .

Met native advertentieplatforms kunt u ervoor zorgen dat de inhoud in relevante contexten bij de besluitvormers terechtkomt. U kunt campagnes ook uitbreiden naar geavanceerde tv en advertenties leveren aan belangrijke accounts. Deze multikanaalsbenadering zorgt voor consistent overseinen op verschillende platforms, waarbij de betrokkenheid en conversietarieven worden gemaximaliseerd.

## Vereisten {#prerequisites}

Lees de volgende secties voor de stappen die u in de eerste plaats moet uitvoeren voordat u [!DNL Bombora] verbindt met Experience Platform.

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het nalaten om uw gebied-specifieke IP adressen aan uw lijst van gewenste personen toe te voegen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [ IP pagina van de lijst van gewenste personen van het adres ](../../ip-address-allow-list.md) voor meer informatie.

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Bombora] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/abac/ui/permissions.md).

### Naamgevingsbeperkingen voor bestanden en mappen

Met de onderstaande beperkingen moet rekening worden gehouden bij de naamgeving van uw cloudopslagbestand of -map:

* Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
* De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
* De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
* De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
* Ongeldige URL-padtekens zijn niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
* De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

### Vereiste referenties verzamelen

[!DNL Bombora] op Experience Platform wordt gehost door [!DNL Google Cloud Storage] . Als u uw [!DNL Bombora] -account wilt verifiëren, moet u de juiste waarden opgeven voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoets-id | De toegangssleutel-id van [!DNL Bombora] . Dit is een alfanumerieke tekenreeks van 61 tekens die vereist is om uw account bij Experience Platform te verifiëren. |
| Geheim toegangssleutel | De sleutel voor toegang tot het [!DNL Bombora] -geheim. Dit is een tekenreeks van 40 tekens met een basiscodering van 64 tekens die vereist is om uw account bij Experience Platform te verifiëren. |
| Naam van emmertje | Het [!DNL Bombora] emmertje waaruit gegevens worden opgehaald. |

Voor meer informatie over deze geloofsbrieven, leest de [[!DNL Google Cloud Storage]  handleiding van de sleutels HMAC ](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Voor stappen op hoe te om uw eigen toegangssleutel te produceren, lees de [ in de eerste plaats vereiste gids in het  [!DNL Google Cloud Storage]  bronoverzicht ](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## [!DNL Bombora] schema {#schema}

Lees deze sectie voor informatie over het schema en de gegevensstructuur van [!DNL Bombora] .

Het [!DNL Bombora] schema wordt genoemd **B2B Bombora Intent van de Rekening**. Het is de wekelijkse intentinformatie (anonieme B2B-kopersonderzoek en inhoudconsumptie) over gespecificeerde rekeningen en onderwerpen. De gegevens hebben de parketindeling.

* Klasse - XDM [!DNL Bombora Account Intent]
* Naamruimte - B2B [!DNL Bombora Account Intent]
* Primaire identiteit - `intentID`
* Relaties - B2B-account

| Veldnaam | Gegevenstype | Beschrijving |
|------------------------|-----------|----------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJECT | Dit veld wordt door het systeem gebruikt voor de controle van het bronsysteem. |
| `_id` | TEKENREEKS | Dit veld wordt door het systeem gebruikt als een unieke id. |
| `accountDomain` | TEKENREEKS | Dit veld bevat het accountdomein. |
| `accountID` | TEKENREEKS | Dit veld bevat de B2B-account-id waaraan deze intentrecord is gekoppeld. |
| `bomboraAccountName` | TEKENREEKS | Dit veld bevat de bedrijfs-id in Bombora. |
| `clusterID` | TEKENREEKS | Dit veld bevat de cluster-id. |
| `clusterName` | TEKENREEKS | Dit veld bevat de clusternaam. |
| `compositeScore` | INTEGER | Dit veld bevat de samengestelde score van de intentie. |
| `intentID` | TEKENREEKS | Dit veld bevat een door het systeem gegenereerde unieke waarde. |
| `partitionDate` | DATE | Dit veld bevat de datum van de partitie. Dit gebeurt wekelijks, aan het einde van de week, in `mm/dd/yyyy` formaat. |
| `topicID` | TEKENREEKS | Dit gebied bevat intent onderwerpidentiteitskaart van Bombora. |
| `topicName` | TEKENREEKS | Dit veld bevat de intentonderwerpnaam uit Bombora. |

{style="table-layout:auto"}

>[!TIP]
>
>Wijzigingen in het schema worden vooraf aan Adobe meegedeeld. Om naadloze schemaevolutie te steunen, is het handhaven van achterwaartse verenigbaarheid essentieel. Experience Platform past een benadering met alleen additieve versies toe en zorgt ervoor dat updates van het schema niet-destructief zijn. Dit betekent dat het doorbreken van veranderingen strikt worden verboden, en slechts veranderingen die het bestaande schema verbeteren of uitbreiden worden toegestaan.

## Sluit uw [!DNL Bombora] -account aan op Experience Platform in de gebruikersinterface

Zodra u uw in de eerste plaats vereiste opstelling hebt voltooid, lees het leerprogramma op [ verbindend uw  [!DNL Bombora]  rekening met Experience Platform ](../../tutorials/ui/create/data-partners/bombora.md) om uw integratie te beginnen.

## Veelgestelde vragen {#faq}

Lees deze sectie voor antwoorden op veelgestelde vragen over de [!DNL Bombora] bron.

### Moet ik een bestaand contract met [!DNL Bombora] hebben om hun gegevens van de rekeningintentie in Real-Time CDP B2B edition te gebruiken?

+++Antwoord

Ja, u moet een actief contract hebben met [!DNL Bombora] om hun intentgegevens binnen Experience Platform en Real-Time CDP B2B edition te openen en te gebruiken. De integratie maakt gebruik van uw bestaande overeenkomst met de [!DNL Bombora] om accountintentsignalen in Experience Platform en Real-Time CDP in te voeren en te activeren.

+++

### Worden aangepaste velden van [!DNL Bombora] ondersteund in deze integratie?

+++Antwoord

U kunt op dit moment alleen standaard [!DNL Bombora] -velden gebruiken voor inname en activering. Om de lijst van gesteunde gebieden te bekijken, lees de [[!DNL Bombora]  schemagids ](#schema) voor de details op gebiedsbeschikbaarheid.

+++

### Kan ik ad-hocgegevens van [!DNL Bombora] naar Experience Platform invoeren?

+++Antwoord

Ja, u kunt ad-hocgegevens van [!DNL Bombora] invoeren. U kunt een nieuwe gegevensstroom creëren om de recentste intentgegevens in te voeren, zolang er nieuwe gegevens van [!DNL Bombora] zijn. U kunt echter slechts één actieve gegevensstroom tegelijk hebben. Zorg daarom dat u de bestaande gegevensstroom verwijdert voordat u een nieuwe maakt.

+++

### Wat is het validatieproces voor intentgegevens en hoe kan ik controleren welke intentgegevens zijn gekoppeld aan een specifieke account?

+++Antwoord

Om intentgegevens te bevestigen en te bepalen welke intentsignalen met specifieke rekeningen verbonden zijn, gebruik [ de Dienst van de Vraag van Adobe Experience Platform ](../../../query-service/home.md) door AccountID.

+++

### Hoe kan ik een intent opzoeken voor een bepaald bedrijf?

+++Antwoord

Voer een SQL vraag in [ Dienst van de Vraag ](../../../query-service/home.md) uit om naar intentgegevens te zoeken gebruikend de bedrijfsnaam of AccountID. Om alle intentgegevens voor een specifiek bedrijf te bekijken, kunt u een SQL vraag in de Dienst van de Vraag in werking stellen gebruikend de bedrijfsnaam of AccountID om alle bijbehorende intentsignalen te halen.

+++


### Ik heb een probleem gevonden met het rekeningafstemmingsproces in Experience Platform. Wat moet ik doen?

+++Antwoord

De resolutie hangt af van de specifieke kwestie:

* **Onjuist of ontbrekend bedrijfdomein in Experience Platform**: Als de kwestie uit een onjuiste waarde van het bedrijfdomein in de rekeningsgegevens voortkomt, werk het gebied van het bedrijfdomein in Experience Platform bij om nauwkeurige aanpassing te verzekeren.
* **Onjuiste gebiedstoewijzing in dataflow**: Als de kwestie aan een onjuiste weg van het bedrijfdomeingebied in dataflow toe te schrijven is, werk de dataflow configuratie bij om de correcte gebiedspad van verwijzingen te voorzien.

+++

### Hoe verwijder ik intentgegevens in Experience Platform?

+++Antwoord

U moet [ de dataset ](../../../catalog/datasets/user-guide.md#delete-a-dataset) schrappen om intentgegevens in Experience Platform te schrappen.

+++

### Welk veld wordt gebruikt om accounts van [!DNL Bombora] aan Experience Platform aan te passen?

+++Antwoord

Het veld `accountOrganization.domain` wordt gebruikt voor overeenkomende accounts. Als uw organisatie een ander aangepast veld gebruikt om de naam van de website op te slaan, zorgt u ervoor dat u het juiste veldpad opgeeft voor nauwkeurige toewijzing.

+++

### Wat gebeurt er als een bedrijfsdomein wordt bijgewerkt in Experience Platform?

+++Antwoord

Wanneer een bedrijfdomein wordt bijgewerkt, zal de nieuwe domeinwaarde in de volgende dataflow looppas worden toegepast. Dit zorgt ervoor dat:

* Toekomstige gegevensinvoer met intentie gebruikt het bijgewerkte domein voor afstemming van account.
* Eerder niet-overeenkomende intentsignalen kunnen nu op de juiste wijze worden uitgelijnd op het bedoelde account.
* Er worden geen terugwerkende wijzigingen aangebracht in het verleden ingesloten alleen-gegevens. De nieuwe gegevens weerspiegelen de update.

+++

### Wat is het domein passende proces?

+++Antwoord

Domeinovereenkomst in Experience Platform is gebaseerd op een exacte overeenkomst met de waarde van het scrubbed-domeinveld. Experience Platform verwijdert automatisch voorvoegsels (bijvoorbeeld https:/<span>/www.) en behoudt het domein op hoofdniveau (bijvoorbeeld adobe.com). Voor overeenkomende items is een exacte domeinwaarde vereist, zonder ondersteuning voor vage overeenkomsten of subdomeinen.

+++

### Waar kan ik intentgegevens gebruiken?

+++Antwoord

De intentiegegevens kunnen in [ Soorten van de Rekening ](../../../segmentation/types/account-audiences.md) worden gebruikt om het richten, segmentatie, en verpersoonlijking te verbeteren. Door het hefboomwerkings intentiesignalen, kunnen de ondernemingen zich identificeren en met rekeningen in dienst nemen die hoge interesse in specifieke onderwerpen tonen, optimaliserend marketing en verkoopoutreach.

+++
