---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Gids voor Real-time Customer Data Platform
user-guide-description: Breng bekende en anonieme gegevens van meerdere bronnen van bedrijven bij elkaar om klantprofielen te maken, doelgroepsegmenten van die profielen te maken, en die segmenten voor externe doelen te activeren.
role: Admin
source-git-commit: 74a73b568c850f8e749afea039afd2821858bd69
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 16%

---


# Real-Time Customer Data Platform Help {#rtcdp}

* [Real-Time CDP-documentatie](home.md)
* Aan de slag {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Real-Time CDP-overzicht](overview.md)
      * [Aan de slag met Real-Time CDP](get-started.md)
      * [Homepage](home-page-dashboards.md)
   * Real-Time CDP B2B Edition {#rtcdpb2b-intro}
      * [Real-Time CDP B2B edition - overzicht](b2b-overview.md)
      * [Voorbeeld van gebruik](./b2b-use-case.md)
      * [Volledige zelfstudie](./b2b-tutorial.md)
      * [Real-Time CDP B2B edition guardrails](b2b-guardrails.md)
      * [Real-Time CDP B2B edition-architectuurupgrades](b2b-architecture-upgrade.md)
* Audience Manager en Real-Time CDP {#evolution}
   * [Evolutie uit Audience Manager](aam-to-rtcdp.md)
* Accountprofielen {#account}
   * [Overzicht van het accountprofiel](accounts/account-profile-overview.md)
   * [Gebruikersgids voor accountprofielen](accounts/account-profile-ui-guide.md)
* Beheer {#admin}
   * [Overzicht van beheer](administration/admin-overview.md)
* Splitsen en segmenteren {#segmentation}
   * [Overzicht van segmentatie](segmentation/segmentation-overview.md)
   * [Handleiding Audience Builder](segmentation/audience-builder.md)
   * [Segmentering in Real-Time CDP B2B edition](segmentation/b2b.md)
   * [Customer AI](segmentation/customer-ai.md)
* Gegevenssets {#datasets}
   * [Gegevenssets](datasets/dataset.md)
   * [Gegevenskwaliteit op Experience Platform](datasets/data-quality.md)
* Bestemmingen {#destinations}
   * [Overzicht van doelen](destinations/overview.md)
   * [Doelen in Real-Time CDP B2B edition](destinations/b2b.md)
* Guardrails {#guardrails}
   * [Overzicht van Real-Time CDP-instructies](guardrails/overview.md)
   * [&#x200B; Guardrails voor gegevensopname](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html){target="_blank"}
   * [&#x200B; Guardrails voor  [!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/){target="_blank"}
   * [&#x200B; Guardrails voor  [!DNL Real-Time Customer Profile]  gegevens en segmentatie](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html){target="_blank"}
   * [&#x200B; Guardrails voor  [!DNL Identity Service]  gegevens](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html){target="_blank"}
   * [&#x200B; Guardrails voor  [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html){target="_blank"}
   * [&#x200B; Grafieken voor gegevensactivering door bestemmingen](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html){target="_blank"}
* Identiteiten {#identity}
   * [Identiteiten en naamruimten](profile/identities-overview.md)
* Beleid samenvoegen {#merge-policies}
   * [Overzicht van beleid samenvoegen](profile/merge-policies.md)
* Privacy en gegevensbeheer {#privacy}
   * [Privacyoverzicht](privacy/privacy-overview.md)
   * [Overzicht van gegevensbeheer](privacy/data-governance-overview.md)
* Profielen {#profile}
   * [Profieloverzicht](profile/profile-overview.md)
   * [Bladeren door profiel](profile/profile-browse.md)
* Real-Time CDP B2B edition AI/ML-services {#b2b-cdp-ai-ml}
   * [Verwante accounts](b2b-ai-ml-services/related-accounts.md)
   * [Overeenkomende lead-account](b2b-ai-ml-services/lead-to-account-matching.md)
   * Voorspelend lood en account scoring {#predictive-lead-and-account-scoring-intro}
      * [Overzicht van voorsprong en accountscoring](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [Voorspelende leads en accountscoring beheren](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* Schema&#39;s {#schemas}
   * [Overzicht van schema&#39;s](schemas/overview.md)
   * [Schemas in Real-Time CDP B2B edition](schemas/b2b.md)
* Bronnen {#sources}
   * [Overzicht van bronnen](sources/sources-overview.md)
   * [Bronnen in Real-Time CDP B2B edition](sources/b2b.md)
* Gebruiksscenario’s {#use-cases}
   * [Overzicht van voorbeelden](/help/rtcdp/use-case-guides/overview.md)
   * Klantenovername {#customer-acquisition}
      * [&#x200B; neemt en verwerft nieuwe klanten zonder gebiedsdeel op derdekoekjes  aan](/help/rtcdp/partner-data/prospecting.md)
      * [Onsite ervaringen voor onbekende bezoekers personaliseren met de erkenning van bezoekers met hulp van partners](/help/rtcdp/partner-data/onsite-personalization.md)
      * [Offsite herbestemming van niet-geverifieerde gebruikers](./partner-data/offsite-retargeting.md)
      * [Niet-geverifieerde herbestemming op de server](./partner-data/unauthenticated-retargeting.md)
   * Profielverrijking {#profile-enrichment}
      * [Voeg eerste-partijprofielen met partner-verstrekte attributen toe](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * Gepersonaliseerde inzichten en betrokkenheid {#personalization-insights-engagement}
      * [Evolueer eenmalig klantenwaarde aan levenwaarde](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [Neem op intelligente wijze uw klanten opnieuw aan](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [Neem op intelligente wijze contact op met uw klanten: Luma-voorbeelden](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [&#x200B; de Nota&#39;s van de Versie van Experience Platform &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest)
* [&#x200B; Verklarende woordenlijst van Experience Platform &#x200B;](https://www.adobe.com/go/platform-glossary-en)