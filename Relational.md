
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

| Column     | Type        | Constraints                                                |
|------------|-------------|------------------------------------------------------------|
| Name       | VARCHAR(50) | PRIMARY KEY                     |
| Country    | VARCHAR(4)  | FOREIGN KEY → Country(Code)                               |
| Province   | VARCHAR(50) | FOREIGN KEY → Province(Name, Country)                     |
| Population | DECIMAL     | CHECK (Population >= 0)                                   |
| Latitude   | DECIMAL     | CHECK (-90 <= Latitude <= 90)                             |
| Longitude  | DECIMAL     | CHECK (-180 <= Longitude <= 180)                          |
| Elevation  | DECIMAL     |                                                            |

# Table Province
*Information about administrative divisions (provinces, states, regions).*

| Column     | Type        | Constraints                                      |
|------------|-------------|--------------------------------------------------|
| Name       | VARCHAR(50) | PRIMARY KEY (Name, Country)                      |
| Country    | VARCHAR(4)  | FOREIGN KEY → Country(Code)                      |
| Population | DECIMAL     | CHECK (Population >= 0)                          |
| Area       | DECIMAL     | CHECK (Area >= 0)                                |
| Capital    | VARCHAR(50) |                                                  |
| CapProv    | VARCHAR(50) |                                                  |


# Table Language
*Information about languages spoken in countries.*
| Column     | Type        | Constraints                                            |
|------------|-------------|--------------------------------------------------------|
| Country    | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)              |
| Name       | VARCHAR(50) | PRIMARY KEY                                            |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)          |


# Table Ethnic Group
*Information about ethnic composition of countries.*
| Column     | Type        | Constraints                                            |
|------------|-------------|--------------------------------------------------------|
| Country    | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)              |
| Name       | VARCHAR(50) | PRIMARY KEY                                            |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)          |


# Table Religion
*Information about religious affiliation in countries.*

| Column     | Type        | Constraints                                            |
|------------|-------------|--------------------------------------------------------|
| Country    | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)              |
| Name       | VARCHAR(50) | PRIMARY KEY                                            |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)          |


# Table Continent
*Information about continents and their size.*

| Column | Type        | Constraints      |
|--------|-------------|------------------|
| Name   | VARCHAR(20) | PRIMARY KEY      |
| Area   | DECIMAL(10) | CHECK (Area >= 0)|


# Table Organization
*Information about international organizations.*

| Column       | Type         | Constraints                                      |
|--------------|--------------|--------------------------------------------------|
| Abbreviation | VARCHAR(12)  | PRIMARY KEY                                      |
| Name         | VARCHAR(100) | NOT NULL, UNIQUE                                 |
| City         | VARCHAR(50)  |                                                  |
| Country      | VARCHAR(4)   | FOREIGN KEY → Country(Code)                     |
| Province     | VARCHAR(50)  |                                                  |
| Established  | DATE         |                                                  |


# Table Airport
*Information about airports and their codes.*

| Column    | Type        | Constraints                                            |
|-----------|-------------|--------------------------------------------------------|
| IATACode  | VARCHAR(3)  | PRIMARY KEY                                            |
| Name      | VARCHAR(100)|                                                        |
| Country   | VARCHAR(4)  | FOREIGN KEY → Country(Code)                            |
| City      | VARCHAR(50) |                                                        |
| Province  | VARCHAR(50) |                                                        |
| Island    | VARCHAR(50) |                                                        |
| Latitude  | DECIMAL     | CHECK (-90 <= Latitude <= 90)                          |
| Longitude | DECIMAL     | CHECK (-180 <= Longitude <= 180)                       |
| Elevation | DECIMAL     |                                                        |
| gmtOffset | DECIMAL     |                                                        |


# Table Mountain
*Geographical information about specific mountains.*

| Column      | Type        | Constraints                                      |
|-------------|-------------|--------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                      |
| MountainSet | VARCHAR(50) |                                                  |
| Elevation   | DECIMAL     | CHECK (Elevation >= 0)                           |
| Type        | VARCHAR(10) |                                                  |
| Coordinates | GeoCoord    | CHECK (valid_lat_lon(Coordinates))               |


