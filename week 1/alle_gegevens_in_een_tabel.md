# Alle gegevens in een tabel:

### 1. De eerste stap naar een relationele opslagestructuur
Een tabel in een relationele database is een basisvorm van gegevensopslag, waarin gegevens in rijen en kolommen zijn georganiseerd. De eerste stap in het opzetten van een relationele database is vaak het ontwerpen van deze tabellen. Elke tabel vertegenwoordigt een entiteit, zoals een "Klant" of een "Bestelling", en bevat gegevens over die entiteit.

**Een voorbeeld:**

| **KlantID** | **Naam**         | **Leeftijd** | **BestellingID** | **Besteldatum** | **Productnaam**  |
|-------------|------------------|--------------|------------------|-----------------|------------------|
| 1           | Jan Jansen       | 35           | 101              | 2024-10-01      | Laptop           |
| 2           | Eva de Vries     | 28           | 102              | 2024-10-02      | Smartphone       |
| 1           | Jan Jansen       | 35           | 103              | 2024-10-05      | Toetsenbord      |

In dit voorbeeld zie je dat sommige informatie (zoals de naam van de klant) herhaald wordt. Dit is vaak het beginpunt van databaseontwerp, maar in dit stadium kan er sprake zijn van redundantie, wat leidt tot inefficiëntie.

### 2. Redundantie en gecontroleerde redundantie
**Redundantie** verwijst naar het onnodig dupliceren van gegevens binnen een database. In het voorbeeld hierboven is de informatie over "Jan Jansen" herhaald, omdat hij meerdere bestellingen heeft geplaatst. Dit kan leiden tot extra opslagruimte en verhoogt de kans op inconsistentie, bijvoorbeeld als zijn naam of leeftijd verandert.

**Gecontroleerde redundantie**: Hoewel redundantie over het algemeen vermeden moet worden, kan het in sommige gevallen nuttig zijn om bepaalde informatie gecontroleerd te herhalen om prestaties te verbeteren. Dit gebeurt vaak opzettelijk in systemen waar snelheid belangrijker is dan het minimaliseren van opslagruimte.

### 3. Subtabellen: Normalisatie en het elimineren van herhalende gegevens
Om redundantie te elimineren, gebruiken we een proces genaamd **normalisatie**. Dit proces splitst een tabel op in kleinere, gerelateerde subtabellen, waardoor herhaalde gegevens worden verwijderd. De subtabellen worden vervolgens via **sleutels** met elkaar verbonden.

In ons voorbeeld kunnen we de klant- en bestelgegevens opsplitsen in twee tabellen:

**Tabel 1: Klanten**

| **KlantID** | **Naam**         | **Leeftijd** |
|-------------|------------------|--------------|
| 1           | Jan Jansen       | 35           |
| 2           | Eva de Vries     | 28           |

**Tabel 2: Bestellingen**

| **BestellingID** | **KlantID**   | **Besteldatum** | **Productnaam**  |
|------------------|---------------|-----------------|------------------|
| 101              | 1             | 2024-10-01      | Laptop           |
| 102              | 2             | 2024-10-02      | Smartphone       |
| 103              | 1             | 2024-10-05      | Toetsenbord      |

In dit geval bevat de klantentabel alleen gegevens over klanten, en de bestellingen worden opgeslagen in een aparte tabel. Door gebruik te maken van de **KlantID**-sleutel kunnen we de gegevens uit beide tabellen koppelen.

### 4. Herhalende groepen
Een **herhalende groep** verwijst naar een set van gegevens die binnen één record meerdere keren voorkomt. In ons oorspronkelijke voorbeeld hadden we meerdere bestellingen voor dezelfde klant in één tabel, wat een voorbeeld is van een herhalende groep.

Het opsplitsen van deze gegevens in subtabellen (zoals in het normalisatieproces hierboven) helpt om deze herhalende groepen te elimineren en de gegevens op een meer efficiënte manier te organiseren.

### 5. Opmerken en behandelen van herhalende groepen
Om herhalende groepen te **opmerken** tijdens het ontwerpen van een database, moet je letten op gegevens die meerdere keren voorkomen voor een bepaalde entiteit. Bijvoorbeeld, als een klant meerdere bestellingen kan plaatsen, zou elke bestelling afzonderlijk moeten worden opgeslagen in een aparte tabel in plaats van meerdere keren de klantgegevens te herhalen.

De **behandeling** van herhalende groepen wordt meestal gedaan door de tabel in meerdere tabellen te splitsen, zoals we hierboven hebben laten zien. Dit proces wordt ondersteund door relationele **sleutels** (zoals primaire en vreemde sleutels) om de gegevens in verschillende tabellen aan elkaar te koppelen.

### Samenvatting
- Een **tabel** in een database is de eerste stap in een relationele opslagestructuur.
- **Redundantie** kan leiden tot inefficiëntie, maar **gecontroleerde redundantie** kan soms nuttig zijn.
- **Subtabellen** worden gebruikt om gegevens op te splitsen en redundantie te vermijden via normalisatie.
- **Herhalende groepen** ontstaan wanneer dezelfde informatie meerdere keren voorkomt voor één entiteit, en dit kan worden opgelost door normalisatie en het creëren van subtabellen.

