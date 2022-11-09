---
Tags: ead toProcess
---
Links: [[EAD|HomePage]]
# DataBases - ADO.Net

## Architecture
```mermaid
graph TD
	A[Console App]
	subgraph ADO.NET
		a[SqlConnection]
		b[SqlCommand]
		c[SqlDataReader]
		subgraph .
			1[ExecuteNonQuery]
			2[ExecuteReader]
			3[ExecuteScalar]
			subgraph -
				1a[Insert]
				1b[Update]
				1c[Delete]
			end
			1 --> 1a
			1 --> 1b
			1 --> 1c
		end

		b --> 1
		b --> 2
		b --> 3
		end
	B[("RDBMS<br>------<br>Ms SQL Server")]
	A --> a
	a --> B
```

## Package
`Microsoft.Data.sqlClient`

## Process
```cs
using System;

class program
{
    public static void Main()
    {
        // 1. Create Connection
        string connectionString = "Something";
        SqlConnection con = new SqlConnection(connectionString); 
        con.Open();

		// 2. Make A query Command
		string query = "Select * from Table";
		SqlCommand cmd = new SqlCommand(query, con);

		// 3. Execute Query
		SqlDataReader dr = cmd.ExecuteReader();

		while (dr.Read())
		{
			//do your stuff
			Console.WriteLine(dr['col1'] + " " + dr['col2'] + "\n");
		}
		// 4. Close Connection
		con.Close();
    }
}
```


## API



---
> Freedom is not worth having if it does not connote freedom to err.
> — <cite>Mahatma Gandhi</cite>

Created: 2022-11-08