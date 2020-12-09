---
keywords: Experience Platform;home;Data Science Workspace;popular topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Toegang tot en functies van Data Science Workspace
topic: Access and features for data science workspace
description: 'Het volgende document schetst de toestemmingen van de Werkruimte van de Wetenschap van Gegevens en toegang tot eigenschappen. '
translation-type: tm+mt
source-git-commit: 40181fc9b1b08c2e21f806caae76b8af0ec9e5e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 2%

---


# Toegang tot en functies van Data Science Workspace

Het volgende document schetst de toestemmingen van de Werkruimte van de Wetenschap van Gegevens en toegang tot eigenschappen.

![DSW-tabbladen](./images/access/platform-tabs.png)

- **Laptops:** Biedt een interactieve ontwikkelomgeving ([JupyterLab](./jupyterlab/overview.md)) voor het verkennen, analyseren en modelleren van uw gegevens op het Experience Platform.
- **Modellen:** Verstrekt hulpmiddelen die worden gebruikt om, geavanceerde machine het leren recepten en modellen tot stand te brengen te publiceren en op te slaan. Ga voor meer informatie naar de zelfstudie voor het [maken en publiceren van een model](./models-recipes/create-publish-model.md) voor machinleren.
- **Services:** Bevat zowel de Adobe-geleverde diensten zoals de [Intelligente Diensten](../intelligent-services/home.md) als om het even welke douanediensten u met de Werkruimte van de Wetenschap van Gegevens creeerde.

Waarom zie ik slechts het lusje van de Diensten?

- Uw organisatie mag alleen recht hebben op RTCDP (Real-Time Customer Data Platform), dat de Intelligent Service Customer AI omvat.

Als u om het even welke lusjes van de Wetenschap **van** Gegevens niet kunt zien en wenst om de eigenschappen van de Werkruimte van de Wetenschap van Gegevens te gebruiken, contacteer uw bedrijfbeheerder om te controleren of hebt u een vergunning van de Intelligentie van Adobe Experience Platform.

## Toevoeging Adobe Experience Platform Intelligence-pakket

In de volgende tabel worden enkele belangrijke verschillen voor de Data Science Workspace beschreven, met en zonder het addon-pakket voor Adobe Experience Platform Intelligence:

>[!NOTE]
>
>U kunt meer dan één pakket van de Intelligentie goedkeuring verlenen en de verhoogde capaciteit wordt toegevoegd aan uw algemene recht. Als u bijvoorbeeld een licentie hebt verleend voor 2 toevoeging aan het Adobe Experience Platform Intelligence-pakket, hebt u recht op in totaal 20 gelijktijdige gebruikers van laptops.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] met toevoeging van het inlichtingenpakket |
| --- | :---: | :---: |
| Aantal ondersteunde laptopgebruikers. | 5 gelijktijdige gebruikers | Met het eerste pakket worden 5 gelijktijdige gebruikers toegevoegd en met extra aankopen worden 10 gelijktijdige gebruikers per pakket toegevoegd. |
| Hiermee worden geïntegreerde Jupyter-laptops toegestaan voor verkennende gegevensanalyse en modelontwerp (R, Python, Scala, PySpark) | X | X |
| Geïntegreerde integratie met Query-service. Mogelijkheid om gegevenssets te verkennen en vorm te geven met SQL in notebooks. | X | X |
| Toegang tot vooraf gebouwde laptopsjablonen voor voorspellende analyse. | X | X |
| Teken handmatig modellen met Jupyter-laptops en scoren deze. | X | X |
| Implementeer en operationele modellen met de mogelijkheid om trainingen te plannen en taken te evalueren. |  | X |
| Ontvang een framework om modellen eenvoudig te configureren, te evalueren, op te leiden, te scoren en te publiceren in productie. |  | X |
| Door de gebruikersinterface gestuurde modelexperimenten en -evaluaties. |  | X |
| Diepe leerondersteuning voor Tensorflow-modellen (GPU Compute). |  | X |
| Op parken gebaseerde verdeelde computer om te trainen en tegen grote datasets (10MM + rijen) te scoren. |  | X |

## Toegangsbeheer

Toegangscontrole voor Experience Platform wordt beheerd via de [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden. Zie het [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie.

Om de Werkruimte van de Wetenschap van Gegevens te gebruiken, moet de toestemming &quot;van de Werkruimte van de Wetenschap van Gegevens&quot;worden toegelaten. In de volgende tabel worden de effecten weergegeven van het inschakelen of uitschakelen van deze machtiging:

| Machtiging | Ingeschakeld | Uitgeschakeld |
|---|---|---|
| Werkruimte voor gegevenswetenschap beheren | Verleent toegang tot alle diensten in de Werkruimte van de Wetenschap van Gegevens. | API- en UI-toegang tot alle services in de Data Science Workspace is uitgeschakeld. Als deze optie is uitgeschakeld, kunt u de pagina&#39;s **Laptops**, **Modellen** en **Services** niet selecteren. <li>Toegang tot **services** is mogelijk nog steeds beschikbaar via Real-time Customer Data Platform (RTCDP).</li> |

## Sandbox-ondersteuning

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke instantie van het Platform steunt één productie zandbak en veelvoudige niet productiesandboxes, elk handhaven zijn eigen bibliotheek van Platform middelen. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op de productiesandbox. Zie het [sandboxoverzicht](../sandboxes/home.md)voor meer informatie over sandboxen.

Momenteel geldt voor de Data Science Workspace de volgende sandbox-beperking:

- Compute resources worden gedeeld door de productiesandbox en niet-productiesandboxen.

## Volgende stappen

Dit document schetste de verschillende soorten toegang en eigenschappen beschikbaar in de Werkruimte van de Wetenschap van Gegevens.

Om meer over de Werkruimte van de Wetenschap van Gegevens, zoals een volledig dagelijks werkschema te leren, gelieve te beginnen door de documentatie van de de werkruimte van de Wetenschap van [Gegevens te lezen](./walkthrough.md) . Meer algemene informatie vindt u in het overzicht [van de](./home.md)Data Science Workspace.