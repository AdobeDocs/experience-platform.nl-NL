---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;
title: Op attributen-Gebaseerde Gids van de Controle van de Toegang van begin tot eind
description: Dit document verstrekt een gids van begin tot eind op op attribuut-gebaseerde toegangsbeheer in Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 230bcfdb92c3fbacf2e24e7210d61e2dbe0beb86
workflow-type: tm+mt
source-wordcount: '2196'
ht-degree: 0%

---

# Op attributen-gebaseerde toegangsbeheergids van begin tot eind

Toegangsbeheer op basis van kenmerken is een Adobe Experience Platform-functie die privacybewuste merken meer flexibiliteit biedt om gebruikerstoegang te beheren. Afzonderlijke objecten zoals schemavelden en segmenten kunnen worden toegewezen aan gebruikersrollen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke gebruikers van Platforms in uw organisatie.

Deze functionaliteit staat u toe om schemagebieden, segmenten, etc. met etiketten te categoriseren die organisatie of gegevensgebruikswerkingsgebied bepalen. In Adobe Journey Optimizer kunt u dezelfde labels toepassen op reizen en aanbiedingen. Tegelijkertijd kunnen beheerders toegangsbeleid definiëren rondom XDM-schemavelden en beter bepalen welke gebruikers of groepen (interne, externe of externe gebruikers) toegang hebben tot deze velden.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): De segmenteringsengine binnen [!DNL Platform] gebruikt om publiekssegmenten van uw klantenprofielen tot stand te brengen die op klantengedrag en attributen worden gebaseerd.

### Hoofdlettergebruik

In deze handleiding wordt een voorbeeld gebruikt van het beperken van de toegang tot vertrouwelijke gegevens om de workflow aan te tonen. U zult door een op voorbeeldattributen-gebaseerde toegangsbeheerwerkschema gaan waar u rollen, etiketten, en beleid zult creëren en toewijzen om te vormen of uw gebruikers tot bepaalde middelen in uw organisatie kunnen of niet kunnen toegang hebben. Dit gebruiksgeval wordt hieronder beschreven:

U bent een zorgleverancier en u wilt toegang tot middelen in uw organisatie vormen.

* Uw interne marketingteam moet toegang hebben tot **[!UICONTROL PHI/ Regulated Health Data]** gegevens.
* Uw externe instantie mag geen toegang krijgen tot **[!UICONTROL PHI/ Regulated Health Data]** gegevens.

Om dit te doen, moet u rollen, middelen, en beleid vormen.

U zult:

* [Label de rollen voor uw gebruikers](#label-roles): Gebruik het voorbeeld van een zorgleverancier (ACME Business Group) wiens marketinggroep samenwerkt met externe bureaus.
* [Etiketteer uw middelen (schemagebieden en segmenten)](#label-resources): Wijs het **[!UICONTROL PHI/ Regulated Health Data]** label aan schemamiddelen en segmenten.
* [Het beleid maken dat ze met elkaar verbindt](#policy): Creeer een beleid om de etiketten op uw middelen aan de etiketten in uw rol te verbinden ontkennend toegang tot schemagebieden en segmenten. Hierdoor wordt toegang tot het schemaveld en -segment in alle sandboxen geweigerd voor gebruikers die geen overeenkomende labels hebben.

## Toestemmingen

[!UICONTROL Permissions] is het gebied van Experience Cloud waar de beheerders gebruikersrollen en toegangsbeleid kunnen bepalen om toegangstoestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren.

Doorheen [!UICONTROL Permissions], kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. [!UICONTROL Permissions] kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld.

Als u geen beheerdersrechten hebt, neemt u contact op met de systeembeheerder om toegang te krijgen.

Als u beheerdersrechten hebt, gaat u naar [Adobe Experience Cloud](https://experience.adobe.com/) en meld u aan met uw Adobe-referenties. Zodra het programma geopend, **[!UICONTROL Overview]** wordt weergegeven voor uw organisatie waarvoor u beheerdersrechten hebt. Op deze pagina worden de producten weergegeven waarop uw organisatie is geabonneerd, samen met andere besturingselementen voor het toevoegen van gebruikers en beheerders aan de organisatie als geheel. Selecteren **[!UICONTROL Permissions]** om de werkruimte voor de integratie van uw Platform te openen.

![Afbeelding van het machtigingsproduct dat wordt geselecteerd in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

De werkruimte voor machtigingen voor de gebruikersinterface van het Platform wordt geopend in het dialoogvenster **[!UICONTROL Roles]** pagina.

## Labels op een rol toepassen {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Wat zijn labels?"
>abstract="Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Platform biedt verschillende Adobe-gedefinieerde &quot;core&quot;-labels voor gegevensgebruik, die een groot aantal gemeenschappelijke beperkingen omvatten die van toepassing zijn op gegevensbeheer. Met gevoelige &quot;S&quot;-labels zoals RHD (Gereglementeerde gezondheidsgegevens) kunt u bijvoorbeeld gegevens categoriseren die verwijzen naar beschermde gezondheidsinformatie (PHI). U kunt ook uw eigen aangepaste labels definiëren die aan de behoeften van uw organisatie voldoen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Overzicht van labels voor gegevensgebruik"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Nieuw label maken"
>abstract="U kunt uw eigen aangepaste labels maken die aansluiten op de behoeften van uw organisatie. De etiketten van de douane kunnen worden gebruikt om zowel gegevensbeheer als toegangsbeheerconfiguraties op uw gegevens toe te passen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Aangepaste labels beheren"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Wat zijn rollen?"
>abstract="Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan en bouwstenen van toegangsbeheerbeleid zijn. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Rollen beheren"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Nieuwe rol maken"
>abstract="U kunt een nieuwe rol tot stand brengen om gebruikers beter te categoriseren die tot uw instantie van het Platform toegang hebben. Bijvoorbeeld, kunt u een rol voor een Intern Team van de Marketing tot stand brengen en het etiket RHD op die rol toepassen, die uw Intern Team van de Marketing zal toestaan om tot de Beschermde Informatie van de Gezondheid (PHI) toegang te hebben. Alternatief, kunt u een rol voor een Extern Agentschap ook tot stand brengen en die roltoegang tot PHI gegevens ontkennen door het etiket RHD op die rol niet toe te passen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Een nieuwe rol maken"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Roloverzicht"
>abstract="In het dialoogvenster Roloverzicht worden de bronnen en sandboxen weergegeven waartoe een bepaalde rol toegang heeft."

Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan, en bouwstenen van toegangsbeheerbeleid zijn. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van toegang worden toegewezen zij nodig hebben.

Selecteer **[!UICONTROL ACME Business Group]** van de **[!UICONTROL Roles]** pagina.

![Afbeelding met de ACME Business Role die wordt geselecteerd in Rollen](../images/abac-end-to-end-user-guide/abac-select-role.png)

Selecteer vervolgens **[!UICONTROL Labels]** en selecteer vervolgens **[!UICONTROL Add Labels]**.

![Afbeelding met de optie Labels toevoegen die is geselecteerd op het tabblad Labels](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Er wordt een lijst met alle labels in uw organisatie weergegeven. Selecteren **[!UICONTROL RHD]** om het label toe te voegen voor **[!UICONTROL PHI/Regulated Health Data]**. Laat even een blauw vinkje naast het label staan en selecteer **[!UICONTROL Save]**.

![Afbeelding met het RHD-label dat wordt geselecteerd en opgeslagen](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## Labels toepassen op schemavelden {#label-resources}

Nu u een gebruikersrol met hebt gevormd [!UICONTROL RHD] label, de volgende stap is dat het zelfde etiket aan de middelen toe te voegen die u voor die rol wilt controleren.

Selecteren **[!UICONTROL Schemas]** van de linkernavigatie en selecteer dan **[!UICONTROL ACME Healthcare]** in de lijst met schema&#39;s die worden weergegeven.

![Afbeelding met het ACME-schema voor gezondheidszorg dat wordt geselecteerd op het tabblad Schema&#39;s](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Selecteer vervolgens **[!UICONTROL Labels]** om een lijst te zien die de gebieden verbonden aan uw schema toont. Hier kunt u labels toewijzen aan een of meerdere velden tegelijk. Selecteer **[!UICONTROL BloodGlucose]** en **[!UICONTROL InsulinLevel]** velden, en selecteer vervolgens **[!UICONTROL Edit governance labels]**.

![Afbeelding waarin de geselecteerde labels BloodGlucose en InsulinLevel worden weergegeven en de geselecteerde governancelabels worden bewerkt](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

De **[!UICONTROL Edit labels]** wordt weergegeven, zodat u de labels kunt kiezen die u op de schemavelden wilt toepassen. Selecteer voor dit gebruik de optie **[!UICONTROL PHI/ Regulated Health Data]** label, selecteert u vervolgens **[!UICONTROL Save]**.

![Afbeelding met het RHD-label dat wordt geselecteerd en opgeslagen](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Wanneer een label aan een veld wordt toegevoegd, wordt dat label toegepast op de bovenliggende bron van dat veld (een klasse of een veldgroep). Als de ouderklasse of de gebiedsgroep door andere schema&#39;s wordt gebruikt, zullen die schema&#39;s het zelfde etiket erven.

## Labels toepassen op segmenten

Nadat u de schemavelden hebt gelabeld, kunt u nu beginnen met het labelen van de segmenten.

Selecteren **[!UICONTROL Segments]** in de linkernavigatie. Een lijst van segmenten beschikbaar in uw organisatie wordt getoond. In dit voorbeeld moeten de volgende twee segmenten worden gelabeld omdat ze gevoelige gezondheidsgegevens bevatten:

* Bloedglucose > 100
* Insuline &lt;50

Selecteren **[!UICONTROL Blood Glucose >100]** om het segment te labelen.

![Afbeelding waarop op het tabblad Segmenten de optie Bloedglucose > 100 wordt weergegeven](../images/abac-end-to-end-user-guide/abac-select-segment.png)

Het segment **[!UICONTROL Details]** wordt weergegeven. Selecteer **[!UICONTROL Manage Access]**.

![Afbeelding waarin de selectie van de toegang voor Beheren wordt getoond](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

De **[!UICONTROL Edit labels]** wordt weergegeven, zodat u de labels kunt kiezen die u op het segment wilt toepassen. Selecteer voor dit gebruik de optie **[!UICONTROL PHI/ Regulated Health Data]** label, selecteert u vervolgens **[!UICONTROL Save]**.

![Afbeelding waarin de selectie van het RHD-label wordt getoond en opslaan dat wordt geselecteerd](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Herhaal bovenstaande stappen met **[!UICONTROL Insulin <50]**.

## Creeer een beleid van de toegangscontrole {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Wat is het beleid?"
>abstract="Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Elke organisatie komt met een standaardbeleid dat u moet activeren om regels voor middelen zoals segmenten en schemagebieden te bepalen. Standaardbeleid kan niet worden bewerkt of verwijderd. Het standaardbeleid kan echter worden geactiveerd of gedeactiveerd."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Beleid beheren"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Een beleid maken"
>abstract="Creeer een beleid om de acties te bepalen die uw gebruikers tegen uw segmenten en schemagebieden kunnen en kunnen nemen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Een beleid maken"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Toelaatbare en ontoelaatbare acties voor een beleid configureren"
>abstract="A <b>toegang weigeren tot</b> beleid zal gebruikers toegang ontzeggen wanneer aan de criteria wordt voldaan. Indien gecombineerd met <b>De volgende fout is onwaar</b> - alle gebruikers krijgen geen toegang tenzij zij voldoen aan de desbetreffende criteria. Dit type van beleid staat u toe om een gevoelig middel te beschermen en slechts toegang tot gebruikers toe te staan die passende etiketten hebben. <br>A <b>toegang tot</b> het beleid zal gebruikers toegang verlenen wanneer aan de criteria wordt voldaan . Indien gecombineerd met <b>Het volgende is waar</b> - gebruikers krijgen toegang als zij voldoen aan de criteria die hiervoor zijn vastgesteld. Dit ontkent niet uitdrukkelijk toegang tot gebruikers, maar voegt een vergunningstoegang toe. Dit type van beleid staat u toe om extra toegang tot middel en naast die gebruikers te verlenen die reeds toegang door roltoestemmingen zouden kunnen hebben.&quot;</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Een beleid bewerken"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Machtigingen voor een bron configureren"
>abstract="Een bron is het element dat of het object dat een gebruiker kan of kan benaderen. De middelen kunnen segmenten of schema&#39;s zijn. U kunt schrijven vormen, lezen, of schrappen toestemmingen voor segmenten en schemagebieden."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Voorwaarden bewerken"
>abstract="Pas voorwaardelijke verklaringen op uw beleid toe om gebruikerstoegang tot bepaalde middelen te vormen. Selecteer gelijke allen om gebruikers te vereisen om rollen met de nauwkeurige zelfde etiketten te hebben zoals een middel om toegang te worden toegestaan. Selecteer gelijke om het even welk om gebruikers slechts te vereisen om een rol met enkel één etiket te hebben dat een middel aanpast. De etiketten kunnen of als kern of douanelabels worden bepaald, met kernetiketten die etiketten vertegenwoordigen die worden gecreeerd en door Adobe en douanelabels worden verstrekt die etiketten vertegenwoordigen die u voor uw organisatie creeerde."

Het beleid van de controle van de toegang hefboomhefboometiketten om te bepalen welke gebruikersrollen toegang tot specifieke middelen van het Platform hebben. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. In dit voorbeeld wordt toegang tot schemavelden en -segmenten in alle sandboxen geweigerd voor gebruikers die niet over de overeenkomende labels in het schemaveld beschikken.

Als u een toegangsbeheerbeleid wilt maken, selecteert u **[!UICONTROL Permissions]** van de linkernavigatie en selecteer dan **[!UICONTROL Policies]**. Selecteer vervolgens **[!UICONTROL Create policy]**.

![Afbeelding met het pictogram Beleid maken dat wordt geselecteerd in de machtigingen](../images/abac-end-to-end-user-guide/abac-create-policy.png)

De **[!UICONTROL Create new policy]** wordt weergegeven en u wordt gevraagd een naam en een optionele beschrijving in te voeren. Selecteren **[!UICONTROL Confirm]** wanneer gereed.

![Afbeelding met het dialoogvenster Nieuw beleid maken en de optie Bevestigen](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Als u toegang tot de schemavelden wilt weigeren, gebruikt u de vervolgkeuzepijl en selecteert u **[!UICONTROL Deny access to]** en selecteer vervolgens **[!UICONTROL No resource selected]**. Selecteer vervolgens **[!UICONTROL Schema Field]** en selecteer vervolgens **[!UICONTROL All]**.

![Afbeelding met Weigeren toegang en geselecteerde bronnen](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

In de onderstaande tabel staan de voorwaarden die beschikbaar zijn bij het maken van een beleid:

| Voorwaarden | Beschrijving |
| --- | --- |
| De volgende fout is onwaar | Wanneer &#39;Toegang weigeren&#39; is ingesteld, wordt de toegang beperkt als de gebruiker niet voldoet aan de geselecteerde criteria. |
| Het volgende is waar | Wanneer &#39;Toegang toestaan tot&#39; is ingesteld, wordt de toegang beperkt als de gebruiker aan de geselecteerde criteria voldoet. |
| Komt overeen met alle | De gebruiker heeft een label dat overeenkomt met een willekeurig label dat op een bron is toegepast. |
| Komt overeen met alles | De gebruiker heeft alle labels die overeenkomen met alle labels die op een bron zijn toegepast. |
| Kernlabel | Een kernlabel is een door Adobe gedefinieerd label dat in alle instanties van het Platform beschikbaar is. |
| Aangepast label | Een aangepast label is een label dat door uw organisatie is gemaakt. |

Selecteren **[!UICONTROL The following being false]** en selecteer vervolgens **[!UICONTROL No attribute selected]**. Selecteer vervolgens de gebruiker **[!UICONTROL Core label]** selecteert u vervolgens **[!UICONTROL Matches all]**. Selecteer de bron **[!UICONTROL Core label]** en selecteert u **[!UICONTROL Add resource]**.

![Afbeelding met de voorwaarden die worden geselecteerd en Bron toevoegen die wordt geselecteerd](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>Een bron is het element dat of het object dat een onderwerp kan of kan benaderen. De middelen kunnen segmenten of schema&#39;s zijn.

Als u toegang tot de segmenten wilt weigeren, gebruikt u de vervolgkeuzepijl en selecteert u **[!UICONTROL Deny access to]** en selecteer vervolgens **[!UICONTROL No resource selected]**. Selecteer vervolgens **[!UICONTROL Segment]** en selecteer vervolgens **[!UICONTROL All]**.

Selecteren **[!UICONTROL The following being false]** en selecteer vervolgens **[!UICONTROL No attribute selected]**. Selecteer vervolgens de gebruiker **[!UICONTROL Core label]** selecteert u vervolgens **[!UICONTROL Matches all]**. Selecteer de bron **[!UICONTROL Core label]** en selecteert u **[!UICONTROL Save]**.

![Afbeelding met de geselecteerde voorwaarden en Opslaan geselecteerd](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Selecteren **[!UICONTROL Activate]** om het beleid te activeren, en er verschijnt een dialoogvenster waarin u wordt gevraagd de activering te bevestigen. Selecteren **[!UICONTROL Confirm]** en selecteer vervolgens **[!UICONTROL Close]**.

![Afbeelding waarin het beleid wordt weergegeven dat wordt geactiveerd ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Volgende stappen

U hebt de toepassing van labels op een rol, schemagebieden, en segmenten voltooid. Het externe agentschap dat aan deze rollen wordt toegewezen wordt beperkt van het bekijken van deze etiketten en hun waarden in het schema, de dataset, en de profielmening. Deze gebieden worden ook beperkt van worden gebruikt in de segmentdefinitie wanneer het gebruiken van de Bouwer van het Segment.

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie [op attributen-gebaseerd toegangsbeheeroverzicht](./overview.md).
