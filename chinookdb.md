1. Provide a query that shows the most purchased Media Type.
```sql
SELECT Sum(invoice.total) AS TotalSales, 
       track.name, 
       mediatype.name     AS MediaType 
FROM   invoiceline 
       JOIN track 
         ON track.trackid = invoiceline.trackid 
       JOIN invoice 
         ON invoice.invoiceid = invoiceline.invoiceid 
       JOIN mediatype 
         ON mediatype.mediatypeid = track.mediatypeid 
GROUP  BY track.name 
ORDER  BY totalsales DESC 
``` 

---


2. Provide a query that shows the top 3 best-selling artists.
```sql
SELECT Sum(invoiceline.quantity) AS NumberOfTracksSold, 
       track.name, 
       invoice.invoicedate       AS DateSold, 
       artist.name               AS ArtistName 
FROM   invoiceline 
       JOIN track 
         ON track.trackid = invoiceline.trackid 
       JOIN invoice 
         ON invoice.invoiceid = invoiceline.invoiceid 
       JOIN album 
         ON album.albumid = track.albumid 
       JOIN artist 
         ON artist.artistid = album.artistid 
GROUP  BY track.name 
ORDER  BY numberoftrackssold DESC 
LIMIT  3
``` 

---



3. Provide a query that shows the top 5 most purchased tracks over all.
```sql
SELECT Sum(invoiceline.quantity) AS NumberOfTracksSold, 
       track.name, 
       invoice.invoicedate       AS DateSold 
FROM   invoiceline 
       JOIN track 
         ON track.trackid = invoiceline.trackid 
       JOIN invoice 
         ON invoice.invoiceid = invoiceline.invoiceid 
GROUP  BY track.name 
ORDER  BY numberoftrackssold DESC 
LIMIT  5 
``` 

---


4. Provide a query that shows total sales made by each sales agent.
```sql
SELECT employee.firstname, 
       employee.lastname, 
       Sum(invoice.total) 
FROM   invoice 
       JOIN customer 
         ON customer.customerid = invoice.customerid 
       JOIN employee 
         ON employee.employeeid = customer.supportrepid 
GROUP  BY employee.employeeid
``` 

---

 

5. Provide a query that shows all Invoices but includes the # of invoice line items.
```sql
SELECT invoice.invoiceid, 
       Count(invoiceline.invoicelineid) AS NumberOfInvoiceLines 
FROM   invoice 
       JOIN invoiceline 
         ON invoice.invoiceid = invoiceline.invoiceid 
GROUP  BY invoice.invoiceid 
``` 

---


6. Provide a query that shows all the Tracks but displays no IDs. The resultant table should include the Album name, Media type and Genre.
```sql
SELECT album.title    AS AlbumTitle, 
       track.NAME     AS TrackName, 
       mediatype.NAME AS MediaType, 
       genre.NAME     AS Genre 
FROM   track 
       JOIN album 
         ON album.albumid = track.albumid 
       JOIN mediatype 
         ON mediatype.mediatypeid = track.mediatypeid 
       JOIN genre 
         ON genre.genreid = track.genreid 
``` 

---


7. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table.
```sql
SELECT pl.NAME, 
       Count(pt.trackid) 
FROM   playlist pl 
       JOIN playlisttrack pt 
         ON pt.playlistid = pl.playlistid 
GROUP  BY pl.NAME 
``` 

---


8. Provide a query that includes the purchased track name AND artist name with each invoice line item.
```sql
SELECT invoicelineid, 
       track.NAME  AS TrackName, 
       artist.NAME AS ArtistName 
FROM   track 
       JOIN invoiceline 
         ON invoiceline.trackid = track.trackid 
       JOIN album 
         ON album.albumid = track.albumid 
       JOIN artist 
         ON artist.artistid = album.albumid 
``` 

---


9. Provide a query that includes the track name with each invoice line item.
```sql
SELECT invoicelineid, 
       track.NAME 
FROM   track 
       JOIN invoiceline 
         ON invoiceline.trackid = track.trackid 
``` 

