---
title: Demandbase-intentie
description: Meer informatie over de Demandbase Intent-bron op Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: 78aae71ff48fc710aaaabf4ef71f6e50d2a8c12e
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 0%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] is een op account gebaseerd marketingplatform dat u kunt gebruiken voor B2B-verkoop en -marketing. [!DNL Demandbase Intent] is een Adobe Experience Platform-bron die u kunt gebruiken om uw [!DNL Demandbase] -account te verbinden met Experience Platform en uw gegevens over uw accountintenties te integreren.

Met de [!DNL Demandbase] -bron kunt u rentedragende accounts identificeren op basis van realtime-overeenkomsten. Door aan de sterkste intentsignalen voorrang te geven, kunt u nauwkeurige segmenten tot stand brengen en hyper-gerichte campagnes leveren, ervoor zorgen dat uw marketing inspanningen zich op de rekeningen concentreren die het meest waarschijnlijk zullen omzetten. Door het activeren van intentieverklarende strategieën kunt u uw uitgaven optimaliseren, de betrokkenheid verhogen en het rendement op investeringen verhogen.

Lees dit document voor noodzakelijke informatie over de [!DNL Demandbase] bron.

## Vereisten {#prerequisites}

Lees de volgende secties voor de stappen die u in de eerste plaats moet uitvoeren voordat u [!DNL Demandbase] verbindt met Experience Platform.

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het nalaten om uw gebied-specifieke IP adressen aan uw lijst van gewenste personen toe te voegen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [ IP pagina van de lijst van gewenste personen van het adres ](../../ip-address-allow-list.md) voor meer informatie.

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Demandbase] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/abac/ui/permissions.md).

### Naamgevingsbeperkingen voor bestanden en mappen

Met de onderstaande beperkingen moet rekening worden gehouden bij de naamgeving van uw cloudopslagbestand of -map:

* Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
* De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
* De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
* De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
* Ongeldige URL-padtekens zijn niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
* De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

### Vereiste referenties verzamelen

[!DNL Demandbase] op Experience Platform wordt gehost door [!DNL Google Cloud Storage] . Als u uw [!DNL Demandbase] -account wilt verifiëren, moet u de juiste waarden opgeven voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoets-id | De toegangssleutel-id van [!DNL Demandbase] . Dit is een alfanumerieke tekenreeks van 61 tekens die vereist is om uw account bij Experience Platform te verifiëren. |
| Geheim toegangssleutel | De sleutel voor toegang tot het [!DNL Demandbase] -geheim. Dit is een tekenreeks van 40 tekens met een basiscodering van 64 tekens die vereist is om uw account bij Experience Platform te verifiëren. |
| Naam van emmertje | Het [!DNL Demandbase] emmertje waaruit gegevens worden opgehaald. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. |

