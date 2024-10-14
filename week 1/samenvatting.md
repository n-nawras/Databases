# Alle gegevens in een tabel:
- Een **tabel** in een database is de eerste stap in een relationele opslagestructuur.
- **Redundantie** kan leiden tot inefficiëntie, maar **gecontroleerde redundantie** kan soms nuttig zijn.
- **Subtabellen** worden gebruikt om gegevens op te splitsen en redundantie te vermijden via normalisatie.
- **Herhalende groepen** ontstaan wanneer dezelfde informatie meerdere keren voorkomt voor één entiteit, en dit kan worden opgelost door normalisatie en het creëren van subtabellen.

# Verbeteren Tabelstructuren
- **Herhalende groepen** worden geëlimineerd door gegevens naar aparte tabellen te verplaatsen en relaties te definiëren.
- **Redundantie** wordt voorkomen door gegevens op te splitsen in kleinere tabellen via **normalisatie**.
- Elk **entiteittype** krijgt zijn eigen tabel, wat zorgt voor een georganiseerde database-structuur.
- **Normalisatie** zorgt voor gestandaardiseerde en efficiënte opslag van gegevens door afhankelijkheden te minimaliseren.
- **Relaties tussen tabellen** worden beheerd door middel van primaire en vreemde sleutels, die verschillende soorten koppelingen ondersteunen (zoals een-op-veel en veel-op-veel).

## Samenvatting van het proces:

1. **Alle gegevens in één tabel**: De beginstap, waarbij alle gegevens zonder normalisatie in één tabel worden opgeslagen, wat leidt tot redundantie en inefficiëntie.
2. **Elimineren van herhalende groepen**: We verplaatsen de herhalende gegevens (zoals meerdere producten per bestelling) naar aparte tabellen.
3. **Elimineren van redundantie**: We verplaatsen redundante gegevens (zoals klantinformatie) naar hun eigen tabellen en koppelen ze via sleutels.
4. **Elk entiteittype in eigen tabel**: Elke entiteit (klant, bestelling, product) krijgt zijn eigen tabel.
5. **Normaliseren en standaardiseren**: Door het toepassen van normalisatie naar de derde normale vorm minimaliseren we redundantie en afhankelijkheden.
6. **Structuur en populatie**: Nadat de structuur is bepaald, kunnen we de tabellen vullen met gegevens, terwijl we de integriteit behouden door relaties te definiëren.
7. **Tabellen en relaties**: Relaties tussen tabellen worden beheerd door primaire en vreemde sleutels, wat de efficiëntie van gegevensopslag en opvraging verbetert.