---


10. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
```sql
SELECT total, 
       customer.firstname AS CustFirstName, 
       customer.lastname  AS CustLastName, 
       employee.firstname AS EmpFirstName, 
       employee.lastname  AS EmpLastName, 
       customer.country   AS CustCountry, 
       supportrepid 
FROM   invoice 
       JOIN customer 
         ON customer.customerid = invoice.customerid 
       JOIN employee 
         ON employee.employeeid = customer.supportrepid 
``` 

---


11. Provide a query that shows the most purchased track of 2013.
```sql
SELECT *, 
       Count(t.trackid) AS COUNT 
FROM   invoiceline AS il 
       JOIN invoice AS i 
         ON i.invoiceid = il.invoiceid 
       JOIN track AS t 
         ON t.trackid = il.trackid 
WHERE  i.invoicedate BETWEEN '2013-01-01' AND '2013-12-31' 
GROUP  BY t.trackid 
ORDER  BY count DESC
``` 

---


12. Provide a query that shows the # of customers assigned to each sales agent.
```sql
SELECT e.*, 
       Count(c.customerid) AS 'TotalCustomers' 
FROM   employee AS e 
       JOIN customer AS c 
         ON e.employeeid = c.supportrepid 
GROUP  BY e.employeeid 
``` 

---



13. Which sales agent made the most in sales over all?
```sql
SELECT *, 
       Max(total) 
FROM   (SELECT e.*, 
               Sum(total) AS 'Total' 
        FROM   employee AS e 
               JOIN customer AS c 
                 ON e.employeeid = c.supportrepid 
               JOIN invoice AS i 
                 ON i.customerid = c.customerid 
        GROUP  BY e.employeeid)
``` 

---



14. Which sales agent made the most in sales in 2010?
```sql
SELECT *, 
       Max(total) 
FROM   (SELECT e.*, 
               Sum(total) AS 'Total' 
        FROM   employee AS e 
               JOIN customer AS c 
                 ON e.employeeid = c.supportrepid 
               JOIN invoice AS i 
                 ON i.customerid = c.customerid 
        WHERE  i.invoicedate BETWEEN '2010-01-00' AND '2010-12-31' 
        GROUP  BY e.employeeid) 
``` 

---



15. Which sales agent made the most in sales in 2009?
```sql
SELECT *, 
       Max(total) 
FROM   (SELECT e.*, 
               Sum(total) AS 'Total' 
        FROM   employee AS e 
               JOIN customer AS c 
                 ON e.employeeid = c.supportrepid 
               JOIN invoice AS i 
                 ON i.customerid = c.customerid 
        WHERE  i.invoicedate BETWEEN '2009-01-00' AND '2009-12-31' 
        GROUP  BY e.employeeid) 
``` 

---



16. Provide a query that shows total sales made by each sales agent.
```sql
SELECT e.*, 
       Count(i.invoiceid) AS 'Total Number of Sales' 
FROM   employee AS e 
       JOIN customer AS c 
         ON e.employeeid = c.supportrepid 
       JOIN invoice AS i 
         ON i.customerid = c.customerid 
GROUP  BY e.employeeid
``` 

---



17. Provide a query that shows all the Tracks but displays no IDs. The resultant table should include the Album name, Media type and Genre.
```sql
SELECT t.NAME  AS 'track', 
       t.composer, 
       t.milliseconds, 
       t.bytes, 
       t.unitprice, 
       a.title AS 'album', 
       g.NAME  AS 'genre', 
       m.NAME  AS 'media type' 
FROM   track AS t 
       JOIN album AS a 
         ON a.albumid = t.albumid 
       JOIN genre AS g 
         ON g.genreid = t.genreid 
       JOIN mediatype AS m 
         ON m.mediatypeid = t.mediatypeid 
``` 

---



