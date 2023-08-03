## Digital Media Store Analysis

This project analyzes a digital media store database to extract information about playlists, customer invoices, employee details, and sales data. It demonstrates the use of window functions and common table expressions. The project also focused on exploring track-related details like album names, media types, and genres. Furthermore, it aimed to identify the top-performing sales agent based on total sales in a specific year.

```
-- Select the playlist name, number of tracks on the playlist, and artist and track name of all songs on the playlist
WITH cte AS (
    SELECT 
        PT.PlaylistId, 
        P.Name AS Playlist,
        AR.Name AS Artist,
        T.Name AS Track,
        COUNT(T.Trackid) OVER (PARTITION BY PT.Playlistid) AS num_of_tracks
    FROM playlist_track PT
    JOIN tracks T
    ON PT.Trackid = T.Trackid
    JOIN playlists P
    ON P.Playlistid = PT.Playlistid
    JOIN albums ALB
    ON ALB.Albumid = T.albumid
    JOIN artists AR
    ON AR.Artistid = ALB.Artistid
    )
    SELECT 
        Playlist,
        num_of_tracks,
        Artist,
        Track
    FROM cte
    WHERE num_of_tracks < 50
    ORDER BY num_of_tracks;
	
-- Find the Invoices of customers who are from Brazil. The resulting table should show the customer's full name, Invoice ID, Date of the invoice, and billing country
SELECT C.FirstName, C.LastName, I.Invoiceid, I.InvoiceDate, I.BillingCountry
FROM customers C
JOIN invoices I 
ON C.Customerid = I.Customerid
WHERE C.Country = 'Brazil';

-- Show the Employees who are Sales Agents
SELECT FirstName, LastName, Title
FROM employees
WHERE Title LIKE 'sales%agent';

-- Find a unique/distinct list of billing countries from the Invoice table
SELECT DISTINCT BillingCountry
FROM invoices;

-- Provide a query that shows the invoices associated with each sales agent. The resulting table should include the Sales Agent's full name
SELECT E.FirstName, E.LastName, E.Title, I.Invoiceid, 
FROM invoices I 
JOIN customers C 
ON I.Customerid = C.Customerid 
JOIN employees E 
ON E.Employeeid = C.SupportRepid 
WHERE E.Title LIKE 'sales%agent'; 

-- Show the Invoice Total, Customer name, Country, and Sales Agent name for all invoices and customers
SELECT 
    I.Total, 
    C.FirstName AS cust_fname, 
    C.LastName AS cust_lname,
    C.Country AS cust_country,
    E.FirstName AS rep_fname,
    E.LastName AS rep_lname,
    E.Title AS rep_title
FROM invoices I
LEFT JOIN customers C
ON I.Customerid = C.Customerid
LEFT JOIN employees E
ON E.EmployeeId = C.SupportRepid;

-- How many Invoices were there in 2009?
SELECT COUNT(*)
FROM invoices 
WHERE InvoiceDate LIKE '2009%';  --returns 0 if '=' is used instead of 'LIKE'. Why?

--What are the total sales for 2009?
SELECT 2009 AS year, SUM(Total) AS total_sales
FROM invoices
WHERE InvoiceDate LIKE '2009%';

-- Write a query that includes the purchased track name with each invoice line ID
SELECT 
    T.Name,
    I.InvoiceLineId
FROM invoice_items I
JOIN tracks T
ON I.TrackId = T.TrackId;

-- Write a query that includes the purchased track name AND artist name with each invoice line ID
SELECT 
    T.Name AS track,
    Ar.Name AS artist,
    I.InvoiceLineId
FROM invoice_items I
JOIN tracks T
ON I.TrackId = T.TrackId
JOIN albums Alb
ON Alb.AlbumId = T.AlbumId
JOIN artists Ar
ON Ar.ArtistId = Alb.ArtistId;

-- Provide a query that shows all the Tracks, and include the Album name, Media type, and Genre
SELECT
    T.Name AS track,
    A.Title AS album,
    M.Name AS media_type,
    G.Name AS genre
FROM tracks T
JOIN albums A
ON T.AlbumId = A.albumId
JOIN media_types M
ON T.MediaTypeId = M.MediaTypeId
JOIN genres G
ON T.GenreId = G.GenreId;

-- Show the total sales made by each sales agent
SELECT
    E.EmployeeId, 
    E.FirstName,
    E.LastName,
    SUM(I.Total) AS total_sales
FROM invoices I
JOIN customers C
ON I.CustomerId = C.CustomerId
RIGHT JOIN employees E
ON E.EmployeeId = C.SupportRepId
WHERE E.Title LIKE 'sales%agent'
GROUP BY E.EmployeeId;

-- Which sales agent made the most dollars in sales in 2009?
SELECT
    E.EmployeeId, 
    E.FirstName,
    E.LastName,
    SUM(I.Total) AS total_sales
FROM invoices I
JOIN customers C
ON I.CustomerId = C.CustomerId
RIGHT JOIN employees E
ON E.EmployeeId = C.SupportRepId
WHERE E.Title LIKE 'sales%agent'
GROUP BY E.EmployeeId
ORDER BY total_sales DESC
LIMIT 1;
```
