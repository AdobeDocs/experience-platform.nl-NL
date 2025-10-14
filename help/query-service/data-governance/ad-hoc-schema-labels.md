---
title: Op kenmerken gebaseerde ondersteuning voor toegangsbeheer voor ad-hocschema's
description: Een handleiding voor het beperken van toegang tot gegevensvelden in ad-hocschema's die via Adobe Experience Platform Query Service worden gegenereerd.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 0%

---

# Op kenmerken gebaseerde ondersteuning voor toegangsbeheer voor ad-hocschema&#39;s

Gegevens die naar Adobe Experience Platform worden overgebracht, worden ingekapseld door XDM-schema&#39;s (Experience Data Model) en kunnen onderworpen zijn aan gebruiksbeperkingen die door uw organisatie of wettelijke voorschriften zijn gedefinieerd.

Door een vraag CTAS door de Dienst van de Vraag uit te voeren wanneer geen schema wordt gespecificeerd, wordt een ad hoc schema automatisch geproduceerd. Het is vaak noodzakelijk het gebruik van bepaalde velden, of gegevensreeksen, van ad-hocregelingen te beperken om de toegang tot zowel gevoelige persoonsgegevens als persoonlijk identificeerbare informatie te controleren. Adobe Experience Platform vergemakkelijkt dit toegangsbeheer door u toe te staan om schemagebieden door Experience Platform UI te etiketteren gebruikend het op attribuut-gebaseerde toegangsbeheervermogen.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. Het is echter aan te raden om gegevens te labelen zodra ze in Experience Platform worden ingevoerd of zodra ze beschikbaar komen voor gebruik in Experience Platform.

Het op schema-gebaseerde etiketteren is een belangrijke component van op attribuut-gebaseerde toegangsbeheer om de toegang beter te beheren die aan gebruikers of groepen gebruikers wordt gegeven. Met Adobe Experience Platform kunt u de toegang tot elk veld in een ad-hocschema beperken door labels te maken en toe te passen.