# Table Desert
*Geographical information about deserts.*

| Column      | Type        | Constraints                                      |
|-------------|-------------|--------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                      |
| Area        | DECIMAL     | CHECK (Area >= 0)                                |
| Coordinates | GeoCoord    | CHECK (valid_lat_lon(Coordinates))               |

# Table Island
*Geographical information about islands.*

| Column      | Type        | Constraints                                      |
|-------------|-------------|--------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                      |
| IslandGroup | VARCHAR(50) |                                                  |
| Area        | DECIMAL     | CHECK (Area >= 0)                                |
| Elevation   | DECIMAL     |                                                  |
| Type        | VARCHAR(15) |                                                  |
| Coordinates | GeoCoord    | CHECK (valid_lat_lon(Coordinates))               |


# Table Sea
*Geographical information about seas and oceans.*

| Column | Type        | Constraints                     |
|--------|-------------|----------------------------------|
| Name   | VARCHAR(50) | PRIMARY KEY                      |
| Area   | DECIMAL     | CHECK (Area >= 0)                |
| Depth  | DECIMAL     | CHECK (Depth >= 0)               |


# Table Lake
*Geographical information about lakes.*

| Column      | Type        | Constraints                                        |
|-------------|-------------|----------------------------------------------------|
| Name        | VARCHAR(50) | PRIMARY KEY                                        |
| River       | VARCHAR(50) | FOREIGN KEY → River(Name)                          |
| Area        | DECIMAL     | CHECK (Area >= 0)                                  |
| Elevation   | DECIMAL     |                                                    |
| Depth       | DECIMAL     | CHECK (Depth >= 0)                                 |
| Height      | DECIMAL     | CHECK (Height > 0)                                 |
| Type        | VARCHAR(12) |                                                    |
| Coordinates | GeoCoord    | CHECK (valid_lat_lon(Coordinates))                 |


# Table River
*Geographical information about rivers and their paths.*

| Column           | Type        | Constraints                                                      |
|------------------|-------------|------------------------------------------------------------------|
| Name             | VARCHAR(50) | PRIMARY KEY                                                      |
| River            | VARCHAR(50) | FOREIGN KEY → River(Name)                                        |
| Lake             | VARCHAR(50) | FOREIGN KEY → Lake(Name)                                         |
| Sea              | VARCHAR(50) | FOREIGN KEY → Sea(Name)                                          |
| Length           | DECIMAL     | CHECK (Length >= 0)                                             |
| Area             | DECIMAL     | CHECK (Area >= 0)                                               |
| Source           | GeoCoord    | CHECK (valid_lat_lon(Source))                                    |
| Mountains        | VARCHAR(50) |                                                                  |
| SourceElevation  | DECIMAL     |                                                                  |
| Estuary          | GeoCoord    | CHECK (valid_lat_lon(Estuary))                                   |
| EstuaryElevation | DECIMAL     |                                                                  |
| RivFlowsInto     | CHECK ( (River IS NOT NULL) + (Lake IS NOT NULL) + (Sea IS NOT NULL) = 1 )     |


# Table Economy
*Economical information about the countries.*

| Column        | Type        | Constraints                                 |
|---------------|-------------|---------------------------------------------|
| Country       | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)    |
| GDP           | DECIMAL     | CHECK (GDP >= 0)                            |
| Agriculture   | DECIMAL     | CHECK (Agriculture >= 0)                    |
| Service       | DECIMAL     | CHECK (Service >= 0)                        |
| Industry      | DECIMAL     | CHECK (Industry >= 0)                       |
| Inflation     | DECIMAL     |                                             |
| Unemployment  | DECIMAL     |                                             |


# Table Politics
*Political information about the countries.*

