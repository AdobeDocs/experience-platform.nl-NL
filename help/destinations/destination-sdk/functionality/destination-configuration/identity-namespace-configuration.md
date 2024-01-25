---
description: Leer hoe te om de gesteunde doelidentiteiten voor bestemmingen te vormen die met Destination SDK worden gebouwd.
title: Configuratie naamruimte voor identiteit
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# Configuratie naamruimte voor identiteit

Experience Platform gebruikt naamruimten om het type van specifieke identiteiten te beschrijven. Bijvoorbeeld, een identiteitsnaamruimte genoemd `Email` geeft een vergelijkbare waarde aan `name@email.com` als e-mailadres.

Bij het maken van een bestemming via Destination SDK, naast [het vormen van een partnerschema](schema-configuration.md) dat de gebruikers profielattributen en identiteiten aan kunnen in kaart brengen, kunt u identiteitsnamespaces ook bepalen die door uw bestemmingsplatform worden gesteund.

Wanneer u dit doet, kunnen gebruikers naast de kenmerken van het doelprofiel ook doelidentiteiten selecteren.

Voor meer informatie over naamruimten in Experience Platform raadpleegt u de [documentatie over naamruimten](../../../../identity-service/features/namespaces.md).

Wanneer het vormen van identiteitsnamespaces voor uw bestemming, kunt u de afbeelding van de doelidentiteit verfijnen die door uw bestemming wordt gesteund, zoals:

* Gebruikers toestaan XDM-kenmerken toe te wijzen aan naamruimten.
* Toestaan dat gebruikers een kaart maken [standaardnaamruimten](../../../../identity-service/features/namespaces.md#standard) naar uw eigen naamruimten.
* Toestaan dat gebruikers een kaart maken [aangepaste naamruimten](../../../../identity-service/features/namespaces.md#manage-namespaces) naar uw eigen naamruimten.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of bekijk de gids over hoe te [gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

U kunt uw ondersteunde naamruimten configureren via het dialoogvenster `/authoring/destinations` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde configuratieopties voor naamruimten beschreven die u voor uw bestemming kunt gebruiken, en wordt getoond welke klanten in de interface van het platform zullen zien.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde parameters {#supported-parameters}

Wanneer het bepalen van de doelidentiteiten die uw bestemming steunt, kunt u de parameters gebruiken die in de lijst worden beschreven hieronder om hun gedrag te vormen.

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---------|----------|---|------|
| `acceptsAttributes` | Boolean | Optioneel | Geeft aan of klanten standaardprofielkenmerken kunnen toewijzen aan de identiteit die u configureert. |
| `acceptsCustomNamespaces` | Boolean | Optioneel | Geeft aan of klanten aangepaste naamruimten kunnen toewijzen aan de naamruimte van de identiteit die u configureert. |
| `acceptedGlobalNamespaces` | - | Optioneel | Geeft aan welke [standaardnaamruimten](../../../../identity-service/features/namespaces.md#standard) (bijvoorbeeld [!UICONTROL IDFA]) kunnen klanten toewijzen aan de identiteit die u configureert. |
| `transformation` | String | Optioneel | Hiermee geeft u het dialoogvenster [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) Schakel het selectievakje in in de interface van het platform wanneer het bronveld een XDM-kenmerk of een naamruimte voor een aangepaste identiteit is. Gebruik deze optie om gebruikers de mogelijkheid te geven bronkenmerken bij het exporteren te hashen. Als u deze optie wilt inschakelen, stelt u de waarde in op `sha256(lower($))`. |
| `requiredTransformation` | String | Optioneel | Wanneer klanten deze naamruimte voor de bronidentiteit selecteren, [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) schakelt u deze optie automatisch in op de toewijzing en klanten kunnen deze niet uitschakelen. Als u deze optie wilt inschakelen, stelt u de waarde in op `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

U moet aangeven welke [!DNL Platform] id&#39;s die klanten kunnen exporteren naar uw bestemming. Enkele voorbeelden zijn [!DNL Experience Cloud ID], gehashte e-mail, apparaat-id ([!DNL IDFA], [!DNL GAID]). Deze waarden zijn [!DNL Platform] identiteitsnaamruimten die klanten vanaf uw bestemming kunnen toewijzen aan naamruimten.

Naamruimten vereisen geen 1-op-1-overeenkomst tussen [!DNL Platform] en uw bestemming.
Klanten kunnen bijvoorbeeld een [!DNL Platform] [!DNL IDFA] naamruimte naar een [!DNL IDFA] naamruimte vanaf uw bestemming, of ze kunnen hetzelfde toewijzen [!DNL Platform] [!DNL IDFA] naamruimte naar een [!DNL Customer ID] naamruimte in uw doel.

Meer informatie over identiteiten in het dialoogvenster [Overzicht van naamruimte in identiteit](../../../../identity-service/features/namespaces.md).

## Toewijzingsoverwegingen

Als klanten een naamruimte voor de bronidentiteit selecteren en geen doeltoewijzing selecteren, wordt de doeltoewijzing automatisch ingevuld met een kenmerk met dezelfde naam.

## Optionele hashing voor bronvelden configureren

Klanten van Experience Platforms kunnen ervoor kiezen om gegevens in te voeren in Platform met hashing of in onbewerkte tekst. Als uw bestemmingsplatform zowel gehakt als unhashed gegevens goedkeurt, kunt u klanten de optie geven om te kiezen of Platform de waarden van brongebieden zou moeten hakken wanneer zij worden uitgevoerd naar uw bestemming.

De onderstaande configuratie maakt de optionele [Transformatie toepassen](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) in de UI van het Platform, in de stap van de Afbeelding.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Schakel deze optie in als u niet-gehashte bronvelden gebruikt, zodat Adobe Experience Platform deze automatisch verbergt bij activering.

Wanneer u ongehashte bronkenmerken toewijst aan doelkenmerken die de bestemming verwacht te worden gehasht (bijvoorbeeld: `email_lc_sha256` of `phone_sha256`), controleert u **Transformatie toepassen** als u wilt dat Adobe Experience Platform de bronkenmerken bij activering automatisch hasht.

## Verplichte hash voor bronvelden configureren

Als uw bestemming slechts gehakte gegevens goedkeurt, kunt u de uitgevoerde attributen vormen om automatisch door Platform worden gehakt. De onderstaande configuratie controleert automatisch de **Transformatie toepassen** als de `Email` en `Phone` identiteiten worden toegewezen.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe te om uw identiteit namespaces voor bestemmingen te vormen die met Destination SDK worden gebouwd.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Verificatie door klant](customer-authentication.md)
* [OAuth2-vergunning](oauth2-authorization.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)
