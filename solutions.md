#Foreign Keys New Table

##  Create a new table called Movie with an ID, Title, and MediaTypeId.
##  Make MediaTypeId a foreign key to the MediaTypeId column on the MediaType table.
##  Add a new entry into the Movie table with a Title and MediaTypeId.
##  Query the Movie table to get your entry.

###Solution
CREATE TABLE Movie(
ID SERIAL PRIMARY KEY,
Title TEXT,
MediaTypeId TEXT,
FOREIGN KEY(MediaTypeId) REFERENCES MediaType(MediaTypeId)
);

INSERT INTO movie
(Title, MediaTypeId)
VALUES
('Where the Red Fern Grows', 3),
('Iron Man', 1),
('The Rescuers', 2),
('Puss in Boots', 2),
('The Hot Chick', 4),
('WaterBoy', 4),
('Indiana Jones', 1);

SELECT * FROM movie;
 
-- SELECT * FROM mediatype;

#Foreign Keys - Existing Table

##Add a new column called GenreId that references the Genre table
##Query the Movie table to see your entry.

ALTER TABLE Movie
ADD COLUMN GenreId INTEGER REFERENCES Genre(GenreId);

SELECT * FROM Movie;

#Updating Rows

##Update the first entry in the Movie table to a GenreId of 22.
##Query the Movie table to see your entry.

UPDATE Movie
SET GenreId=22
WHERE ID=1;

SELECT * FROM Movie;

#Using Joins

##Summary
##Now that we know how to make foreign keys and change data, let's do some practice queries. The simplest way to use a foreign key is via a join statement.

##Instructions
##Join the Artist and Album tables to list out the Artist name and Album name.

SELECT a.title, ar.Name 
FROM Album a 
JOIN Artist ar ON a.ArtistId = ar.ArtistId;

#Using nested queries/sub-selects

##Use a sub-select statement to get all tracks from the Track table where the GenreId is either Jazz or Blues.
SELECT * FROM Track 
WHERE GenreId IN ( SELECT GenreId FROM Genre WHERE Name = 'Jazz' OR Name = 'Blues' );

#Setting values to null

##Update Phone on the Employee table to null where the EmployeeId is 1.
##Query the Employee table to get the employee you just updated.
UPDATE Employee SET Phone=null WHERE EmployeeId=1;
SELECT * FROM Employee;

#Querying a null value

##Get all customers from the Customer table who do not have a company.

SELECT * FROM Customer WHERE Company IS null;

#Group by

##Select all artist ids, artist names, and count how many albums they have.

SELECT ar.artistId, ar.name, count(*) 
FROM Artist ar
JOIN Album a ON ar.ArtistId = a.ArtistId 
GROUP BY ar.artistId;

#Distinct

##Get all countries from the Customer table with no duplicates.
SELECT DISTINCT Country FROM Customer;


#Delete Rows

##Select all records from the Customer table where fax is null;
##Delete all records from the Customer table where fax is null;
SELECT * FROM Customer WHERE Fax IS null;
DELETE FROM Customer WHERE Fax IS null;