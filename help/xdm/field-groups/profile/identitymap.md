---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
title: IdentityMap-schemaveldgroep
description: Meer informatie over de klasse XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [ de naamupdates van de gebiedsgroep ](../name-updates.md) voor meer informatie.

[!UICONTROL IdentityMap] is een standaardgroep van het schemagebied voor de [[!UICONTROL XDM ExperienceEvent] klasse ](../../classes/experienceevent.md) en een compatibele gebiedsgroep voor de [[!UICONTROL XDM Individual Profile] klasse ](../../classes/individual-profile.md). De veldgroep bevat één kaartveld dat een set gebruikersidentiteiten bevat die door naamruimte worden vastgehouden.

![ A diagram van de [!UICONTROL IdentityMap] groep van het schemagebied ](../../images/field-groups/identitymap.png)

Zie de sectie over identiteitskaarten in de [ grondbeginselen van schemacompositie ](../../schema/composition.md#identityMap) voor meer informatie over hun gebruiksgeval, met inbegrip van hun voordelen en nadelen.

**voorbeeld**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Voor meer details op de gebiedsgroep, verwijs naar het [ volledige schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) in de openbare bewaarplaats XDM.
