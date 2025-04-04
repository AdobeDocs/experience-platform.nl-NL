---
keywords: Experience Platform;home;populaire onderwerpen;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Een Source-verbinding met PostSQL maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een PostSQL-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# Een [!DNL PostgreSQL] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL PostgreSQL] bronaansluiting met behulp van de gebruikersinterface van [!DNL Experience Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL PostgreSQL] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL PostgreSQL] account op [!DNL Experience Platform] , moet u de volgende waarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account is gekoppeld. Het patroon van de [!DNL PostgreSQL] verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}` . |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL PostgreSQL]  document ](https://www.postgresql.org/docs/9.2/app-psql.html).

#### SSL-versleuteling inschakelen voor uw verbindingstekenreeks

U kunt SSL-codering inschakelen voor de [!DNL PostgreSQL] -verbindingstekenreeks door uw verbindingstekenreeks toe te voegen met de volgende eigenschappen:

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `EncryptionMethod` | Hiermee kunt u SSL-codering inschakelen voor uw [!DNL PostgreSQL] -gegevens. | <uL><li>`EncryptionMethod=0` (Uitgeschakeld)</li><li>`EncryptionMethod=1` (Ingeschakeld)</li><li>`EncryptionMethod=6` (RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Hiermee wordt het certificaat gevalideerd dat door de [!DNL PostgreSQL] -database wordt verzonden wanneer `EncryptionMethod` wordt toegepast. | <uL><li>`ValidationServerCertificate=0` (Uitgeschakeld)</li><li>`ValidationServerCertificate=1` (Ingeschakeld)</li></ul> |

Hier volgt een voorbeeld van een [!DNL PostgreSQL] verbindingstekenreeks die is toegevoegd met SSL-codering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1` .

## Sluit uw [!DNL PostgreSQL] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL PostgreSQL] -account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL PostgreSQL DB]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL PostgreSQL] -connector te maken.

![](../../../../images/tutorials/create/postgresql/catalog.png)

De pagina **[!UICONTROL Connect to [!DNL PostgreSQL]]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL PostgreSQL] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/postgresql/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL PostgreSQL] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL PostgreSQL] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
