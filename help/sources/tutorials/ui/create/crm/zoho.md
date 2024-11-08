---
keywords: Experience Platform;home;populaire onderwerpen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Creeer een Verbinding van Source van Zoho CRM in UI
type: Tutorial
description: Leer hoe u een Zoho CRM-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Een [!DNL Zoho CRM] bronverbinding maken in de gebruikersinterface

>[!WARNING]
>
>De bron [!DNL Zoho CRM] wordt eind juni 2025 vervangen.

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een bepaalde planning extern gesourceerde CRM-gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Zoho CRM] bronaansluiting met behulp van de gebruikersinterface van [!DNL Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Zoho CRM] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/crm.md).

### Vereiste referenties verzamelen

Als u [!DNL Zoho CRM] wilt verbinden met Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Endpoint | Het eindpunt van de [!DNL Zoho CRM] server u uw verzoek doet aan. |
| Accounts-URL | De account-URL wordt gebruikt om uw toegangs- en vernieuwingstokens te genereren. De URL moet domeinspecifiek zijn. |
| Client-id | De client-id die overeenkomt met uw [!DNL Zoho CRM] -gebruikersaccount. |
| Clientgeheim | Het clientgeheim dat overeenkomt met uw [!DNL Zoho CRM] -gebruikersaccount. |
| Toegangstoken | Met het toegangstoken hebt u tijdelijk en veilig toegang tot uw [!DNL Zoho CRM] -account. |
| Token vernieuwen | Een vernieuwingstoken is een teken dat wordt gebruikt om een nieuw toegangstoken te produceren, zodra uw toegangstoken is verlopen. |

Voor meer informatie over deze geloofsbrieven, zie de documentatie over [[!DNL Zoho CRM]  authentificatie ](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Sluit uw [!DNL Zoho CRM] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Zoho CRM] -account te koppelen aan [!DNL Platform] .

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL CRM] de optie **[!UICONTROL Zoho CRM]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ catalogus ](../../../../images/tutorials/create/zoho/catalog.png)

De pagina **[!UICONTROL Connect Zoho CRM account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Zoho CRM] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/zoho/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en uw [!DNL Zoho CRM] -referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

>[!TIP]
>
>Het URL-domein van uw accounts moet overeenkomen met de juiste domeinlocatie. Hieronder ziet u de verschillende domeinen en de bijbehorende account-URL&#39;s:<ul><li>Verenigde Staten: https://accounts.zoho.com</li><li>Australië: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![ nieuw ](../../../../images/tutorials/create/zoho/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Zoho CRM] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Platform ](../../dataflow/crm.md) te brengen.