Voor meer informatie over deze geloofsbrieven, leest de [[!DNL Google Cloud Storage]  handleiding van de sleutels HMAC ](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Voor stappen op hoe te om uw eigen toegangssleutel te produceren, lees de [ in de eerste plaats vereiste gids in het  [!DNL Google Cloud Storage]  bronoverzicht ](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## [!DNL Demandbase] schema

Lees deze sectie voor informatie over het schema en de gegevensstructuur van [!DNL Demandbase] .

Het [!DNL Demandbase] schema wordt genoemd {de Intentie van het 1} Bedrijf Wekelijks **.** Het is de wekelijkse intentinformatie (anonieme B2B-kopersonderzoek en inhoudsverbruik) voor opgegeven account en trefwoorden. De gegevens hebben de parketindeling.

| Veldnaam | Datatype | Vereist | Zakelijke sleutel | Notities |
| --- | --- | --- | --- | --- |
| `company_id` | TEKENREEKS | TRUE | JA | De canonieke bedrijfs-id. |
| `domain` | TEKENREEKS | TRUE | JA | Het geïdentificeerde domein van de rekening die intent toont. |
| `start_date` | DATE | TRUE | JA | De begindatum van het tijdstip waarop de activiteit van de intentie zich in de periode voordeed. |
| `end_date` | DATE | TRUE | JA | De einddatum van het tijdstip waarop de activiteit van de intentie zich tijdens de periode heeft voorgedaan. |
| `duration_type` | TEKENREEKS | TRUE | JA | Het type duur. In het algemeen kan deze waarde dagelijks, wekelijks of maandelijks zijn, afhankelijk van de gekozen roll-up duur. Voor dit gegevensvoorbeeld is deze waarde `week` . |
| `keyword_set_id` | TEKENREEKS | TRUE | JA | De trefwoordenset-id. Dit is uniek per bepaalde klant. |
| `keyword_set` | TEKENREEKS | TRUE | JA | De naam van de trefwoordset. |
| `is_trending` | TEKENREEKS | TRUE | | De huidige toestand van een bepaalde trend. De trendstaat wordt gemeten als een uitbarsting van de intentactiviteit in de laatste week ten opzichte van gemiddelden in de voorafgaande zeven weken. |
| `intent_strength` | ENUM [ TEKENREEKS ] | TRUE | | Een gekwantificeerde maat van de sterkte van de intentie. Tot de geaccepteerde waarden behoren: `HIGH`, `MED` en `LOW` . |
| `num_people_researching` | INTEGER | TRUE | | Het aantal personen dat in de afgelopen zeven dagen tot het trefwoord `company_id` behoort dat het trefwoord onderzoekt. |
| `num_trending_days` | INTEGER | TRUE | | Het aantal dagen dat het trefwoord in een bepaalde periode trending. |
| `trending_score` | INTEGER | TRUE | | De trending score. |
| `record_id` | TEKENREEKS | TRUE | | De unieke primaire record-id. |
| `partition_date` | DATE | TRUE | | De kalenderdatum van de momentopname. Dit gebeurt wekelijks, aan het einde van de week. |

{style="table-layout:auto"}

>[!TIP]
>
>Wijzigingen in het schema worden vooraf aan Adobe meegedeeld. Om naadloze schemaevolutie te steunen, is het handhaven van achterwaartse verenigbaarheid essentieel. Experience Platform past een benadering met alleen additieve versies toe en zorgt ervoor dat updates van het schema niet-destructief zijn. Dit betekent dat het doorbreken van veranderingen strikt worden verboden, en slechts veranderingen die het bestaande schema verbeteren of uitbreiden worden toegestaan.

## Sluit uw [!DNL Demandbase] -account aan op Experience Platform in de gebruikersinterface

Zodra u uw in de eerste plaats vereiste opstelling hebt voltooid, lees het leerprogramma op [ verbindend uw  [!DNL Demandbase]  rekening met Experience Platform ](../../tutorials/ui/create/data-partners/demandbase.md) om uw integratie te beginnen.

## Veelgestelde vragen {#faq}

Lees deze sectie voor antwoorden op veelgestelde vragen over de [!DNL Demandbase] bron.

### Moet ik een bestaand contract met [!DNL Demandbase] hebben om hun gegevens van de rekeningintentie in Real-Time CDP B2B edition te gebruiken?

+++Antwoord

Ja, u moet een actief contract hebben met [!DNL Demandbase] om hun intentgegevens binnen Experience Platform en Real-Time CDP B2B edition te openen en te gebruiken. De integratie maakt gebruik van uw bestaande overeenkomst met de [!DNL Demandbase] om accountintentsignalen in Experience Platform en Real-Time CDP in te voeren en te activeren.

+++

### Worden aangepaste velden van [!DNL Demandbase] ondersteund in deze integratie?

+++Antwoord

U kunt op dit moment alleen standaard [!DNL Demandbase] -velden gebruiken voor inname en activering. Om de lijst van gesteunde gebieden te bekijken, lees de [[!DNL Demandbase]  schemagids ](#schema) voor de details op gebiedsbeschikbaarheid.

+++

### Kan ik ad-hocgegevens van [!DNL Demandbase] naar Experience Platform invoeren?

+++Antwoord

Ja, u kunt ad-hocgegevens van [!DNL Demandbase] invoeren. U kunt een nieuwe gegevensstroom creëren om de recentste intentgegevens in te voeren, zolang er nieuwe gegevens van [!DNL Demandbase] zijn. U kunt echter slechts één actieve gegevensstroom tegelijk hebben. Zorg daarom dat u de bestaande gegevensstroom verwijdert voordat u een nieuwe maakt.

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

### Welk veld wordt gebruikt om accounts van [!DNL Demandbase] aan Experience Platform aan te passen?

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

De intentiegegevens kunnen in [ Soorten van de Rekening ](../../../segmentation/types/account-audiences.md) worden gebruikt om het richten, segmentatie, en verpersoonlijking te verbeteren. Door intentiesignalen leveraging, kunnen de ondernemingen zich identificeren en met rekeningen in dienst nemen die hoge interesse in specifieke onderwerpen tonen, optimaliserend marketing en verkoopverbetering

+++
