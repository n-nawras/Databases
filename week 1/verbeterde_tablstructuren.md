# Verbeteren Tabelstructuren

Bij het werken met relationele databases is een van de eerste stappen in het ontwerp het verbeteren van de tabelstructuren. Dit proces helpt bij het optimaliseren van de database, waarbij redundantie wordt verminderd en gegevens efficiënter worden opgeslagen. In een boek over **Relationele databases en SQL** worden de volgende concepten vaak uitgebreid behandeld.

## 1. Elimineren van de herhalende groep
Herhalende groepen verwijzen naar kolommen of velden die meerdere waarden voor een enkel record kunnen bevatten. In een slecht ontworpen tabel kunnen bijvoorbeeld meerdere kolommen worden gebruikt om de producten die bij één bestelling horen op te slaan (bijvoorbeeld: Product1, Product2, etc.).

**Oplossing**:  
Door de tabel op te splitsen en de herhalende gegevens naar een andere tabel te verplaatsen, kunnen we de herhalende groepen elimineren. Dit betekent dat in plaats van meerdere kolommen voor herhalende waarden, een aparte tabel wordt gebruikt met relaties om deze te koppelen aan het oorspronkelijke record.

**Voorbeeld**:  
Stel dat een klant meerdere producten bestelt in één transactie. In plaats van kolommen zoals "Product1", "Product2", enz., zou je een aparte tabel kunnen maken voor bestelde producten, die aan de bestellingen worden gekoppeld via een **BestellingID**.

| BestellingID | KlantID | Besteldatum   |
|--------------|---------|---------------|
| 101          | 1       | 2024-10-01    |
| 102          | 2       | 2024-10-02    |

| BestellingID | Productnaam |
|--------------|-------------|
| 101          | Laptop      |
| 101          | Toetsenbord |
| 102          | Smartphone  |

Hier zijn de herhalende producten in een aparte tabel geplaatst en gelinkt aan de **BestellingID**.

## 2. Elimineren van redundantie
Redundantie in databases verwijst naar het onnodig dupliceren van gegevens. Dit kan leiden tot problemen zoals verhoogde opslagvereisten en inconsistente gegevens wanneer wijzigingen worden aangebracht. In relationele databases willen we redundantie zoveel mogelijk vermijden.

**Oplossing**:  
Door **normalisatie** worden tabellen opgesplitst in kleinere gerelateerde tabellen die via sleutels met elkaar zijn verbonden. Dit zorgt ervoor dat elk gegeven slechts op één plek wordt opgeslagen. Door deze splitsing wordt data-integriteit beter gewaarborgd en is de kans op fouten kleiner.

**Voorbeeld van redundantie elimineren**:  
In een klant- en bestellingen-scenario wil je bijvoorbeeld voorkomen dat de klantgegevens herhaald worden voor elke bestelling. In plaats daarvan creëer je een aparte **Klantentabel** en gebruik je een **KlantID** om deze te koppelen aan de bestellingen.

| KlantID | Naam        | Leeftijd |
|---------|-------------|----------|
| 1       | Jan Jansen  | 35       |
| 2       | Eva de Vries| 28       |

## 3. Alternatief: Eerst elimineren van redundantie
Sommige ontwerpstrategieën in boeken over relationele databases geven de voorkeur aan het eerst elimineren van redundantie, voordat ze herhalende groepen aanpakken. Het idee hier is dat het verwijderen van duplicaten van gegevens hogere prioriteit heeft, omdat redundantie grotere risico's op inconsistente gegevens oplevert.

Na het elimineren van redundantie kun je verder verfijnen door herhalende groepen te identificeren en op te splitsen.

## 4. Elk entiteittype zijn eigen tabel
Een van de belangrijkste principes van relationele databases is dat **elk entiteittype** zijn eigen tabel krijgt. Een **entiteit** kan bijvoorbeeld een klant, bestelling of product zijn. Het idee is dat elk type gegeven zijn eigen tabel moet hebben, waarin de relevante attributen worden opgeslagen.

