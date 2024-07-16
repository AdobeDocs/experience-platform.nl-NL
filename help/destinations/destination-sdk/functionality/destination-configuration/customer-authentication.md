---
description: Leer hoe te opstelling een authentificatiemechanisme voor uw bestemming en krijgt inzicht in wat de gebruikers in UI afhankelijk van de authentificatiemethode zullen zien u selecteert.
title: Configuratie van klantverificatie
exl-id: 3912012e-0870-47d2-9a6f-7f1fc469a781
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 0%

---

# Configuratie van klantverificatie

Experience Platform verstrekt grote flexibiliteit in de authentificatieprotocollen beschikbaar aan partners en klanten. U kunt uw bestemming vormen om het even welke industrie-standaardauthentificatiemethodes zoals [!DNL OAuth2], toonder symbolische authentificatie, wachtwoordauthentificatie, en vele meer te steunen.

Deze pagina verklaart hoe te opstelling uw bestemming gebruikend uw aangewezen authentificatiemethode. Gebaseerd op de authentificatieconfiguratie die u gebruikt wanneer u uw bestemming creeert, zullen de klanten verschillende soorten authentificatiepagina&#39;s zien wanneer het verbinden met de bestemming in Experience Platform UI.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [ documentatie van configuratieopties ](../configuration-options.md) of zie de volgende pagina&#39;s van het overzicht van bestemmingsconfiguratie:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Alvorens de klanten gegevens van Platform naar uw bestemming kunnen uitvoeren, moeten zij een nieuwe verbinding tussen Experience Platform en uw bestemming tot stand brengen, door de stappen te volgen die in het ](../../../ui/connect-destination.md) leerprogramma worden beschreven 0} bestemmingsverbinding {.[

