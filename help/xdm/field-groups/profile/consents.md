---
solution: Experience Platform
title: Inhoud en Voorkeuren voor schemaveldgroep
description: Meer informatie over de veldgroep Inhoud en Voorkeuren.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] veldgroep

[!UICONTROL Consents and Preferences] is een standaardgebiedsgroep voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../classes/individual-profile.md) die toestemming en voorkeurinformatie voor een individuele klant vangt.

>[!NOTE]
>
>Aangezien deze veldgroep alleen compatibel is met [!DNL XDM Individual Profile] , kan deze niet worden gebruikt voor [!DNL XDM ExperienceEvent] -schema&#39;s. Als u toestemmings en voorkeursgegevens in uw schema van de Gebeurtenis van de Ervaring wilt omvatten, voeg het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype &#x200B;](../../data-types/consents.md) aan het schema door het gebruik van de groep van het a [&#x200B; douanegebied &#x200B;](../../ui/resources/field-groups.md#create) in plaats daarvan toe.

## Groepsstructuur van veld {#structure}

De veldgroep [!UICONTROL Consents and Preferences] biedt één objecttype veld, `consents` , waarin toestemmings- en voorkeursgegevens worden vastgelegd. Dit veld is een uitbreiding van het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype &#x200B;](../../data-types/consents.md) , waarbij het veld `adID` wordt verwijderd en een kaartveld `idSpecific` wordt toegevoegd.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Zie de gids op [&#x200B; het onderzoeken van middelen XDM &#x200B;](../../ui/explore.md) aan voor stappen op hoe te om het even welk middel XDM op te zoeken en zijn structuur in Experience Platform UI te inspecteren.

