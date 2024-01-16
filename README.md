## create two tables 
animals column1 animal_id datatype INT PRIMARY KEY
   column2 animal_name datatype VARCHAR(50)
   column3 species datatype VARCHAR(50),
   column4 habitat_id datatype  INT
## habitats 
 habitat_id INT PRIMARY KEY,
    habitat_name VARCHAR(50),
    climate VARCHAR(50)

practice group by, and sub queries , provide a list of habitata with their IDs, names, and the total number of animals in each habitat

```SQL
CREATE TABLE animals (
	animal_id INT PRIMARY KEY,
	animal_name VARCHAR(50),
	species VARCHAR(50),
	habitat_id INT
);

CREATE TABLE habitats (
	habitat_id INT PRIMARY KEY,
	habitat_name VARCHAR(50),
	climate VARCHAR(50)
);

INSERT INTO habitats VALUES
( 1, 'Forest', 'Temperate'),
( 2, 'Desert', 'Arid'),
( 3, 'Ocean', 'Marine');

INSERT INTO animals VALUES
( 1, 'Lion', 'Mammal', 1 ),
( 2, 'Tiger', 'Mammal', 1 ),
( 3, 'Eagle', 'Bird', 2 ),
( 4, 'Snake', 'Reptile', 2 ),
( 5, 'Shark', 'Fish', 3 ),
( 6, 'Dolphin', 'Mammal', 3 ),
( 7, 'Octopus', 'Invertebrate', 3);

SELECT
	h.habitat_id,
	h.habitat_name,
	h.climate,
	COUNT( a.animal_id ) AS total_animals
FROM
	habitats h
LEFT JOIN
	animals a ON h.habitat_id = a.habitat_id
GROUP BY
    h.habitat_id, h.habitat_name, h.climate;

SELECT (
		SELECT MAX(a_count)
		FROM (
			SELECT COUNT( animal_id ) AS a_count
			FROM animals WHERE habitat_id = 2
		) AS avg_count) 
	AS animals_in_habitat_ocean, 
	COUNT( animal_id ) AS max_animals 
FROM animals;
```
