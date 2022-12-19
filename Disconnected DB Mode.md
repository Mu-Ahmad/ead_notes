---
Tags: completed lec9 db
---
Links: [[EAD]]
# Disconnected DB Mode


## Connected DB Mode
A connection-based architecture relies on an open connection to the database in order to execute commands and retrieve data. This means that the connection must be established, the command must be executed, and the data must be retrieved, all within a single transaction. If the connection is closed or disrupted, the transaction will fail.
`DataReader` used for it.
## Disconnected DB Mode
a connectionless architecture does not require an open connection to the database in order to work. Instead, it uses a disconnected model, where data is retrieved from the database and stored in a local data cache (such as a DataSet) and then manipulated and updated as needed. This allows the data to be accessed and manipulated even if the connection to the database is lost or unavailable.
`DataAdapter` used for it.
##### Data Structures
`DataTable` `DataSet`

##### Process
Here is a step-by-step procedure for working with ADO.NET in a disconnected architecture:

1.  Add the appropriate Data Provider to your project.
2.  Create a connection string that specifies the connection details for the database, such as the server name, database name, and login credentials.
3.  Create a connection object using the Data Provider's connection class.
4.  Open the connection to the database using the Open() method of the connection object.
5.  Create a command object using the Data Provider's command class.
6.  Set the command's text property to the desired SQL statement, and set the connection property to the connection object.
7.  Create a DataAdapter object using the Data Provider's DataAdapter class (e.g. SqlDataAdapter for the SqlClient Data Provider).
8.  Set the DataAdapter's SelectCommand property to the command object.
9.  Create a DataSet object to store the data retrieved from the database.
10.  Use the DataAdapter's Fill() method to populate the DataSet with the data returned by the command.
11.  Close the connection to the database using the Close() method of the connection object.
12.  Use the DataSet's methods and properties to manipulate and update the data as needed.
13.  When you are ready to update the database with the changes made to the DataSet, use the DataAdapter's Update() method to apply the changes to the database.

##### Code Example
```cs
public static void Main()
{
	SqlConnection con = new SqlConnection(GetConnectionString());
	
	string selectQuery = "SELECT * FROM tbl";
	SqlCommand selectCommand = new SqlCommand(selectQuery, con);
	
	String insertQuery = $"INSERT INTO tbl values(@c1, @c2)";
	SqlCommand insertCommand = new SqlCommand(insertQuery, con);
	
	SqlParameter p1 = new SqlParameter("c1", SqlDBType.NCHar, 10, "Col1");
	SqlParameter p2 = new SqlParameter("c2", SqlDBType.NCHar, 10, "Col2");
	
	insertCommand.Parameter.Add(p1);
	insertCommand.Parameter.Add(p2);

	String updateQuery = $"UPDATE tbl set col2 = @c2 where col1=@c1";
	SqlCommand updateCommand = new SqlCommand(selectQuery, con);
	
	SqlParameter p3 = new SqlParameter("c1", SqlDBType.NCHar, 10, "Col1");
	SqlParameter p4 = new SqlParameter("c2", SqlDBType.NCHar, 10, "Col2");
	
	updateCommand.Parameter.Add(p3);
	updateCommand.Parameter.Add(p4);


	String deleteQuery = $"DELETE * FROM tbl WHERE col1 = @c1";
	SqlCommand delteCommand = new SqlCommand(deleteQuery, con);
	
	SqlParameter p5 = new SqlParameter("c1", SqlDBType.NCHar, 10, "Col1");

	deleteCommand.Parameter.Add(p5);

	// initialise DataAdapter
	SqlDataAdapter da = new();
	
	da.SelectCommand = selectCommand;
	da.InsertCommand = insertCommand;
	da.UpdateCommand = updateCommand;
	
	// Fill in DataTable
	DataTable tbl = new();
	da.Fill(tbl);

	// View Data

	foreach (DataRow row in dtbl)
	{
		// process and stuff
	}

	// Adding new record in, in-memory table
	DataRow newRow = tbl.NewRow();
	newRow["Col1"] = "Hey how you doing?";
	newRow["Col2"] = "Well I am doing just fine";
	tbl.Rows.Add(newRow);

	// push changes to DB
	da.Update(tbl);
}
```

<u>There are several ways to query a `DataSet` object in C#. Here are a few options:</u>
1.  Use the `DataSet.Tables` property to access a specific table in the `DataSet`, and then use the `DataTable.Select` method to retrieve rows that match a specified filter criteria. For example:
```cs
DataRow[] rows = myDataSet.Tables["Customers"].Select("Country='USA'");
```
2. Use LINQ to query the `DataSet` using the `AsEnumerable` method. This allows you to use LINQ operators such as `Where`, `Select`, and `OrderBy` to filter and transform the data. For example:
```cs
var query = from r in myDataSet.Tables["Customers"].AsEnumerable()
            where r.Field<string>("Country") == "USA"
            select r;
```
3.  Use the `DataView` class to create a view of the data in the `DataSet`. A `DataView` allows you to specify a sort order and filter criteria for the data, and then bind the view to a UI control such as a `DataGridView`. You can use the `DataView.RowFilter` property to specify a filter expression, and the `DataView.Sort` property to specify a sort order.
```cs
DataView view = new DataView(myDataSet.Tables["Customers"]);
view.RowFilter = "Country='USA'";
view.Sort = "CompanyName ASC";
```

----

> Fame usually comes to those who are thinking about something else.
> — <cite>Oliver Wendell Holmes Jr.</cite>

Created: 2022-11-22