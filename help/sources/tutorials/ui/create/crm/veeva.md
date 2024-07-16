---
keywords: Experience Platform;thuis;populaire onderwerpen;Veeva CRM;veeva
solution: Experience Platform
title: Een Veeva CRM Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Veeva CRM-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Een [!DNL Veeva CRM] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een bepaalde planning extern gesourceerde CRM-gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Veeva CRM] bronaansluiting met behulp van de gebruikersinterface van [!DNL Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Veeva CRM] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de broninstantie [!DNL Veeva CRM] . |
| `username` | De gebruikersnaam voor de gebruikersaccount van [!DNL Veeva CRM] . |
| `password` | Het wachtwoord voor de [!DNL Veeva CRM] -gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount van [!DNL Veeva CRM] . |

Voor meer informatie bij het worden begonnen, verwijs naar dit [[!DNL Veeva CRM]  document ](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Sluit uw [!DNL Veeva CRM] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Veeva CRM] -account te koppelen aan [!DNL Platform] .

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL CRM] de optie **[!UICONTROL Veeva CRM]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ catalogus ](../../../../images/tutorials/create/veeva/catalog.png)

De pagina **[!UICONTROL Connect Veeva CRM account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Veeva CRM] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/veeva/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en uw [!DNL Veeva CRM] -referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ nieuw ](../../../../images/tutorials/create/veeva/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Veeva CRM] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Platform ](../../dataflow/crm.md) te brengen.