| Column        | Type        | Constraints                                          |
|---------------|-------------|------------------------------------------------------|
| Country       | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)             |
| Independence  | DATE        |                                                      |
| WasDependent  | VARCHAR(50) |                                                      |
| Dependent     | VARCHAR(4)  | FOREIGN KEY → Country(Code)                          |
| Government    | VARCHAR(120)|                                                      |


# Table Population
*Information about the population of the countries.*

| Column            | Type        | Constraints                                  |
|-------------------|-------------|----------------------------------------------|
| Country           | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)     |
| PopulationGrowth  | DECIMAL     |                                              |
| InfantMortality   | DECIMAL     |                                              |

# Table Countrypops
*Information about the population number of the countries in different years.*

| Column      | Type        | Constraints                                      |
|-------------|-------------|--------------------------------------------------|
| Country     | VARCHAR(4)  | FOREIGN KEY → Country(Code)                      |
| Population  | DECIMAL     | CHECK (Population >= 0)                           |
| Year        | DECIMAL     | CHECK (Year >= 0), PRIMARY KEY (Country, Year)   |


# Table CountryLocalName
*Information about the local name of the country.*

| Column     | Type        | Constraints                                  |
|------------|-------------|----------------------------------------------|
| Country    | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)     |
| LocalName  | VARCHAR(300)|                                              |


# Table borders
*Informations about neighboring countries (relation is not symmetric).*

| Column    | Type        | Constraints                                  |
|-----------|-------------|----------------------------------------------|
| Country1  | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)     |
| Country2  | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)     |
| Length    | DECIMAL     | CHECK (Length > 0)                            |


# Table encompasses
*Information to which continents a country belongs.*

| Column     | Type        | Constraints                                         |
|------------|-------------|-----------------------------------------------------|
| Country    | VARCHAR(4)  | FOREIGN KEY → Country(Code), PRIMARY KEY            |
| Continent  | VARCHAR(20) | FOREIGN KEY → Continent(Name), PRIMARY KEY          |
| Percentage | DECIMAL     | CHECK (Percentage > 0 AND Percentage <= 100)        |

# Table Citypops
*Information about the population number of the cities in different years.*

| Column      | Type        | Constraints                                                      |
|-------------|-------------|------------------------------------------------------------------|
| City        | VARCHAR(50) | PRIMARY KEY                                                      |
| Country     | VARCHAR(4)  | PRIMARY KEY                                                      |
| Province    | VARCHAR(50) | PRIMARY KEY                                                      |
| Population  | DECIMAL     | CHECK (Population >= 0)                                          |
| Year        | DECIMAL     | PRIMARY KEY, CHECK (Year >= 0)                                   |
|             |             | FOREIGN KEY (City, Country, Province) → City(Name, Country, Province) |


# Table CityLocalName
*Information about the local name of the city.*
| Column      | Type        | Constraints                                                       |
|-------------|-------------|-------------------------------------------------------------------|
| City        | VARCHAR(50) | PRIMARY KEY                                                       |
| Country     | VARCHAR(4)  | PRIMARY KEY                                                       |
| Province    | VARCHAR(50) | PRIMARY KEY                                                       |
| LocalName   | VARCHAR(300)|                                                                   |
|             |             | FOREIGN KEY (City, Country, Province) → City(Name, Country, Province) |


# Table Provpops
*Information about the population number of the provinces in different years.*

| Column      | Type        | Constraints                                          |
|-------------|-------------|------------------------------------------------------|
| Province    | VARCHAR(50) | PRIMARY KEY                                          |
| Country     | VARCHAR(4)  | PRIMARY KEY                                          |
| Population  | DECIMAL     | CHECK (Population >= 0)                               |
| Year        | DECIMAL     | PRIMARY KEY, CHECK (Year >= 0)                        |
|             |             | FOREIGN KEY (Province, Country) → Province(Name, Country) |


# Table ProvinceLocalName
*Information about the local name of the province.*

| Column     | Type        | Constraints                                          |
|------------|-------------|------------------------------------------------------|
| Province   | VARCHAR(50) | PRIMARY KEY                                          |
| Country    | VARCHAR(4)  | PRIMARY KEY                                          |
| LocalName  | VARCHAR(300)|                                                      |
|            |             | FOREIGN KEY (Province, Country) → Province(Name, Country) |


