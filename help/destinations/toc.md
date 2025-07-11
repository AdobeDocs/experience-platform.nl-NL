---
audience: user
user-guide-title: Handleiding voor bestemmingen
user-guide-description: Activeer uw bekende en onbekende gegevens voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en meer.
description: In dit document wordt de inhoudsopgave voor Adobe Experience Platform-doelen weergegeven
feature: Destinations
role: Admin,User
source-git-commit: 75dec8987827a84cf791ed08f725baed5a8865ae
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 2%

---


# Bestemmingen {#destinations}

* [Overzicht van doelen](./home.md)
* [Doeltypen en -categorieën](./destination-types.md)
* [Garanties voor bestemmingen (activering)](./guardrails.md)
* Hoe werken bestemmingen? {#how-destinations-work}
   * [Configureerbare en algemene exportinstellingen in doelen](./how-destinations-work/destinations-configurations.md)
   * [Profielexportgedrag voor verschillende doeltypen](./how-destinations-work/profile-export-behavior.md)
   * [Identiteitsverwerking in de workflow voor doelactivering](./how-destinations-work/identity-handling.md)
* API-zelfstudies {#api}
   * [ activeer gegevens aan op dossier-gebaseerde bestemmingen door de Dienst API van de Stroom te gebruiken ](/help/destinations/api/activate-segments-file-based-destinations.md)
   * [Verbinding maken met streaming doelen en gegevens activeren met de Flow Service API](./api/streaming-destinations.md)
   * [Verbind met op dossier-gebaseerde e-mailmarketing bestemmingen en activeer gegevens gebruikend de Dienst API van de Stroom](./api/connect-activate-batch-destinations.md)
   * [Het publiek activeren naar batchbestemmingen via de API voor ad-hocactivering](./api/ad-hoc-activation-api.md)
   * [Doel bewerken](./api/edit-destination.md)
   * [Doelgegevens bijwerken](./api/update-destination-dataflows.md)
   * [Doelaccounts verwijderen](./api/delete-destination-account.md)
   * [Doelgegevens verwijderen](./api/delete-destination-dataflow.md)
   * [Gegevensbestanden exporteren](/help/destinations/api/export-datasets.md)
   * [ Soort en filter API reacties voor bestemmingen ](https://experienceleague.adobe.com/docs/experience-platform/dataflows/api/sort-and-filter.html?lang=nl-NL#use-cases)
* UI-hulplijnen {#ui}
   * [Werkruimte Doelen](./ui/destinations-workspace.md)
   * [Een nieuwe doelverbinding maken](./ui/connect-destination.md)
   * Gegevens naar doelen activeren{#activate}
      * [Overzicht van activering](./ui/activation-overview.md)
      * [Het publiek activeren voor streaming doelpubliek voor exportdoelen](./ui/activate-segment-streaming-destinations.md)
      * [Stimulansen voor het streamen van exportdoelen voor profielen activeren](./ui/activate-streaming-profile-destinations.md)
      * [Soorten publiek activeren om exportdoelen voor batchprofielen te gebruiken](./ui/activate-batch-profile-destinations.md)
      * [Het publiek activeren voor verpersoonlijkingsdoelen van randen](./ui/activate-edge-personalization-destinations.md)
      * [Profielkenmerken aan de rand in real-time opzoeken](./ui/activate-edge-profile-lookup.md)
      * [Het publiek activeren op gekrulde doelen op basis van LiveRamp-id&#39;s](./ui/activate-curated-destinations.md)
      * [Activeren het potentiële publiek aan bestemmingen](./ui/activate-prospect-audiences.md)
      * [Accountpubliek naar doelen activeren](./ui/activate-account-audiences.md)
      * [Bestanden op aanvraag exporteren naar batchbestemmingen met de gebruikersinterface van Experience Platform](./ui/export-file-now.md)
      * [Gegevenssets exporteren met de gebruikersinterface van Experience Platform](./ui/export-datasets.md)
      * [(Beta) Gebruik het laatste XDM-attribuut voor kwalificatietijd in de nieuwe bètawolkenopslagdoelen](./ui/activate-last-qualification-time.md)
      * [Arrays, kaarten en objecten exporteren](/help/destinations/ui/export-arrays-maps-objects.md)
      * [Transformaties uitvoeren op gegevens die naar cloudopslagbestemmingen worden geëxporteerd](/help/destinations/ui/data-transformations-calculated-fields.md)
   * [Doelgegevens weergeven](./ui/destination-details-page.md)
   * [Doelaccounts bijwerken](./ui/update-accounts.md)
   * [Doelaccounts verwijderen](./ui/delete-destination-account.md)
   * [Activeringsgegevens bewerken](./ui/edit-activation.md)
   * [Doelen verwijderen](./ui/delete-destinations.md)
   * [Dataflows bewaken](./ui/monitor-dataflows.md)
   * [Opties voor bestandsindeling configureren voor op bestanden gebaseerde doelen](./ui/batch-destinations-file-formatting-options.md)
   * [Abonneren op in-context-bestemmingswaarschuwingen](ui/alerts.md)
* Doelcatalogus {#catalog}
   * [Overzicht van de doelcatalogus](./catalog/overview.md)
   * Adobe-bestemmingen{#adobe}
      * [Overzicht Adobe-bestemmingen](./catalog/adobe/overview.md)
      * [Experience Cloud-publiek](/help/destinations/catalog/adobe/experience-cloud-audiences.md)
      * [Marketo Engage-verbinding](./catalog/adobe/marketo-engage.md)
      * [(Beta) Marketo Engage Person Sync verbinding](./catalog/adobe/marketo-engage-person-sync.md)
      * [Marketo Measure Ultimate-verbinding](./catalog/adobe/marketo-measure-ultimate.md)
      * [ het publiek dat van Experience Platform  deelt](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL)
      * [ Federated de verbinding van de Samenstelling van het publiek ](https://www.adobe.com/go/destinations-federated-audience-composition)
   * Advertising-bestemmingen{#advertising}
      * [(Beta) Acxiom Audience Distribution](./catalog/advertising/acxiom-audience-distribution.md)
      * [Overzicht Advertising-bestemmingen](./catalog/advertising/overview.md)
      * [Cloud-verbinding voor Adobe Advertising](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud Extension](./catalog/advertising/adobe-advertising-cloud.md)
      * [Amazon Ads-verbinding](./catalog/advertising/amazon-ads.md)
      * [Awin Advertiser Conversion Tag-extensie](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag extension](./catalog/advertising/awin-mastertag.md)
      * [De extensie Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Bombora-verbinding](./catalog/advertising/bombora.md)
      * [Vertakkingsextensie](./catalog/advertising/branch.md)
      * [Criteverbinding](./catalog/advertising/criteo.md)
      * [Demandbase-verbinding](./catalog/advertising/demandbase.md)
      * [Demandbase People-verbinding](./catalog/advertising/demandbase-people.md)
      * [DoubleClick Floodlight-extensie (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel Extension](./catalog/advertising/facebook-pixel.md)
      * [OneTag-extensie knipperen](./catalog/advertising/flashtalking.md)
      * [Google Ads-verbinding](./catalog/advertising/google-ads-destination.md)
      * [Google Ads-extensie](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager-verbinding](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Google Ad Manager 360-verbinding](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google Customer Match-verbinding](./catalog/advertising/google-customer-match.md)
      * [Google Customer Match + DV360-verbinding](./catalog/advertising/google-customer-match-dv360.md)
      * [Google Display &amp; Video 360-verbinding](./catalog/advertising/google-dv360.md)
      * [Google-tag-extensie](./catalog/advertising/gtag-advertising.md)
      * [LinkedIn Insight-tagextensie](./catalog/advertising/linkedin.md)
      * [LiveRamp - Verbinding aan boord](./catalog/advertising/liveramp-onboarding.md)
      * [LiveRamp - Distribution-verbinding](./catalog/advertising/liveramp-distribution.md)
      * [Magnite Batch](/help/destinations/catalog/advertising/magnite-batch.md)
      * [Magnite Streaming Real-time verbinding](/help/destinations/catalog/advertising/magnite-streaming.md)
      * [Microsoft Bing-verbinding](./catalog/advertising/bing.md)
      * [Pinterest Conversion Tracking-extensie](./catalog/advertising/pinterest-extension.md)
      * [Verbinding met Pinterest Customer List](./catalog/advertising/pinterest.md)
      * [Pinterest-verbindingsupgrade](./catalog/advertising/pinterest-upgrade.md)
      * [PubMatic Connect-verbinding](./catalog/advertising/pubmatic.md)
      * [Verbinding Snapchat Ads](./catalog/advertising/snap-inc.md)
      * [De verbinding van de handelsbureau](./catalog/advertising/tradedesk.md)
      * [De Trade Desk CRM-verbinding](./catalog/advertising/tradedesk-emails.md)
      * [Twitter Universal Website Tag-extensie](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX-verbinding](./catalog/advertising/datax.md)
   * Analysedoelen {#analytics}
      * [Overzicht van analysedoelen](./catalog/analytics/overview.md)
      * [De extensie Adform Website Tracking](./catalog/analytics/adform.md)
      * [Adobe Analytics-extensie](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics voor audio- en video-extensie](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale extensie](./catalog/analytics/clicktale.md)
      * [Contentsquare-extensie](./catalog/analytics/contentsquare.md)
      * [Decibel-extensie](./catalog/analytics/decibel.md)
      * [Demandbase-extensie](./catalog/analytics/demandbase.md)
      * [DialogTech-extensie](./catalog/analytics/dialogtech.md)
      * [PX-verbinding ophalen](./catalog/analytics/gainsight-px.md)
      * [Google Global Site Tag-extensie](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics-extensie](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics-extensie (Beta)](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK-extensie](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA Handler extension](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS Player Handler extension](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly Analytics-extensie](./catalog/analytics/parsely.md)
      * [Quantum Metric extension](./catalog/analytics/quantum-metric.md)
      * [SessionCam-extensie](./catalog/analytics/sessioncam.md)
      * [TMMData-extensie](./catalog/analytics/tmmdata.md)
      * [De extensie Tekstomzetting bijhouden](./catalog/analytics/yext.md)
   * Opslagdoelen voor cloud {#cloud-storage}
      * [Overzicht van Cloud Storage-bestemmingen](./catalog/cloud-storage/overview.md)
      * [Amazon Kinesis-verbinding](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3-verbinding](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob-verbinding](./catalog/cloud-storage/azure-blob.md)
      * [Azure Data Lake Storage Gen2](./catalog/cloud-storage/adls-gen2.md)
      * [Azure Event Hubs-verbinding](./catalog/cloud-storage/azure-event-hubs.md)
      * [Gegevenslandingszone](./catalog/cloud-storage/data-landing-zone.md)
      * [Google Cloud Storage](./catalog/cloud-storage/google-cloud-storage.md)
      * [SFTP-verbinding](./catalog/cloud-storage/sftp.md)
      * [Snowflake-verbinding](./catalog/cloud-storage/snowflake.md)
      * [IP adres lijst van gewenste personen voor op dossier-gebaseerde cloudopslagbestemmingen](./catalog/cloud-storage/ip-address-allow-list.md)
   * Klantrelaties (CRM)-bestemmingen {#crm}
      * [Hubspot-verbinding](./catalog/crm/hubspot.md)
      * [Salesforce CRM-verbinding](./catalog/crm/salesforce.md)
      * [Microsoft Dynamics 365-verbinding](./catalog/crm/microsoft-dynamics-365.md)
      * [Verbinding buiten bereik](catalog/crm/outreach.md)
      * [Zendesk-verbinding](catalog/crm/zendesk.md)
   * Gebieden van het Platform voor gegevensbeheer {#data-management}
      * [Overzicht van bestemmingen in het Data Management Platform (DMP)](./catalog/data-management/overview.md)
      * [Audience Manager DIL Extension](./catalog/data-management/aam-dil-extension.md)
      * [Zeta Marketing Platform](/help/destinations/catalog/data-management/zeta-marketing-platform.md)
   * Partner gegevens en identiteit {#data-partner}
      * [Acxiom-perspectiefonderdrukking](./catalog/data-partner/acxiom-prospect-suppression.md)
      * [Verbetering van acxiom-gegevens](./catalog/data-partner/acxiom-data-enhancement.md)
      * [Merkury Enterprise Connections](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md)
      * [Merkury Enterprise Identity](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md)
   * eCommerce-bestemmingen {#ecommerce}
      * [SAP COMMERCE](./catalog/ecommerce/sap-commerce.md)
   * E-maildoelen {#email}
      * [Bizible extension](./catalog/email/bizible.md)
      * [Marketo-extensie](./catalog/email/marketo.md)
      * [Marketo Munchkin Extension](./catalog/email/marketo-munchkin.md)
      * [PebblePost-extensie](./catalog/email/pebblepost.md)
   * E-mailmarketingdoelen {#email-marketing}
      * [Overzicht van e-mailmarketingdoelen](./catalog/email-marketing/overview.md)
      * [Adobe Campaign-verbinding](./catalog/email-marketing/adobe-campaign.md)
      * [Adobe Campaign Managed Cloud Services-verbinding](./catalog/email-marketing/adobe-campaign-managed-services.md)
      * [Mailchimp-rentecategorieën](./catalog/email-marketing/mailchimp-interest-categories.md)
      * [Mailchimp-tags](./catalog/email-marketing/mailchimp-tags.md)
      * [(API) Oracle Eloqua-verbinding](./catalog/email-marketing/oracle-eloqua-api.md)
      * [(Bestanden) Oracle Eloqua-verbinding](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle Responsys-verbinding](./catalog/email-marketing/oracle-responsys.md)
      * [(API) Salesforce Marketing Cloud-verbinding](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [(Bestanden) Salesforce Marketing Cloud-verbinding](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [[!DNL Salesforce Marketing Cloud Account Engagement]](./catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
      * [SendGrid-verbinding](./catalog/email-marketing/sendgrid.md)
   * Extensies labelen {#launch-extensions}
      * [Overzicht van de extensie Tag](./catalog/launch-extensions/overview.md)
   * Marketing automatiseren {#marketing-automation}
      * [ Profielen van de Deelnemer RainFocus ](/help/destinations/catalog/marketing-automation/rainfocus.md)
   * Mobiele betrokkenheidsdoelen {#mobile-engagement}
      * [Overzicht van mobiele betrokkenheidsdoelen](./catalog/mobile-engagement/overview.md)
      * [Koppeling met kenmerken van het luchtschip](./catalog/mobile-engagement/airship-attributes.md)
      * [Koppeling met vliegtuigcodes](./catalog/mobile-engagement/airship-tags.md)
      * [Braze verbinding](./catalog/mobile-engagement/braze.md)
      * [Lijnverbinding](./catalog/mobile-engagement/line.md)
      * [Verbinding maken](./catalog/mobile-engagement/moengage.md)
   * Personalization-bestemmingen {#personalization}
      * [Overzicht Personalization-bestemmingen](./catalog/personalization/overview.md)
      * [(Beperkte beschikbaarheid) Analyse publiek](./catalog/personalization/audience-analysis.md)
      * [Adobe Commerce-verbinding](./catalog/personalization/adobe-commerce.md)
      * [Adobe Target-verbinding](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target-extensie](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2-extensie](./catalog/personalization/adobe-target-v2.md)
      * [Algolië-verbinding](./catalog/personalization/algolia.md)
      * [Beemray-extensie](./catalog/personalization/beemray.md)
      * [Aangepaste verpersoonlijkingsverbinding](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Bezoeker Intelligence-extensie](./catalog/personalization/dnb.md)
      * [Experience Cloud ID Service-extensie](./catalog/personalization/adobe-ecid.md)
      * [Verkenningsextensie](./catalog/personalization/gainsight.md)
      * [KickFire-extensie](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization-extensie](./catalog/personalization/marketo-web-personalization.md)
      * [Pega CDH Realtime Audience-verbinding](./catalog/personalization/pega.md)
      * [(V2) Pega CDH Realtime Audience Connection](./catalog/personalization/pega-v2.md)
      * [Verbinding met Pega-profiel](./catalog/personalization/pega-profile.md)
   * Sociale bestemmingen{#social}
      * [Overzicht van sociale bestemmingen](./catalog/social/overview.md)
      * [Facebook-verbinding](./catalog/social/facebook.md)
      * [(Bedrijven) LinkedIn-verbinding voor passend publiek](./catalog/social/linkedin-b2b.md)
      * [Verbinding LinkedIn met soorten publiek](./catalog/social/linkedin.md)
      * [TikTok-verbinding](./catalog/social/tiktok.md)
      * [[!DNL Twitter Custom Audiences] verbinding](./catalog/social/twitter.md)
   * Streaming doelen {#streaming}
      * [HTTP API-verbinding](./catalog/streaming/http-destination.md)
      * [IP adres lijst van gewenste personen voor het stromen bestemmingen](./catalog/streaming/ip-address-allow-list.md)
   * Onderzoeksbestemmingen {#survey}
      * [Overzicht van de enquêtedoelen](./catalog/survey/overview.md)
      * [Doel van Qualtrict Automations](./catalog/survey/qualtrics-automations.md)
      * [Verwachte extensiebestemming](./catalog/survey/foresee.md)
      * [InMoment-extensie](./catalog/survey/inmoment.md)
      * [Qualtrics Website Feedback-extensie](./catalog/survey/qualtrics.md)
      * [Extension QuestionPro Intercept Surveys](./catalog/survey/web-intercept-surveys.md)
   * Stem van de klantenbestemmingen {#voice}
      * [Stem van het overzicht van de bestemmingen van de Klant](./catalog/voice/overview.md)
      * [De extensie Digitale feedback bevestigen](./catalog/voice/confirmit-digital-feedback.md)
      * [Invoc-tags, extensie](./catalog/voice/invoca.md)
      * [verbinding met Medallia](./catalog/voice/medallia-connector.md)
      * [extensie Medallia](./catalog/voice/medallia.md)
      * [URL-inbox-extensie Talk](./catalog/voice/talkurl.md)
* Destination SDK {#destination-sdk}
   * [Overzicht](./destination-sdk/overview.md)
   * [Integratievereisten](./destination-sdk/integration-prerequisites.md)
   * [Aan de slag met Destination SDK](./destination-sdk/getting-started.md)
   * [Woordenlijst](/help/destinations/destination-sdk/glossary.md)
   * Functionaliteit {#functionality}
      * [Configuratieopties](./destination-sdk/functionality/configuration-options.md)
      * Bestemmingsservercomponenten {#destination-server}
         * [Serverspecificaties](./destination-sdk/functionality/destination-server/server-specs.md)
         * [Sjabloonspecificaties](./destination-sdk/functionality/destination-server/templating-specs.md)
         * [Berichtindeling](./destination-sdk/functionality/destination-server/message-format.md)
         * [Ondersteunde transformatiefuncties](./destination-sdk/functionality/destination-server/supported-functions.md)
         * [Configuratie bestandsindeling](./destination-sdk/functionality/destination-server/file-formatting.md)
      * Componenten voor doelconfiguratie {#destination-configuration}
         * [Type publieksgegevens configureren](./destination-sdk/functionality/destination-configuration/audience-data-type.md)
         * [Configuratie van klantverificatie](./destination-sdk/functionality/destination-configuration/customer-authentication.md)
         * [OAuth2-vergunning](./destination-sdk/functionality/destination-configuration/oauth2-authorization.md)
         * [Gegevensvelden van de klant](./destination-sdk/functionality/destination-configuration/customer-data-fields.md)
         * [UI-kenmerken](./destination-sdk/functionality/destination-configuration/ui-attributes.md)
         * [Configuratie partnerschema](./destination-sdk/functionality/destination-configuration/schema-configuration.md)
         * [Configuratie naamruimte voor identiteit](./destination-sdk/functionality/destination-configuration/identity-namespace-configuration.md)
         * [Ondersteunde toewijzingsconfiguraties](./destination-sdk/functionality/destination-configuration/supported-mapping-configurations.md)
         * [Levering bestemming](./destination-sdk/functionality/destination-configuration/destination-delivery.md)
         * [Configuratie van metagegevens voor publiek](./destination-sdk/functionality/destination-configuration/audience-metadata-configuration.md)
         * [Samenvoegingsbeleid](./destination-sdk/functionality/destination-configuration/aggregation-policy.md)
         * [Batchconfiguratie](./destination-sdk/functionality/destination-configuration/batch-configuration.md)
         * [Historische profielkwalificaties](./destination-sdk/functionality/destination-configuration/historical-profile-qualifications.md)
      * [Het beperken van snelheid en herprobeert beleid voor het stromen bestemmingen](./destination-sdk/functionality/rate-limiting-retry-policy.md)
      * [Metagegevensbeheer voor het publiek](./destination-sdk/functionality/audience-metadata-management.md)
   * Gidsen {#guides}
      * [Destination SDK gebruiken om een streamingbestemming te configureren](./destination-sdk/guides/configure-destination-instructions.md)
      * [Destination SDK gebruiken om een bestandsgebaseerde bestemming te configureren](./destination-sdk/guides/configure-file-based-destination-instructions.md)
      * [Ter controle verzenden naar een bestemming die is geschreven in Destination SDK](./destination-sdk/guides/submit-destination.md)
      * Bestandsgebaseerde doelen configureren {#configure-file-based-destinations}
         * [ vorm dossier het formatteren opties ](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)
         * [Een Amazon S3-bestemming configureren met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnaam](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md)
         * [Een Amazon S3-bestemming configureren met aangepaste bestandsnaam en opmaakopties](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-custom-file-formatting.md)
         * [Een Azure Blob Storage-bestemming configureren met aangepaste opties voor bestandsindeling en aangepaste configuratie van bestandsnamen](../destinations/destination-sdk/guides/batch/configure-blob-destination-with-custom-file-formatting.md)
         * [Een Azure Data Lake Storage-bestemming configureren met aangepaste opties voor bestandsindeling en aangepaste configuratie van bestandsnamen](../destinations/destination-sdk/guides/batch/configure-adls-destination-with-custom-file-formatting.md)
         * [Vorm een bestemming van de Landing van Gegevens (DLZ) met de opties van de douanedossier het formatteren en de configuratie van de douanenaam van het dossier](../destinations/destination-sdk/guides/batch/configure-dlz-destination-with-custom-file-formatting.md)
         * [Een SFTP-bestemming configureren met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnaam](../destinations/destination-sdk/guides/batch/configure-sftp-destination-with-predefined-file-formatting.md)
         * [Vorm een op dossier-gebaseerde bestemming om perspectiefpubliek uit te voeren](/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md)
   * Referentie voor API voor doelontwerp {#authoring-api}
      * [ Destination SDK (Authoring van de Bestemming) API verwijzing ](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * Bestemmingsserverbewerkingen {#server-operations}
         * [Een doelserverconfiguratie maken](./destination-sdk/authoring-api/destination-server/create-destination-server.md)
         * [De configuratie van een doelserver ophalen](./destination-sdk/authoring-api/destination-server/retrieve-destination-server.md)
         * [Een doelserverconfiguratie bijwerken](./destination-sdk/authoring-api/destination-server/update-destination-server.md)
         * [Een doelserverconfiguratie verwijderen](./destination-sdk/authoring-api/destination-server/delete-destination-server.md)
      * Doelconfiguratiebewerkingen {#destination-operations}
         * [Een doelconfiguratie maken](./destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md)
         * [Een doelconfiguratie ophalen](./destination-sdk/authoring-api/destination-configuration/retrieve-destination-configuration.md)
         * [Een doelconfiguratie bijwerken](./destination-sdk/authoring-api/destination-configuration/update-destination-configuration.md)
         * [Een doelconfiguratie verwijderen](./destination-sdk/authoring-api/destination-configuration/delete-destination-configuration.md)
   * Referentie voor API-metagegevens van het publiek {#audience-template-api}
      * [Een publiekssjabloon maken](./destination-sdk/metadata-api/create-audience-template.md)
      * [Een publiekssjabloon ophalen](./destination-sdk/metadata-api/retrieve-audience-template.md)
      * [Een publiekssjabloon bijwerken](./destination-sdk/metadata-api/update-audience-template.md)
      * [Een publiekssjabloon verwijderen](./destination-sdk/metadata-api/delete-audience-template.md)
   * Referentie voor API voor referentieconfiguratie {#credentials-api}
      * [Een referentieconfiguratie maken](./destination-sdk/credentials-api/create-credential-configuration.md)
      * [Een referentieconfiguratie ophalen](./destination-sdk/credentials-api/retrieve-credential-configuration.md)
      * [Een referentieconfiguratie bijwerken](./destination-sdk/credentials-api/update-credential-configuration.md)
      * [Een referentieconfiguratie verwijderen](./destination-sdk/credentials-api/delete-credential-configuration.md)
   * Referentie voor API voor doeltests {#testing-api}
      * API voor streaming doeltest {#streaming-destinations}
         * [Overzicht van de API voor streaming-doeltests](./destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md)
         * [Voorbeeldprofielen genereren op basis van een bronschema](./destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)
         * [Een transformatiesjabloon voor een voorbeeldbericht genereren](./destination-sdk/testing-api/streaming-destinations/sample-template-api.md)
         * [Geëxporteerde profielstructuur valideren](./destination-sdk/testing-api/streaming-destinations/render-template-api.md)
         * [Streaming doel testen met voorbeeldprofielen](./destination-sdk/testing-api/streaming-destinations/destination-testing-api.md)
         * [Een sjabloon voor berichttransformatie maken en testen](./destination-sdk/testing-api/streaming-destinations/create-template.md)
      * API voor doeltesten op basis van bestanden {#batch-destinations}
         * [ Op dossier-gebaseerde bestemming het testen API overzicht ](./destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)
         * [Voorbeeldprofielen genereren op basis van een bronschema](./destination-sdk/testing-api/batch-destinations/file-based-sample-profile-generation-api.md)
         * [Bestandsgebaseerde bestemming testen met voorbeeldprofielen](./destination-sdk/testing-api/batch-destinations/file-based-destination-testing-api.md)
         * [Gedetailleerde activeringsresultaten weergeven](./destination-sdk/testing-api/batch-destinations/file-based-destination-results-api.md)
         * [Gevalideerde klantvelden valideren](./destination-sdk/testing-api/batch-destinations/file-based-render-template-api.md)
   * Referentie voor publicatie-API van bestemming {#publishing-api}
      * [Een doelpublicatieverzoek maken](./destination-sdk/publishing-api/create-publishing-request.md)
      * [Een doelpublicatieverzoek ophalen](./destination-sdk/publishing-api/retrieve-publishing-request.md)
   * Uw doel documenteren {#document-destination}
      * [Uw doel documenteren in Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Zelfbedieningssjabloon voor documentatie](./destination-sdk/docs-framework/self-service-template.md)
      * [Aanbevolen werkwijzen ontwerpen](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Veelgestelde vragen](./destinations-faq.md)
* [Releaseopmerkingen bij Experience Platform](https://experienceleague.adobe.com/nl/docs/experience-platform/release-notes/latest)
