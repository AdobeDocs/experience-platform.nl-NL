---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van DULE Policy Service API
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---


# Handleiding voor DULE [!DNL Policy Service] API-ontwikkelaars

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste mechanisme van Adobe Experience Platform [!DNL Data Governance]. DULE [!DNL Policy Service] verstrekt RESTful API die u toestaat om het beleid van het gegevensgebruik tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden ondernomen die met bepaalde etiketten van het gegevensgebruik zijn geëtiketteerd.

Dit document bevat instructies voor het uitvoeren van de belangrijkste bewerkingen die beschikbaar zijn in de [!DNL Policy Service] API. Als u dat nog niet hebt gedaan, bekijkt u eerst het overzicht [van](../home.md) gegevensbeheer om het DULE-kader te leren kennen. Voor geleidelijke instructies voor het creëren van en het handhaven van DULE beleid, zie het [DULE beleidsleerprogramma](../policies/create.md).

Dit document biedt een inleiding tot de kernconcepten u moet kennen alvorens te proberen om vraag aan [!DNL Policy Service] API te maken.

## Aan de slag met DULE [!DNL Policy Service]

Voordat u met de toepassing begint te werken, [!DNL Policy Service][!DNL Experience Platform] moeten in de gegevens over de code de juiste DULE-labels zijn toegepast. De volledige geleidelijke instructies voor het toepassen van de etiketten van het gegevensgebruik op datasets en gebieden kunnen in de [DULE handleiding](../labels/user-guide.md)van de etikettengebruiker worden gevonden.

## Vereisten

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [!DNL Data Governance](../home.md): Het kader waarmee de naleving van het gegevensgebruik wordt [!DNL Experience Platform] afgedwongen.
   * [DULE-labels](../labels/overview.md): Labels voor gegevensgebruik worden toegepast op [!DNL Experience Data Model] (XDM)-gegevensvelden, waarbij beperkingen worden opgegeven voor de manier waarop die gegevens kunnen worden benaderd.
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
* [!DNL Real-time Customer Profile](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

## Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Data Governance]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Core vs aangepaste bronnen

Binnen de [!DNL Policy Service] API worden alle beleid- en marketingacties ofwel `core` ofwel `custom` bronnen genoemd.

De `core` bronnen worden gedefinieerd en onderhouden door Adobe, terwijl `custom` bronnen worden gemaakt en onderhouden door individuele klanten en daarom uniek en zichtbaar zijn voor alleen de IMS-organisatie die ze heeft gemaakt. Als dusdanig, zijn de lijst en de raadplegingsverrichtingen (`GET`) de enige verrichtingen toegestaan op `core` middelen, terwijl de lijsten, de raadpleging en de updateverrichtingen (`POST`, `PUT`, `PATCH`, en `DELETE`) voor `custom` middelen beschikbaar zijn.

## Beleidstatus

Beleid voor gegevensgebruik kan een van de volgende drie statussen hebben: `DRAFT`, `ENABLED`of `DISABLED`.

Door gebrek, slechts &quot;ENABLED&quot;beleid neemt aan beleidsevaluatie deel.

Het beleid van de &quot;CONCEPT&quot;kan ook in beleidsevaluatie worden overwogen, maar slechts door de vraagparameter te plaatsen `?includeDraft=true`. Meer informatie over beleidsevaluatie vindt u in het document over [beleidshandhaving](../enforcement/overview.md) aan het einde van dit document.

## Namen van marketingacties {#marketing-actions}

Namen van marketingacties zijn unieke id&#39;s voor marketingacties. Elke `core` marketingactie heeft een unieke naam die van toepassing is op alle IMS-ordes. Deze namen worden gedefinieerd en onderhouden door Adobe. Ondertussen, zijn alle klant-bepaalde marketing acties (`custom` middelen) uniek binnen uw individuele organisatie en niet zichtbaar of gedeeld met andere organisaties IMS.

De stappen voor het werken met marketing acties in [!DNL Policy Service] API worden beschreven in de sectie van de Acties [van de](#marketing-actions) Marketing later in dit document.

## Volgende stappen

Nu u de eerste kennis en de geloofsbrieven hebt, kunt u de steekproefAPI vraag blijven lezen die in deze ontwikkelaarsgids wordt verstrekt:

* [Marketingacties](marketing-actions.md)
* [Beleid](policies.md)