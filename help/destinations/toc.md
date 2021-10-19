---
audience: user
user-guide-title: Doelgids
user-guide-description: Activeer uw bekende en onbekende gegevens voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
description: In dit document wordt de inhoudsopgave voor Adobe Experience Platform-doelen weergegeven
feature: Destinations
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---


# Doelen {#destinations}

* [Overzicht van doelen](./home.md)
* [Doeltypen en -categorieën](./destination-types.md)
* API-zelfstudies {#api}
   * [Verbinding maken met streaming doelen en gegevens activeren met de Flow Service API](./api/streaming-destinations.md)
   * [Verbinding maken met marketingdoelen voor e-mail en gegevens activeren met de Flow Service API](./api/email-marketing.md)
* UI-hulplijnen {#ui}
   * [Werkruimte Doelen](./ui/destinations-workspace.md)
   * [Een nieuwe doelverbinding maken](./ui/connect-destination.md)
   * De publieksgegevens van Activa aan bestemmingen{#activate}
      * [Overzicht van activering](./ui/activation-overview.md)
      * [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](./ui/activate-segment-streaming-destinations.md)
      * [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](./ui/activate-streaming-profile-destinations.md)
      * [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](./ui/activate-batch-profile-destinations.md)
      * [De publieksgegevens van de activering aan de bestemmingen van het profielverzoek (Bèta)](./ui/activate-profile-request-destinations.md)
   * [Doelgegevens weergeven](./ui/destination-details-page.md)
   * [Doelaccounts bijwerken](./ui/update-accounts.md)
   * [Activeringsstromen bewerken](./ui/edit-activation.md)
   * [Doelen verwijderen](./ui/delete-destinations.md)
   * [Dataflows bewaken](./ui/monitor-dataflows.md)
* Doelcatalogus {#catalog}
   * [Overzicht van de doelcatalogus](./catalog/overview.md)
   * [ (Alpha) HTTP-verbinding](./catalog/http-destination.md)
   * Adobe-bestemmingen{#adobe}
      * [Overzicht van Adobe-doelen](./catalog/adobe/overview.md)
      * [(bèta) Marketo Engage-verbinding](./catalog/adobe/marketo-engage.md)
      * [Delen van Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Reclamebestemmingen{#advertising}
      * [Overzicht van advertentiebestemmingen](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud-extensie](./catalog/advertising/adobe-advertising-cloud.md)
      * [Awin Advertiser Conversion Tag-extensie](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag-extensie](./catalog/advertising/awin-mastertag.md)
      * [De extensie Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Vertakkingsextensie](./catalog/advertising/branch.md)
      * [DoubleClick Floodlight (bèta)-extensie](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel-extensie](./catalog/advertising/facebook-pixel.md)
      * [OneTag-extensie knipperen](./catalog/advertising/flashtalking.md)
      * [Google Ads-verbinding](./catalog/advertising/google-ads-destination.md)
      * [Google Ads-extensie](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager-verbinding](./catalog/advertising/google-ad-manager.md)
      * [Google Customer Match-verbinding](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360-verbinding](./catalog/advertising/google-dv360.md)
      * [Google-tag-extensie](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag-extensie](./catalog/advertising/linkedin.md)
      * [Microsoft Bing-verbinding](./catalog/advertising/bing.md)
      * [Pinterest Conversion Tracking-extensie](./catalog/advertising/pinterest-extension.md)
      * [Verbinding met pinterest Customer List](./catalog/advertising/pinterest.md)
      * [De verbinding van de handelsbureau](./catalog/advertising/tradedesk.md)
      * [Twitter Universal Website Tag-extensie](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX-verbinding](./catalog/advertising/datax.md)
   * Analysedoelen {#analytics}
      * [Overzicht van analysedoelen](./catalog/analytics/overview.md)
      * [Adform Website Tracking extension](./catalog/analytics/adform.md)
      * [Adobe Analytics-extensie](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics voor audio- en video-extensie](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale extensie](./catalog/analytics/clicktale.md)
      * [Contentsquare-extensie](./catalog/analytics/contentsquare.md)
      * [Decibel-extensie](./catalog/analytics/decibel.md)
      * [Demandbase-extensie](./catalog/analytics/demandbase.md)
      * [DialogTech-extensie](./catalog/analytics/dialogtech.md)
      * [Google Global Site Tag-extensie](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics-extensie](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics-extensie (Bèta)](./catalog/analytics/jw-player-analytics.md)
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
      * [(Beta) Amazon Kinesis-verbinding](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3-verbinding](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob-verbinding](./catalog/cloud-storage/azure-blob.md)
      * [(Beta) Azure Event Hubs-verbinding](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP-verbinding](./catalog/cloud-storage/sftp.md)
      * [IP adres lijst van gewenste personen](./catalog/cloud-storage/ip-address-allow-list.md)
   * Platforms voor gegevensbeheer {#data-management}
      * [Overzicht van DMP-doelen (Data Management Platform)](./catalog/data-management/overview.md)
      * [Audience Manager DIL-extensie](./catalog/data-management/aam-dil-extension.md)
   * E-maildoelen {#email}
      * [Bizible-extensie](./catalog/email/bizible.md)
      * [Marketo-extensie](./catalog/email/marketo.md)
      * [Marketo Munchkin-extensie](./catalog/email/marketo-munchkin.md)
      * [PebblePost-extensie](./catalog/email/pebblepost.md)
   * E-mailmarketingdoelen {#email-marketing}
      * [Overzicht van e-mailmarketingdoelen](./catalog/email-marketing/overview.md)
      * [Adobe Campaign-verbinding](./catalog/email-marketing/adobe-campaign.md)
      * [Oracle Eloqua-verbinding](./catalog/email-marketing/oracle-eloqua.md)
      * [Verbinding oracle Responsys](./catalog/email-marketing/oracle-responsys.md)
      * [Verbinding met Salesforce-Marketing Cloud](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * Tagextensies {#launch-extensions}
      * [Overzicht van de extensie Tag](./catalog/launch-extensions/overview.md)
   * Mobiele betrokkenheidsdoelen {#mobile-engagement}
      * [Overzicht van mobiele betrokkenheidsdoelen](./catalog/mobile-engagement/overview.md)
      * [Koppeling met kenmerken van luchtschip](./catalog/mobile-engagement/airship-attributes.md)
      * [Koppeling met vliegtuigcodes](./catalog/mobile-engagement/airship-tags.md)
      * [Braze verbinding](./catalog/mobile-engagement/braze.md)
   * Aanpassingsdoelen {#personalization}
      * [Overzicht van personalisatiedoelen](./catalog/personalization/overview.md)
      * [Adobe Target-verbinding (bèta)](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target-extensie](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2-extensie](./catalog/personalization/adobe-target-v2.md)
      * [Beemray-extensie](./catalog/personalization/beemray.md)
      * [Aangepaste aanpassingsverbinding (bèta)](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Bezoeker Intelligence-extensie](./catalog/personalization/dnb.md)
      * [Experience Cloud ID Service-extensie](./catalog/personalization/adobe-ecid.md)
      * [Verkenningsextensie](./catalog/personalization/gainsight.md)
      * [KickFire-extensie](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization-extensie](./catalog/personalization/marketo-web-personalization.md)
   * Sociale bestemmingen{#social}
      * [Overzicht van sociale bestemmingen](./catalog/social/overview.md)
      * [Adobe Livefyre-extensie](./catalog/social/adobe-livefyre.md)
      * [Facebook-verbinding](./catalog/social/facebook.md)
      * [linkedIn-verbinding voor passend publiek](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] verbinding](./catalog/social/twitter.md)
   * Onderzoeksbestemmingen {#survey}
      * [Overzicht van de enquêtedoelen](./catalog/survey/overview.md)
      * [Verwachte extensiebestemming](./catalog/survey/foresee.md)
      * [InMoment-extensie](./catalog/survey/inmoment.md)
      * [Qualtrics Website Feedback-extensie](./catalog/survey/qualtrics.md)
      * [QuestionPro Intercept Surveys-extensie](./catalog/survey/web-intercept-surveys.md)
   * Stem van de klantenbestemmingen {#voice}
      * [Stem van het overzicht van de bestemmingen van de Klant](./catalog/voice/overview.md)
      * [De extensie Digitale feedback bevestigen](./catalog/voice/confirmit-digital-feedback.md)
      * [Invoc-tags, extensie](./catalog/voice/invoca.md)
      * [extensie Medallia](./catalog/voice/medallia.md)
      * [URL-inbox-extensie Talk](./catalog/voice/talkurl.md)
* Doel-SDK {#destination-sdk}
   * [Overzicht](./destination-sdk/overview.md)
   * [Integratievereisten](./destination-sdk/integration-prerequisites.md)
   * [Aan de slag](./destination-sdk/getting-started.md)
   * Functionaliteit van doel-SDK {#functionality}
      * [Configuratieopties](./destination-sdk/configuration-options.md)
      * [Doelconfiguratie](./destination-sdk/destination-configuration.md)
      * [Server- en sjabloonspecificaties](./destination-sdk/server-and-template-configuration.md)
      * [Berichtindeling](./destination-sdk/message-format.md)
      * [Metagegevensbeheer voor het publiek](./destination-sdk/audience-metadata-management.md)
      * [Verificatieconfiguratie](./destination-sdk/credentials-configuration.md)
      * [OAuth 2-verificatie](./destination-sdk/oauth2-authentication.md)
      * Gereedschappen voor ontwikkelaars {#developer-tools}
         * [Een sjabloon voor berichttransformatie maken en testen](./destination-sdk/create-template.md)
         * [De doelconfiguratie testen](./destination-sdk/test-destination.md)
   * API-referentie {#api-reference}
      * [API-bewerkingen voor bestemmingspunten](./destination-sdk/destination-configuration-api.md)
      * [API-bewerkingen voor eindpunt doelserver](./destination-sdk/destination-server-api.md)
      * [API-bewerkingen voor het eindpunt van metagegevens van het publiek](./destination-sdk/audience-metadata-api.md)
      * [API-bewerkingen van het eindpunt Credentials](./destination-sdk/credentials-configuration-api.md)
      * [API-bewerkingen voor eindpunten publiceren](./destination-sdk/destination-publish-api.md)
      * Referentie voor ontwikkelaarsgereedschappen {#developer-tools-reference}
         * [API-bewerkingen voor voorbeeldsjablonen ophalen](./destination-sdk/sample-template-api.md)
         * [API-bewerkingen voor sjablonen renderen](./destination-sdk/render-template-api.md)
         * [API-bewerkingen voor doeltesten](./destination-sdk/destination-testing-api.md)
         * [Voorbeeld van API-bewerkingen voor het genereren van profielen](./destination-sdk/sample-profile-generation-api.md)
   * Hulplijnen {#guides}
      * [Doel SDK gebruiken om een streamingbestemming te configureren](./destination-sdk/configure-destination-instructions.md)
   * Uw doel documenteren {#document-destination}
      * [Uw doel documenteren in Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Gebruik de het Webinterface van GitHub om een pagina van de bestemmingsdocumentatie tot stand te brengen](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Zelfservicesjabloon voor documentatie](./destination-sdk/docs-framework/self-service-template.md)
* [Veelgestelde vragen](./destinations-faq.md)
* [Opmerkingen bij de release Platform](https://www.adobe.com/go/platform-release-notes-en)
