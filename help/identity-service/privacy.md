---
keywords: Experience Platform;home;populaire onderwerpen
title: Privacy Request-verwerking in Identity-service
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonlijke gegevens te verwijderen, zoals gedefinieerd in een groot aantal privacyregels. Dit document behandelt essentiële concepten met betrekking tot de verwerking van privacyverzoeken voor identiteitsdiensten.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Behandeling van privacyverzoek in [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang tot hun persoonsgegevens, om te weigeren deze te verkopen of om hun persoonsgegevens te verwijderen, zoals bepaald in privacyvoorschriften zoals de algemene gegevensbeschermingsverordening (GDPR), en [!DNL California Consumer Privacy Act] (CCPA).

In dit document worden de belangrijkste concepten besproken die betrekking hebben op de verwerking van verzoeken om privacy voor [!DNL Identity Service] in Adobe Experience Platform.

>[!NOTE]
>
>In deze handleiding wordt alleen uitgelegd hoe u privacyaanvragen voor de opslag van identiteitsgegevens in Experience Platform kunt indienen. Als u ook privacyverzoeken wilt indienen voor het gegevensmeer van het Platform of [!DNL Real-Time Customer Profile], raadpleegt u de handleiding op [verwerking van privacyverzoeken in het datumpigment](../catalog/privacy.md) en aan de gids [verwerking van privacyverzoeken voor profiel](../profile/privacy.md) in aanvulling op deze zelfstudie.
>
>Raadpleeg voor meer informatie over het indienen van privacyverzoeken voor andere Adobe Experience Cloud-toepassingen de [Documentatie Privacy Service](../privacy-service/experience-cloud-apps.md).

## Aan de slag

U wordt aangeraden het volgende goed te begrijpen [!DNL Experience Platform] services vóór het lezen van deze handleiding:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-Time Customer Profile]](home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] brugt de gegevens van de klantenidentiteit over systemen en apparaten. [!DNL Identity Service] gebruik **naamruimten** context te verschaffen aan identiteitswaarden door deze te koppelen aan hun systeem van oorsprong. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over naamruimten in [!DNL Experience Platform], zie de [Overzicht van naamruimte in identiteit](../identity-service/features/namespaces.md).

## Verzoeken indienen {#submit}

In de volgende secties wordt beschreven hoe u privacyverzoeken kunt indienen voor [!DNL Identity Service] met de [!DNL Privacy Service] API of UI. Voordat u deze secties leest, wordt u ten zeerste aangeraden de [Privacy Service-API](../privacy-service/api/getting-started.md) of [UI PRIVACY SERVICE](../privacy-service/ui/overview.md) documentatie voor volledige stappen over hoe te om een privacybaan voor te leggen, met inbegrip van hoe te om gebruikersgegevens in verzoek te formatteren lading.

### De API gebruiken

Bij het maken van taakaanvragen in de API, alle id&#39;s die binnen `userIDs` moet een specifieke `namespace` en `type`. Een geldige [naamruimte identity](#namespaces) erkend door [!DNL Identity Service] moet worden voorzien in `namespace` waarde, terwijl de `type` moet ofwel `standard` of `unregistered` (voor respectievelijk standaard- en aangepaste naamruimten).

Bovendien `include` array van de aanvraag payload moet de productwaarden voor de verschillende gegevensopslagruimten bevatten waarnaar de aanvraag wordt verzonden. Bij het indienen van verzoeken aan [!DNL Identity], moet de array de waarde bevatten `Identity`.

Met het volgende verzoek wordt een nieuwe privacytaak onder de GDPR gemaakt voor de gegevens van één klant in de [!DNL Identity] opslaan. Er zijn twee identiteitswaarden voor de klant in de `userIDs` array; één met de standaard `Email` naamruimte identiteit en de andere naamruimte gebruiken `ECID` namespace, omvat ook de productwaarde voor [!DNL Identity] (`Identity`) in de `include` array:

>[!TIP]
>
>Wanneer u een aangepaste naamruimte verwijdert met behulp van de API, moet u het identiteitssymbool opgeven als de naamruimte in plaats van de weergavenaam.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### UI gebruiken

