# excel-generic-workflows
# This repo contains common business ops related to excel
# Following are some of the codes used for excel ops

# To Get Matched Records

Datatable Out_Matched_Data = In_DataTable1.AsEnumerable().Where(function(row) In_DataTable2.AsEnumerable().Select(function(r) r.Field(Of Int32)(In_DT2_ColName_To_Match.ToString)).Any(function(x) x = row.Field(Of Int32)(In_DT1_ColName_To_Match.ToString))).CopyToDataTable()

# To Get Not Matched Records

Datatable Out_NonMatched_Data = In_DataTable1.AsEnumerable().Where(function(row) Not In_DataTable2.AsEnumerable().Select(function(r) r.Field(Of Int32)(In_DT2_ColName_To_Match.ToString)).Any(function(x) x = row.Field(Of Int32)(In_DT1_ColName_To_Match.ToString))).CopyToDataTable()

#  Refer the below code to remove the empty row from the Data Table.

DataTableName=DataTableName.Rows.Cast(Of DataRow)().Where(Function(row) Not row.ItemArray.All(Function(field) field Is DBNull.Value Or field.Equals(""))).CopyToDataTable()


#  to find sum based on condition

dtTesting.AsEnumerable.Sum(Function (x) If(Double.TryParse(x.item("Column2").ToString, Nothing), Double.Parse(x.Item("Column2").ToString), 0))


#  to find sum of a column without condition
Dt.AsEnumerable().Sum(Function(x) Double.Parse(x.Item(5).ToString))

#  to get dublicate
datatable variable** (From p in dt.Select() where( From q in dt.Select() where string.Join(",",q.ItemArray).Equals(string.Join(",",p.ItemArray)) Select q).ToArray.Count>1 Select p).ToArray.CopyToDataTable

#  Remove rows based on particular column is empty.
DataTableName.Select("Convert(column3, System.String)< >''").CopyToDataTable()
or
DataTableName.Select("column3< >''").CopyToDataTable()

# Distinct Based on the specific column name from the data table and need to return the hole data.
Remove Duplicate record from the Data Table based on Column Name
dt.AsEnumerable().GroupBy(Function(i) i.Field(Of String)("ColumnName")).Select(Function(g) g.First).CopyToDataTable()
Or
((From LineNo In dt.DefaultView.ToTable(True,"Product").Select().ToList() Select (From row In dt.Select Where row("Product").ToString=LineNo("Product").ToString Select row).ToList(0)).ToList()).CopyToDatatable()

#  Distinct Based on the specific column name from the data table.

DataView view = new DataView(table)
DataTable distinctValues = view.ToTable(true, "Column1", "Column2" ...)
or
DataTable =DataTable.DefaultView.ToTable(true)

Sorting the data table based on particular column name
dt = dt.Select("",[ColumnName] asc").CopyToDataTable()

# Duplicate records from the same data table
(From p in dt.Select() where( From q in dt.Select() where string.Join(",",q.ItemArray).Equals(string.Join(",",p.ItemArray)) Select q).ToArray.Count>1 Select p).ToArray.CopyToDataTable()

# Duplicate records from the same data table and
If you want specific Column alone mention the column name
(From p in dt.Select() where( From q in dt.Select() where q("ColumnName").Equals(p("ColumnName")) Select q).ToArray.Count>1 Select p).ToArray.CopyToDataTable()

# Get Max value from the data table column value
int MaxValue=Convert.ToInt32(dt.AsEnumerable().Max(Function(row) row("Column2")))


# find a value in an array and get the value
(from name in febaFiles where name.Contains("At") select name).First.ToString


# regex to remove hidden characters in a string

System.Text.RegularExpressions.Regex.Replace(Input variable, "[^\x20-\x7F]", "")

