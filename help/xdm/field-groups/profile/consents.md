---
solution: Experience Platform
title: Inhoud en Voorkeuren voor schemaveldgroep
description: Meer informatie over de veldgroep Inhoud en Voorkeuren.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] veldgroep

[!UICONTROL Consents and Preferences] is een standaardgebiedsgroep voor de [[!DNL XDM Individual Profile]  klasse ](../../classes/individual-profile.md) die toestemming en voorkeurinformatie voor een individuele klant vangt.

>[!NOTE]
>
>Aangezien deze veldgroep alleen compatibel is met [!DNL XDM Individual Profile] , kan deze niet worden gebruikt voor [!DNL XDM ExperienceEvent] -schema&#39;s. Als u toestemmings en voorkeursgegevens in uw schema van de Gebeurtenis van de Ervaring wilt omvatten, voeg het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype ](../../data-types/consents.md) aan het schema door het gebruik van de groep van het a [ douanegebied ](../../ui/resources/field-groups.md#create) in plaats daarvan toe.

## Groepsstructuur van veld {#structure}

De veldgroep [!UICONTROL Consents and Preferences] biedt één objecttype veld, `consents` , waarin toestemmings- en voorkeursgegevens worden vastgelegd. Dit veld is een uitbreiding van het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype ](../../data-types/consents.md) , waarbij het veld `adID` wordt verwijderd en een kaartveld `idSpecific` wordt toegevoegd.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Zie de gids op [ het onderzoeken van middelen XDM ](../../ui/explore.md) aan voor stappen op hoe te om het even welk middel XDM op te zoeken en zijn structuur in Experience Platform UI te inspecteren.

In het volgende JSON-voorbeeld ziet u het type gegevens dat de veldgroep [!UICONTROL Consents and Preferences] kan verwerken. Voor informatie over hoe te om de meeste gebieden te gebruiken die door de gebiedsgroep worden verstrekt, verwijs naar de gids op het [ gegevenstype van de Inhoud en van de Voorkeur ](../../data-types/consents.md). De subsecties hieronder richten zich op de unieke attributen die de gebiedsgroep aan het gegevenstype toevoegt.

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
>* [ produceer steekproefgegevens in UI ](../../ui/sample.md)
>* [ produceer steekproefgegevens in API ](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kan worden gebruikt wanneer een bepaalde toestemming of voorkeur niet universeel op een klant van toepassing is, maar tot één apparaat of identiteitskaart beperkt is. Zo kan een klant ervoor kiezen geen e-mails naar het ene adres te ontvangen, terwijl e-mails naar een ander adres mogelijk worden toegestaan.

>[!IMPORTANT]
>
>De toestemmingen en voorkeuren op kanaalniveau (dat wil zeggen de onder `consents` buiten `idSpecific` opgegeven waarden) zijn van toepassing op alle id&#39;s in dat kanaal. Alle toestemming en voorkeuren op kanaalniveau worden daarom rechtstreeks toegepast, ongeacht of de equivalente id- of apparaatspecifieke instellingen worden gerespecteerd:
>
>* Als de klant heeft opgegeven dat de toepassing is uitgeschakeld op het kanaalniveau, worden gelijkwaardige toestemmingen of voorkeuren in `idSpecific` genegeerd.
>* Als de toestemming of voorkeur op kanaalniveau niet is ingesteld of als de klant zich heeft aangemeld, worden de equivalente toestemmingen of voorkeuren in `idSpecific` gerespecteerd.

Elke sleutel in het `idSpecific` -object vertegenwoordigt een specifieke naamruimte die wordt herkend door de Adobe Experience Platform Identity Service. Hoewel u uw eigen aangepaste naamruimten kunt definiëren om verschillende id&#39;s te categoriseren, wordt u aangeraden een van de standaardnaamruimten van Identity Service te gebruiken om opslaggrootten voor Real-Time Klantprofiel te reduceren. Voor meer informatie over identiteit namespaces, zie het [ overzicht van identiteitskaart namespace ](../../../identity-service/features/namespaces.md) in de documentatie van de Dienst van de Identiteit.

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

De velden `any` en `preferred` worden niet ondersteund binnen `marketing` -objecten die worden aangeboden in de sectie `idSpecific` . Deze velden kunnen alleen op gebruikersniveau worden geconfigureerd. Daarnaast bieden de `idSpecific` marketingvoorkeuren voor `email` , `sms` en `push` geen ondersteuning voor `subscriptions` -velden.

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

Zie het leerprogramma op [ creërend een schema in UI ](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) voor stappen op hoe te om gebiedsgroepen aan gebieden toe te wijzen. Zodra u een schema hebt gecreeerd dat een gebied met de [!UICONTROL Consents and Preferences] gebiedsgroep bevat, verwijs naar de sectie op [ creërend een dataset ](../../../catalog/datasets/user-guide.md#create) in de gids van de datasetgebruiker, na de stappen om een dataset met een bestaand schema tot stand te brengen.

>[!IMPORTANT]
>
>Als u toestemmingsgegevens naar [!DNL Real-Time Customer Profile] wilt verzenden, is het vereist dat u een [!DNL Profile] -ingeschakeld schema maakt op basis van de [!DNL XDM Individual Profile] -klasse die de [!UICONTROL Consents and Preferences] -veldgroep bevat. De dataset die u creeert die op dat schema wordt gebaseerd moet ook voor [!DNL Profile] worden toegelaten. Raadpleeg de zelfstudies die hierboven zijn gekoppeld voor specifieke stappen met betrekking tot [!DNL Real-Time Customer Profile] -vereisten voor schema&#39;s en gegevenssets.
>
>Bovendien moet u ook ervoor zorgen dat uw samenvoegingsbeleid wordt gevormd om aan de dataset(s) voorrang te geven die de recentste toestemmings en voorkeursgegevens bevatten, opdat de klantenprofielen correct worden bijgewerkt. Zie het overzicht op [ fusiebeleid ](../../../rtcdp/profile/merge-policies.md) voor meer informatie.

## Verwerking van toestemmings- en preferenties

Wanneer een klant hun toestemmingen of voorkeur op uw website verandert, zouden deze veranderingen moeten worden verzameld en onmiddellijk worden afgedwongen gebruikend het [ Web SDK van Adobe Experience Platform ](../../../web-sdk/commands/setconsent.md). Als een klant ervoor kiest geen gegevens meer te verzamelen, moet de gegevensverzameling onmiddellijk worden beëindigd. Als een klant uit personalisatie kiest, dan zou er geen personalisatie op de volgende pagina moeten zijn die zij laden.

## Volgende stappen

Dit document behandelt de structuur en het gebruik van de veldgroep [!UICONTROL Consents and Preferences] . Zie het document over het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype ](../../data-types/consents.md) voor meer informatie over de andere velden die door de veldgroep worden verschaft.