Dit document biedt een zelfstudie om de toegang tot gevoelige gegevens te beheren door labels toe te passen op gegevensvelden van ad-hocschema&#39;s die via Query Service worden gegenereerd.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Model van de Gegevens van de Ervaring (XDM) Systeem &#x200B;](../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [[!DNL Schema Editor]](../../xdm/ui/overview.md): Leer hoe u schema&#39;s en andere bronnen maakt en beheert in de gebruikersinterface van Experience Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): Leer hoe u in [!DNL Data Governance] klantgegevens kunt beheren en hoe u ervoor kunt zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd.
* [&#x200B; op attributen-Gebaseerd toegangsbeheer &#x200B;](../../access-control/abac/overview.md): Op attributen-gebaseerd toegangsbeheer is een vermogen van Adobe Experience Platform dat beheerders toelaat om toegang tot specifieke voorwerpen en/of mogelijkheden te controleren die op attributen worden gebaseerd. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een ad-hocveld of een regulier schemaveld wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

## Een ad-hocschema maken

Zodra uw vraag is uitgevoerd en de resultaten zijn geproduceerd, wordt een ad hoc schema automatisch geproduceerd en toegevoegd aan de schemainventaris.

Als u een gegevenslabel wilt toevoegen, navigeert u naar het tabblad Bladeren van het [!UICONTROL Schemas] dashboard door [!UICONTROL Schemas] te selecteren in de linkertrack van de gebruikersinterface van Experience Platform. Het schema-overzicht wordt weergegeven.

>[!NOTE]
>
>Ad hoc schema&#39;s worden niet door gebrek getoond in de schemainventaris.

## Ontdek ad-hocschema&#39;s in de schemainventaris van de gebruikersinterface van Experience Platform {#discover-ad-hoc-schemas}

Om de vertoning van ad hoc schema&#39;s in Experience Platform toe te laten UI, selecteer het filterpictogram (![&#x200B; het filterpictogram van A.](/help/images/icons/filter.png)) links van het onderzoeksgebied, en selecteer dan ** [!UICONTROL Show adhoc schemas] in de linkerspoorlijn die verschijnt.

![&#x200B; de optie van het de filterfilter van het Schema linkerspoor met toegelaten de knevel van het &quot;Wijs adhoc schema&quot;toe.](../images/data-governance/adhoc-schema-toggle.png)

Selecteer de naam van het onlangs gemaakte ad-hocschema in de beschikbare lijst. Er wordt een visualisatie van de structuur van het ad-hocschema weergegeven.

![&#x200B; het diagram van de model ad hoc schemastructuur.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Regelgevingslabels bewerken

Als u gegevenslabels voor uw ad-hocschema wilt bewerken, selecteert u de tab [!UICONTROL Labels] . Met de werkruimte voor labels kunt u labels toepassen, maken en bewerken in uw ad-hocschemavelden en toegangsmachtigingen beheren via de gebruikersinterface. Alle velden in het ad-hocschema worden hier weergegeven.

## Labels voor het schema of veld bewerken

Om de etiketten voor het volledige schema uit te geven, selecteer het potloodpictogram (![&#x200B; het potloodpictogram van A.](/help/images/icons/edit.png) ) aan de kant van de naam van het schema onder de tab [!UICONTROL Labels] .

![&#x200B; de etiketmening in de schemawerkruimte met het benadrukte potloodpictogram.](../images/data-governance/edit-entire-schema-labels.png)

Als u een label op een bestaand veld wilt toepassen, selecteert u een of meer velden in de lijst gevolgd door [!UICONTROL Edit governance labels] in de rechterzijbalk.

![&#x200B; de etikettenmening in de schemawerkruimte met de &quot;geeft governance etiketten&quot;optie uit die in het rechterzijpaneel wordt benadrukt.](../images/data-governance/edit-governance-labels.png)

## Pop-up Labels bewerken

De pop-up [!UICONTROL Edit labels] wordt weergegeven. Vanuit deze weergave kunt u bestaande governancelabels maken of bewerken via de gebruikersinterface.

![&#x200B; Edit etiketten popover.](../images/data-governance/edit-labels-popover.png)

Zie de documentatie voor begeleiding op hoe te [&#x200B; tot stand brengen of labels voor het geselecteerde schema of gebied &#x200B;](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) uitgeven.

>[!NOTE]
>
>Voor het maken van een nieuw label of het bewerken van een bestaand label zijn beheerdersmachtigingen voor uw organisatie vereist. Als u geen beheerdersrechten hebt, neemt u contact op met uw systeembeheerder om de toegang te regelen.

De etiketten kunnen ook worden gecreeerd gebruikend de toestemmingenwerkruimte. Zie de [&#x200B; gids bij het creëren van etiketten in de toestemmingenwerkruimte &#x200B;](../../access-control/abac/ui/labels.md) voor instructies.

Zodra het aangewezen niveau van op attributen-gebaseerde toegangsbeheer is toegepast, is het volgende systeemgedrag op om het even welke vraag van toepassing die via de Dienst van de Vraag wordt uitgevoerd wanneer een gebruiker probeert om tot niet-toegankelijke gegevens toegang te hebben:

1. Als een gebruiker toegang tot één van de gebieden binnen een schema wordt geweigerd, zal de gebruiker niet op het beperkte gebied kunnen lezen of schrijven. Dit geldt voor de volgende algemene scenario&#39;s:

   * Wanneer een gebruiker een vraag met slechts een beperkte kolom probeert uit te voeren, zal het systeem een fout werpen dat de kolom niet bestaat.
   * Wanneer een gebruiker probeert om een vraag met veelvoudige kolommen uit te voeren die een beperkte kolom omvatten, zal het systeem output voor alle niet-beperkte slechts kolommen terugkeren.

1. Als een gebruiker om toegang tot een berekend gebied verzoekt, wordt de gebruiker vereist om toegang tot alle gebieden te hebben die in de samenstelling worden gebruikt of het systeem zal toegang tot het berekende gebied ontkennen.

Als een identiteit of primaire identiteit op ad hoc schema wordt geplaatst, neemt het systeem automatisch om het even welke bijbehorende verzoeken van de gegevenshygiëne in acht en ontruimt de gegevens in die datasets verbonden aan de identiteitskolom.

## Volgende stappen

Na het lezen van dit document hebt u een beter inzicht in hoe te om de etiketten van het gegevensgebruik aan ad hoc regelingen toe te voegen die door de vragen van de Dienst CTAS van de Vraag worden gecreeerd. Als u dit nog niet hebt gedaan, zijn de volgende documenten nuttig om uw inzicht in gegevensbeheer in de Dienst van de Vraag te verbeteren:

* [Identiteiten ad-hocschema](./ad-hoc-schema-identities.md)
* [Datagovernance](../../data-governance/home.md)
