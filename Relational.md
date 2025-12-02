
# Table Country
*Information about the countries, including capital and size.*

| Column    | Type        | Restriccions                     |
|------------|-------------|-----------------------------------|
| Name       | VARCHAR(50) | NOT NULL, UNIQUE                  |
| Code       | VARCHAR(4)  | PRIMARY KEY                       |
| Capital    | VARCHAR(50) |                                   |
| Province   | VARCHAR(50) |                                   |
| Area       | DECIMAL     | CHECK (Area >= 0)                  |
| Population | DECIMAL     | CHECK (Population >= 0)            |

# Table City
*Information about cities, their location and population.*

| Column    | Type        | Restriccions                                 |
|------------|-------------|-----------------------------------------------|
| Name       | VARCHAR(50) | Parte de PRIMARY KEY                          |
| Country    | VARCHAR(4)  | Parte de PRIMARY KEY                          |
| Province   | VARCHAR(50) | Parte de PRIMARY KEY                          |
| Population | DECIMAL     | CHECK (Population >= 0)                       |
| Latitude   | DECIMAL     | CHECK (-90 <= Latitude <= 90)                 |
| Longitude  | DECIMAL     | CHECK (-180 <= Longitude <= 180)              |
| Elevation  | DECIMAL     |                                               |

# Table Province
*Information about administrative divisions (provinces, states, regions).*

| Column    | Typo        | Restriccions                   |
|------------|-------------|---------------------------------|
| Name       | VARCHAR(50) | NOT NULL, PK (Name, Country)    |
| Country    | VARCHAR(4)  | NOT NULL                        |
| Population | DECIMAL     | CHECK (Population >= 0)         |
| Area       | DECIMAL     | CHECK (Area >= 0)               |
| Capital    | VARCHAR(50) |                                 |
| CapProv    | VARCHAR(50) |                                 |

# Table Language
*Information about languages spoken in countries.*
| Columna    | Tipo        | Restricciones                                     |
|------------|-------------|---------------------------------------------------|
| Country    | VARCHAR(4)  | Parte de PRIMARY KEY                              |
| Name       | VARCHAR(50) | Parte de PRIMARY KEY                              |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)      |

# Table Ethnic Group
*Information about ethnic composition of countries.*

| Columna    | Tipo        | Restricciones                                     |
|------------|-------------|---------------------------------------------------|
| Country    | VARCHAR(4)  | Parte de PRIMARY KEY                              |
| Name       | VARCHAR(50) | Parte de PRIMARY KEY                              |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)      |

# Table Religion
*Information about religious affiliation in countries.*

| Columna    | Tipo        | Restricciones                                     |
|------------|-------------|---------------------------------------------------|
| Country    | VARCHAR(4)  | Parte de PRIMARY KEY                              |
| Name       | VARCHAR(50) | Parte de PRIMARY KEY                              |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)      |

# Table Continent
*Information about continents and their size.*

| Columna | Tipo        | Restricciones       |
|---------|-------------|---------------------|
| Name    | VARCHAR(20) | PRIMARY KEY         |
| Area    | DECIMAL(10) |                     |

# Table Organization
*Information about international organizations.*

| Columna      | Tipo         | Restricciones                  |
|--------------|--------------|--------------------------------|
| Abbreviation | VARCHAR(12)  | PRIMARY KEY                    |
| Name         | VARCHAR(100) | NOT NULL, UNIQUE(Name)         |
| City         | VARCHAR(50)  |                                |
| Country      | VARCHAR(4)   |                                |
| Province     | VARCHAR(50)  |                                |
| Established  | DATE         |                                |

# Table Airport
*Information about airports and their codes.*

| Columna    | Tipo        | Restricciones                               |
|------------|-------------|---------------------------------------------|
| IATACode   | VARCHAR(3)  | PRIMARY KEY                                 |
| Name       | VARCHAR(100)|                                             |
| Country    | VARCHAR(4)  |                                             |
| City       | VARCHAR(50) |                                             |
| Province   | VARCHAR(50) |                                             |
| Island     | VARCHAR(50) |                                             |
| Latitude   | DECIMAL     | CHECK (-90 <= Latitude <= 90)               |
| Longitude  | DECIMAL     | CHECK (-180 <= Longitude <= 180)            |
| Elevation  | DECIMAL     |                                             |
| gmtOffset  | DECIMAL     |                                             |

