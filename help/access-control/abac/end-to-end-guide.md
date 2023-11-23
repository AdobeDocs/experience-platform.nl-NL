---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;
title: Op attributen-Gebaseerde Gids van de Controle van de Toegang van begin tot eind
description: Dit document verstrekt een gids van begin tot eind op op attribuut-gebaseerde toegangsbeheer in Adobe Experience Platform
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: 2b3c4a7aed804a1059708a698f3ba5edfb007926
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# Op attributen-gebaseerde toegangsbeheergids van begin tot eind

Gebruik op kenmerken gebaseerde toegangscontrole op Adobe Experience Platform om uzelf en andere privacybewuste klanten meer flexibiliteit te bieden om gebruikerstoegang te beheren. De toegang tot individuele voorwerpen, zoals schemagebieden en segmenten, kan met beleid worden verleend dat op de attributen en de rol van de objecten wordt gebaseerd. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Deze functionaliteit staat u toe om schemagebieden, segmenten, etc. met etiketten te categoriseren die organisatie of gegevensgebruikswerkingsgebied bepalen. U kunt dezelfde labels toepassen op reizen, aanbiedingen en andere objecten in Adobe Journey Optimizer. Tegelijkertijd kunnen beheerders toegangsbeleid definiëren rondom XDM-schemavelden (Experience Data Model) en beter beheren welke gebruikers of groepen (interne, externe of externe gebruikers) toegang hebben tot deze velden.

>[!NOTE]
>
>Dit document concentreert zich op het gebruiksgeval van het beleid van de toegangscontrole. Als u beleid wilt instellen om het **gebruiken** van gegevens eerder dan welke gebruikers van het Platform toegang tot het hebben, zie de gids van begin tot eind op [gegevensbeheer](../../data-governance/e2e.md) in plaats daarvan.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende platformcomponenten:

* [[!DNL Experience Data Model (XDM)] Systeem](../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): De segmenteringsengine binnen [!DNL Platform] gebruikt om publiekssegmenten van uw klantenprofielen tot stand te brengen die op klantengedrag en attributen worden gebaseerd.

### Hoofdlettergebruik

U zult door een op voorbeeldattributen-gebaseerde toegangsbeheerwerkschema gaan waar u rollen, etiketten, en beleid zult creëren en toewijzen om te vormen of uw gebruikers tot specifieke middelen in uw organisatie kunnen of niet kunnen toegang hebben. In deze handleiding wordt een voorbeeld gebruikt van het beperken van de toegang tot vertrouwelijke gegevens om de workflow te demonstreren. Dit gebruiksgeval wordt hieronder beschreven:

U bent een gezondheidszorgleverancier en wilt toegang tot middelen in uw organisatie vormen.

* Uw interne marketingteam moet toegang hebben tot **[!UICONTROL PHI/ Regulated Health Data]** gegevens.
* Uw externe instantie mag geen toegang krijgen tot **[!UICONTROL PHI/ Regulated Health Data]** gegevens.

Om dit te doen, moet u rollen, middelen, en beleid vormen.

U zult:

