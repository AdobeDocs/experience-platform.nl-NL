---
title: Waarden versleutelen
description: Leer hoe u gevoelige waarden versleutelt met de Reactor-API.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Waarden versleutelen

Bij het gebruik van tags in Adobe Experience Platform moeten bepaalde workflows gevoelige waarden leveren (bijvoorbeeld een persoonlijke sleutel voor het leveren van bibliotheken aan omgevingen via hosts). De gevoelige aard van die geloofsbrieven vereist veilige overdracht en opslag.

In dit document wordt beschreven hoe u vertrouwelijke waarden versleutelt met [GnuPG-codering](https://www.gnupg.org/gph/en/manual/x110.html) (ook wel GPG genoemd), zodat alleen het tagsysteem deze kan lezen.

## De openbare GPG-sleutel en controlesom verkrijgen

Na [downloaden](https://gnupg.org/download/) en het installeren van de recentste versie van GPG moet u de openbare sleutel van GPG voor de milieu van de markeringsproductie verkrijgen:

* [GPG-toets](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Checksum](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## De sleutel importeren in de sleutelketen

Nadat u de sleutel op uw computer hebt opgeslagen, bestaat de volgende stap uit het toevoegen van de sleutel aan uw GPG-sleutelhanger.

**Syntaxis**

```shell
gpg --import {KEY_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{KEY_NAME}` | De naam van het bestand met de openbare sleutel. |

{style="table-layout:auto"}

**Voorbeeld**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Waarden versleutelen

Nadat u de sleutel aan uw sleutelhanger hebt toegevoegd, kunt u waarden beginnen te coderen door `--encrypt` markering. Het volgende script laat zien hoe deze opdracht werkt:

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Deze opdracht kan als volgt worden verdeeld:

* Invoer wordt geleverd aan de `gpg` gebruiken.
* `--armor` maakt uitvoer met ASCII-structuur in plaats van binair. Dit vereenvoudigt het overbrengen van de waarde via JSON.
* `--encrypt` GPG wordt geïnstrueerd de gegevens te coderen.
* `-r` Hiermee stelt u de ontvanger voor de gegevens in. Alleen de ontvanger (de houder van de persoonlijke sleutel die overeenkomt met de openbare sleutel) kan de gegevens ontsleutelen. De naam van de ontvanger van de gewenste sleutel kan worden gevonden door de output van te onderzoeken `gpg --list-keys`.

De bovenstaande opdracht gebruikt de openbare sleutel voor `Tags Data Encryption <launch@adobe.com>` om de waarde te coderen, `Example value`, in ASCII-formaat.

De output van het bevel zou op het volgende lijken:

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

Deze uitvoer kan alleen worden ontsleuteld door systemen met de persoonlijke sleutel die overeenkomt met de `Tags Data Encryption <launch@adobe.com>` openbare sleutel.

Deze uitvoer is de waarde die op een computer moet worden opgegeven wanneer gegevens naar de Reactor-API worden verzonden. Het systeem slaat deze gecodeerde uitvoer op en decodeert deze tijdelijk indien nodig. Het systeem decodeert bijvoorbeeld de hostgegevens lang genoeg om een verbinding met de server te maken en verwijdert vervolgens onmiddellijk alle sporen van de gedecodeerde waarde.

>[!NOTE]
>
>De indeling van de gepantserde, gecodeerde waarde is belangrijk. Zorg ervoor dat regeleinden correct worden beschermd in de waarde die in de aanvraag wordt opgegeven.