# Table Mountain
*Geographical information about specific mountains.*

| Columna     | Tipo      | Restricciones                                   |
|-------------|-----------|-------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                   |
| Mountains   | VARCHAR(50) |                                               |
| Elevation   | DECIMAL     |                                               |
| Type        | VARCHAR(10) |                                               |
| Coordinates | GeoCoord    | CHECK coords within valid lat/lon ranges      |

# Table Desert
*Geographical information about deserts.*

| Columna     | Tipo      | Restricciones                                   |
|-------------|-----------|-------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                   |
| Area        | DECIMAL     |                                               |
| Coordinates | GeoCoord    | CHECK coords within valid lat/lon ranges      |

# Table Island
*Geographical information about islands.*

| Columna     | Tipo        | Restricciones                                   |
|-------------|-------------|-------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                     |
| Islands     | VARCHAR(50) |                                                 |
| Area        | DECIMAL     | CHECK (Area >= 0)                               |
| Elevation   | DECIMAL     |                                                 |
| Type        | VARCHAR(15) |                                                 |
| Coordinates | GeoCoord    | CHECK coords within valid lat/lon ranges        |

# Table Sea
*Geographical information about seas and oceans.*

| Columna | Tipo        | Restricciones                  |
|---------|-------------|--------------------------------|
| Name    | VARCHAR(50) | PRIMARY KEY                    |
| Area    | DECIMAL     | CHECK (Area >= 0)              |
| Depth   | DECIMAL     | CHECK (Depth >= 0)             |

# Table Lake
*Geographical information about lakes.*

| Columna    | Tipo      | Restricciones                                   |
|------------|-----------|-------------------------------------------------|
| Name       | VARCHAR(50) | PRIMARY KEY                                   |
| River      | VARCHAR(50) |                                               |
| Area       | DECIMAL     | CHECK (Area >= 0)                             |
| Elevation  | DECIMAL     |                                               |
| Depth      | DECIMAL     | CHECK (Depth >= 0)                            |
| Height     | DECIMAL     | CHECK (Height > 0)                            |
| Type       | VARCHAR(12) |                                               |
| Coordinates| GeoCoord    | CHECK coords within valid lat/lon ranges      |

# Table River
*Geographical information about rivers and their paths.*

| Columna          | Tipo       | Restricciones                                   |
|------------------|------------|-------------------------------------------------|
| Name             | VARCHAR(50)| PRIMARY KEY                                     |
| River            | VARCHAR(50)|                                                 |
| Lake             | VARCHAR(50)|                                                 |
| Sea              | VARCHAR(50)|                                                 |
| Length           | DECIMAL    | CHECK (Length >= 0)                             |
| Area             | DECIMAL    | CHECK (Area >= 0)                               |
| Source           | GeoCoord   | CHECK coords within valid lat/lon ranges        |
| Mountains        | VARCHAR(50)|                                                 |
| SourceElevation  | DECIMAL    |                                                 |
| Estuary          | GeoCoord   | CHECK coords within valid lat/lon ranges        |
| EstuaryElevation | DECIMAL    |                                                 |
| RivFlowsInto     | CHECK      | Valid combinations of River/Lake/Sea (solo uno) |

# Table Economy
*Economical information about the countries.*

| Column | Description |
| :--- | :--- |
| **country** | The country code |
| **GDP** | Gross domestic product (in million $) |
| **agriculture** | Percentage of agriculture of the GDP |
| **service** | Percentage of services of the GDP |
| **industry** | Percentage of industry of the GDP |
| **inflation** | Inflation rate (per annum) |
| **unemployment** | Unemployment rate |

# Table Politics
*Political information about the countries.*

| Column | Description |
| :--- | :--- |
| **country** | The country code |
| **independence** | Date of independence (if independent) |
| **wasdependent** | The political body where the area was dependent of; usually a country (but not always) |
| **dependent** | The country code where the area belongs to |
| **government** | Type of government |

# Table Population
*Information about the population of the countries.*

| Column | Description |
| :--- | :--- |
| **country** | The country code |
| **population growth** | Population growth rate (per annum) |
| **infant mortality** | Infant mortality (per thousand) |

# Table Countrypops
*Information about the population number of the countries in different years.*