**Voorbeeld**:  
- Een tabel voor **klanten** bevat informatie over klanten, zoals naam en leeftijd.
- Een tabel voor **bestellingen** bevat informatie over individuele bestellingen, zoals besteldatum en producten.
- Een tabel voor **producten** bevat informatie over de verschillende producten die beschikbaar zijn.

Door elke entiteit in een aparte tabel op te slaan, wordt het makkelijker om de database te onderhouden en gegevens te koppelen via relaties.

## 5. Normaliseren en standaardiseren
**Normalisatie** is een proces dat zorgt voor een logische organisatie van gegevens in tabellen. Het doel van normalisatie is om redundantie te elimineren en afhankelijkheden tussen gegevens te minimaliseren. Dit wordt vaak bereikt door de database te standaardiseren naar verschillende **normale vormen**, zoals:

- **Eerste normale vorm (1NF)**: Verwijdert herhalende groepen en zorgt ervoor dat alle kolommen atomaire waarden bevatten.
- **Tweede normale vorm (2NF)**: Elimineert partiële afhankelijkheden door ervoor te zorgen dat alle niet-sleutelattributen volledig afhankelijk zijn van de primaire sleutel.
- **Derde normale vorm (3NF)**: Verwijdert transitieve afhankelijkheden, waarbij niet-sleutelattributen alleen afhankelijk zijn van de primaire sleutel en niet van elkaar.

Door het toepassen van normalisatie, kan de database worden gestandaardiseerd, wat resulteert in een efficiëntere en makkelijkere structuur voor gegevensbeheer.

## 6. Structuur en populatie
Na het normalisatieproces wordt een **database-structuur** opgezet die bestaat uit verschillende tabellen die met elkaar in relatie staan. Zodra de structuur is gedefinieerd, kun je de tabellen gaan **populeren** met daadwerkelijke gegevens.

Populatie verwijst naar het vullen van tabellen met records. Het is belangrijk dat gegevens in overeenstemming blijven met de ontworpen structuur. Daarom zijn relaties tussen tabellen belangrijk, zodat gegevens consistent en verbonden blijven.

## 7. Tabellen en relaties
In een relationele database zijn **relaties** tussen tabellen van cruciaal belang. Relaties worden gedefinieerd met behulp van **sleutels**:

- **Primaire sleutels**: Een unieke identificator voor een rij in een tabel.
- **Vreemde sleutels**: Een kolom die verwijst naar een primaire sleutel in een andere tabel, waarmee een relatie wordt gelegd.

**Soorten relaties**:
- **Een-op-een**: Elk record in de ene tabel komt overeen met één record in een andere tabel.
- **Een-op-veel**: Eén record in de ene tabel kan overeenkomen met meerdere records in een andere tabel (bijv. een klant kan meerdere bestellingen hebben).
- **Veel-op-veel**: Meerdere records in de ene tabel kunnen overeenkomen met meerdere records in een andere tabel. Dit vereist een **koppeltabel** (bijv. een bestelling kan meerdere producten bevatten en een product kan in meerdere bestellingen voorkomen).

Deze relaties zorgen ervoor dat gegevens op een efficiënte manier georganiseerd blijven en dat gegevens eenvoudig kunnen worden opgevraagd.

## Samenvatting
- **Herhalende groepen** worden geëlimineerd door gegevens naar aparte tabellen te verplaatsen en relaties te definiëren.
- **Redundantie** wordt voorkomen door gegevens op te splitsen in kleinere tabellen via **normalisatie**.
- Elk **entiteittype** krijgt zijn eigen tabel, wat zorgt voor een georganiseerde database-structuur.
- **Normalisatie** zorgt voor gestandaardiseerde en efficiënte opslag van gegevens door afhankelijkheden te minimaliseren.
- **Relaties tussen tabellen** worden beheerd door middel van primaire en vreemde sleutels, die verschillende soorten koppelingen ondersteunen (zoals een-op-veel en veel-op-veel).
