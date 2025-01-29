# Export workitems from azure devops board

## a)Using Azure DevOps Web Interface
1. Navigate to Queries:
Go to the Boards area in your Azure DevOps project.
Click on Queries.

2. Create a New Query:
Click on New query.
Set the filters to include all work items you want to export. For example:
Work Item Type = [Any]
State = [Any]

3. Run the Query:
Click on the Run button to execute the query.

4. Export to CSV:
Once the query results are displayed, click on the Export button.
Choose CSV to download the work items in CSV format.

## b)Using Azure DevOps REST API
You can also use the Azure DevOps REST API to export work items programmatically:

1. Run a WIQL Query:
Create a WIQL query to fetch the work items you need.
POST https://dev.azure.com/{organization}/{project}/_apis/wit/wiql?api-version=7.0
Content-Type: application/json

```
{
  "query": "SELECT [System.Id], [System.Title], [System.State] FROM workitems 
  WHERE [System.TeamProject] = 'YourProject'"
}
```

2. Get Work Item IDs:
The response will contain the work item IDs.
```
{
  "workItems": [
    { "id": 1 },
    { "id": 2 },
    { "id": 3 }
    // ...
  ]
}
```

3. Retrieve Work Item Details:
Use the Get Work Items Batch API to retrieve details of all the work items.
POST https://dev.azure.com/{organization}/{project}/_apis/wit/workitemsbatch?api-version=7.0
Content-Type: application/json
```
{
  "ids": [1, 2, 3, ...],
  "fields": ["System.Id", "System.Title", "System.State"]
}
```
