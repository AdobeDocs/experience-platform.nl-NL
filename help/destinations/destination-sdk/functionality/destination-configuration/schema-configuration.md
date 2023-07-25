---
description: Leer hoe te om het partnerschema voor bestemmingen te vormen die met Destination SDK worden gebouwd.
title: Configuratie partnerschema
source-git-commit: ca4fb2dce097197aa1a97e0716e6294546bfee38
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 1%

---


# Configuratie partnerschema

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Wanneer het gegeven in Platform wordt opgenomen, is het gestructureerd volgens een schema XDM. Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie [grondbeginselen van de schemacompositie](../../../../xdm/schema/composition.md).

Wanneer het bouwen van een bestemming met Destination SDK, kunt u uw eigen partnerschema bepalen dat door uw bestemmingsplatform moet worden gebruikt. Dit geeft gebruikers de capaciteit om profielattributen van Platform aan specifieke gebieden in kaart te brengen die uw bestemmingsplatform, allen binnen Platform UI herkent.

Wanneer het vormen van het partnerschema voor uw bestemming, kunt u de gebiedstoewijzing verfijnen die door uw bestemmingsplatform wordt gesteund, zoals:

* Gebruikers toestaan een kaart toe te wijzen `phoneNumber` XDM-kenmerk naar een `phone` door het doelplatform wordt ondersteund.
* Creeer dynamische partnerschema&#39;s die het Experience Platform kan dynamisch roepen om een lijst van alle gesteunde attributen binnen uw bestemming terug te winnen.
* Geef verplichte veldtoewijzingen op die uw doelplatform nodig heeft.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of bekijk de gids over hoe te [gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

U kunt uw schema-instellingen configureren via de `/authoring/destinations` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

Dit artikel beschrijft alle gesteunde opties van de schemaconfiguratie die u voor uw bestemming kunt gebruiken, en toont welke klanten in de Platform UI zullen zien.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde schemaconfiguratie {#supported-schema-types}

Destination SDK ondersteunt meerdere schemaconfiguraties:

* Statische schema&#39;s worden gedefinieerd door de `profileFields` in de `schemaConfig` sectie. In een statisch schema, bepaalt u elk doelattribuut dat in het Experience Platform UI in zou moeten worden getoond `profileFields` array. Als u uw schema moet bijwerken, moet u [de doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Dynamische schema&#39;s gebruiken een extra type van bestemmingsserver, genoemd een [dynamische schema-server](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), om de ondersteunde doelkenmerken dynamisch op te halen en schema&#39;s te genereren op basis van uw eigen API. Dynamische schema&#39;s gebruiken niet de `profileFields` array. Als u uw schema moet bijwerken, is het niet nodig om [de doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md). In plaats daarvan haalt de dynamische schemaserver het bijgewerkte schema van uw API terug.
* Binnen de schemaconfiguratie, hebt u de optie om vereiste (of vooraf bepaalde) afbeeldingen toe te voegen. Dit zijn afbeeldingen die gebruikers kunnen weergeven in de gebruikersinterface van het Platform, maar ze kunnen deze niet wijzigen wanneer ze een verbinding met uw doel instellen. U kunt bijvoorbeeld afdwingen dat het veld E-mailadres altijd naar de bestemming wordt verzonden.

De `schemaConfig` de sectie gebruikt veelvoudige configuratieparameters, afhankelijk van het type van schema dat u, zoals aangetoond in de hieronder secties nodig hebt.

## Een statisch schema maken {#attributes-schema}

Als u een statisch schema met profielkenmerken wilt maken, definieert u de doelkenmerken in het dialoogvenster `profileFields` array, zoals hieronder weergegeven.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---------|----------|------|---|
| `profileFields` | Array | Optioneel | Definieert de array met doelkenmerken die door het doelplatform worden geaccepteerd en waaraan klanten hun profielkenmerken kunnen toewijzen. Wanneer u een `profileFields` -array, u kunt de `useCustomerSchemaForAttributeMapping` parameter volledig. |
| `useCustomerSchemaForAttributeMapping` | Boolean | Optioneel | Hiermee schakelt u het toewijzen van kenmerken vanuit het klantschema in of uit op de kenmerken die u in het dialoogvenster `profileFields` array. <ul><li>Indien ingesteld op `true`, zien gebruikers alleen de bronkolom in het toewijzingsveld. `profileFields` zijn in dit geval niet van toepassing.</li><li>Indien ingesteld op `false`, kunnen gebruikers bronkenmerken vanuit hun schema toewijzen aan de kenmerken die u in het dialoogvenster `profileFields` array.</li></ul> De standaardwaarde is `false`. |
| `profileRequired` | Boolean | Optioneel | Gebruiken `true` als gebruikers de profielkenmerken van het Experience Platform aan douanekenmerken op uw bestemmingsplatform zouden moeten kunnen in kaart brengen. |
| `segmentRequired` | Boolean | Vereist | Deze parameter wordt vereist door Destination SDK en moet altijd worden ingesteld op `true`. |
| `identityRequired` | Boolean | Vereist | Instellen op `true` als gebruikers in staat moeten zijn om een kaart te maken [identiteitstypen](identity-namespace-configuration.md) van Experience Platform naar de kenmerken die u in het dialoogvenster `profileFields` array. |
| `segmentNamespaceAllowList` | Array | Optioneel | Hiermee definieert u specifieke publieksnaamruimten waaruit gebruikers doelgroepen kunnen toewijzen. Gebruik deze parameter om gebruikers van het Platform te beperken om publiek uit slechts de publieksnamespaces uit te voeren die u in de serie bepaalt. Deze parameter kan niet samen met `segmentNamespaceDenyList`.<br> <br> Voorbeeld: `"segmentNamespaceAllowList": ["AudienceManager"]` Hiermee kunnen gebruikers alleen publiek toewijzen vanuit de `AudienceManager` naamruimte naar dit doel. <br> <br> Om gebruikers toe te staan om het even welk publiek naar uw bestemming uit te voeren, kunt u deze parameter negeren. <br> <br> Als beide `segmentNamespaceAllowList` en `segmentNamespaceDenyList` ontbreken in uw configuratie, kunnen de gebruikers slechts publiek uitvoeren dat uit van [Segmenteringsservice](../../../../segmentation/home.md). |
| `segmentNamespaceDenyList` | Array | Optioneel | Beperkt gebruikers van het in kaart brengen van publiek aan de bestemming, van de publieksnamespaces die in de serie worden bepaald. Kan niet samen met `segmentNamespaceAllowed`. <br> <br> Voorbeeld: `"segmentNamespaceDenyList": ["AudienceManager"]` blokkeert gebruikers om het publiek van de `AudienceManager` naamruimte naar dit doel. <br> <br> Om gebruikers toe te staan om het even welk publiek naar uw bestemming uit te voeren, kunt u deze parameter negeren. <br> <br> Als beide `segmentNamespaceAllowed` en `segmentNamespaceDenyList` ontbreken in uw configuratie, kunnen de gebruikers slechts publiek uitvoeren dat uit van [Segmenteringsservice](../../../../segmentation/home.md). <br> <br> Om de uitvoer van alle soorten publiek mogelijk te maken, ongeacht de oorsprong, stelt u `"segmentNamespaceDenyList":[]`. |

{style="table-layout:auto"}

De resulterende ervaring met de gebruikersinterface wordt weergegeven in de onderstaande afbeeldingen.

Wanneer gebruikers de doeltoewijzing selecteren, kunnen ze de velden zien die zijn gedefinieerd in het dialoogvenster `profileFields` array.

![UI-afbeelding die het scherm met doelkenmerken weergeeft.](../../assets/functionality/destination-configuration/select-attributes.png)

Na het selecteren van de attributen, kunnen zij hen in de kolom van het doelgebied zien.

![UI-afbeelding die een statisch doelschema met kenmerken weergeeft](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Een dynamisch schema maken {#dynamic-schema-configuration}

Destination SDK steunt de verwezenlijking van dynamische partnerschema&#39;s. In tegenstelling tot een statisch schema, gebruikt een dynamisch schema geen `profileFields` array. In plaats daarvan gebruiken dynamische schema&#39;s een dynamische schemaserver die met uw eigen API verbindt van waar het de schemaconfiguratie terugwint.

>[!IMPORTANT]
>
>Voordat u een dynamisch schema maakt, moet u [een dynamische schemaserver maken](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

In een dynamische schemeconfiguratie, `profileFields` array wordt vervangen door de `dynamicSchemaConfig` zoals hieronder weergegeven.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | Tekenreeks | Vereist | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich bij uw systeem via om het even welke beschreven authentificatiemethodes aanmelden [hier](customer-authentication.md). </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u [een object met referenties maken](../../credentials-api/create-credential-configuration.md) met de Credentials API. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `dynamicEnum.destinationServerId` | Tekenreeks | Vereist | De `instanceId` van uw dynamische schemaserver. Deze bestemmingsserver omvat het API eindpunt dat het Experience Platform zal roepen om het dynamische schema terug te winnen. |
| `dynamicEnum.value` | Tekenreeks | Vereist | De naam van het dynamische schema, zoals die in de dynamische configuratie van de schemaserver wordt bepaald. |
| `dynamicEnum.responseFormat` | Tekenreeks | Vereist | Altijd instellen op `SCHEMA` bij het definiëren van een dynamisch schema. |
| `profileRequired` | Boolean | Optioneel | Gebruiken `true` als gebruikers de profielkenmerken van het Experience Platform aan douanekenmerken op uw bestemmingsplatform zouden moeten kunnen in kaart brengen. |
| `segmentRequired` | Boolean | Vereist | Deze parameter wordt vereist door Destination SDK en moet altijd worden ingesteld op `true`. |
| `identityRequired` | Boolean | Vereist | Instellen op `true` als gebruikers in staat moeten zijn om een kaart te maken [identiteitstypen](identity-namespace-configuration.md) van Experience Platform naar de kenmerken die u in het dialoogvenster `profileFields` array. |

{style="table-layout:auto"}

## Vereiste toewijzingen {#required-mappings}

Binnen de schemaconfiguratie, naast uw statisch of dynamisch schema, hebt u de optie om vereiste (of vooraf bepaalde) afbeeldingen toe te voegen. Dit zijn afbeeldingen die gebruikers kunnen weergeven in de gebruikersinterface van het Platform, maar ze kunnen deze niet wijzigen wanneer ze een verbinding met uw doel instellen.

U kunt bijvoorbeeld afdwingen dat het veld E-mailadres altijd naar de bestemming wordt verzonden.

>[!NOTE]
>
>De volgende combinaties van vereiste toewijzingen worden momenteel ondersteund:
>* U kunt een vereist brongebied en een vereist bestemmingsgebied vormen. In dit geval kunnen gebruikers geen van de twee velden bewerken of selecteren en alleen de selectie weergeven.
>* U kunt een vereist bestemmingsgebied slechts vormen. In dit geval kunnen gebruikers een bronveld selecteren om toe te wijzen aan het doel.
>
> Alleen een vereist bronveld configureren is momenteel *niet* ondersteund.

Zie onder twee voorbeelden van een schemaconfiguratie met vereiste afbeeldingen en hoe deze in de afbeeldingsstap van het [gegevens activeren naar workflow voor batchdoelen](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Vereiste bron- en bestemmingstoewijzingen]

In het onderstaande voorbeeld ziet u zowel de vereiste bron- als doeltoewijzingen. Wanneer zowel bron- als doelvelden als vereiste toewijzingen zijn opgegeven, kunnen gebruikers geen van de twee velden selecteren of bewerken en alleen de vooraf gedefinieerde selectie weergeven.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---|---|---|---|
| `requiredMappingsOnly` | Boolean | Optioneel | Wanneer deze waarde is ingesteld op true, kunnen gebruikers geen andere kenmerken en identiteiten in de activeringsflow toewijzen, behalve de vereiste toewijzingen die u in het dialoogvenster `requiredMappings` array. |
| `requiredMappings.sourceType` | Tekenreeks | Vereist | Geeft het type van de `source` veld. Ondersteunde waarden: <ul><li>`text/x.schema-path`: Gebruik deze waarde als de `source` field is een profielkenmerk van een XDM-schema.</li><li>`text/x.aep-xl`: Gebruik deze waarde als uw `source` Veld wordt gedefinieerd door een reguliere expressie. Voorbeeld: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Gebruik deze waarde als uw `source` veld wordt gedefinieerd door een macrosjabloon. Momenteel is de enige ondersteunde macrosjabloon `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Tekenreeks | Vereist | Hiermee wordt de waarde van het bronveld aangegeven. Ondersteunde waardetypen: <ul><li>XDM-profielkenmerken. Voorbeeld: `personalEmail.address`. Wanneer uw bronattribuut een XDM profielattribuut is, plaats `sourceType` parameter to `text/x.schema-path`.</li><li>Reguliere expressies. Voorbeeld: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Wanneer uw bronattribuut een regelmatige uitdrukking is, plaats `sourceType` parameter to `text/x.aep-xl`.</li><li>Macrosjablonen. Voorbeeld:`metadata.segment.alias`. Wanneer uw bronattribuut een macromalplaatje is, plaats `sourceType` parameter to `text/plain`. Momenteel is de enige ondersteunde macrosjabloon `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Tekenreeks | Vereist | Hiermee wordt de waarde van het doelveld aangegeven. Wanneer zowel bron- als doelvelden als vereiste toewijzingen zijn opgegeven, kunnen gebruikers geen van de twee velden selecteren of bewerken en alleen de selectie weergeven. |

{style="table-layout:auto"}

Als gevolg hiervan **[!UICONTROL Source field]** en **[!UICONTROL Target field]** secties in de gebruikersinterface van het Platform worden grijs weergegeven.

![Afbeelding van de vereiste toewijzingen in de activeringsstroom van de gebruikersinterface.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Vereiste bestemmingstoewijzing]

In het onderstaande voorbeeld ziet u een vereiste doeltoewijzing. Als alleen het doelveld naar wens is opgegeven, kunnen gebruikers selecteren welk bronveld ernaar moet worden toegewezen.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---|---|---|---|
| `requiredMappingsOnly` | Boolean | Optioneel | Wanneer deze waarde is ingesteld op true, kunnen gebruikers geen andere kenmerken en identiteiten in de activeringsflow toewijzen, behalve de vereiste toewijzingen die u in het dialoogvenster `requiredMappings` array. |
| `requiredMappings.destination` | Tekenreeks | Vereist | Hiermee wordt de waarde van het doelveld aangegeven. Wanneer alleen het doelveld wordt opgegeven, kunnen gebruikers een bronveld selecteren om toe te wijzen aan het doel. |
| `mandatoryRequired` | Boolean | Optioneel | Geeft aan of de toewijzing moet worden gemarkeerd als een [mandatory, kenmerk](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Boolean | Optioneel | Geeft aan of de toewijzing moet worden gemarkeerd als een [deduplicatiesleutel](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Als gevolg hiervan **[!UICONTROL Target field]** in de gebruikersinterface van het Platform wordt grijs weergegeven, terwijl de **[!UICONTROL Source field]** is actief en kunnen gebruikers ermee werken. De **[!UICONTROL Mandatory key]** en **[!UICONTROL Deduplication key]** zijn actief en gebruikers kunnen deze niet wijzigen.

![Afbeelding van de vereiste toewijzingen in de activeringsstroom van de gebruikersinterface.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u beter inzicht moeten hebben in welke schematypen door Destination SDK worden gesteund en hoe u uw schema kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Verificatie door klant](customer-authentication.md)
* [OAuth2-verificatie](oauth2-authentication.md)
* [UI-kenmerken](ui-attributes.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [Configuratie naamruimte identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)