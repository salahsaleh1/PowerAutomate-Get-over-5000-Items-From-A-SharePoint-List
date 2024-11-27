# PowerAutomate-Get-over-5000-Items-From-A-SharePoint-List
Lets learn how to pull more than 5000 items in PowerAutomate from SharePoint List


In this article, we explore two methods to handle large SharePoint lists with Power Automate. First, the SharePoint – Get Items action can retrieve more than 5,000 list items by increasing the top count and enabling pagination. For lists exceeding 100,000 items, the SharePoint – Send An HTTP Request action is required. Both techniques are detailed in this article.



# Method#1: Increase Top Count and Enable Pagination
The simplest method to retrieve over 5,000 records from a SharePoint list is by using the SharePoint Get Items action. To achieve this, set the Top Count in the Get Items action to 5,000, enable pagination, and adjust the threshold to 100,000 items. This configuration will allow you to fetch up to 100,000 items.

### Create A Large SharePoint List With Over 5000 Items
We need to build a SharePoint list with 5000 items. Make a new list named Large SP List and Include Following columns:
- ID - unique identifer
- Title - tile
- Country - single line of text
- Food - single line of text

| ID | Title | Country | Food |
|----------|----------|----------|----------|
| 1    | Item01     | Austria     | Seafood paella     |
| 2    | Item01     | Mali     | Lamb Chops     |
| 3    | Item03     | Croatia     | Chicken fajitas     |
| 4    | Item04     | Poland     | Pancakes     |
| ..   | ..         | ..      | ..     |
| 45000    | Item45000     | Ireland     | Apple Sauce     |


Populate the SharePoint list with items. In my example I created a list with 45000 items.


![SPLargeList](https://github.com/user-attachments/assets/2b2fe5c5-be11-422c-85bb-da461f38dbff)

<br><br><br>

### Get Items From SharePoint And Increase Top Count To 5000
In Power Automae create a new flow with an instant trigger named Get Items Large SharePoint List.
Add a SharePoint - Get Items action to the flow and select the Large SP List. The Get Items action will only fetch 100 list items by default. We can increase the maximum number of list items retrieved to over 100,000 items by changing two settings.

Increase the Top Count to 5,000. This will allow us to get 5,000 records on each page of results. It is the maximum value allowed in the Top Count field.
<br><br>

![get-ItemActions](https://github.com/user-attachments/assets/69c8757c-aad0-419e-b5c8-6b2785df46b1)

<br><br>
Then go to Settings tab in Get Items action and enable pagination. Set the threshold to 100,000 records. It is the maximum value for this field. The flow will now get up to 100,000 records by requesting 5,000 records at a time.
<br>
![get-ItemSettings](https://github.com/user-attachments/assets/e97bcf42-001e-485f-9eae-ee55101b48c3)
<br><br><br><br><br>
Finally, we want to verify the number of SharePoint list items retrieved. Insert a Compose action into the flow.
<br><br><br><br>
![compose-countItems](https://github.com/user-attachments/assets/f54d03c5-6406-46c5-b67f-f9fb311006d6)
<br><br><br><br>
Then add this Power Automate expression to calculate the number of items returned.
<br>
`length(outputs('Get_items')?['body/value'])                                         `

<br><br><br>
### Run The Flow To Get Over 5000 List Items
<br>
<img src="https://github.com/user-attachments/assets/01963926-6f5e-46a7-883a-2c6b08d6a227" alt="Final Compose Outcome" width="700" height="700">