In het volgende JSON-voorbeeld ziet u het type gegevens dat de veldgroep [!UICONTROL Consents and Preferences] kan verwerken. Voor informatie over hoe te om de meeste gebieden te gebruiken die door de gebiedsgroep worden verstrekt, verwijs naar de gids op het [&#x200B; gegevenstype van de Inhoud en van de Voorkeur &#x200B;](../../data-types/consents.md). De subsecties hieronder richten zich op de unieke attributen die de gebiedsgroep aan het gegevenstype toevoegt.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
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
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>U kunt voorbeeld-JSON-gegevens genereren voor elk XDM-schema dat u in Experience Platform definieert om te helpen visualiseren hoe de toestemming en voorkeursgegevens van uw klant moeten worden toegewezen. Raadpleeg de volgende documentatie voor meer informatie:
>
>* [&#x200B; produceer steekproefgegevens in UI &#x200B;](../../ui/sample.md)
>* [&#x200B; produceer steekproefgegevens in API &#x200B;](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kan worden gebruikt wanneer een bepaalde toestemming of voorkeur niet universeel op een klant van toepassing is, maar tot één apparaat of identiteitskaart beperkt is. Zo kan een klant ervoor kiezen geen e-mails naar het ene adres te ontvangen, terwijl e-mails naar een ander adres mogelijk worden toegestaan.

>[!IMPORTANT]
>
>De toestemmingen en voorkeuren op kanaalniveau (dat wil zeggen de onder `consents` buiten `idSpecific` opgegeven waarden) zijn van toepassing op alle id&#39;s in dat kanaal. Alle toestemming en voorkeuren op kanaalniveau worden daarom rechtstreeks toegepast, ongeacht of de equivalente id- of apparaatspecifieke instellingen worden gerespecteerd:
>
>* Als de klant heeft opgegeven dat de toepassing is uitgeschakeld op het kanaalniveau, worden gelijkwaardige toestemmingen of voorkeuren in `idSpecific` genegeerd.
>* Als de toestemming of voorkeur op kanaalniveau niet is ingesteld of als de klant zich heeft aangemeld, worden de equivalente toestemmingen of voorkeuren in `idSpecific` gerespecteerd.

Elke sleutel in het `idSpecific` -object vertegenwoordigt een specifieke naamruimte die wordt herkend door de Adobe Experience Platform Identity Service. Hoewel u uw eigen aangepaste naamruimten kunt definiëren om verschillende id&#39;s te categoriseren, wordt u aangeraden een van de standaardnaamruimten van Identity Service te gebruiken om opslaggrootten voor Real-Time Klantprofiel te reduceren. Voor meer informatie over identiteit namespaces, zie het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](/help/identity-service/features/namespaces.md) in de documentatie van de Dienst van de Identiteit.

De sleutels voor elk namespacevoorwerp vertegenwoordigen de unieke identiteitswaarden waarvoor de klant voorkeur heeft geplaatst. Elke identiteitswaarde kan een volledige reeks toestemmingen en voorkeur bevatten, die op de zelfde manier zoals `consents` wordt geformatteerd.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

De velden `marketing` en `idSpecific` worden niet ondersteund binnen `any` -objecten die worden aangeboden in de sectie `preferred` . Deze velden kunnen alleen op gebruikersniveau worden geconfigureerd. Daarnaast bieden de `idSpecific` marketingvoorkeuren voor `email` , `sms` en `push` geen ondersteuning voor `subscriptions` -velden.

Er is ook een toestemming die alleen kan worden opgegeven in de sectie `idSpecific` : `adID` . Dit veld wordt behandeld in de onderafdeling hieronder.

#### `adID`

De `adID` toestemming geeft de toestemming van de klant weer om te bepalen of een adverteerder-id (IDFA of GAID) kan worden gebruikt om de klant te koppelen tussen apps op dit apparaat. Deze waarde kan alleen worden geconfigureerd onder de naamruimte `ECID` in de sectie `idSpecific` en kan niet worden ingesteld voor andere naamruimten of op gebruikersniveau voor deze veldgroep.

```json
"idSpecific": {
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Deze waarde wordt niet rechtstreeks ingesteld, omdat de Adobe Experience Platform Mobile SDK deze waarde automatisch instelt wanneer dit van toepassing is.

## Gegevens invoegen met de veldgroep {#ingest}

Als u de veldgroep [!UICONTROL Consents and Preferences] wilt gebruiken om toestemmingsgegevens van uw klanten in te voeren, moet u een dataset tot stand brengen die op een schema wordt gebaseerd dat die gebiedsgroep bevat.

Zie het leerprogramma op [&#x200B; creërend een schema in UI &#x200B;](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) voor stappen op hoe te om gebiedsgroepen aan gebieden toe te wijzen. Zodra u een schema hebt gecreeerd dat een gebied met de [!UICONTROL Consents and Preferences] gebiedsgroep bevat, verwijs naar de sectie op [&#x200B; creërend een dataset &#x200B;](/help/catalog/datasets/user-guide.md#create) in de gids van de datasetgebruiker, na de stappen om een dataset met een bestaand schema tot stand te brengen.

>[!IMPORTANT]
>
>Als u toestemmingsgegevens naar [!DNL Real-Time Customer Profile] wilt verzenden, is het vereist dat u een [!DNL Profile] -ingeschakeld schema maakt op basis van de [!DNL XDM Individual Profile] -klasse die de [!UICONTROL Consents and Preferences] -veldgroep bevat. De dataset die u creeert die op dat schema wordt gebaseerd moet ook voor [!DNL Profile] worden toegelaten. Raadpleeg de zelfstudies die hierboven zijn gekoppeld voor specifieke stappen met betrekking tot [!DNL Real-Time Customer Profile] -vereisten voor schema&#39;s en gegevenssets.
>
>Bovendien moet u ook ervoor zorgen dat uw samenvoegingsbeleid wordt gevormd om aan de dataset(s) voorrang te geven die de recentste toestemmings en voorkeursgegevens bevatten, opdat de klantenprofielen correct worden bijgewerkt. Zie het overzicht op [&#x200B; fusiebeleid &#x200B;](/help/rtcdp/profile/merge-policies.md) voor meer informatie.

## Verwerking van toestemmings- en preferenties

Wanneer een klant zijn toestemming of voorkeuren op uw website wijzigt, moeten deze wijzigingen worden verzameld en onmiddellijk worden doorgevoerd door toestemming in te stellen in de bibliotheek voor gegevensverzameling die wordt gebruikt. Als een klant ervoor kiest geen gegevens meer te verzamelen, moet de gegevensverzameling onmiddellijk worden beëindigd. Als een klant uit personalisatie kiest, dan zou er geen verpersoonlijking op de volgende pagina moeten zijn die zij laden. Zie [`setConsent`](/help/collection/js/commands/setconsent.md) met de JavaScript-bibliotheek of de [[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md) -actie met de extensie van de Web SDK-tag.

## Volgende stappen

Dit document behandelt de structuur en het gebruik van de veldgroep [!UICONTROL Consents and Preferences] . Zie het document over het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype &#x200B;](../../data-types/consents.md) voor meer informatie over de andere velden die door de veldgroep worden verschaft.
