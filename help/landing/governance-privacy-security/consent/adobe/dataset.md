---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Een gegevensset configureren voor het vastleggen van toestemmings- en voorkeursgegevens
topic: getting started
description: Leer hoe u een XDM-schema (Experience Data Model) en een gegevensset configureert voor het vastleggen van toestemmings- en voorkeursgegevens in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 980bff169659d3ffc92a0678f8a0b153b3189906
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---


# Een gegevensset configureren om toestemmings- en voorkeursgegevens vast te leggen

Adobe Experience Platform kan uw toestemming-/voorkeursgegevens van de klant alleen verwerken als die gegevens worden verzonden naar een gegevensset waarvan het schema velden bevat die betrekking hebben op toestemmingen en andere machtigingen. Specifiek, moet deze dataset op de [!DNL XDM Individual Profile] klasse worden gebaseerd, en voor gebruik in [!DNL Real-time Customer Profile] worden toegelaten.

Dit document verstrekt stappen om een dataset te vormen om toestemmingsgegevens in Experience Platform te verwerken. Voor een overzicht van de volledige workflow voor het verwerken van toestemmings-/voorkeursgegevens in Platform, raadpleegt u het [overzicht van de verwerking van toestemmingen](./overview.md).

>[!IMPORTANT]
>
>In de voorbeelden in deze handleiding wordt een gestandaardiseerde set velden gebruikt voor de weergave van toestemmingswaarden voor klanten, zoals gedefinieerd door het XDM-gegevenstype [Inhoud en voorkeuren](../../../../xdm/data-types/consents.md). De structuur van deze velden is bedoeld om een efficiënt gegevensmodel te bieden voor een groot aantal gemeenschappelijke gevallen waarin toestemming wordt gegeven.
>
>U kunt echter ook uw eigen combinaties definiëren om toestemming te vertegenwoordigen op basis van uw eigen gegevensmodellen. Vraag uw juridische team om goedkeuring voor een gegevensmodel voor toestemming dat past bij uw bedrijfsbehoeften, op basis van de volgende opties:
>
>* De gestandaardiseerde mengvoeders
>* Een combinatie van aangepaste toestemming die door uw organisatie is gemaakt
>* Een combinatie van de gestandaardiseerde toestemmingsmix en aanvullende velden die worden verstrekt door een aangepaste toestemmingsmix


