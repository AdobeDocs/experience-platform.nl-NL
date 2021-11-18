---
solution: Experience Platform
title: Inhoud en Voorkeuren voor schemaveldgroep
topic-legacy: overview
description: Dit document bevat een overzicht van de veldgroep Inhoud en Voorkeuren.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: d2c71423165776bf7c106a7503514c5acc284f8e
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] veldgroep

[!UICONTROL Consents and Preferences] is een standaardveldgroep voor de [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) die toestemmings- en voorkeursgegevens voor een individuele klant vastleggen.

>[!NOTE]
>
>Aangezien deze veldgroep alleen compatibel is met [!DNL XDM Individual Profile]niet kan worden gebruikt voor [!DNL XDM ExperienceEvent] schema&#39;s. Als u toestemmings- en voorkeursgegevens wilt opnemen in uw Experience Event-schema, voegt u de opdracht [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype](../../data-types/consents.md) aan het schema door [aangepaste veldgroep](../../ui/resources/field-groups.md#create) in plaats daarvan.

## Groepsstructuur van veld {#structure}

De [!UICONTROL Consents and Preferences] veldgroep levert één objecttype veld, `consents`, om toestemmings- en voorkeursinformatie vast te leggen. Dit veld breidt het [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype](../../data-types/consents.md), de `adID` veld en een `idSpecific` kaartveld.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Zie de handleiding op [XDM-bronnen verkennen](../../ui/explore.md) aan voor stappen op hoe te om het even welk middel XDM op te zoeken en zijn structuur in het Platform UI te inspecteren.

In het volgende JSON-bestand wordt een voorbeeld getoond van het type gegevens dat [!UICONTROL Consents and Preferences] veldgroep kan verwerken. In de volgende secties wordt informatie gegeven over het specifieke gebruik van elk van deze velden.

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
>U kunt steekproefJSON gegevens voor om het even welk XDM schema produceren dat u in Experience Platform bepaalt helpen visualiseren hoe uw klantentoestemming en voorkeursgegevens zouden moeten in kaart worden gebracht. Raadpleeg de volgende documentatie voor meer informatie:
>
>* [Voorbeeldgegevens genereren in de gebruikersinterface](../../ui/sample.md)
>* [Voorbeeldgegevens genereren in de API](../../api/sample-data.md)


Raadpleeg de handleiding bij het dialoogvenster [Gegevenstype Inhoud en Voorkeuren](../../data-types/consents.md). De subsecties hieronder richten zich op de unieke attributen die de gebiedsgroep aan het gegevenstype toevoegt.

### `idSpecific`

`idSpecific` kan worden gebruikt wanneer een bepaalde toestemming of voorkeur niet universeel op een klant van toepassing is, maar tot één enkel apparaat of identiteitskaart beperkt is. Zo kan een klant ervoor kiezen geen e-mails naar het ene adres te ontvangen, terwijl e-mails naar een ander adres mogelijk worden toegestaan.

>[!IMPORTANT]
>
>Toestemmingen en voorkeuren op kanaalniveau (d.w.z. die welke onder `consents` buiten `idSpecific`) wordt toegepast op alle id&#39;s in dat kanaal. Alle toestemming en voorkeuren op kanaalniveau worden daarom rechtstreeks toegepast, ongeacht of de equivalente id- of apparaatspecifieke instellingen worden gerespecteerd:
>
>* Als de klant de optie op kanaalniveau heeft uitgeschakeld, worden gelijkwaardige toestemmingen of voorkeuren in `idSpecific` worden genegeerd.
>* Als de toestemming of voorkeur op kanaalniveau niet is ingesteld, of de klant heeft ervoor gekozen, worden de equivalente toestemmingen of voorkeuren in `idSpecific` zijn vereerd.


Elke toets in het dialoogvenster `idSpecific` -object staat voor een specifieke naamruimte die door Adobe Experience Platform Identity Service wordt herkend. Hoewel u uw eigen aangepaste naamruimten kunt definiëren om verschillende id&#39;s te categoriseren, wordt u aangeraden een van de standaardnaamruimten van Identity Service te gebruiken om opslaggrootten voor Real-time klantprofiel te reduceren. Voor meer informatie over naamruimten raadpleegt u de [Overzicht van naamruimte in identiteit](../../../identity-service/namespaces.md) in de documentatie van de identiteitsdienst.

