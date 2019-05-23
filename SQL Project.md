**QUERY A DIGITAL MUSIC STORE DATABASE (Chinook Database)**


**Introduction**

In this project, you will query the Chinook Database. The Chinook Database holds information about a music store. For this project, you will be assisting the Chinook team with understanding the media in their store, their customers and employees, and their invoice information. To assist you in the queries ahead, the schema for the Chinook Database is provided below. You can see the columns that link tables together via the arrows.


All of the below instructions are discussed in detail as we work through this lesson on your way to completing this project. The below serves as a quick reference of what you will be doing as you progress through the completion of this project.

**Instructions**

You will need to follow the instructions on the next three concepts to get the Chinook database up and running on your own machine, and check that it is set up correctly. There will be two parts to this project.

1. The first part is a series of questions that will assure you have mastered the main concepts taught throughout the SQL lessons. Though these questions will not be "graded" by a reviewer, they will help you self assess.


2. The second part is a presentation. Similar to the first project, there isn't a 'right answer' for the second portion of the project. You have the ability to be creative in the questions you ask. You will then write a SQL query to pull the data needed to successfully answer your question. Use the pulled data to build a visual (bar chart, histogram, or another plot) that answers your question. The essentials of your project submission are discussed in the next sections. In order to review your presentation, you will need to save your slides as a PDF.

---

**1. Which Playlist has the most tracks?**
```sql
SELECT P.NAME   PlaylistName, 
       Count(*) "Number of Tracks" 
FROM   PlaylistTrack PT 
       JOIN Playlist P 
         ON PT.PlaylistId = P.PlaylistId 
GROUP  BY 1 
ORDER  BY 2 DESC 
```
![](https://github.com/nishajagan/nishajagan.github.io/blob/master/query1.png)

***

**2. Which country has the most total orders?**
```sql
SELECT C.Country, 
       sum(I.Total) TotalInvoice 
FROM   Customer C 
       JOIN Invoice I 
         ON C.CustomerId = I.CustomerId 
GROUP  BY 1 
ORDER  BY 2 DESC 
LIMIT  10 
```


***

**3. What is the monthly income for Rock genre in 2009?**
```sql
SELECT strftime('%m', I.InvoiceDate)   Month, 
       sum(IL.Quantity * IL.UnitPrice) Income 
FROM   Invoice I 
       JOIN InvoiceLine IL 
         ON I.InvoiceId = IL.InvoiceId 
       JOIN Track T 
         ON T.TrackId = IL.TrackId 
       JOIN Genre G 
         ON T.GenreId = G.GenreId 
WHERE  G.NAME = 'Rock' 
       AND strftime('%Y', I.InvoiceDate) = '2009' 
GROUP  BY 1 
```


***

**4. What is the yearly income according to genre?**
```sql
SELECT strftime('%Y', I.InvoiceDate)   Year, 
       sum(IL.Quantity * IL.UnitPrice) Income,
     G.Name                Genre_Name
FROM   Invoice I 
       JOIN InvoiceLine IL 
         ON I.InvoiceId = IL.InvoiceId 
       JOIN Track T 
         ON T.TrackId = IL.TrackId 
       JOIN Genre G 
         ON T.GenreId = G.GenreId 
WHERE  G.NAME In ("Alternative & Punk", "Blues", "Jazz", "Latin", "Reggae", "Rock") 
GROUP  BY 1, 3
```