* [Label de rollen voor uw gebruikers](#label-roles): Gebruik het voorbeeld van een zorgleverancier (ACME Business Group) wiens marketinggroep samenwerkt met externe bureaus.
* [Etiketteer uw middelen (schemagebieden en segmenten)](#label-resources): Wijs het **[!UICONTROL PHI/ Regulated Health Data]** label aan schemamiddelen en segmenten.
* 
   * [Activeer het beleid dat hen verbindt:](#policy): Laat het standaardbeleid toe om toegang tot schemagebieden en segmenten te verhinderen door de etiketten op uw middelen aan de etiketten in uw rol te verbinden. Gebruikers met overeenkomende labels krijgen dan toegang tot het schemaveld en segmenten in alle sandboxen.

## Toestemmingen

[!UICONTROL Permissions] is het gebied van Experience Cloud waar de beheerders gebruikersrollen en beleid kunnen bepalen om toestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren.

Doorheen [!UICONTROL Permissions], kunt u rollen tot stand brengen en beheren en de gewenste middeltoestemmingen voor deze rollen toewijzen. [!UICONTROL Permissions] kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld.

Neem contact op met de systeembeheerder als u geen beheerdersrechten hebt.

Als u beheerdersrechten hebt, gaat u naar [Adobe Experience Cloud](https://experience.adobe.com/) en meld u aan met uw Adobe. Zodra het programma geopend, **[!UICONTROL Overview]** wordt weergegeven voor uw organisatie waarvoor u beheerdersrechten hebt. Deze pagina toont de producten uw organisatie aan, samen met andere controles wordt geabonneerd om gebruikers en beheerders aan de organisatie toe te voegen. Selecteren **[!UICONTROL Permissions]** om de werkruimte voor uw platformintegratie te openen.

![Afbeelding van het machtigingsproduct dat wordt geselecteerd in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

De werkruimte voor machtigingen voor de gebruikersinterface van het platform wordt geopend in het dialoogvenster **[!UICONTROL Roles]** pagina.

## Labels op een rol toepassen {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Wat zijn labels?"
>abstract="Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Het platform biedt verschillende Adobe-definieert &quot;kern&quot;gegevensgebruiksetiketten, die een grote verscheidenheid aan gemeenschappelijke beperkingen omvatten die van toepassing zijn op gegevensbeheer. Met gevoelige &quot;S&quot;-labels zoals RHD (Gereglementeerde gezondheidsgegevens) kunt u bijvoorbeeld gegevens categoriseren die verwijzen naar beschermde gezondheidsinformatie (PHI). U kunt ook uw eigen aangepaste labels definiëren die aan de behoeften van uw organisatie voldoen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html#understanding-data-usage-labels" text="Overzicht van labels voor gegevensgebruik"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Nieuw label maken"
>abstract="U kunt uw eigen aangepaste labels maken die aansluiten op de behoeften van uw organisatie. De etiketten van de douane kunnen worden gebruikt om zowel gegevensbeheer als toegangsbeheerconfiguraties op uw gegevens toe te passen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html#manage-labels" text="Aangepaste labels beheren"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Wat zijn rollen?"
>abstract="Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan en bouwstenen van toegangsbeheerbeleid zijn. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html" text="Rollen beheren"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Nieuwe rol maken"
>abstract="U kunt een nieuwe rol tot stand brengen om gebruikers beter te categoriseren die tot uw instantie van het Platform toegang hebben. Bijvoorbeeld, kunt u een rol voor een Intern Team van de Marketing tot stand brengen en het etiket RHD op die rol toepassen, toestaand uw Intern Team van de Marketing om tot de Beschermde Informatie van de Gezondheid (PHI) toegang te hebben. Alternatief, kunt u een rol voor een Extern Agentschap ook tot stand brengen en die roltoegang tot PHI gegevens ontkennen door het etiket RHD op die rol niet toe te passen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html#create-a-new-role" text="Een nieuwe rol maken"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Roloverzicht"
>abstract="In het dialoogvenster Roloverzicht worden de bronnen en sandboxen weergegeven waartoe een bepaalde rol toegang heeft."

Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan en zijn bouwstenen van toegangsbeheerbeleid. Een rol heeft een bepaalde reeks toestemmingen, en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van toegang worden toegewezen zij nodig hebben.

Selecteer **[!UICONTROL ACME Business Group]** van de **[!UICONTROL Roles]** pagina.

![Afbeelding met de ACME Business Role die wordt geselecteerd in Rollen](../images/abac-end-to-end-user-guide/abac-select-role.png)

Selecteer vervolgens **[!UICONTROL Labels]** en selecteer vervolgens **[!UICONTROL Add Labels]**.

![Afbeelding met de optie Labels toevoegen die is geselecteerd op het tabblad Labels](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Er wordt een lijst met alle labels in uw organisatie weergegeven. Selecteren **[!UICONTROL RHD]** om het label toe te voegen voor **[!UICONTROL PHI/Regulated Health Data]**. Laat even een blauw vinkje naast het label staan en selecteer **[!UICONTROL Save]**.

![Afbeelding met het RHD-label dat wordt geselecteerd en opgeslagen](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Wanneer het toevoegen van een organisatiegroep aan een rol, zullen alle gebruikers in die groep aan de rol worden toegevoegd. Wijzigingen in de organisatiegroep (gebruikers verwijderd of toegevoegd) worden automatisch bijgewerkt binnen de rol.

## Labels toepassen op schemavelden {#label-resources}

Nu u een gebruikersrol met hebt gevormd [!UICONTROL RHD] label, de volgende stap is dat het zelfde etiket aan de middelen toe te voegen die u voor die rol wilt controleren.

Selecteren **[!UICONTROL Schemas]** van de linkernavigatie en selecteer dan **[!UICONTROL ACME Healthcare]** in de lijst met schema&#39;s die worden weergegeven.

![Afbeelding met het ACME-schema voor gezondheidszorg dat wordt geselecteerd op het tabblad Schema&#39;s](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Selecteer vervolgens **[!UICONTROL Labels]** om een lijst te zien die de gebieden verbonden aan uw schema toont. Hier kunt u labels toewijzen aan een of meerdere velden tegelijk. Selecteer de **[!UICONTROL BloodGlucose]** en **[!UICONTROL InsulinLevel]** en selecteer vervolgens **[!UICONTROL Apply access and data governance labels]**.

![Afbeelding waarop de geselecteerde labels BloodGlucose en InsulinLevel worden weergegeven en waarop de geselecteerde labels voor toegang en gegevensbeheer worden toegepast](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

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

## Activeer het beleid van de toegangscontrole {#policy}

Het standaardtoegangsbeheerbeleid zal hefboometiketten gebruiken om te bepalen welke gebruikersrollen toegang tot specifieke middelen van het Platform hebben. In dit voorbeeld wordt toegang tot schemavelden en -segmenten in alle sandboxen geweigerd voor gebruikers die zich niet in een rol bevinden die de bijbehorende labels in het schemaveld heeft.

Als u het toegangsbeheerbeleid wilt activeren, selecteert u [!UICONTROL Permissions] van de linkernavigatie en selecteer dan **[!UICONTROL Policies]**.

![Lijst met weergegeven beleidsregels](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Selecteer vervolgens de ellips (`...`) naast de naam van het beleid en een vervolgkeuzelijst bevat besturingselementen voor het bewerken, activeren, verwijderen of dupliceren van de rol. Selecteren **[!UICONTROL Activate]** in de vervolgkeuzelijst.

![Vervolgkeuzelijst om beleid te activeren](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Het dialoogvenster voor het activeren van het beleid wordt weergegeven waarin u wordt gevraagd de activering te bevestigen. Selecteer **[!UICONTROL Confirm]**.

![Beleidsdialoogvenster activeren](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Bevestiging van beleidsactivering is ontvangen en u wordt teruggestuurd naar de [!UICONTROL Policies] pagina.

![Beleidsbevestiging activeren](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Volgende stappen

U hebt de toepassing van labels op een rol, schemagebieden, en segmenten voltooid. Het externe agentschap dat aan deze rollen wordt toegewezen wordt beperkt van het bekijken van deze etiketten en hun waarden in het schema, de dataset, en de profielmening. Deze gebieden worden ook beperkt van worden gebruikt in de segmentdefinitie wanneer het gebruiken van de Bouwer van het Segment.

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie [op attributen-gebaseerd toegangsbeheeroverzicht](./overview.md).

De volgende video is bedoeld om uw begrip van op attribuut-gebaseerde toegangscontrole te steunen, en schetst hoe te om rollen, middelen, en beleid te vormen.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)