De sleutels voor elk namespacevoorwerp vertegenwoordigen de unieke identiteitswaarden waarvoor de klant voorkeur heeft geplaatst. Elke identiteitswaarde kan een volledige reeks toestemmingen en voorkeur bevatten, die op de zelfde manier wordt geformatteerd zoals `consents`.

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
  "ECID" : {
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

Within `marketing` objecten die in het `idSpecific` de `any` en `preferred` velden worden niet ondersteund. Deze velden kunnen alleen op gebruikersniveau worden geconfigureerd. Bovendien `idSpecific` marketingvoorkeuren voor `email`, `sms`, en `push` ondersteunen `subscriptions` velden.

Er is ook een toestemming die alleen kan worden gegeven in de `idSpecific` sectie: `adID`. Dit veld wordt behandeld in de onderafdeling hieronder.

#### `adID`

De `adID` instemming geeft de toestemming van de klant voor het feit of een adverteerder-id (IDFA of GAID) kan worden gebruikt om de klant te koppelen tussen apps op dit apparaat. Deze waarde kan alleen worden geconfigureerd onder de `ECID` naamruimte identiteit in het dialoogvenster `idSpecific` en kan niet worden ingesteld voor andere naamruimten of op gebruikersniveau voor deze veldgroep.

```json
"idSpecific": {
  "ECID" : {
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
>Deze waarde wordt niet rechtstreeks ingesteld, aangezien de Adobe Experience Platform Mobile SDK deze waarde automatisch instelt wanneer dit van toepassing is.

## Gegevens invoegen met de veldgroep {#ingest}

Voor het gebruik van de [!UICONTROL Consents and Preferences] de gebiedsgroep om toestemmingsgegevens van uw klanten in te voeren, moet u een dataset tot stand brengen die op een schema wordt gebaseerd dat die gebiedsgroep bevat.

Zie de zelfstudie aan [het creëren van een schema in UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) voor stappen over het toewijzen van veldgroepen aan velden. Nadat u een schema hebt gemaakt dat een veld bevat met de opdracht [!UICONTROL Consents and Preferences] veldgroep, zie de sectie over [een gegevensset maken](../../../catalog/datasets/user-guide.md#create) in de datasetgebruikersgids, die de stappen volgt om een dataset met een bestaand schema tot stand te brengen.

>[!IMPORTANT]
>
>Als u toestemmingsgegevens wilt verzenden naar [!DNL Real-time Customer Profile]moet u een [!DNL Profile]- toegelaten schema dat op wordt gebaseerd [!DNL XDM Individual Profile] klasse die de [!UICONTROL Consents and Preferences] veldgroep. De dataset die u creeert die op dat schema wordt gebaseerd moet ook worden toegelaten voor [!DNL Profile]. Raadpleeg de bovenstaande zelfstudies voor specifieke stappen met betrekking tot [!DNL Real-time Customer Profile] voorschriften voor schema&#39;s en gegevensreeksen.
>
>Bovendien moet u ook ervoor zorgen dat uw samenvoegingsbeleid wordt gevormd om aan de dataset(s) voorrang te geven die de recentste toestemmings en voorkeursgegevens bevatten, opdat de klantenprofielen correct worden bijgewerkt. Zie het overzicht op [beleid samenvoegen](../../../rtcdp/profile/merge-policies.md) voor meer informatie .

## Verwerking van toestemmings- en voorkeurswijzigingen

Wanneer een klant zijn toestemming of voorkeuren op uw website wijzigt, moeten deze wijzigingen worden verzameld en onmiddellijk worden doorgevoerd met de [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Als een klant ervoor kiest geen gegevens meer te verzamelen, moet de gegevensverzameling onmiddellijk worden beëindigd. Als een klant ervoor kiest geen personalisatie meer te gebruiken, dan is er geen personalisatie aanwezig op de volgende pagina die zij bezoeken.

## Volgende stappen

In dit document worden de structuur en het gebruik van de [!UICONTROL Consents and Preferences] veldgroep. Zie het document in de [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype](../../data-types/consents.md).
