---
keywords: Experience Platform;home;Data Science Workspace;populaire onderwerpen;toegangsbeheer;sandbox;inlichtingenpakket;dsw-functies;dsw-toegang;Adobe Experience Platform Intelligence;intelligence;aep-informatiepakket
solution: Experience Platform
title: Toegang tot en functies van Data Science Workspace
topic-legacy: Access and features for data science workspace
description: Het volgende document schetst de toestemmingen van de Werkruimte van de Wetenschap van Gegevens en toegang tot eigenschappen.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Toegang tot en functies van Data Science Workspace

Het volgende document schetst de toestemmingen van de Werkruimte van de Wetenschap van Gegevens en toegang tot eigenschappen.

![DSW-tabbladen](./images/access/platform-tabs.png)

- **Laptops:** Biedt een interactieve ontwikkelomgeving ([JupyterLab](./jupyterlab/overview.md)) om uw gegevens op het Experience Platform te verkennen, te analyseren en te modelleren.
- **Modellen:** Verstrekt hulpmiddelen die worden gebruikt om, geavanceerde machine het leren recepten en modellen tot stand te brengen te publiceren en op te slaan. Ga voor meer informatie naar de [een leermodel voor computers maken en publiceren](./models-recipes/create-publish-model.md) zelfstudie.
- **Services:** Bevat beide door Adobe geleverde services, zoals [AI/ML-services](../intelligent-services/home.md) en alle aangepaste services die u hebt gemaakt met Data Science Workspace.

Waarom zie ik slechts het lusje van de Diensten?

- Uw organisatie heeft alleen recht op Adobe Real-time Customer Data Platform (Real-Time CDP), dat de AI/ML Service van de Klant omvat.

Als u geen van de **Gegevenswetenschap** de dossiers en wensen om de eigenschappen van de Werkruimte van de Wetenschap van Gegevens te gebruiken, contacteer uw bedrijfbeheerder om te controleren of hebt u een vergunning van de Intelligentie van Adobe Experience Platform.

## Gegevenswetenschapswerkruimte verpakken

De mogelijkheden van de Werkruimte van de Wetenschap van gegevens zijn beschikbaar in het pakket van de Intelligentie van Adobe Experience Platform en de Geavanceerde Inlichtingendienst van het Pak

De volgende lijst schetst enkele zeer belangrijke verschillen voor de Toestemmingen van de Werkruimte van de Wetenschap van Gegevens met en zonder de Geavanceerde toe:voegen-on van het Pak van de Intelligentie:

>[!NOTE]
>
>U kunt meer dan één Advanced Intelligence Pack Addon vergunning geven en de verhoogde capaciteit wordt toegevoegd aan uw algemene recht. Als u bijvoorbeeld een licentie hebt verleend voor 2 Adobe Experience Platform Advanced Intelligence Pack Addons, hebt u recht op in totaal 20 gelijktijdige laptopgebruikers.

| Machtiging gegevenswetenschapswerkruimte | Alleen Adobe Experience Platform Intelligence Package | Adobe Experience Platform Intelligence plus Advanced Intelligence Pack Add-on |
| --- | :---: | :---: |
| Aantal ondersteunde laptopgebruikers. | 5 gelijktijdige gebruikers | Met het eerste pakket worden 5 gelijktijdige gebruikers toegevoegd en met extra aankopen worden 10 gelijktijdige gebruikers per pakket toegevoegd. |
| Biedt geïntegreerde Jupyter-laptops voor verkennende gegevensanalyse en modelontwerpdoeleinden. | X (Ondersteunt R-, Python- en Scala-bibliotheken) | X (Voegt PySpark en de bibliotheken van XML van de Vonk toe) |
| Geïntegreerde integratie met Query-service. Mogelijkheid om gegevenssets te verkennen en vorm te geven met SQL in notebooks. | X | X |
| Toegang tot vooraf gebouwde laptopsjablonen voor voorspellende analyse. | X | X |
| Teken handmatig modellen met Jupyter-laptops en scoren deze. | X | X |
| Implementeer en operationele modellen met de mogelijkheid om trainingen te plannen en taken te evalueren. |  | X |
| Ontvang een framework om modellen eenvoudig te configureren, te evalueren, op te leiden, te scoren en te publiceren in productie. |  | X |
| Door de gebruikersinterface gestuurde modelexperimenten en -evaluaties. |  | X |
| Diepe leerondersteuning voor Tensorflow-modellen (GPU Compute). |  | X |
| Op parken gebaseerde verdeelde computer om te trainen en tegen grote datasets (10MM + rijen) te scoren. |  | X |

## Toegangsbeheer

Toegangscontrole voor Experience Platform wordt beheerd via [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden. Zie de [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie .

Om de Werkruimte van de Wetenschap van Gegevens te gebruiken, moet de toestemming &quot;van de Werkruimte van de Wetenschap van Gegevens&quot;worden toegelaten. In de volgende tabel worden de effecten weergegeven van het inschakelen of uitschakelen van deze machtiging:

| Machtiging | Ingeschakeld | Uitgeschakeld |
|---|---|---|
| Werkruimte voor gegevenswetenschap beheren | Verleent toegang tot alle diensten in de Werkruimte van de Wetenschap van Gegevens. | API- en UI-toegang tot alle services in de Data Science Workspace is uitgeschakeld. Als deze optie is uitgeschakeld, selecteert u de **Laptops**, **Modellen**, en **Services** pagina&#39;s zijn niet toegestaan. <li>Toegang tot **Services** kan nog steeds beschikbaar zijn via Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Sandbox-ondersteuning

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke instantie van het Platform steunt veelvoudige productie en niet productie zandbakken, elk die zijn eigen bibliotheek van Platform middelen handhaven. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op uw productiesandboxen. Zie voor meer informatie over sandboxen de [sandboxen, overzicht](../sandboxes/home.md).

Momenteel geldt voor de Data Science Workspace de volgende sandbox-beperking:

- Compute resources worden gedeeld door de productie- en niet-productie-sandboxen.

## Volgende stappen

Dit document schetste de verschillende soorten toegang en eigenschappen beschikbaar in de Werkruimte van de Wetenschap van Gegevens.

Om meer over de Werkruimte van de Wetenschap van Gegevens, zoals een volledig dagelijks werkschema te leren, gelieve te beginnen door te lezen [Analyse van de Data Science Workspace](./walkthrough.md) documentatie. Ga voor meer algemene informatie naar de [Overzicht van de Data Science Workspace](./home.md).
