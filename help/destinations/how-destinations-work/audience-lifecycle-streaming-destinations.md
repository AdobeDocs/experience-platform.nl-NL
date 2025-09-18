---
title: Levenscyclus van het publiek in Experience Platform en streamingbestemmingen
description: Leer hoe publieksnamen en toewijzingen van Experience Platform worden weerspiegeld in streaming doelplatforms.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Levenscyclus van het publiek in het stromen bestemmingen

Op deze pagina wordt beschreven hoe updates en toewijzingen voor de publieksnaam in Experience Platform worden gesynchroniseerd met streaming doelplatforms. Wanneer u publieksnamen wijzigt of publiekstoewijzingen in Experience Platform verwijdert, varieert het gedrag afhankelijk van de mogelijkheden van het doelplatform.

Kennis van deze verschillen is belangrijk voor het beheer van de levenscyclusbewerkingen van de doelgroep en voor het controleren of uw doelplatforms de huidige status van uw publiek in Experience Platform weerspiegelen.

## Doorgiftegedrag naam publiek {#audience-name-propagation}

Wanneer u een publiek aan een het stromen bestemming activeert, wordt de publieksnaam verzonden naar de bestemming tijdens de aanvankelijke activering. Het updategedrag voor de naam van het publiek varieert echter per doel:

* **[Doelen die de updates van de kijknaam](#name-update-supported)** steunen: Als u een publieksnaam in Experience Platform verandert, zal de bijgewerkte naam automatisch aan deze bestemmingen verspreiden.
* **[Doelen die geen updates van de kijknaam](#name-update-not-supported)** steunen: Als u een publieksnaam in Experience Platform verandert, zal de bestemming de originele naam van de aanvankelijke activering blijven gebruiken.

### Doelen die updates van publieksnaam ondersteunen {#name-update-supported}

De volgende streamingdoelen ondersteunen automatische updates van de publieksnaam wanneer u publieksnamen in Experience Platform wijzigt:

* [Acxiom Audience Connection](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandes](../catalog/advertising/demandbase-people.md)
* [Experience Cloud-doelgroepen](../catalog/adobe/experience-cloud-audiences.md)
* [Aangepast publiek Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [REGEL](../catalog/mobile-engagement/line.md)
* [(Bedrijven) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [LinkedIn Matched Audience](../catalog/social/linkedin.md)
* [(Verouderd) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Magnetische Inc.](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Aangepast publiek Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Doelen die geen ondersteuning bieden voor updates van publieksnaam {#name-update-not-supported}

Voor bestemmingen die hierboven niet worden vermeld, blijven de publieksnamen statisch na de aanvankelijke activering. Als u een publieksnaam voor deze bestemmingen moet bijwerken, moet u:

1. Een nieuw publiek maken in Experience Platform met de gewenste naam
2. Activeer het nieuwe publiek aan de bestemming

>[!TIP]
>
>Om verwarring te vermijden, gebruik beschrijvende publieksnamen van de eerste activering, vooral wanneer het activeren aan bestemmingen die de updates van de publieksnaam niet steunen.

## Doelen die het verwijderen van het publiek ondersteunen {#support-removal}

Wanneer u een publiek verwijdert (unmap) uit een streamingdoel, probeert Experience Platform het overeenkomstige publiek te verwijderen uit het doelplatform. Nochtans, niet steunen alle bestemmingen deze functionaliteit.

De volgende streamingdoelen ondersteunen automatische publieksverwijdering wanneer u een publiek van de bestemming demapping:

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Bedrijven) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [(Verouderd) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora-accountpubliek](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Experience Cloud-doelgroepen](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [REGEL](../catalog/mobile-engagement/line.md)
* [Gekoppeld publiek gekoppeld aan](../catalog/social/linkedin.md)
* [LiveRamp - Distributie](../catalog/advertising/liveramp-distribution.md)
* [Mailchimp-rentecategorieën](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud-accountbetrokkenheid](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Magnetische Inc.](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Aangepast publiek Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Doelen die het verwijderen van het publiek niet ondersteunen

Voor bestemmingen die hierboven niet worden vermeld, wanneer u een publiek van de bestemming losmaakt, verwijdert Experience Platform slechts de afbeelding. Het publiek in het bestemmingsplatform blijft actief tot u het in het partnerplatform manueel schrapt.
