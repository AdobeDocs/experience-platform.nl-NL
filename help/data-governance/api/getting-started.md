---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van DULE Policy Service API
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Handleiding voor ontwikkelaars van DULE Policy Service API

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste mechanisme van het Beleid van de Gegevens van het Platform van de Ervaring van Adobe. De dienst van het Beleid DULE verstrekt RESTful API die u toestaat om het beleid van het gegevensgebruik tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden genomen die met bepaalde etiketten van het gegevensgebruik zijn geëtiketteerd.

Dit document bevat instructies voor het uitvoeren van de belangrijkste bewerkingen die beschikbaar zijn in de API voor Beleidsservice. Als u dat nog niet hebt gedaan, bekijkt u eerst het overzicht [van](../home.md) gegevensbeheer om het DULE-kader te leren kennen. Voor geleidelijke instructies voor het creëren van en het handhaven van DULE beleid, zie het [DULE beleidsleerprogramma](../policies/create.md).

Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Dienst API van het Beleid te maken.

## Aan de slag met DULE Policy Service

Voordat u begint te werken met de Beleidsservice, moeten voor gegevens over het ervaringsplatform de juiste labels DULE zijn toegepast. De volledige geleidelijke instructies voor het toepassen van de etiketten van het gegevensgebruik op datasets en gebieden kunnen in de [DULE handleiding](../labels/user-guide.md)van de etikettengebruiker worden gevonden.

## Vereisten

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Gegevensbeheer](../home.md): Het framework waarmee Experience Platform naleving van gegevensgebruik afdwingt.
   * [DULE-labels](../labels/overview.md): Labels voor gegevensgebruik worden toegepast op XDM-gegevensvelden (Experience Data Model), waarbij beperkingen worden opgegeven voor de manier waarop die gegevens kunnen worden benaderd.
* [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
* [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief de bronnen die tot gegevensbeheer behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Core vs aangepaste bronnen

Binnen de API van de Dienst van het Beleid, worden alle beleid en marketing acties bedoeld als of `core` of `custom` middelen.

De `core` bronnen worden gedefinieerd en onderhouden door Adobe, terwijl `custom` bronnen worden gemaakt en onderhouden door individuele klanten en daarom uniek en zichtbaar zijn voor alleen de IMS-organisatie die ze heeft gemaakt. Als dusdanig, zijn de lijst en de raadplegingsverrichtingen (`GET`) de enige verrichtingen toegestaan op `core` middelen, terwijl de lijsten, de raadpleging en de updateverrichtingen (`POST`, `PUT`, `PATCH`, en `DELETE`) voor `custom` middelen beschikbaar zijn.

## Beleidstatus

Beleid voor gegevensgebruik kan een van de volgende drie statussen hebben: `DRAFT`, `ENABLED`, of `DISABLED`.

Door gebrek, slechts &quot;ENABLED&quot;beleid neemt aan beleidsevaluatie deel.

Het beleid van de &quot;CONCEPT&quot;kan ook in beleidsevaluatie worden overwogen, maar slechts door de vraagparameter te plaatsen `?includeDraft=true`. Meer informatie over beleidsevaluatie vindt u in het document over [beleidshandhaving](../enforcement/overview.md) aan het einde van dit document.

## Namen van marketingacties {#marketing-actions}

Namen van marketingacties zijn unieke id&#39;s voor marketingacties. Elke `core` marketingactie heeft een unieke naam die van toepassing is op alle IMS-ordes. Deze namen worden gedefinieerd en onderhouden door Adobe. Ondertussen, zijn alle klant-bepaalde marketing acties (`custom` middelen) uniek binnen uw individuele organisatie en niet zichtbaar of gedeeld met andere organisaties IMS.

De stappen voor het werken met marketing acties in de Dienst API van het Beleid worden geschetst in de sectie van de Acties [van de](#marketing-actions) Marketing later in dit document.

## Volgende stappen

Nu u de eerste kennis en de geloofsbrieven hebt, kunt u de steekproefAPI vraag blijven lezen die in deze ontwikkelaarsgids wordt verstrekt:

* [Marketingacties](marketing-actions.md)
* [Beleid](policies.md)