Wanneer [ creërend een bestemming ](../../authoring-api/destination-configuration/create-destination-configuration.md) door Destination SDK, bepaalt de `customerAuthenticationConfigurations` sectie welke klanten in het [ authentificatiescherm ](../../../ui/connect-destination.md#authenticate) zien. Afhankelijk van het type van bestemmingsauthentificatie, moeten de klanten diverse authentificatiedetails, zoals verstrekken:

* Voor bestemmingen die [ basisauthentificatie ](#basic) gebruiken, moeten de gebruikers een gebruikersbenaming en een wachtwoord direct in de Experience Platform UI authentificatiepagina verstrekken.
* Voor bestemmingen die [ dragerauthentificatie ](#bearer) gebruiken, moeten de gebruikers een dragertoken verstrekken.
* Voor bestemmingen die [ vergunning gebruiken OAuth2 ](#oauth2), worden de gebruikers opnieuw gericht aan login van uw bestemming pagina waar zij met hun geloofsbrieven kunnen login.
* Voor [ Amazon S3 ](#s3) bestemmingen, moeten de gebruikers hun [!DNL Amazon S3] toegangssleutel en geheime sleutel verstrekken.
* Voor [ Azure Klob ](#blob) bestemmingen, moeten de gebruikers hun [!DNL Azure Blob] verbindingskoord verstrekken.

U kunt de details van de klantenauthentificatie via het `/authoring/destinations` eindpunt vormen. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

Dit artikel beschrijft alle gesteunde configuraties van de klantenauthentificatie die u voor uw bestemming kunt gebruiken, en toont welke klanten in het Experience Platform UI zullen zien die op de authentificatiemethode wordt gebaseerd die u opstelling voor uw bestemming.

>[!IMPORTANT]
>
>De configuratie van de klantenauthentificatie vereist u niet om het even welke parameters te vormen. U kunt de fragmenten kopiëren en kleven die in deze pagina in uw API vraag worden getoond wanneer [ creërend ](../../authoring-api/destination-configuration/create-destination-configuration.md) of [ het bijwerken ](../../authoring-api/destination-configuration/update-destination-configuration.md) een bestemmingsconfiguratie, en uw gebruikers het overeenkomstige authentificatiescherm in het Platform UI zullen zien.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Configuratie van verificatieregel {#authentication-rule}

Wanneer het gebruiken van om het even welke configuraties van de klantenauthentificatie die in deze pagina worden beschreven, plaats altijd de `authenticationRule` parameter in [ bestemmingslevering ](destination-delivery.md) aan `"CUSTOMER_AUTHENTICATION"`, zoals hieronder getoond.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Basisverificatie {#basic}

Basisverificatie wordt ondersteund voor realtime (streaming) integratie in Experience Platform.

Wanneer u het basisidentificatietype vormt, moeten de gebruikers een gebruikersbenaming en een wachtwoord invoeren om met uw bestemming te verbinden.

![ UI teruggeeft met basisauthentificatie ](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Als u basisverificatie voor uw doel wilt instellen, configureert u de sectie `customerAuthenticationConfigurations` via het `/destinations` -eindpunt, zoals hieronder wordt getoond:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Waardere verificatie {#bearer}

Wanneer u het dragerauthentificatietype vormt, worden de gebruikers vereist om het dragerteken in te voeren dat zij uit uw bestemming verkrijgen.

![ UI teruggeeft met dragerauthentificatie ](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Als u verificatie met meer typen wilt instellen voor uw doel, configureert u de sectie `customerAuthenticationConfigurations` via het `/destinations` -eindpunt, zoals hieronder wordt getoond:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2-verificatie {#oauth2}

Gebruikers selecteren **[!UICONTROL Connect to destination]** om de OAuth 2-verificatiestroom naar uw doel te activeren, zoals in het onderstaande voorbeeld voor de bestemming Aangepast publiek van Twitter wordt getoond. Voor gedetailleerde informatie bij het vormen van OAuth 2 authentificatie aan uw bestemmingshindpunt, lees de specifieke [ Destination SDK OAuth 2 authentificatiepagina ](oauth2-authorization.md).

![ UI teruggeeft met 2 authentificatie OAuth ](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Als u [!DNL OAuth2] -verificatie wilt instellen voor uw doel, configureert u de `customerAuthenticationConfigurations` -sectie via het `/destinations` -eindpunt, zoals hieronder wordt weergegeven:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3-verificatie {#s3}

[!DNL Amazon S3] -verificatie wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

Wanneer u het Amazon S3 authentificatietype vormt, worden de gebruikers vereist om hun S3 geloofsbrieven in te voeren.

![ UI teruggeeft met S3 authentificatie ](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Als u [!DNL Amazon S3] -verificatie wilt instellen voor uw doel, configureert u de `customerAuthenticationConfigurations` -sectie via het `/destinations` -eindpunt, zoals hieronder wordt weergegeven:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob-verificatie  {#blob}

[!DNL Azure Blob Storage] -verificatie wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

Wanneer u het verificatietype Azure Blob configureert, moeten gebruikers de verbindingstekenreeks invoeren.

![ UI teruggeeft met authentificatie Blob ](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Als u [!DNL Azure Blob] -verificatie wilt instellen voor uw doel, configureert u de parameter `customerAuthenticationConfigurations` in het eindpunt `/destinations` , zoals hieronder wordt weergegeven:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] verificatie {#adls}

[!DNL Azure Data Lake Storage] -verificatie wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

Wanneer u het [!DNL Azure Data Lake Storage] authentificatietype vormt, worden de gebruikers vereist om de Azure Belangrijkste geloofsbrieven van de Dienst en hun huurdersinformatie in te voeren.

![ UI teruggeeft met [!DNL Azure Data Lake Storage] authentificatie ](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Als u [!DNL Azure Data Lake Storage] (ADLS)-verificatie wilt instellen voor uw doel, configureert u de parameter `customerAuthenticationConfigurations` in het eindpunt `/destinations` , zoals hieronder wordt weergegeven:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP met wachtwoordverificatie

[!DNL SFTP] -verificatie met wachtwoord wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

Wanneer u SFTP met het type van wachtwoordauthentificatie vormt, worden de gebruikers vereist om de gebruikersbenaming en het wachtwoord van SFTP, evenals het domein en de haven van SFTP in te voeren (de standaardhaven is 22).

![ UI teruggeeft met SFTP met wachtwoordauthentificatie ](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Als u SFTP-verificatie wilt instellen met een wachtwoord voor uw doel, configureert u de parameter `customerAuthenticationConfigurations` in het `/destinations` -eindpunt, zoals hieronder wordt weergegeven:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP met SSH-sleutelverificatie

[!DNL SFTP] -verificatie met de [!DNL SSH] -toets wordt ondersteund voor op een bestand gebaseerde doelen in Experience Platform.

Wanneer u SFTP met SSH zeer belangrijke authentificatietype vormt, worden de gebruikers vereist om de gebruikersbenaming van SFTP en de sleutel van SSH, evenals het domein en de haven van SFTP in te voeren (de standaardhaven is 22).

![ UI teruggeeft met SFTP met SSH zeer belangrijke authentificatie ](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Als u SFTP-verificatie wilt instellen met SSH-sleutel voor uw doel, configureert u de parameter `customerAuthenticationConfigurations` in het `/destinations` -eindpunt, zoals hieronder wordt getoond:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] verificatie {#gcs}

[!DNL Google Cloud Storage] -verificatie wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

Wanneer u het verificatietype [!DNL Google Cloud Storage] configureert, moeten gebruikers hun [!DNL Google Cloud Storage] [!UICONTROL access key ID] en [!UICONTROL secret access key] invoeren.

![ UI teruggeeft met de authentificatie van de Opslag van de Wolk van Google ](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Als u [!DNL Google Cloud Storage] -verificatie wilt instellen voor uw doel, configureert u de parameter `customerAuthenticationConfigurations` in het eindpunt `/destinations` , zoals hieronder wordt weergegeven:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u gebruikersauthentificatie aan uw bestemmingsplatform kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

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