>[!TIP]
>
>Wanneer u een aangepaste naamruimte verwijdert via de gebruikersinterface, moet u het identiteitssymbool opgeven als de naamruimte in plaats van de weergavenaam. Bovendien kunt u geen aangepaste naamruimten in de gebruikersinterface verwijderen voor niet-productiesandboxen.

Zorg ervoor dat u bij het maken van taakaanvragen in de gebruikersinterface **[!UICONTROL Identity]** krachtens **[!UICONTROL Products]** om taken te verwerken voor gegevens die zijn opgeslagen in [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Verzoek om verwerking verwijderen

Wanneer [!DNL Experience Platform] ontvangt een verwijderingsverzoek van [!DNL Privacy Service], [!DNL Platform] stuurt bevestiging naar [!DNL Privacy Service] dat het verzoek is ontvangen en de betrokken gegevens zijn gemarkeerd voor verwijdering. De verwijdering van de individuele identiteit is gebaseerd op de opgegeven naamruimte en/of ID-waarde. Bovendien worden alle sandboxen die bij een bepaalde organisatie horen, verwijderd.

Afhankelijk van of u ook Real-Time Klantprofiel (`ProfileService`) en het datumpeer (`aepDataLake`) als producten in uw privacyaanvraag voor identiteitsservice (`identity`), worden verschillende gegevenssets met betrekking tot de identiteit op mogelijk verschillende tijdstippen uit het systeem verwijderd:

| Producten inbegrepen | Effecten |
| --- | --- |
| `identity` alleen | De opgegeven identiteit wordt verwijderd zodra Platform de bevestiging verzendt dat het verwijderingsverzoek is ontvangen. Het profiel dat is samengesteld uit die identiteitsgrafiek blijft behouden, maar wordt niet bijgewerkt wanneer nieuwe gegevens worden ingevoerd omdat de identiteitskoppelingen nu worden verwijderd. De gegevens die aan het profiel zijn gekoppeld, blijven ook in het datumpeer staan. |
| `identity` en `ProfileService` | De opgegeven identiteit wordt verwijderd zodra Platform de bevestiging verzendt dat het verwijderingsverzoek is ontvangen. De gegevens die aan het profiel zijn gekoppeld, blijven in het datumpeer. |
| `identity` en `aepDataLake` | De opgegeven identiteit wordt verwijderd zodra Platform de bevestiging verzendt dat het verwijderingsverzoek is ontvangen. Het profiel dat is samengesteld uit die identiteitsgrafiek blijft behouden, maar wordt niet bijgewerkt wanneer nieuwe gegevens worden ingevoerd omdat de identiteitskoppelingen nu worden verwijderd.<br><br>Wanneer het gegevens meer product antwoordt dat het verzoek werd ontvangen en momenteel verwerkt, worden de gegevens verbonden aan het profiel zachte geschrapt en zijn daarom niet toegankelijk door om het even welk [!DNL Platform] service. Zodra de baan wordt voltooid, worden de gegevens volledig verwijderd uit het gegevens meer. |
| `identity`, `ProfileService`, en `aepDataLake` | De opgegeven identiteit wordt verwijderd zodra Platform de bevestiging verzendt dat het verwijderingsverzoek is ontvangen.<br><br>Wanneer het gegevens meer product antwoordt dat het verzoek werd ontvangen en momenteel verwerkt, worden de gegevens verbonden aan het profiel zachte geschrapt en zijn daarom niet toegankelijk door om het even welk [!DNL Platform] service. Zodra de baan wordt voltooid, worden de gegevens volledig verwijderd uit het gegevens meer. |

Zie de [[!DNL Privacy Service] documentatie](../privacy-service/home.md#monitor) voor meer informatie over het bijhouden van de taakstatus.

## Volgende stappen

Door dit document te lezen, hebt u kennis gemaakt met de belangrijke concepten die betrekking hebben op het verwerken van privacyverzoeken in [!DNL Identity Service]. Voor informatie over het verwerken van privacyverzoeken voor andere [!DNL Experience Cloud] toepassingen, zie het document op [[!DNL Privacy Service] en [!DNL Experience Cloud] toepassingen](../privacy-service/experience-cloud-apps.md).
