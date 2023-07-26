---
title: Uw Salesforce-account aansluiten via de gebruikersinterface van het Experience Platform
description: Leer hoe u uw Salesforce-account koppelt en uw CRM-gegevens via de gebruikersinterface naar het Experience Platform brengt.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Verbind uw [!DNL Salesforce] account aan Experience Platform met behulp van de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Salesforce] en breng uw gegevens van CRM naar Adobe Experience Platform gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geverifieerde [!DNL Salesforce] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het vormen van een gegevensstroom voor de gegevens van CRM](../../dataflow/crm.md).

### Vereiste referenties verzamelen {#gather-required-credentials}

Om uw [!DNL Salesforce] account voor Experience Platform, moet u waarden opgeven die overeenkomen met het volgende [!DNL Salesforce] referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de [!DNL Salesforce] broninstantie. |
| `username` | De gebruikersnaam voor de [!DNL Salesforce] gebruikersaccount. |
| `password` | Het wachtwoord voor de [!DNL Salesforce] gebruikersaccount. |
| `securityToken` | De beveiligingstoken voor de [!DNL Salesforce] gebruikersaccount. |
| `apiVersion` | (Optioneel) De REST API-versie van de [!DNL Salesforce] -instantie die u gebruikt. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Raadpleeg voor meer informatie over verificatie de [dit [!DNL Salesforce] verificatiehandleiding](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om verbinding te maken met uw [!DNL Salesforce] aan Experience Platform.

## Verbind uw [!DNL Salesforce] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot de bronwerkruimte toegang te hebben. De *[!UICONTROL Catalog]* het scherm toont een verscheidenheid van bronnen beschikbaar in de catalogus van bronnen van het Experience Platform.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook een specifieke bron zoeken met de zoekoptie.

Selecteren **[!UICONTROL CRM]** in de lijst met categorieën bronnen en selecteer vervolgens **[!UICONTROL Add data]** van de [!DNL Salesforce] kaart.

![De broncatalogus op het Experience Platform UI met de Salesforce-bronkaart geselecteerd.](../../../../images/tutorials/create/salesforce/catalog.png)

De **[!UICONTROL Connect to Salesforce]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!BEGINTABS]

>[!TAB Bestaande Salesforce-account gebruiken]

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven. Selecteer **[!UICONTROL Next]** om verder te gaan.

![Een lijst met geverifieerde Salesforce-accounts die al in uw organisatie bestaan.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Een nieuw Salesforce-account maken]

Als u een nieuwe account wilt gebruiken, selecteert u **[!UICONTROL New account]** en geef een naam, beschrijving en uw [!DNL Salesforce] verificatiegegevens. Selecteer **[!UICONTROL Connect to source]** en wacht een paar seconden tot de nieuwe verbinding tot stand is gebracht.

![De interface waarin u een nieuwe rekening kunt tot stand brengen Salesforce door de aangewezen authentificatiegeloofsbrieven te verstrekken.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/crm.md).
