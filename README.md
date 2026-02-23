# celestialbodies-project
This project demonstrates the creation of a universe database with tables for comet, galaxy, moon, planet, and star. The database schema follows specified requirements and uses various data types and relationships to structure the universe's components.

<strong>Database Setup</strong>

To use the database, connect to it with the following command:

<pre>
\c universe
</pre>

<strong>Table Structure and Relationships</strong>

1. <em>comet</em>

The comet table stores information about comets that may orbit planets. It includes the following columns:

<pre>
comet_id (Primary Key, AUTO_INCREMENT, INT)

name (VARCHAR, UNIQUE, NOT NULL)

planet_id (Foreign Key, INT, references planet.planet_id)

description (TEXT)

is_active (BOOLEAN, default TRUE)
</pre>

2. <em>galaxy</em>

The galaxy table contains information about galaxies. It has the following columns:

<pre>
galaxy_id (Primary Key, AUTO_INCREMENT, INT)

name (VARCHAR, UNIQUE, NOT NULL)

size (INT, NOT NULL)

distance (NUMERIC)

habitable (BOOLEAN, default FALSE)

star_count (INT, NOT NULL)
</pre>
    
3. <em>moon</em>

The moon table stores details about moons orbiting planets. The columns are:

<pre>
moon_id (Primary Key, AUTO_INCREMENT, INT)

name (VARCHAR, UNIQUE, NOT NULL)

planet_id (Foreign Key, INT, references planet.planet_id)

radius (INT)

distance_from_planet (NUMERIC)

has_atmosphere (BOOLEAN, default FALSE)
</pre>

4. <em>planet</em>

The planet table contains information about planets within a star's influence. The columns are:

<pre>
planet_id (Primary Key, AUTO_INCREMENT, INT)

name (VARCHAR, UNIQUE, NOT NULL)

star_id (Foreign Key, INT, references star.star_id)

radius (INT)

mass (INT)

has_rings (BOOLEAN, default FALSE)

distance_from_star (NUMERIC)
</pre>

5. <em>star</em>

The star table stores data on stars within galaxies. It has the following columns:

<pre>
star_id (Primary Key, AUTO_INCREMENT, INT)

name (VARCHAR, UNIQUE, NOT NULL)

galaxy_id (Foreign Key, INT, references galaxy.galaxy_id)

luminosity (INT, NOT NULL)

temperature (NUMERIC)

is_supernova (BOOLEAN, default FALSE)
</pre>

<strong>Data Types Used</strong>

INT: Used for integer values such as IDs, size, radius, luminosity, etc.

NUMERIC: Used for values that require high precision, like distances and temperatures.

TEXT: Used for descriptions or other free-form text fields.

BOOLEAN: Used for true/false values, such as whether a comet is active or whether a moon has an atmosphere.

VARCHAR: Used for name columns, ensuring unique and required entries.

<strong>Table Relationships</strong>

<em>Comet</em>: Linked to planet via planet_id (Foreign Key).

<em>Galaxy</em>: Linked to star via galaxy_id (Foreign Key).

<em>Planet</em>: Linked to star via star_id (Foreign Key).

<em>Moon</em>: Linked to planet via planet_id (Foreign Key).

<em>Star</em>: Linked to galaxy via galaxy_id (Foreign Key).

<strong>Constraints</strong>

<em>Primary Keys</em>: Each table has a primary key that is automatically incremented (e.g., comet_id, galaxy_id, moon_id, planet_id, star_id).

<em>Foreign Keys</em>: Foreign key relationships ensure referential integrity between the tables (e.g., planet_id in comet references planet_id in planet).

<em>Unique</em>: Each table has a unique constraint on the name column to ensure no duplicate names (e.g., comet_name_key, galaxy_name_key, etc.).

<em>Not Null</em>: At least two columns per table are set to NOT NULL (e.g., name, size, star_count, etc.).

<em>Defaults</em>: Default values are set for Boolean columns (e.g., is_active, habitable, has_atmosphere).

<strong>Data Insertion</strong>
Example Insert Statements:


Insert row into galaxy:

<pre>
INSERT INTO public.galaxy (name, size, distance, habitable, star_count) 
VALUES ('Milky Way', 100000, 0, TRUE, 100);
</pre>

Insert row into star:

<pre>
INSERT INTO public.star (name, galaxy_id, luminosity, temperature, is_supernova) 
VALUES ('Sun', 1, 100, 5778, FALSE);
</pre>

Insert row into planet:

<pre>
INSERT INTO public.planet (name, star_id, radius, mass, has_rings, distance_from_star) 
VALUES ('Earth', 1, 6371, 5974, FALSE, 1);
</pre>

Insert row into moon:

<pre>
INSERT INTO public.moon (name, planet_id, radius, distance_from_planet, has_atmosphere) 
VALUES ('Moon', 1, 1737, 384400, TRUE);
</pre>

Insert row into comet:

<pre>
INSERT INTO public.comet (name, planet_id, description, is_active) 
VALUES ('Halleys Comet', 1, 'A periodic comet visible from Earth every 75-76 years.', TRUE); 
</pre>

<strong>Sequence Details</strong>

Each table has an associated sequence for auto-incrementing primary key values, ensuring unique IDs for each entry.

For example:

<pre>
CREATE SEQUENCE public.comet_comet_id_seq
    AS integer
    START WITH 1
    INCREMENT BY 1;
</pre>

<strong>Example Queries</strong>

To retrieve all comets that are active:

<pre>
SELECT * FROM public.comet WHERE is_active = TRUE;
</pre>

To get all moons orbiting Earth:

<pre>
SELECT * FROM public.moon WHERE planet_id = 1;
</pre>

<strong>Conclusion</strong>

This project sets up a comprehensive relational database that models a universe containing galaxies, stars, planets, moons, and comets. The structure is well-normalized, with the necessary constraints, foreign keys, and auto-incrementing primary keys to ensure data integrity.
