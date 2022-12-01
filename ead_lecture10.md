---
Tags: toProcess
---
Links: [[EAD]]
# Disconnected DB Mode


## Connected DB Mode

## Disconnected DB Mode

We will use `SqlDataAdapter` class for this purpose.
##### Data Structures
`DataTable` `DataSet`

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


----

Created: 2022-11-22