---
title: Experience Platform-gegevens beheren met Python en SQLAlchemy
description: Leer hoe u SQLAlchemy gebruikt om uw Experience Platform-gegevens te beheren met Python in plaats van SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Experience Platform-gegevens beheren met [!DNL Python] en [!DNL SQLAlchemy]

Leer hoe u SQLAlchemy kunt gebruiken voor meer flexibiliteit bij het beheer van uw Adobe Experience Platform-gegevens. Voor degenen die niet zo vertrouwd met SQL zijn, kan SQLAlchemy ontwikkelingstijd zeer verbeteren wanneer het werken met relationele gegevensbanken. Dit document bevat instructies en voorbeelden voor het tot stand brengen van een verbinding tussen [!DNL SQLAlchemy] en Query Service en het gebruik van Python voor de interactie met uw databases.

[!DNL SQLAlchemy] is een object Relational Mapper (ORM) en een [!DNL Python] codebibliotheek die gegevens die zijn opgeslagen in een SQL-database, kunnen overbrengen naar [!DNL Python] -objecten. Vervolgens kunt u met [!DNL Python] -code CRUD-bewerkingen uitvoeren op gegevens die in het Experience Platform-gegevensmeer worden opgeslagen. Hierdoor hoeft u geen gegevens te beheren met alleen PSQL.

## Aan de slag

U hebt toegang tot de werkruimte Query&#39;s in de gebruikersinterface van Experience Platform nodig om de referenties te verkrijgen waarmee u [!DNL SQLAlchemy] kunt verbinden met Experience Platform. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte Query&#39;s.

## [!DNL Query Service] referenties {#credentials}

Meld u aan bij de gebruikersinterface van Experience Platform en selecteer **[!UICONTROL Queries]** in de linkernavigatie, gevolgd door **[!UICONTROL Credentials]** om uw referenties te zoeken. Voor volledige richtingen op hoe te om uw login geloofsbrieven te vinden, te lezen gelieve de [ gids van geloofsbrieven ](../ui/credentials.md).

![ het Credentiële lusje met het verlopen van geloofsbrieven voor de benadrukte Dienst van de Vraag.](../images/use-cases/credentials.png)

Hoewel haven 80 de geadviseerde haven voor een verbinding aan de Dienst van de Vraag is, kunt u haven 5432 ook gebruiken.

>[!IMPORTANT]
>
>Als u het verlopen geloofsbrieven (zoals die in het beeld hierboven worden gezien) gebruikt om met de Dienst van de Vraag te verbinden, zal het zittingsleven voor uw verbinding na de vastgestelde periode verlopen die in de montages van uw organisatie wordt bepaald. Deze periode is standaard 24 uur. Zie de documentatie leren hoe te om [ een cliënt met niet-het verlopen geloofsbrieven ](../ui/credentials.md#non-expiring-credentials) te verbinden, of hoe te [ het zittingsleven voor uw het verlopen geloofsbrieven ](../ui/credentials.md#expiring-credentials) veranderen.

Wanneer u toegang hebt tot uw QS-referenties, opent u de [!DNL Python] -editor.

### Referenties opslaan in [!DNL Python] {#store-credentials}

Importeer in de [!DNL Python] -editor de `urllib.parse.quote` -bibliotheek en sla elke referentie-variabele op als een parameter. De module `urllib.parse` biedt een standaardinterface voor het onderverdelen van URL-tekenreeksen in componenten. De aanhalingsfunctie vervangt speciale tekens in de URL-tekenreeks om de gegevens veilig te maken voor gebruik als URL-componenten. Hieronder ziet u een voorbeeld van de vereiste code:

>[!TIP]
>
>Gebruik de driedubbele aanhalingstekens van [!DNL Python] om de tekenreeks voor het wachtwoord voor meerdere regels in te voeren.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>Het wachtwoord dat u opgeeft om [!DNL SQLAlchemy] verbinding te maken met Experience Platform, verloopt als u uw aanmeldingsgegevens gebruikt. Zie de [ geloofsbrieven sectie ](#credentials) voor meer informatie.

### Een motorinstantie maken [#create-engine ]

Nadat de variabelen zijn gecreeerd, voer de `create_engine` functie in en creeer een koord om uw geloofsbrieven van de Dienst van de Vraag in SQLAlchemy te compileren en te formatteren. De functie `create_engine` wordt vervolgens gebruikt om een motorinstantie te maken.

>[!NOTE]
>
>`create_engine` keert een geval van een motor terug. Nochtans, opent het niet de verbinding aan de Dienst van de Vraag tot een vraag wordt geroepen die een verbinding vereist.

SSL moet zijn ingeschakeld wanneer u Experience Platform opent met behulp van externe clients. Als onderdeel van de engine voert u aanvullende trefwoordargumenten in via `connect_args` . U wordt aangeraden de SSL-modus in te stellen op `require` . Zie de [ SSL wijzedocumentatie ](../clients/ssl-modes.md) voor meer informatie over toegelaten waarden.

In het onderstaande voorbeeld wordt de [!DNL Python] -code weergegeven die nodig is om een engine- en verbindingstekenreeks te initialiseren.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>Het wachtwoord dat u opgeeft om [!DNL SQLAlchemy] verbinding te maken met Experience Platform, verloopt als u uw aanmeldingsgegevens gebruikt. Zie de [ geloofsbrieven sectie ](#credentials) voor meer informatie.

U kunt nu Experience Platform-gegevens opvragen met [!DNL Python] . In het onderstaande voorbeeld wordt een array met tabelnamen van Query Service geretourneerd.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
