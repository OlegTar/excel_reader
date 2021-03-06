# excel_reader
PHP library for reading excel files

This is excel_reader2.php library. I fixed some bugs in it.

# Usage
```php
$reader = new Spreadsheet_Excel_Reader("price.xls");
for ($i = 1; $i <= $reader->sheets[0]['numRows']; $i++) {
  for ($j = 1; $j <= $reader->sheets[0]['numCols']; $j++) {
      $value = mb_strtolower($reader->sheets[0]['cells'][$i][$j], "utf8");
			$value = trim($value);
			print $value;
  }
  print "\n";
}
```

# Creating The Reader Object
```php
$data = new Spreadsheet_Excel_Reader("test.xls");
```
Or conserve memory for large worksheets by not storing the extended information about cells like fonts, colors, etc.

```php
$data = new Spreadsheet_Excel_Reader("test.xls",false);
```
To use a coding other than UTF-8 (default) you can pass it as the 3rd parameter.

```php
$data = new Spreadsheet_Excel_Reader("test.xls",true,"UTF-16");
```

# Dumping Worksheet Contents
The simplest way to interact with an XLS file is to just dump it to HTML for display in a browser. This method will generate a table with inline CSS and all available formatting.
```php
$data->dump($row_numbers=false,$col_letters=false,$sheet=0,$table_class='excel')
```
# Accessing Cell Values

It is recommended that the public API functions be used to access data rather than relying on the underlying data structure, which may change between releases.

Retrieve the formatted value of a cell (what is displayed by Excel) on the first (or only) worksheet:

```php 
$data->val($row,$col) 
```
You can also use column names rather than numbers:

```php 
$data->val(10,'AZ') 
```
Access data on a different sheet:

```php 
$data->val($row,$col,$sheet_index) 
```
Sheet Info
Get the count of how many rows/cols are on a sheet (default: first sheet):

```php 
$data->rowcount($sheet_index=0) $data->colcount($sheet_index=0) 
```

# Cell Info
The type of data in the cell: number|date|unknown

```php 
$data->type($row,$col,$sheet=0) 
```
The raw data stored for the cell. For example, a cell may contain 123.456 but display as 123.5 because of the cell's format. Raw accesses the underlying value.
```php 
$data->raw($row,$col,$sheet=0) 
```
If the cell has a hyperlink associated with it, the url can be retrieved.

```php 
$data->hyperlink($row,$col,$sheet=0) 
```
Rowspan/Colspan of the cell.

```php 
$data->rowspan($row,$col,$sheet=0) $data->colspan($row,$col,$sheet=0) 
```
# Formatting Details
The style method retrieves all available formatting information and returns a CSS string with all attributes.

```php 
$data->style($row,$col,$sheet=0) 
```
The format string for the cell.

```php 
$data->format($row,$col,$sheet=0) 
```
Cell alignment. Either 'right', 'center', or '' (left)

```php
$data->align($row,$col,$sheet=0) 
```
Background color, in #FFFFFF format.

```php 
$data->bgColor($row,$col,$sheet=0) 
```
Get border type for any of the cell's sides. Possible return values are:
```
Thin
Medium
Dashed
Dotted
Thick
Double
Hair
Medium dashed
Thin dash-dotted
Medium dash-dotted
Thin dash-dot-dotted
Medium dash-dot-dotted
Slanted medium dash-dotted
```

```php
$data->borderLeft($row,$col,$sheet=0)
$data->borderRight($row,$col,$sheet=0)
$data->borderTop($row,$col,$sheet=0)
$data->borderBottom($row,$col,$sheet=0)
```
Get the color of each of the borders, in #FFFFFF format.
```php
$data->borderLeftColor($row,$col,$sheet=0)
$data->borderRightColor($row,$col,$sheet=0)
$data->borderTopColor($row,$col,$sheet=0)
$data->borderBottomColor($row,$col,$sheet=0)
```
The font color, which may be determined either by cell properties or by format properties, in #FFFFFF format.

```php 
$data->color($row,$col,$sheet=0) 
```
# Other font properties:
```php
$data->bold($row,$col,$sheet=0) // Boolean
$data->italic($row,$col,$sheet=0) // Boolean
$data->underline($row,$col,$sheet=0) // Boolean
$data->height($row,$col,$sheet=0) // Number in pixels
$data->font($row,$col,$sheet=0) // Font name
```
