---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Een gegevensset configureren voor het vastleggen van toestemmings- en voorkeursgegevens
topic-legacy: getting started
description: Leer hoe u een XDM-schema (Experience Data Model) en een gegevensset configureert voor het vastleggen van toestemmings- en voorkeursgegevens in Adobe Experience Platform.
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# Een gegevensset configureren om toestemmings- en voorkeursgegevens vast te leggen

Adobe Experience Platform kan uw toestemming-/voorkeursgegevens van de klant alleen verwerken als die gegevens worden verzonden naar een gegevensset waarvan het schema velden bevat die betrekking hebben op toestemmingen en andere machtigingen. Deze gegevensset moet met name gebaseerd zijn op de [!DNL XDM Individual Profile] en ingeschakeld voor gebruik in [!DNL Real-time Customer Profile].

Dit document verstrekt stappen om een dataset te vormen om toestemmingsgegevens in Experience Platform te verwerken. Voor een overzicht van de volledige workflow voor het verwerken van toestemmings-/voorkeursgegevens in Platform raadpleegt u de [overzicht van verwerking van toestemming](./overview.md).

>[!IMPORTANT]
>
>In de voorbeelden in deze handleiding wordt een gestandaardiseerde set velden gebruikt voor de weergave van waarden voor de toestemming van de klant, zoals gedefinieerd door de [[!UICONTROL Consent and Preference Details] schemaveldgroep](../../../../xdm/field-groups/profile/consents.md). De structuur van deze velden is bedoeld om een efficiënt gegevensmodel te bieden voor een groot aantal gemeenschappelijke gevallen waarin toestemming wordt gegeven.
>
>U kunt echter ook uw eigen veldgroepen definiëren om toestemming te vertegenwoordigen op basis van uw eigen gegevensmodellen. Vraag uw juridische team om goedkeuring voor een gegevensmodel voor toestemming dat past bij uw bedrijfsbehoeften, op basis van de volgende opties:
>
>* De standaardveldgroep voor toestemming
>* Een veldgroep voor aangepaste toestemming die door uw organisatie is gemaakt
>* Een combinatie van de standaardveldgroep voor toestemming en aanvullende velden die worden verstrekt door een veldgroep voor aangepaste toestemming


## Vereisten

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [Klantprofiel in realtime](../../../../profile/home.md): Consolideert klantgegevens van verschillende bronnen in een volledige, verenigde mening terwijl het aanbieden van een actionable, timestamped rekening van elke klanteninteractie.

>[!IMPORTANT]
>
>In deze zelfstudie wordt ervan uitgegaan dat u de [!DNL Profile] schema in Platform dat u wilt gebruiken om de informatie van de klantenattributen te vangen. Ongeacht de methode die u gebruikt voor het verzamelen van toestemmingsgegevens, moet dit schema [ingeschakeld voor realtime klantprofiel](../../../../xdm/ui/resources/schemas.md#profile). Bovendien kan de primaire identiteit van het schema geen direct identificeerbaar veld zijn dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.

## [!UICONTROL Consent and Preference Details] veldgroepstructuur {#structure}

De [!UICONTROL Consent and Preference Details] de gebiedsgroep verstrekt gestandaardiseerde toestemmingsgebieden aan een schema. Deze veldgroep is momenteel alleen compatibel met schema&#39;s op basis van de [!DNL XDM Individual Profile] klasse.

De veldgroep bevat één veld van het objecttype. `consents`, waarvan de subeigenschappen een reeks gestandaardiseerde toestemmingsvelden vastleggen. Het volgende JSON is een voorbeeld van het soort gegevens `consents` verwacht bij gegevensinvoer:

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Voor meer informatie over de structuur en betekenis van de subeigenschappen in `consents`, zie het overzicht op [[!UICONTROL Consent and Preference Details] veldgroep](../../../../xdm/field-groups/profile/consents.md).

## Voeg de vereiste veldgroepen toe aan uw [!DNL Profile] schema {#add-field-group}

Als u gegevens over toestemming wilt verzamelen met de Adobe-standaard, moet u een schema voor Profiel hebben dat de volgende twee veldgroepen bevat:

* [!UICONTROL Consent and Preference Details]
* [!UICONTROL IdentityMap] (vereist als het gebruiken van het Web van het Platform of Mobiele SDK om toestemmingssignalen te verzenden)

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Schemas]** in de linkernavigatie, dan selecteer **[!UICONTROL Browse]** om een lijst met bestaande schema&#39;s weer te geven. Selecteer hier de naam van de [!DNL Profile]-enabled schema dat u toestemmingsgebieden aan wilt toevoegen. In de schermafbeeldingen in deze sectie wordt het schema &quot;Loyalty-leden&quot; gebruikt dat is ingebouwd in het [zelfstudie over het maken van schema&#39;s](../../../../xdm/tutorials/create-schema-ui.md) als voorbeeld.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>U kunt de zoek- en filtermogelijkheden van de werkruimte gebruiken om uw schema gemakkelijker te vinden. Zie de handleiding op [XDM-bronnen verkennen](../../../../xdm/ui/explore.md) voor meer informatie .

