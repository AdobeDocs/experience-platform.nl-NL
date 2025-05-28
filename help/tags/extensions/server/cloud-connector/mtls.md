---
title: Het wederzijdse Overzicht van de Veiligheid van de Laag van het Vervoer (mTLS)
description: Leer hoe u mTLS kunt gebruiken om openbare certificaten veilig op te halen die door Adobe zijn uitgegeven voor het doorsturen van gebeurtenissen.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Overzicht van wederzijdse beveiliging van transportlagen ([!DNL mTLS])

Bind de Wederzijdse certificaten van de Veiligheid van de Laag van het Vervoer ([!DNL mTLS]) in [!UICONTROL Environments UI] om controle van de veiligheid van uw uitbreiding te nemen. Het [!DNL mTLS] -certificaat is een digitale referentie die de identiteit van een server of client in veilige communicatie aantoont. Wanneer u de service-API van [!DNL mTLS] gebruikt, kunt u met deze certificaten uw interactie met Adobe Experience Platform Event Forwarding verifiëren en coderen. Dit proces beschermt niet alleen uw gegevens maar zorgt er ook voor dat elke verbinding afkomstig is van een vertrouwde partner.

## [!DNL mTLS] implementeren in een nieuwe omgeving {#implement-mtls}

Stel de omgeving voor het doorsturen van gebeurtenissen in om ervoor te zorgen dat uw bibliotheek correct wordt geïmplementeerd in het Edge-netwerk. Tijdens de installatie kunt u de hostingoptie selecteren die het best aansluit bij uw implementatiebehoeften. Er wordt automatisch een [!DNL mTLS] -certificaat toegevoegd aan uw nieuwe omgeving voor veilige communicatie.

Als u een nieuwe omgeving wilt maken, selecteert u de tab **[!UICONTROL Environments]** in het linkerdeelvenster van de eigenschappen voor het doorsturen van gebeurtenissen en selecteert u vervolgens **[!UICONTROL Add Environment]** .

![ Gebeurtenis door:sturen eigenschappen die bestaande milieu&#39;s tonen, die [!UICONTROL Add Environment] benadrukken.](../../../images/extensions/server/cloud-connector/add-environment.png)

Selecteer op de volgende pagina de omgeving die u voor deze installatie wilt gebruiken. Er zijn drie omgevingen beschikbaar:

>[!NOTE]
>
>Een eigenschap is beperkt tot één ontwikkeling, één ophaling en één productieomgeving.

| Omgeving | Beschrijving |
| --- | --- |
| Ontwikkeling | De ontwikkelomgeving is voor teamleden om bibliotheken of wijzigingen in Event Forwarding te testen. |
| Staging | De testomgeving is optioneel en stelt goedgekeurde teamleden in staat een bibliotheek te testen en goed te keuren voordat deze wordt gepubliceerd. |
| Productie | De productieomgeving wordt gebruikt voor levende productiegegevens. |

![ het milieu uitgezocht scherm, dat [!UICONTROL Select] voor Ontwikkeling benadrukt.](../../../images/extensions/server/cloud-connector/select-environment.png)

Voor de **[!UICONTROL Create Environment]** pagina, ga a **[!UICONTROL Name]** in en selecteer ***Beheerde Adobe*** van het **[!UICONTROL Select Host]** dropdown menu. **[!UICONTROL Certificate]** wordt ***automatisch toegevoegd***. Selecteer ten slotte **[!UICONTROL Save]** .

![ de Create pagina van het Milieu van de Ontwikkeling, die [!UICONTROL Name], [!UICONTROL Select Host], en [!UICONTROL Save] benadrukt.](../../../images/extensions/server/cloud-connector/create-environment.png)

De omgeving is gemaakt en u keert terug naar het tabblad **[!UICONTROL Environments]** , waarin de nieuwe omgeving wordt weergegeven.

![ het [!UICONTROL Environments] lusje, dat het milieu van de Ontwikkelaar benadrukt.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Certificaatdetails van omgeving weergeven {#view-certificate}

Als u de certificaatdetails voor een omgeving wilt weergeven, selecteert u het tabblad **[!UICONTROL Environments]** in het linkerdeelvenster van de eigenschappen voor het doorsturen van gebeurtenissen en selecteert u de omgeving voor het weergeven van details.

De volgende certificaatdetails worden weergegeven:

| Veldnaam | Beschrijving |
| --- | --- |
| Certificaat | Gegevens van het certificaat, met inbegrip van:<ul><li>**Naam**: De naam van het certificaat.</li><li>**gecreeerd Datum**: De datum toen het certificaat werd gecreeerd.</li><li>**Status**: De huidige status van het certificaat:<ul><li>**Huidige**: Het certificaat is actief in gebruik.</li><li>**verouderd**: Het certificaat is niet in gebruik maar nog niet verlopen. Deze kan nog steeds voor gebruik worden geselecteerd.</li><li>**Verlopen**: Het certificaat is verlopen, grijs uit, en niet meer beschikbaar voor gebruik.</li></ul></ul> |
| Verloopt | De datum waarop het certificaat vervalt. |
| Naam variabele | De variabelenaam van het certificaat. |
| Status | De huidige status van het certificaat:<ul><li>**Gedepolyed**: Het certificaat is met succes opgesteld en is actief.</li><li>**die** opstelt: Het certificaat is in het proces om worden opgesteld.</li><li>**vereist Plaatsing**: Deze status verschijnt wanneer een verouderd certificaat wordt geselecteerd.</li></ul> |

![ de Edit pagina van het Milieu van de Ontwikkeling, die [!UICONTROL Certificate] details benadrukt.](../../../images/extensions/server/cloud-connector/certificate-details.png)

### Een verouderd certificaat selecteren en implementeren {#deploy-obsolete-certificate}

Als u een verouderd certificaat wilt gebruiken, navigeert u naar het tabblad **[!UICONTROL Environments]** in het linkerdeelvenster van de eigenschappen voor het doorsturen van gebeurtenissen en selecteert u de omgeving om de details weer te geven.

![ het [!UICONTROL Environments] lusje, dat het milieu van de Ontwikkelaar benadrukt.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

Selecteer in het vervolgkeuzemenu **[!UICONTROL Certificate]** een verouderd certificaat en selecteer vervolgens **[!UICONTROL Save]** .

![ de Edit pagina van het Milieu van de Ontwikkeling, die [!UICONTROL Certificate] dropdown met verouderd certificaat en sparen benadrukte benadrukt.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Selecteer **[!UICONTROL Save and deploy]** in het dialoogvenster **[!UICONTROL Deploy Certificate]** als u het certificaat wilt gebruiken.

![ stel certificaatdialoog met sparen op en stel benadrukt op.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Volgende stappen {#next-steps}

In dit document wordt getoond hoe u een omgeving maakt voor uw eigenschap Gebeurtenis doorsturen, een certificaat toevoegt en een verouderd certificaat gebruikt. Voor meer informatie over de [!DNL mTLS] certificaten, zie [[!DNL mTLS]  het Overzicht van de Dienst API ](../../../../data-governance/mtls-api/overview.md)

Leren hoe te om [!DNL mTLS] certificaten in Gebeurtenis te gebruiken die regels door:sturen, verwijs naar het [ overzicht van de de uitbreidingsuitbreiding van de Verbinding van de Wolk ](../cloud-connector/overview.md/#mtls-rules).