# Table isMember
*Memberships in political and economical organizations.*

| Column        | Type        | Constraints                                         |
|---------------|-------------|-----------------------------------------------------|
| Organization  | VARCHAR(12) | PRIMARY KEY, FOREIGN KEY → Organization(Abbreviation) |
| Country       | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)            |
| Type          | VARCHAR(60) | DEFAULT 'member'                                     |


# Table RiverThrough
*Information about rivers flowing through lakes.*

| Column | Type        | Constraints                                         |
|--------|-------------|-----------------------------------------------------|
| River  | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → River(Name)             |
| Lake   | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Lake(Name)              |


# Table geo Mountain
*Geographical information about mountains (Analogous for geo island, desert, river, lake, sea, source, estuary).*

| Column   | Type        | Constraints                                                        |
|----------|-------------|--------------------------------------------------------------------|
| Mountain | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Mountain(Name)                         |
| Country  | VARCHAR(4)  | PRIMARY KEY, FOREIGN KEY → Country(Code)                           |
| Province | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY (Province, Country) → Province(Name, Country) |

# Table mergesWith
*Information about neighboring seas (relation is not symmetric).*

| Column | Type        | Constraints                             |
|--------|-------------|-----------------------------------------|
| Sea1   | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Sea(Name)    |
| Sea2   | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Sea(Name)    |


# Table located
*Information about cities located at rivers, lakes, and seas.*

| Column   | Type        | Constraints                                                       |
|----------|-------------|-------------------------------------------------------------------|
| City     | VARCHAR(50) | PRIMARY KEY                                                       |
| Country  | VARCHAR(4)  | PRIMARY KEY                                                       |
| Province | VARCHAR(50) | PRIMARY KEY                                                       |
| River    | VARCHAR(50) | FOREIGN KEY → River(Name)                                        |
| Lake     | VARCHAR(50) | FOREIGN KEY → Lake(Name)                                         |
| Sea      | VARCHAR(50) | FOREIGN KEY → Sea(Name)                                          |
|          |             | FOREIGN KEY (City, Country, Province) → City(Name, Country, Province) |


# Table locatedOn
*Information about cities located in islands.*

| Column   | Type        | Constraints                                                       |
|----------|-------------|-------------------------------------------------------------------|
| City     | VARCHAR(50) | PRIMARY KEY                                                       |
| Country  | VARCHAR(4)  | PRIMARY KEY                                                       |
| Province | VARCHAR(50) | PRIMARY KEY                                                       |
| Island   | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Island(Name)                          |
|          |             | FOREIGN KEY (City, Country, Province) → City(Name, Country, Province) |


# Table islandIn
*Information the waters where the islands are located in.*

| Column  | Type        | Constraints                             |
|---------|-------------|-------------------------------------------|
| Island  | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Island(Name)   |
| Sea     | VARCHAR(50) | FOREIGN KEY → Sea(Name)                  |
| Lake    | VARCHAR(50) | FOREIGN KEY → Lake(Name)                 |
| River   | VARCHAR(50) | FOREIGN KEY → River(Name)                |

# Table MountainOnIsland
*Information which mountains are located on islands.*

| Column   | Type        | Constraints                                      |
|----------|-------------|--------------------------------------------------|
| Mountain | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Mountain(Name)        |
| Island   | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Island(Name)          |

# Table RiverOnIsland
*Information which rivers are located on islands.*
| Column | Type        | Constraints                               |
|--------|-------------|-------------------------------------------|
| River  | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → River(Name)    |
| Island | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Island(Name)   |


# Table LakeOnIsland
*Information which lakes are located on islands.*

| Column | Type        | Constraints                              |
|--------|-------------|------------------------------------------|
| Lake   | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Lake(Name)    |
| Island | VARCHAR(50) | PRIMARY KEY, FOREIGN KEY → Island(Name)  |