## Vereisten

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM (Experience Data Model)](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [Klantprofiel](../../../../profile/home.md) in realtime: Consolideert klantgegevens van verschillende bronnen in een volledige, verenigde mening terwijl het aanbieden van een actionable, timestamped rekening van elke klanteninteractie.

>[!IMPORTANT]
>
>In deze zelfstudie wordt ervan uitgegaan dat u het schema [!DNL Profile] in het Platform kent dat u wilt gebruiken om kenmerkgegevens van de klant vast te leggen. Ongeacht de methode u gebruikt om toestemmingsgegevens te verzamelen, moet dit schema [toegelaten voor het Profiel van de Klant in real time](../../../../xdm/ui/resources/schemas.md#profile) zijn. Bovendien kan de primaire identiteit van het schema geen direct identificeerbaar veld zijn dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.

## Inhoud en voorkeuren, mixingstructuur {#structure}

De [!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]-mix (hierna de &quot;mix van constanten en voorkeuren&quot; genoemd) verschaft gestandaardiseerde toestemmingsvelden voor een schema. Momenteel is deze mix alleen compatibel met schema&#39;s die zijn gebaseerd op de klasse [!DNL XDM Individual Profile].

De mix biedt één objecttype veld, `consents`, waarvan de subeigenschappen een set gestandaardiseerde toestemmingsvelden vastleggen. Het volgende JSON is een voorbeeld van het soort gegevens dat `consents` verwacht na gegevensinvoer:

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
>Voor meer informatie over de structuur en betekenis van de subeigenschappen in `consents`, zie het overzicht op [het gegevenstype van de Inhoud &amp; van de Voorkeur](../../../../xdm/data-types/consents.md).

## Voeg de mix Consents &amp; Preferences toe aan uw [!DNL Profile] schema {#add-mixin}

In Platform UI, selecteer **[!UICONTROL Schemas]** in de linkernavigatie, dan selecteer **[!UICONTROL Browse]** tabel om een lijst van bestaande schema&#39;s te tonen. Van hier, selecteer de naam van [!DNL Profile]-Toegelaten schema dat u toestemmingsgebieden aan wilt toevoegen. De schermafbeeldingen in deze sectie gebruiken het schema &quot;van de Leden van de Loyalty&quot;dat in [schemaaanmaakzelfstudie](../../../../xdm/tutorials/create-schema-ui.md) als voorbeeld wordt gebouwd.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>U kunt de zoek- en filtermogelijkheden van de werkruimte gebruiken om uw schema gemakkelijker te vinden. Zie de handleiding bij [het verkennen van XDM-bronnen](../../../../xdm/ui/explore.md) voor meer informatie.

De [!DNL Schema Editor] verschijnt, die de structuur van het schema in het canvas tonen. Selecteer **[!UICONTROL Add]** onder de sectie **[!UICONTROL Mixins]** links op het canvas.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-mixin.png)

Het dialoogvenster **[!UICONTROL Add mixin]** wordt weergegeven. Selecteer **[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo gemakkelijker de mix te vinden. Selecteer **[!UICONTROL Add mixin]** als de mix is geselecteerd.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/mixin-dialog.png)

Het canvas verschijnt weer en geeft aan dat het object `consents` is toegevoegd aan de schemastructuur. Als u extra toestemmings en voorkeursgebieden die niet door de standaardmengeling worden gevangen vereist, zie de bijlage sectie op [toevoegend de gebieden van de douanetoestemming en voorkeur aan het schema](#custom-consent). Anders, selecteer **[!UICONTROL Save]** om de veranderingen in het schema te voltooien.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

Als het schema u uitgeeft door [!UICONTROL Profile Dataset] wordt gebruikt die in uw de randconfiguratie van SDK van het Web van Platforms wordt gespecificeerd, zal die dataset nu de nieuwe toestemmingsgebieden omvatten. U kunt nu naar [toestemmingsverwerkingsgids](./overview.md#merge-policies) terugkeren om het proces voort te zetten om Experience Platform te vormen om toestemmingsgegevens te verwerken.

Als u geen dataset voor dit schema hebt gecreeerd, volg de stappen in de volgende sectie.

## Creeer een dataset die op uw toestemmingsschema {#dataset} wordt gebaseerd

Zodra u een schema met toestemmingsgebieden hebt gecreeerd, moet u een dataset tot stand brengen die uiteindelijk de gegevens van de klantentoestemming zal opnemen. Deze dataset moet voor [!DNL Real-time Customer Profile] worden toegelaten.

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie en selecteer **[!UICONTROL Create dataset]** in de rechterbovenhoek om te beginnen.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Selecteer **[!UICONTROL Create dataset from schema]** op de volgende pagina.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

De **[!UICONTROL Create dataset from schema]**-workflow wordt weergegeven, te beginnen bij de stap **[!UICONTROL Select schema]**. Zoek in de opgegeven lijst een van de toestemmingsschema&#39;s die u eerder hebt gemaakt. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en het schema gemakkelijker te vinden. Selecteer het keuzerondje naast het gewenste schema en selecteer **[!UICONTROL Next]** om door te gaan.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

De stap **[!UICONTROL Configure dataset]** wordt weergegeven. Geef een unieke, gemakkelijk herkenbare naam en beschrijving voor de gegevensset voordat u **[!UICONTROL Finish]** selecteert.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

De detailspagina voor de pas gecreëerde dataset verschijnt. Als de dataset op uw tijd-reeksen schema gebaseerd is, dan is het proces volledig. Als de dataset op uw verslagschema gebaseerd is, moet de definitieve stap in het proces de dataset voor gebruik in [!DNL Real-time Customer Profile] toelaten.

Selecteer in de rechtertrack de schakeloptie **[!UICONTROL Profile]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Tot slot selecteer **[!UICONTROL Enable]** in bevestigingspopover om het schema voor [!DNL Profile] toe te laten.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

De dataset wordt nu bewaard en toegelaten voor gebruik in [!DNL Profile]. Als u van plan bent gebruikend het Web SDK van het Platform om toestemmingsgegevens naar Profiel te verzenden, moet u deze dataset als [!UICONTROL Profile Dataset] selecteren wanneer vestiging uw [randconfiguratie](../../../../edge/fundamentals/edge-configuration.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u toestemmingsgebieden aan een [!DNL Profile]-Toegelaten schema toegevoegd, waarvan dataset zal worden gebruikt om toestemmingsgegevens in te voeren gebruikend het Web SDK van het Platform of directe opname XDM.

U kunt nu naar [overzicht van de toestemmingsverwerking ](./overview.md#merge-policies) terugkeren om Experience Platform te blijven vormen om toestemmingsgegevens te verwerken.

## Aanhangsel

De volgende sectie bevat extra informatie over het creëren van een dataset om klantentoestemming en voorkeursgegevens in te gaan.

### Aangepaste toestemmings- en voorkeursvelden toevoegen aan het schema {#custom-consent}

Als u extra toestemmingssignalen buiten die moet vangen die door de standaard [!DNL Consents & Preferences] mengen worden vertegenwoordigd, kunt u de componenten van douaneXDM gebruiken om uw toestemmingsschema te verbeteren om uw bijzondere bedrijfsbehoeften aan te passen. In deze sectie worden de basisbeginselen beschreven voor het aanpassen van het toestemmingsschema op een manier die compatibel is met de opdrachten voor het wijzigen van de instemming van Adobe Experience Platform Mobile en Web SDK&#39;s.

>[!IMPORTANT]
>
>U moet de [!DNL Consents & Preferences] mix gebruiken als basislijn voor de structuur van uw toestemmingsgegevens en extra gebieden toevoegen zoals nodig, eerder dan het proberen om de volledige structuur van kras tot stand te brengen.

Als u aangepaste velden wilt toevoegen aan de structuur van een standaardmix, moet u eerst een aangepaste mix maken. Nadat u de [!DNL Consents & Preferences]-mix aan het schema hebt toegevoegd, selecteert u het **plus-pictogram (+)** in de sectie **[!UICONTROL Mixins]** en selecteert u **[!UICONTROL Create new mixin]**. Geef een naam en een optionele beschrijving voor de mix op en selecteer **[!UICONTROL Add mixin]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-mixin.png)

De [!DNL Schema Editor] verschijnt opnieuw met de nieuwe douanemix die in de linkerspoorstaaf wordt geselecteerd. Op het canvas worden besturingselementen weergegeven waarmee u aangepaste velden kunt toevoegen aan de schemastructuur. Als u een nieuw toestemmings- of voorkeursveld wilt toevoegen, selecteert u het pictogram **plus (+)** naast het object `consents`.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Er wordt een nieuw veld weergegeven in het object `consents`. Aangezien u een aangepast veld toevoegt aan een standaard XDM-object, wordt het nieuwe veld gemaakt onder een object dat een naam krijgt toegewezen aan uw huurder-id.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

Geef in de rechtertrack onder **[!UICONTROL Field properties]** een naam en beschrijving voor het veld op. Wanneer u **[!UICONTROL Type]** van het veld selecteert, moet u het juiste standaardgegevenstype gebruiken voor een veld met aangepaste toestemming of voorkeur:

* [[!UICONTROL Generic Consent Field]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Generic Marketing Preference Field]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Generic Marketing Preference Field with Subscriptions]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Generic Personalization Preference Field]](../../../../xdm/data-types/personalization-field.md)

Selecteer **[!UICONTROL Apply]** als u klaar bent.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Het toestemmings- of voorkeursveld wordt toegevoegd aan de schemastructuur. De naamruimte [!UICONTROL Path] die in de rechtertrack wordt weergegeven, bevat de naamruimte `_tenantId`. Deze naamruimte moet worden opgenomen wanneer u in de gegevensbewerkingen naar dit veld verwijst.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Voer de bovenstaande stappen uit om door te gaan met het toevoegen van de toestemmings- en voorkeurvelden die u nodig hebt. Als u klaar bent, selecteert u **[!UICONTROL Save]** om uw wijzigingen te bevestigen.

Als het schema u uitgeeft door [!UICONTROL Profile Dataset] wordt gebruikt die in uw de randconfiguratie van SDK van het Web van Platforms wordt gespecificeerd, zal die dataset nu de nieuwe toestemmingsgebieden omvatten. U kunt nu naar [toestemmingsverwerkingsgids](./overview.md#merge-policies) terugkeren om het proces voort te zetten om Experience Platform te vormen om toestemmingsgegevens te verwerken.

Als u geen dataset voor dit schema hebt gecreeerd, ga aan de sectie op [creërend een dataset](#dataset) verder.