| Column | Description |
| :--- | :--- |
| **country** | The country code |
| **population** | Number of inhabitants |
| **year** | In which year |

# Table CountryLocalName
*Information about the local name of the country.*

| Column | Description |
| :--- | :--- |
| **country** | The country code |
| **localname** | The local name, usually in a local alphabet (UTF-8) |

# Table borders
*Informations about neighboring countries (relation is not symmetric).*

| Column | Description |
| :--- | :--- |
| **country1** | A country code |
| **country2** | A country code |
| **length** | Length of the border between country1 and country2 |

# Table encompasses
*Information to which continents a country belongs.*

| Column | Description |
| :--- | :--- |
| **country** | The country code |
| **continent** | The continent name |
| **percentage** | Percentage, how much of the area of a country belongs to the continent |

# Table Citypops
*Information about the population number of the cities in different years.*

| Column         | Description                                               |
| -------------- | --------------------------------------------------------- |
| **city**       | City name (part of composite PK)                          |
| **country**    | Country code where the city is located                    |
| **province**   | Province name                                             |
| **population** | Number of inhabitants in the specified year               |
| **year**       | Year of the population measurement (part of composite PK) |

# Table CityLocalName
*Information about the local name of the city.*
| Column        | Description                                     |
| ------------- | ----------------------------------------------- |
| **city**      | City name (part of PK/FK)                       |
| **country**   | Country code (part of PK/FK)                    |
| **province**  | Province name (part of PK/FK)                   |
| **localname** | Local or alternate name used within that region |

# Table Provpops
*Information about the population number of the provinces in different years.*

| Column | Description |
| :--- | :--- |
| **province** | The name of the province |
| **country** | The code of the country where it belongs to |
| **population** | Number of inhabitants |
| **year** | In which year |

# Table ProvinceLocalName
*Information about the local name of the province.*

| Column | Description |
| :--- | :--- |
| **province** | The name of the province |
| **country** | The code of the country where it belongs to |
| **localname** | The local name, usually in a local alphabet (UTF-8) |

# Table isMember
*Memberships in political and economical organizations.*

| Column | Description |
| :--- | :--- |
| **organization** | The abbreviation of the organization |
| **country** | The code of the member country |
| **type** | The type of membership |

# Table RiverThrough
*Information about rivers flowing through lakes.*

| Column | Description |
| :--- | :--- |
| **river** | The name of the river |
| **lake** | The lake where it flows through |

# Table geo Mountain
*Geographical information about mountains (Analogous for geo island, desert, river, lake, sea, source, estuary).*

| Column | Description |
| :--- | :--- |
| **mountain** | The name of the mountain |
| **country** | The country code where it is located |
| **province** | The province of this country |

# Table mergesWith
*Information about neighboring seas (relation is not symmetric).*

| Column | Description |
| :--- | :--- |
| **sea1** | A sea |
| **sea2** | A sea |

# Table located
*Information about cities located at rivers, lakes, and seas.*

| Column | Description |
| :--- | :--- |
| **city** | The name of the city |
| **country** | The country code where the city belongs to |
| **province** | The province where the city belongs to |
| **river** | The river where it is located at |
| **lake** | The lake where it is located at |
| **sea** | The sea where it is located at |

# Table locatedOn
*Information about cities located in islands.*

| Column | Description |
| :--- | :--- |
| **city** | The name of the city |
| **country** | The country code where the city belongs to |
| **province** | The province where the city belongs to |
| **island** | The island it is (maybe only partially) located on |

# Table islandIn
*Information the waters where the islands are located in.*

| Column | Description |
| :--- | :--- |
| **island** | The name of the island |
| **sea** | The sea where the island is located in |
| **lake** | The lake where the island is located in |
| **river** | The river where the island is located in |

# Table MountainOnIsland
*Information which mountains are located on islands.*

| Column | Description |
| :--- | :--- |
| **mountain** | The name of the mountain |
| **island** | The name of the island |

# Table RiverOnIsland
*Information which rivers are located on islands.*

| Column | Description |
| :--- | :--- |
| **river** | The name of the river |
| **island** | The name of the island |

# Table LakeOnIsland
*Information which lakes are located on islands.*

| Column | Description |
| :--- | :--- |
| **lake** | The name of the lake |
| **island** | The name of the island |
