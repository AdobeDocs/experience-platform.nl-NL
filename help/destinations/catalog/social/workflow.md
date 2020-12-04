---
keywords: Facebook;facebook;Social network;Social Network;social network authentication;Social network authentication
title: Workflow voor sociale netwerkdoelen
type: Tutorial
seo-title: Workflow voor sociale netwerkdoelen
description: Instructies om verbinding te maken met uw sociale netwerk en accounts
seo-description: Instructies om verbinding te maken met uw sociale netwerk en accounts
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Verificatieworkflow voor bestemmingen voor sociale netwerken {#social-network-destinations-workflow}

## Workflow om sociale netwerkdoelen te maken

Deze zelfstudie gebruikt [!DNL Facebook] als voorbeeld, maar de workflow in Real-time Customer Data Platform zal hetzelfde zijn voor alle sociale netwerkbestemmingen, wanneer er opnieuw aan het product wordt toegevoegd.

Blader in **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]** naar de categorie **[!UICONTROL Sociaal]** . Selecteer uw aangewezen sociale netwerkbestemming, dan uitgezocht **[!UICONTROL vorm]**.

![Verbinden met sociale netwerkbestemming](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](../../ui/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.

Als u in de stap **Verificatie** eerder een verbinding met uw sociale netwerkbestemming had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met uw sociale netwerkbestemming in te stellen. Selecteer **[!UICONTROL Verbinding maken met doel]** . Hiermee gaat u naar de geselecteerde sociale netwerkbestemming om u aan te melden en Adobe Experience Cloud te verbinden met uw sociale netwerk en account Advertentie.

>[!NOTE]
>
>CDP in real time steunt geloofsbevestiging in het authentificatieproces en toont een foutenmelding als u onjuiste geloofsbrieven aan uw identiteitskaart van de sociale netwerkrekening invoert. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinden met sociale netwerkbestemming - authentificatiestap](../../assets/catalog/social/workflow/pre-connect.png)

Zodra uw geloofsbrieven worden bevestigd en Adobe Experience Cloud wordt aangesloten aan uw sociaal netwerk, kunt u **[!UICONTROL Volgende]** selecteren om aan de stap van de **[!UICONTROL Opstelling]** te werk te gaan.

![Credentials bevestigd](../../assets/catalog/social/workflow/post-connect.png)

Voer in de stap **[!UICONTROL Setup]** een [!UICONTROL naam] en een [!UICONTROL beschrijving] in voor de activeringsstroom en vul de [!UICONTROL account-id] van uw sociale netwerk en account in.

Ook in deze stap kunt u elke **[!UICONTROL Gebruikszaak]** voor marketingdoeleinden selecteren die op deze bestemming moet worden toegepast. Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](../../../data-governance/policies/overview.md#core-actions)Gegevens.

Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

>[!IMPORTANT]
>
> * Het marketinggeval *Single Identity Personalization* wordt standaard geselecteerd voor sociale netwerkdoelen en kan niet worden verwijderd.
> * Voor [!DNL Facebook] bestemmingen. **[!UICONTROL Account ID]** is je [!DNL Facebook Ad Account ID]. U vindt deze id in de [!DNL Facebook Ads Manager]lijst. Plaats de id vooraf in de `act_` onderstaande afbeelding:


![Verbinden met sociale netwerkbestemming - opstellingsstap](../../assets/catalog/social/workflow/setup.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [activeren voor sociale netwerken](#activate-segments)voor de rest van de workflow.

## Segmenten activeren op sociale netwerken {#activate-segments}

Voor instructies op hoe te om segmenten aan sociale netwerken te activeren, zie Gegevens aan Doelen [activeren](../../ui/activate-destinations.md).