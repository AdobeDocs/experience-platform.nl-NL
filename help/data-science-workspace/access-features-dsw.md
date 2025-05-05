---
keywords: Experience Platform;home;Data Science Workspace;populaire onderwerpen;toegangscontrole;sandbox;inlichtingenpakket;dsw-functies;dsw-toegang;Adobe Experience Platform Intelligence;intelligentie;aep-inlichtingenpakket
solution: Experience Platform
title: Data Science Workspace Access en functies
description: Het volgende document schetst de toestemmingen van Workspace van de Wetenschap van Gegevens en toegang tot eigenschappen.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# Toegang tot en functies van Data Science Workspace

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Het volgende document schetst de toestemmingen van Workspace van de Wetenschap van Gegevens en toegang tot eigenschappen.

![ de lusjes van DSW ](./images/access/platform-tabs.png)

- **Notitieboekjes:** verstrekt een interactieve ontwikkelomgeving ([ JupyterLab ](./jupyterlab/overview.md)) om, uw gegevens op Experience Platform te onderzoeken te analyseren en te modelleren.
- **Modellen:** verstrekt hulpmiddelen die worden gebruikt om, geavanceerde machine het leren recepten en modellen tot stand te brengen te publiceren en op te slaan. Voor meer informatie, bezoek [ creeer en publiceer een machine het leren model ](./models-recipes/create-publish-model.md) leerprogramma.
- **de Diensten:** bevat zowel de Adobe-Verstrekte diensten zoals [ AI/ML diensten ](../intelligent-services/home.md) en om het even welke douanediensten u met de Wetenschap Workspace van Gegevens creeerde.

Waarom zie ik slechts het lusje van de Diensten?

- Uw organisatie heeft alleen recht op Adobe Real-Time Customer Data Platform (Real-Time CDP), dat de AI/ML Service van de Klant omvat.

Als u om het even welke **Lusjes van de Wetenschap van Gegevens** niet kunt zien en wenst om de eigenschappen van Workspace van de Wetenschap van Gegevens te gebruiken, contacteer uw bedrijfbeheerder om te controleren of hebt u een vergunning van de Intelligentie van Adobe Experience Platform.

## Data Science Workspace-pakket

Data Science Workspace-mogelijkheden zijn beschikbaar in het Adobe Experience Platform Intelligence-pakket en de Advanced Intelligence Pack Add-on

In de volgende tabel worden enkele belangrijke verschillen beschreven voor Data Science Workspace-rechten met en zonder de Advanced Intelligence Pack Add-on:

>[!NOTE]
>
>U kunt meer dan één Advanced Intelligence Pack Addon vergunning geven en de verhoogde capaciteit wordt toegevoegd aan uw algemene recht. Als u bijvoorbeeld een licentie hebt verleend voor 2 Adobe Experience Platform Advanced Intelligence Pack Addons, hebt u recht op in totaal 20 gelijktijdige laptopgebruikers.

| Workspace-machtiging gegevenswetenschap | Alleen Adobe Experience Platform Intelligence Package | Adobe Experience Platform Intelligence plus Advanced Intelligence Pack Add-on |
| --- | :---: | :---: |
| Aantal ondersteunde laptopgebruikers. | 5 gelijktijdige gebruikers | Met het eerste pakket worden 5 gelijktijdige gebruikers toegevoegd en met extra aankopen worden 10 gelijktijdige gebruikers per pakket toegevoegd. |
| Biedt geïntegreerde Jupyter-laptops voor verkennende gegevensanalyse en modelontwerpdoeleinden. | X (Ondersteunt R-, Python- en Scala-bibliotheken) | X (Voegt PySpark en de bibliotheken van XML van de Vonk toe) |
| Geïntegreerde integratie met Query-service. Mogelijkheid om gegevenssets te verkennen en vorm te geven met SQL in notebooks. | X | X |
| Toegang tot vooraf gebouwde laptopsjablonen voor voorspellende analyse. | X | X |
| Teken handmatig modellen met Jupyter-laptops en scoren deze. | X | X |
| Implementeer en operationele modellen met de mogelijkheid om trainingen te plannen en taken te evalueren. | | X |
| Ontvang een framework om modellen eenvoudig te configureren, te evalueren, op te leiden, te scoren en te publiceren in productie. |  | X |
| Door de gebruikersinterface gestuurde modelexperimenten en -evaluaties. | | X |
| Diepe leerondersteuning voor Tensorflow-modellen (GPU Compute). | | X |
| Op parken gebaseerde verdeelde computer om te trainen en tegen grote datasets (10MM + rijen) te scoren. | | X |

## Toegangsbeheer

De controle van de toegang voor Experience Platform wordt beheerd door [ Adobe Admin Console ](https://adminconsole.adobe.com). Deze functionaliteit maakt gebruik van productprofielen in Admin Console, die gebruikers koppelen aan machtigingen en sandboxen. Zie het [ overzicht van de toegangscontrole ](../access-control/home.md) voor meer informatie.

Als u Data Science Workspace wilt gebruiken, moet de machtiging &quot;Manage Data Science Workspace&quot; zijn ingeschakeld. In de volgende tabel worden de effecten weergegeven van het inschakelen of uitschakelen van deze machtiging:

| Machtiging | Ingeschakeld | Uitgeschakeld |
|---|---|---|
| Data Science Workspace beheren | Biedt toegang tot alle services in Data Science Workspace. | API- en UI-toegang tot alle services in Data Science Workspace is uitgeschakeld. Terwijl onbruikbaar gemaakt, wordt het selecteren van de **Notitieboekjes**, **Modellen**, en **de pagina&#39;s van de Diensten** verhinderd. <li>De toegang tot **Diensten** kan nog door Adobe Real-Time Customer Data Platform (Real-Time CDP) beschikbaar zijn.</li> |

## Sandbox-ondersteuning

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke Experience Platform-instantie ondersteunt meerdere productie- en niet-productie sandboxen, elk met een eigen bibliotheek met Experience Platform-bronnen. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op uw productiesandboxen. Voor meer informatie over zandbakken, zie het [ overzicht van zandbakken ](../sandboxes/home.md).

Data Science Workspace heeft momenteel de volgende sandboxbeperking:

- Compute resources worden gedeeld door de productie- en niet-productie-sandboxen.

## Volgende stappen

In dit document worden de verschillende soorten toegang en functies beschreven die beschikbaar zijn in Data Science Workspace.

Om meer over de Wetenschap van Gegevens Workspace, zoals een volledig dagelijks werkschema te leren, gelieve te beginnen door de [&#128279;](./walkthrough.md) documentatie van Workspace van de Wetenschap van 0&rbrace; Gegevens te lezen.  Voor meer algemene informatie, bezoek het [ overzicht van Workspace van de Wetenschap van Gegevens ](./home.md).
