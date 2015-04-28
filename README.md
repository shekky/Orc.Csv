Orc.CsvHelper
=================

[![Join the chat at https://gitter.im/WildGums/Orc.CsvHelper](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/WildGums/Orc.CsvHelper?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Small library of extensions and helper methods for the [CsvHelper](http://joshclose.github.io/CsvHelper) library.

- Static methods are provided to read or write to a csv file with one line of code.
- Sensible configuration options are provided out of the box (but can be overwritten if needed).
- Reading from a csv file will not lock it.
- Capture a meaningful error message when an exception is thrown while reading a csv file. 

Features
----------

- **Code generation** => Use static class *CodeGeneration* for generating C# POCO classes and their associated maps.

```C#
	/// <summary>
    /// Create CSharp files to consume CSV files.
    /// A standard POCO cs file as well as the CsvHelper Mapping cs file will be created.
    /// All properties in the POCO will be of type string. So please update accordingly.
    /// </summary>
    public static class CodeGeneration
    {
        public static void CreateCSharpFilesForAllCsvFiles(string inputFoler, string namespaceName, string outputFolder)
        {
            var csvFiles = GetCsvFiles(inputFoler);

            foreach (var csvFile in csvFiles)
            {
                CreateCSharpFiles(csvFile, namespaceName, outputFolder);
            }
        }
		...
	}
```

- **CsvReader helper** => Use static class *CsvReaderHelper* for reading csv files with a single line of code.

```C#
public static IEnumerable<T> ReadCsv<T>(string csvFilePath, Action<T> initializer = null, Type mapType = null, CsvConfiguration csvConfiguration = null, bool throwOnError = false)

or

public static IEnumerable<T> ReadCsv<T>(string csvFilePath, CsvClassMap map, Action<T> initializer = null, CsvConfiguration csvConfiguration = null, bool throwOnError = false)
```

Example:
```C#
var records = CsvWriterHelper.ReadCsv<MyClass>(scvFilePath, MyClassMap);
```

- **CsvWriter helper** => Use static class *CsvWriterHelper* for writing records into a csv file.

```C#
public static void WriteCsv<TRecord, TMap>(IEnumerable<TRecord> records, string csvFilePath, CsvConfiguration csvConfiguration = null, bool throwOnError = false)
```

- **CsvExtensions** => for writing object collections into a csv file using the *ToCsv()* method.

```C#
public static void ToCsv<TRecord>(this IEnumerable<TRecord> records, string csvFilePath, Type csvMap = null, CsvConfiguration csvConfiguration = null, bool throwOnError = false)
```

Example

```C#
records.ToCsv<MyClass>(csvFilePath, typeof(MyClassMap));

```
