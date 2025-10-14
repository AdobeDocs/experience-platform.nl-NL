---
description: Leer hoe u de ondersteunde doel-id's configureert voor doelen die met Destination SDK zijn gebouwd.
title: Configuratie naamruimte voor identiteit
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Configuratie naamruimte voor identiteit

Experience Platform gebruikt naamruimten om het type van specifieke identiteiten te beschrijven. Een naamruimte voor identiteiten met de naam `Email` identificeert bijvoorbeeld een waarde zoals `name@email.com` als een e-mailadres.

Houd, afhankelijk van het type doel dat u maakt (streaming of op bestand gebaseerd), rekening met de volgende vereisten voor naamruimte voor identiteiten:

* Wanneer het creëren van bestemmingen in real time (het stromen) door Destination SDK, naast [&#x200B; vormend een partnerschema &#x200B;](schema-configuration.md) waaraan de gebruikers profielattributen en identiteiten kunnen in kaart brengen, moet u *minstens één* identiteitsnamespaces ook bepalen die door uw bestemmingsplatform wordt gesteund. Bijvoorbeeld, als uw bestemmingsplatform gehakt e-mail en [!DNL IDFA] goedkeurt, moet u deze twee identiteiten bepalen zoals [&#x200B; verder in dit document &#x200B;](#supported-parameters) wordt beschreven.

  >[!IMPORTANT]
  >
  >Wanneer het activeren van publiek aan het stromen bestemmingen, moeten de gebruikers _minstens één doelidentiteit_, naast de attributen van het doelprofiel ook in kaart brengen. Anders wordt het publiek niet geactiveerd naar het doelplatform.

* Wanneer het creëren van op dossier-gebaseerde bestemmingen door Destination SDK, is de configuratie van identiteit namespaces facultatief __.

Meer over identiteit namespaces in Experience Platform leren, zie de [&#x200B; documentatie van identiteitsnaamruimten &#x200B;](../../../../identity-service/features/namespaces.md).

Wanneer het vormen van identiteitsnamespaces voor uw bestemming, kunt u de afbeelding van de doelidentiteit verfijnen die door uw bestemming wordt gesteund, zoals:

* Gebruikers toestaan XDM-kenmerken toe te wijzen aan naamruimten.
* Toestaan van gebruikers om [&#x200B; standaardidentiteitsnamespaces &#x200B;](../../../../identity-service/features/namespaces.md#standard) aan uw eigen identiteitsnaamruimten in kaart te brengen.
* Toestaan van gebruikers om [&#x200B; naamruimten van de douanetechniek &#x200B;](../../../../identity-service/features/namespaces.md#manage-namespaces) aan uw eigen identiteitsnaamruimten in kaart te brengen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [&#x200B; configuratieopties &#x200B;](../configuration-options.md) documentatie of zie de gids op hoe te [&#x200B; Destination SDK gebruiken om een op dossier-gebaseerde bestemming &#x200B;](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration) te vormen.

U kunt ondersteunde naamruimten configureren via het `/authoring/destinations` -eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde configuratieopties voor naamruimten beschreven die u voor uw doel kunt gebruiken, en wordt aangegeven welke klanten in de gebruikersinterface van Experience Platform zullen zien.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja (vereist) |
| Op bestanden gebaseerde (batch) integratie | Ja (optioneel) |

## Ondersteunde parameters {#supported-parameters}

Wanneer het bepalen van de doelidentiteiten die uw bestemming steunt, kunt u de parameters gebruiken die in de lijst worden beschreven hieronder om hun gedrag te vormen.

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---------|----------|---|------|
| `acceptsAttributes` | Boolean | Optioneel | Geeft aan of klanten standaardprofielkenmerken kunnen toewijzen aan de identiteit die u configureert. |
| `acceptsCustomNamespaces` | Boolean | Optioneel | Geeft aan of klanten aangepaste naamruimten kunnen toewijzen aan de naamruimte van de identiteit die u configureert. |
| `acceptedGlobalNamespaces` | - | Optioneel | Wijst op welke [&#x200B; standaardidentiteitsnamespaces &#x200B;](../../../../identity-service/features/namespaces.md#standard) (bijvoorbeeld, [!UICONTROL IDFA]) klanten aan de identiteit kunnen in kaart brengen die u vormt. |
| `transformation` | String | Optioneel | Hiermee wordt het selectievakje [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) weergegeven in de gebruikersinterface van Experience Platform wanneer het bronveld een XDM-kenmerk of een naamruimte voor een aangepaste identiteit is. Gebruik deze optie om gebruikers de mogelijkheid te geven bronkenmerken bij het exporteren te hashen. Als u deze optie wilt inschakelen, stelt u de waarde in op `sha256(lower($))` . |
| `requiredTransformation` | String | Optioneel | Wanneer klanten deze naamruimte voor de bronidentiteit selecteren, wordt het selectievakje [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) automatisch toegepast op de toewijzing en kunnen klanten deze naamruimte niet uitschakelen. Als u deze optie wilt inschakelen, stelt u de waarde in op `sha256(lower($))` . |

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

U moet aangeven welke [!DNL Experience Platform] -identiteiten klanten kunnen exporteren naar uw doel. Enkele voorbeelden zijn [!DNL Experience Cloud ID] , gehashte e-mail, apparaat-id ([!DNL IDFA], [!DNL GAID] ). Deze waarden zijn [!DNL Experience Platform] naamruimten die klanten vanaf hun bestemming kunnen toewijzen aan naamruimten.

Naamruimten vereisen geen 1-op-1 overeenkomst tussen [!DNL Experience Platform] en uw doel.
Klanten kunnen bijvoorbeeld een naamruimte [!DNL Experience Platform] [!DNL IDFA] aan een naamruimte [!DNL IDFA] toewijzen vanuit uw doel, of ze kunnen dezelfde naamruimte [!DNL Experience Platform] [!DNL IDFA] toewijzen aan een naamruimte [!DNL Customer ID] in uw doel.

Lees meer over identiteiten in het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../../../../identity-service/features/namespaces.md).

## Toewijzingsoverwegingen

Als klanten een naamruimte voor de bronidentiteit selecteren en geen doeltoewijzing selecteren, vult Experience Platform automatisch de doeltoewijzing met een attribuut met dezelfde naam in.

## Optionele hashing voor bronvelden configureren

Experience Platform-klanten kunnen ervoor kiezen om gegevens in te voeren in Experience Platform met een hashing-indeling of in onbewerkte tekst. Als uw bestemmingsplatform zowel gehakt als unhashed gegevens goedkeurt, kunt u klanten de optie geven om te kiezen of Experience Platform de waarden van de brongebieden zou moeten hakken wanneer zij naar uw bestemming worden uitgevoerd.

De configuratie hieronder laat facultatieve [&#x200B; toe past transformatie &#x200B;](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) optie in Experience Platform UI, in de stap van de Afbeelding toe.

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

Wanneer u ongehakte bronattributen aan doelattributen in kaart brengt die de bestemming (bijvoorbeeld: `email_lc_sha256` of `phone_sha256`) verwacht worden gehakt, controleer **transformatie** optie toepassen om Adobe Experience Platform automatisch te hebben de bronattributen bij activering hakt.

## Verplichte hash voor bronvelden configureren

Als uw bestemming slechts gehakte gegevens goedkeurt, kunt u de uitgevoerde attributen vormen om automatisch gehakt te worden door Experience Platform. De configuratie hieronder controleert automatisch **transformatie** optie toepassen wanneer de `Email` en `Phone` identiteiten in kaart worden gebracht.

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

Na het lezen van dit artikel, zou u beter inzicht in moeten hebben hoe te om uw identiteit namespaces voor bestemmingen te vormen die met Destination SDK worden gebouwd.

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
