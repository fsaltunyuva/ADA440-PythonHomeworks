### 1. Which sales agent made the most in sales in 2010? (Provide a query)
```
-- Jane Peacock by 221.92 total sales in 2010.
select employees.EmployeeId, employees.FirstName, employees.LastName, sum(invoices.Total) as TotalSales -- Summing the total of invoices to get total sales
from customers, employees, invoices 
where employees.Title == "Sales Support Agent" -- Getting the sale agents
and employees.EmployeeId == customers.SupportRepId -- Linking the sale agents with their customers
and customers.CustomerId == invoices.CustomerId -- Linking the customers with their invoices
and invoices.InvoiceDate like "2010%" -- Filtering the invoices from 2010
group by employees.FirstName || " " || employees.LastName -- Grouping by the names of the employees to combine the same rows into a single row
order by TotalSales desc; -- Ordering the total sales in invoices in descending order
```
### 2. Which sales agent made the most in sales over all? (Provide a query)
```
-- Jane Peacock by 833.04 total sales.
select employees.EmployeeId, employees.FirstName, employees.LastName, sum(invoices.Total) as TotalSales -- Summing the total of invoices to get total sales
from customers, employees, invoices 
where employees.Title == "Sales Support Agent" -- Getting the sale agents
and employees.EmployeeId == customers.SupportRepId -- Linking the sale agents with their customers
and customers.CustomerId == invoices.CustomerId -- Linking the customers with their invoices
group by employees.FirstName || " " || employees.LastName -- Grouping by the names of the employees to combine same rows into a single row
order by TotalSales desc; -- Ordering the total sales in invoices in descending order
```
### 3. Provide a query that shows the # of customers assigned to each sales agent.
```
select employees.EmployeeId, employees.FirstName, employees.LastName, count(customers.SupportRepId) as "# of customers assigned" -- Counting the sale agents of the customers to get the numer of customers assigned
from customers, employees
where employees.Title == "Sales Support Agent" -- Getting the sale agents
and employees.EmployeeId == customers.SupportRepId -- Linking the sale agents with their customers
group by employees.FirstName || " " || employees.LastName -- Grouping by the names of the employees to combine same rows into a single row
```
### 4. Provide a query that shows the total sales per country. Which country's customers spent the most?
```
-- USA with 91 sales.
select invoices.BillingCountry, count(invoices.InvoiceID) as TotalSales -- Counting total sales as TotalSales to order later
FROM invoices
GROUP BY invoices.BillingCountry -- Grouping by country names
order by TotalSales desc; -- Ordering total sales for the country in descending order
```
### 5. Provide a query that shows the most purchased track of 2013.
```
-- It results as "Where Eagles Dare" with the purchase count 2 but there other tracks that has the purchase count as 2. It can be seen by deleting the last line ("limit 1").
select tracks.name, count(invoice_items.TrackId) as PurchaseCount -- Counting the track ids on invoice items to get purchase count
from tracks, invoice_items, invoices
where tracks.TrackId == invoice_items.TrackId -- Linking tracks with the invoice items
and invoice_items.InvoiceId == invoices.InvoiceId -- Linking invoice items with invoices
and invoices.InvoiceDate like "2013%" -- Filtering the invoices from 2013
group by tracks.Name -- Grouping by the track names
order by PurchaseCount desc -- Ordering by their purchase count
limit 1; -- Getting the most purchased one
```
### 6. Provide a query that shows the top 5 most purchased tracks over all.
```
select tracks.Name, count(invoice_items.TrackId) as PurchaseCount -- Counting the track ids on invoice items to get purchase count
from tracks, invoice_items
where tracks.TrackId == invoice_items.TrackId -- Linking tracks with the invoice items
group by tracks.Name -- Grouping by the track names
order by PurchaseCount desc -- Ordering by their purchase count
limit 5; -- Getting the top 5
```
### 7. Provide a query that shows the top 3 best selling artists.
```
select artists.Name, count(invoice_items.TrackId) as PurchaseCount -- Counting the track ids on invoice items to get purchase count
from artists, invoice_items, tracks, albums
where tracks.TrackId  == invoice_items.TrackId -- Linking tracks with the invoice items
and tracks.AlbumId == albums.AlbumId -- Linking tracks with their albums
and albums.ArtistId == artists.ArtistId -- Linking albums with their artists
group by artists.Name -- Grouping by the artist names
order by PurchaseCount desc -- Ordering by their purchase count
limit 3; -- Getting the top 3
```
### 8. Provide a query that shows the most purchased Media Type.
```
select media_types.Name, count(invoice_items.TrackId) as PurchaseCount -- Counting the track ids on invoice items to get purchase count
from media_types, invoice_items, tracks
where tracks.TrackId == invoice_items.TrackId -- Linking tracks with the invoice items
and tracks.MediaTypeId == media_types.MediaTypeId -- Linking tracks with their media types
group by media_types.Name -- Grouping by media type names
order by PurchaseCount desc -- Ordering by their purchase count
limit 1; -- Getting the top 1
```
### 9. Which customer has the highest average invoice total? (Provide a query)
```
-- Helena Holy with AvgTotalSales as 7.09
select customers.CustomerId, customers.FirstName, customers.LastName, avg(invoices.Total) as AvgTotalSales -- Getting the average of the total of invoices to get average total sales
from customers, invoices
where customers.CustomerId == invoices.CustomerId -- Linking customers with their invoices
group by customers.FirstName || " " || customers.LastName -- Grouping by customer names
order by AvgTotalSales desc; -- Ordering by their average total sales
```
### 10. Provide a query that lists the genres with the most tracks.
```
select genres.Name, count(tracks.TrackId) as CountOfTracksWithThisGenre -- Counting the track ids to get the count of tracks with this genre
from tracks, genres
where genres.GenreId == tracks.GenreId -- Linking genres with tracks
group by genres.Name -- Grouping by genre names
order by CountOfTracksWithThisGenre desc; -- Ordering by their count of tracks with this genre
```