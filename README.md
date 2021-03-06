# ChinookDB
## Database Schema
![alt text](https://github.com/jonathanobise/sql_project/blob/main/DatabaseSchema.png)
```
/*Query 1: In total, how many songs are in the music store per genre?*/
SELECT g.Name, COUNT(t.TrackId) Number
  FROM Track t
  JOIN Genre g ON t.GenreId = g.GenreId
  GROUP BY 1
  ORDER BY 2 DESC
  
  /*Query 2: From the top 5, how much was spent by customers per genre?*/
  SELECT g.Name Genre, SUM(il.UnitPrice * il.Quantity) Total
  FROM Customer c
  JOIN Invoice i ON i.CustomerId = c.CustomerId
  JOIN InvoiceLine il ON il.InvoiceId = i.InvoiceId
  JOIN Track t ON t.TrackId = il.TrackId
  JOIN Genre g ON g.GenreId = t.GenreId
  GROUP BY 1
  ORDER BY 2 DESC
  LIMIT 5
  
  /*Query 3: What is the total amount of money spent by customer with ID 59?*/
  SELECT c.CustomerId, c.LastName, c.FirstName, g.Name Genre,
  SUM(il.UnitPrice * il.Quantity) Total
  FROM Customer c
  JOIN Invoice i ON i.CustomerId = c.CustomerId
  JOIN InvoiceLine il ON il.InvoiceId= i.InvoiceId
  JOIN Track t ON t.TrackId = il.TrackId
  JOIN Genre g ON g.GenreId = t.GenreId
  WHERE c.CustomerId = '59'
  GROUP BY 1,2,3,4
  ORDER BY 1
  
  /*Query 4: Write a query to invite the artists who have written the most jazz or rock music in our dataset.*/
SELECT a.ArtistId, a.Name, g.Name, COUNT(t.Name) AS Songs 
  FROM Artist a JOIN Album al
    ON al.ArtistId = a.ArtistId JOIN Track t
    ON al.AlbumId = t.AlbumId JOIN Genre g
    ON t.GenreId = g.GenreId 
 WHERE g.Name = 'Rock' or g.Name = 'Jazz'
GROUP BY a.ArtistId, a.Name, g.Name 
ORDER BY Songs DESC 
```