18. Provide a query that includes the purchased track name AND artist name with each invoice line item.
```sql
SELECT i.*, 
       t.NAME  AS 'track', 
       ar.NAME AS 'artist' 
FROM   invoiceline AS i 
       JOIN track AS t 
         ON i.trackid = t.trackid 
       JOIN album AS al 
         ON al.albumid = t.albumid 
       JOIN artist AS ar 
         ON ar.artistid = al.artistid 
``` 

---



19. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
```sql
SELECT e.firstname AS 'employee first', 
       e.lastname  AS 'employee last', 
       c.firstname AS 'customer first', 
       c.lastname  AS 'customer last', 
       c.country, 
       i.total 
FROM   employee AS e 
       JOIN customer AS c 
         ON e.employeeid = c.supportrepid 
       JOIN invoice AS i 
         ON c.customerid = i.customerid 
``` 

---



20. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
```sql
SELECT   e.firstname, 
         e.lastname, 
         i.invoiceid, 
         i.customerid, 
         i.invoicedate, 
         i.billingaddress, 
         i.billingcountry, 
         i.billingpostalcode, 
         i.total 
FROM     customer AS c, 
         invoice  AS i 
on c.customerid = i.customerid 
JOIN     employee AS e 
ON       e.employeeid = c.supportrepid 
ORDER BY e.employeeid
``` 

---



21. Find the customer that has spent the most on music for each country.
```sql
WITH t1 AS 
( 
         SELECT   c.country, 
                  Sum(i.total) totalspent, 
                  c.firstname, 
                  c.lastname, 
                  c.customerid 
         FROM     customer c 
         JOIN     invoice i 
         ON       c.customerid = i.customerid 
         GROUP BY c.customerid ) 
SELECT   t1.* 
FROM     t1 
JOIN 
         ( 
                  SELECT   country, 
                           Max(totalspent) AS maxtotalspent, 
                           firstname, 
                           lastname, 
                           customerid 
                  FROM     t1 
                  GROUP BY country )t2 
ON       t1.country = t2.country 
WHERE    t1.totalspent = t2.maxtotalspent 
ORDER BY totalspent DESC, 
         country
LIMIT 7
``` 

---



22. How many rock songs were purchased from each country
```sql
SELECT i.billingcountry Country, 
       Count(*)         RockSongsPurchased 
FROM   invoice i 
       JOIN invoiceline il 
         ON i.invoiceid = il.invoiceid 
       JOIN track t 
         ON il.trackid = t.trackid 
       JOIN genre g 
         ON t.genreid = g.genreid 
WHERE  g.name = 'Rock' 
GROUP  BY billingcountry 
ORDER  BY rocksongspurchased DESC, 
          billingcountry 
LIMIT  7
``` 

---



23. How yearly income varies according to genre
```sql
SELECT   Strftime('%Y', i.invoicedate)   year, 
         Sum(il.quantity * il.unitprice) income, 
         g.NAME                          genrename 
FROM     invoice i 
JOIN     invoiceline il 
ON       i.invoiceid = il.invoiceid 
JOIN     track t 
ON       t.trackid = il.trackid 
JOIN     genre g 
ON       t.genreid = g.genreid 
WHERE    genrename IN ('Rock', 
                       'Blues', 
                       'Bossa Nova', 
                       'Jazz', 
                       'Latin') 
GROUP BY 1, 
         3
``` 

---



24. How monthly income varies in 2013 for Rock genre
```sql
SELECT Strftime('%Y', i.invoicedate)   Year, 
       Strftime('%m', i.invoicedate)   Month, 
       Sum(il.quantity * il.unitprice) Income, 
       g.NAME                          GenreName 
FROM   invoice i 
       JOIN invoiceline il 
         ON i.invoiceid = il.invoiceid 
       JOIN track t 
         ON t.trackid = il.trackid 
       JOIN genre g 
         ON t.genreid = g.genreid 
WHERE  genrename = 'Rock' 
       AND year = '2013' 
GROUP  BY 1, 
          2 
``` 

---



