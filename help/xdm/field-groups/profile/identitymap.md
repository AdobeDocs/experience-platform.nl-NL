---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
title: IdentityMap-schemaveldgroep
description: Meer informatie over de klasse XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../name-updates.md) voor meer informatie .

[!UICONTROL IdentityMap] is een standaardschemagebiedgroep voor [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). De veldgroep bevat één kaartveld dat een set gebruikersidentiteiten bevat die door naamruimte worden vastgehouden.

![Een schema van de [!UICONTROL IdentityMap] schemaveldgroep](../../images/field-groups/identitymap.png)

Zie de sectie over identiteitskaarten in het dialoogvenster [grondbeginselen van de schemacompositie](../../schema/composition.md#identityMap) voor meer informatie over het gebruik ervan , waaronder de voordelen en nadelen .

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

Voor meer informatie over de veldgroep raadpleegt u de [volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) in de openbare XDM-opslagplaats.
