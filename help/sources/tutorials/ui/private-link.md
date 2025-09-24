---
title: Ondersteuning voor privé-koppelingen voor bronnen in de gebruikersinterface
description: Leer hoe u Azure Private Links voor Bronnen gebruikt in de gebruikersinterface van Experience Platform.
exl-id: 2882729e-2d46-48dc-9227-51dda5bf7dfb
source-git-commit: 4d82b0a7f5ae9e0a7607fe7cb75261e4d3489eff
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# Steun van de privé Verbinding voor Bronnen in UI

>[!AVAILABILITY]
>
>Deze functie wordt ondersteund door de volgende bronnen:
>
>* [[!DNL Azure Blob Storage]](../../connectors/cloud-storage/blob.md)
>* [[!DNL ADLS Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>
>Ondersteuning voor privé-koppelingen is momenteel alleen beschikbaar voor organisaties die Adobe Healthcare Shield of Adobe Privacy &amp; Security Shield hebben aangeschaft.

Met de functie Privékoppelingen kunt u persoonlijke eindpunten maken waarmee uw Adobe Experience Platform-bronnen verbinding kunnen maken. Sluit veilig uw bronnen aan een virtueel netwerk aan gebruikend privé IP adressen, die de behoefte aan openbare IPs elimineren en uw aanvalsoppervlakte verminderen. Vereenvoudig uw netwerkopstelling door de behoefte aan complexe firewall of de configuraties van de Vertaling van het Adres van het Netwerk te verwijderen, terwijl het verzekeren van gegevensverkeer slechts de goedgekeurde diensten bereikt.

Lees deze gids om te leren hoe u de bronwerkruimte in Experience Platform UI kunt gebruiken om een privé eindpunt tot stand te brengen en te gebruiken.

>[!BEGINSHADEBOX]

## Licentiegebruiksrechten voor ondersteuning van persoonlijke koppelingen

De machtigingsgegevens voor het gebruik van licenties voor ondersteuning van persoonlijke koppelingen in bronnen zijn als volgt:

* Klanten hebben recht op maximaal 2 TB per jaar gegevensoverdracht via ondersteunde bronnen ([!DNL Azure Blob Storage] , [!DNL ADLS Gen2] en [!DNL Azure File Storage] ) voor alle sandboxen en organisaties.
* Elke organisatie kan een maximum van 10 eindpunten voor alle productie zandbakken hebben.
* Elke organisatie kan een maximum van 1 eindpunt voor alle ontwikkelingszandbakken hebben.

>[!ENDSHADEBOX]

## Een privé-eindpunt maken

Als u aan de slag wilt met persoonlijke koppelingen, navigeert u naar de catalogus *[!UICONTROL Sources]* van de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Private endpoints]** in het menu met tabbladen in de werkruimte Bronnen.

![ de broncatalogus met &quot;Privé eindpunten&quot;.](../../images/tutorials/private-links/catalog.png)

Gebruik de interface om informatie over bestaande privé eindpunten, zoals hun identiteitskaart, bijbehorende bron, en huidige status te bekijken. Selecteer **[!UICONTROL Create private endpoint]** als u een nieuw privé-eindpunt wilt maken.

![ de Privé eindpunten interface met &quot;creeer privé eindpunt&quot;geselecteerd.](../../images/tutorials/private-links/private-endpoints.png)

Kies vervolgens de gewenste bron en voer waarden in voor de volgende eigenschappen:

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw privé eindpunt. |
| `subscriptionId` | De id die is gekoppeld aan uw [!DNL Azure] -abonnement. Voor meer informatie, lees de [!DNL Azure] gids op [ het terugwinnen van uw abonnement en huurder IDs van  [!DNL Azure Portal] ](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | De naam van de bronnengroep op [!DNL Azure] . Een resourcegroep bevat gerelateerde bronnen voor een [!DNL Azure] -oplossing. Voor meer informatie, lees de [!DNL Azure] gids over [ het leiden middelgroepen ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceGroup` | De naam van uw bron. In [!DNL Azure] verwijst een bron naar instanties zoals virtuele machines, webapps en databases. Voor meer informatie, lees de [!DNL Azure] gids op [ die de  [!DNL Azure]  middelmanager ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview) begrijpt. |

{style="table-layout:auto"}

Selecteer **[!UICONTROL Submit]** als u klaar bent.

![ het authentificatievenster voor het creëren van een nieuw privé eindpunt in de bronUI werkruimte.](../../images/tutorials/private-links/create-private-endpoint.png)

### Een privé-eindpunt goedkeuren

Een nieuw gecreeerd eindpunt blijft in een hangende staat tot het door een beheerder wordt goedgekeurd.

Als u een aanvraag voor een privéeindpunt voor de bronnen [!DNL Azure Blob] en [!DNL Azure Data Lake Gen2] wilt goedkeuren, meldt u zich aan bij de map [!DNL Azure Portal] . Selecteer in de linkernavigatie **[!DNL Data storage]** , ga naar de tab **[!DNL Security + networking]** en kies **[!DNL Networking]** . Selecteer vervolgens **[!DNL Private endpoints]** om een lijst weer te geven met persoonlijke eindpunten die zijn gekoppeld aan uw account en de huidige verbindingsstatussen. Als u een aanvraag in behandeling wilt goedkeuren, selecteert u het gewenste eindpunt en klikt u op **[!DNL Approve]** .

![ het Azure portaal met een lijst van hangende privé eindpunten.](../../images/tutorials/private-links/azure.png)

## Een account met een privé-eindpunt maken

Navigeer naar de broncatalogus en selecteer een bron die persoonlijke eindpunten ondersteunt. Maak vervolgens een nieuw account met uw bron en selecteer de schakeloptie **[!UICONTROL Private endpoint]** tijdens accountverificatie. Geef de verificatiereferenties van uw bron op en selecteer vervolgens **[!UICONTROL Connect to source]** Een paar minuten toestaan om de verbinding tot stand te brengen.

>[!NOTE]
>
>Als de optie [!UICONTROL Private endpoint] is ingeschakeld, controleert Experience Platform of er een goedgekeurd privé-eindpunt bestaat voor de geselecteerde bron. Als geen goedgekeurd eindpunt wordt gevonden, zult u geen verbinding kunnen vestigen.

![ de nieuwe stap van de rekeningsauthentificatie met privé toegelaten eindpunten.](../../images/tutorials/private-links/new-account.png)

Navigeer vervolgens naar de interface [!UICONTROL Existing account] van de bron. Gebruik deze interface om een lijst weer te geven van uw bestaande accounts en de bijbehorende status. U kunt het filterpictogram ![ filterpictogram ](../../../images/icons/filter.png) selecteren om slechts de rekeningen te tonen die om met een privé eindpunt zijn toegelaten te verbinden.

![ de bestaande rekeningsinterface in het bronwerkschema toont slechts de gefiltreerde rekeningen die voor privé eindpuntverbindingen worden toegelaten.](../../images/tutorials/private-links/existing-private-endpoints.png)

Selecteer de account die u wilt gebruiken en schakel **[!UICONTROL Interactive Authoring]** in. Met deze schakeloptie activeert u [!UICONTROL Interactive Authoring] , een [!DNL Azure] -functie waarmee u verbindingen kunt testen, kunt bladeren in mappen en gegevens kunt voorvertonen. U moet [!UICONTROL Interactive Authoring] inschakelen voor verbindingen met privéeindpunten. U kunt deze schakeloptie niet handmatig uitschakelen, maar automatisch na 60 minuten.

[!UICONTROL Interactive Authoring] duurt een paar minuten om in te schakelen. Als de instelling is ingeschakeld, selecteert u **[!UICONTROL Next]** om door te gaan naar de volgende stap en de gegevens te selecteren die u wilt invoeren.

![ een bestaande rekening wordt geselecteerd en het interactieve schrijven wordt toegelaten.](../../images/tutorials/private-links/interactive-authoring.png)

## Volgende stappen

Nu u met succes een privé eindpunt hebt gecreeerd, kunt u bronverbindingen en dataflows tot stand brengen, en gegevens opnemen gebruikend privé eindpunten. Lees de volgende hulplijnen voor informatie over het maken van gegevensstromen in de gebruikersinterface:

* [Een gegevensstroom maken voor een bron voor cloudopslag](../ui/dataflow/batch/cloud-storage.md)
* [Een gegevensstroom maken voor een databasebron](../ui/dataflow/databases.md)