De [!DNL Schema Editor] wordt weergegeven en toont u de structuur van het schema in het canvas. Selecteer links op het canvas de optie **[!UICONTROL Add]** onder de **[!UICONTROL Field groups]** sectie.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

De **[!UICONTROL Add field group]** wordt weergegeven. Selecteer **[!UICONTROL Consent and Preference Details]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo de veldgroep gemakkelijker te vinden.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Zoek vervolgens de **[!UICONTROL IdentityMap]** veldgroep in de lijst en selecteer deze ook. Selecteer **[!UICONTROL Add field groups]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

Het canvas verschijnt opnieuw, waarbij wordt getoond dat de `consents` en `identityMap` er zijn velden toegevoegd aan de schemastructuur. Als u aanvullende toestemmings- en voorkeursvelden nodig hebt die niet door de standaardveldgroep worden vastgelegd, raadpleegt u de sectie in de bijlage over [het toevoegen van douane toestemmings en voorkeursgebieden aan het schema](#custom-consent). Anders selecteert u **[!UICONTROL Save]** om de wijzigingen in het schema te voltooien.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Als u een nieuw schema maakt of een bestaand schema bewerkt dat niet is ingeschakeld voor Profiel, moet u [het schema voor profiel inschakelen](../../../../xdm/ui/resources/schemas.md#profile) vóór het opslaan.

Als het schema dat u hebt bewerkt door de [!UICONTROL Profile Dataset] gespecificeerd in uw Platform SDK gegevensstroom van het Web, zal die dataset nu de nieuwe toestemmingsgebieden omvatten. U kunt nu terugkeren naar het dialoogvenster [toestemmingsverwerkingsgids](./overview.md#merge-policies) om het proces voort te zetten van het vormen van Experience Platform om toestemmingsgegevens te verwerken. Als u geen dataset voor dit schema hebt gecreeerd, volg de stappen in de volgende sectie.

## Een gegevensset maken op basis van uw toestemmingsschema {#dataset}

Zodra u een schema met toestemmingsgebieden hebt gecreeerd, moet u een dataset tot stand brengen die uiteindelijk de gegevens van de klantentoestemming zal opnemen. Deze gegevensset moet zijn ingeschakeld voor [!DNL Real-time Customer Profile].

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie selecteert u vervolgens **[!UICONTROL Create dataset]** in de rechterbovenhoek.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Selecteer op de volgende pagina de optie **[!UICONTROL Create dataset from schema]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

De **[!UICONTROL Create dataset from schema]** wordt weergegeven, te beginnen bij de **[!UICONTROL Select schema]** stap. Zoek in de opgegeven lijst een van de toestemmingsschema&#39;s die u eerder hebt gemaakt. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en het schema gemakkelijker te vinden. Selecteer het keuzerondje naast het gewenste schema en selecteer vervolgens **[!UICONTROL Next]** om door te gaan.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

De **[!UICONTROL Configure dataset]** wordt weergegeven. Geef een unieke, gemakkelijk identificeerbare naam en beschrijving voor de gegevensset voordat u **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

De detailspagina voor de pas gecreëerde dataset verschijnt. Als de dataset op uw tijd-reeksen schema gebaseerd is, dan is het proces volledig. Als de dataset op uw verslagschema gebaseerd is, moet de definitieve stap in het proces de dataset voor gebruik toelaten binnen [!DNL Real-time Customer Profile].

Selecteer in het rechterspoor de optie **[!UICONTROL Profile]** schakelen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Tot slot selecteert u **[!UICONTROL Enable]** in de bevestigingspop-up om het schema voor [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

De dataset wordt nu opgeslagen en ingeschakeld voor gebruik in [!DNL Profile]. Als u van plan bent gebruikend SDK van het Web van het Platform om toestemmingsgegevens naar Profiel te verzenden, moet u deze dataset als [!UICONTROL Profile Dataset] wanneer u uw [datastream](../../../../edge/datastreams/overview.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u machtigingsvelden toegevoegd aan een [!DNL Profile]- toegelaten schema, de waarvan dataset zal worden gebruikt om toestemmingsgegevens in te voeren gebruikend het Web SDK van het Platform of directe inname XDM.

U kunt nu terugkeren naar het dialoogvenster [overzicht van verwerking van toestemming](./overview.md#merge-policies) om Experience Platform te blijven vormen om toestemmingsgegevens te verwerken.

## Aanhangsel

De volgende sectie bevat extra informatie over het creëren van een dataset om klantentoestemming en voorkeursgegevens in te gaan.

### Aangepaste toestemmings- en voorkeursvelden toevoegen aan het schema {#custom-consent}

Als u extra toestemmingssignalen buiten die moet vangen die door de norm worden vertegenwoordigd [!UICONTROL Consent and Preference Details] veldgroep, kunt u aangepaste XDM componenten gebruiken om uw toestemmingsschema te verbeteren om uw bijzondere bedrijfsbehoeften aan te passen. In deze sectie worden de basisbeginselen beschreven voor het aanpassen van uw toestemmingsschema om deze signalen in Profiel in te voeren.

>[!IMPORTANT]
>
>Het Web van het Platform en Mobiele SDKs steunt geen douanegebieden in hun toestemming-verandering bevelen. De enige manier om aangepaste toestemmingsvelden in Profiel in te voeren, is door [batch-opname](../../../../ingestion/batch-ingestion/overview.md) of [bronverbinding](../../../../sources/home.md).

Het wordt ten zeerste aanbevolen om de [!UICONTROL Consent and Preference Details] veldgroep als basislijn voor de structuur van uw toestemmingsgegevens en voeg extra gebieden toe zoals nodig, eerder dan het proberen om de volledige structuur van kras tot stand te brengen.

Als u aangepaste velden wilt toevoegen aan de structuur van een standaardveldgroep, moet u eerst een aangepaste veldgroep maken. Na het toevoegen van [!UICONTROL Consent and Preference Details] veldgroep aan het schema, selecteer **plus (+)** in het deelvenster **[!UICONTROL Field groups]** en selecteert u vervolgens **[!UICONTROL Create new field group]**. Geef een naam en een optionele beschrijving voor de veldgroep op en selecteer **[!UICONTROL Add field group]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

De [!DNL Schema Editor] verschijnt weer met de nieuwe aangepaste veldgroep geselecteerd in de linkerrail. Op het canvas worden besturingselementen weergegeven waarmee u aangepaste velden kunt toevoegen aan de schemastructuur. Als u een nieuw toestemmings- of voorkeursveld wilt toevoegen, selecteert u de optie **plus (+)** pictogram naast `consents` object.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Er wordt een nieuw veld weergegeven in het dialoogvenster `consents` object. Aangezien u een aangepast veld toevoegt aan een standaard XDM-object, wordt het nieuwe veld gemaakt onder een object dat een naam krijgt toegewezen aan uw huurder-id.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

In de rechtertrein onder **[!UICONTROL Field properties]** geeft u een naam en een beschrijving voor het veld op. Bij het selecteren van de velden **[!UICONTROL Type]** moet u het juiste standaardgegevenstype voor een aangepast toestemmings- of voorkeursveld gebruiken:

* [[!UICONTROL Generic Consent Field]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Generic Marketing Preference Field]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Generic Marketing Preference Field with Subscriptions]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Generic Personalization Preference Field]](../../../../xdm/data-types/personalization-field.md)

Als u klaar bent, selecteert u **[!UICONTROL Apply]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Het toestemmings- of voorkeursveld wordt toegevoegd aan de schemastructuur. De [!UICONTROL Path] in het rechterspoor wordt de `_tenantId` naamruimte. Deze naamruimte moet worden opgenomen wanneer u in de gegevensbewerkingen naar dit veld verwijst.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Voer de bovenstaande stappen uit om door te gaan met het toevoegen van de toestemmings- en voorkeurvelden die u nodig hebt. Als u klaar bent, selecteert u **[!UICONTROL Save]** om uw wijzigingen te bevestigen.

Als u geen dataset voor dit schema hebt gecreeerd, ga aan de sectie over [een gegevensset maken](#dataset).
