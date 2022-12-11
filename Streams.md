---
Tags: completed ead lec3
---
Links: [[EAD|HomePage]]
# Streams
`C#`  stream classes are standard IO (Input/Output) classes to read/write from different sources like files, memory, network, isolated storage, etc.
`System.IO.Stream` is an abstract class for transfering bytes from different sources. It is base class for all other class that reads\writes bytes to different sources.
`FileStream` class provides reading and writing functionality of bytes to physical file.
Reader & writer classes provides functionality to read bytes from Stream classes (`FileStream`, `MemoryStream` etc) and converts bytes into appropriate encoding.
`StreamReader` provides a helper method to read string from FileStream by converting bytes into strings. `StreamWriter` provides a helper method to write string to FileStream by converting strings into bytes.


![[ead-Streams]]

## FileAccess Enum
Defines constants for read, write, or read/write access to a file. This enumeration supports a bitwise combination of its member values.

| Field     | Value | Function                                                                                             |
| --------- | ----- | ---------------------------------------------------------------------------------------------------- |
| Read      | 1     | Read access to the file. Data can be read from the file. Combine with `Write` for read/write access. |
| ReadWrite | 2     | Read and write access to the file. Data can be written to and read from the file.                    |
| Write     | 3     | Write access to the file. Data can be written to the file. Combine with `Read` for read/write access.                                                                                                   | Write access to the file. Data can be written to the file. Combine with `Read` for read/write access.



## FileMode Enum
A `FileMode` parameter is specified in many of the constructors for `FileStream`, `IsolatedStorageFileStream`, and in the Open methods of `File` and `FileInfo` to control how a file is opened. `FileMode` parameters control whether a file is overwritten, created, opened, or some combination thereof. Use `Open` to open an existing file. To append to a file, use `Append`. To truncate a file or create a file if it doesn't exist, use `Create`.

| Field        | Value | Function                                                                                                                                                                                                                                                                                                                                                                        |
| ------------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CreateNew    | 1     | Specifies that the operating system should create a new file. This requires Write permission. If the file already exists, an `IOException` exception is thrown.                                                                                                                                                                                                                 |
| Create       | 2     | Specifies that the operating system should create a new file. If the file already exists, it will be overwritten. This requires Write permission. `FileMode.Create` is equivalent to requesting that if the file does not exist, use `CreateNew`; otherwise, use `Truncate`. If the file already exists but is a hidden file, an `UnauthorizedAccessException` exception is thrown. |
| Open         | 3     | Specifies that the operating system should open an existing file. The ability to open the file is dependent on the value specified by the `FileAccess` enumeration. A `FileNotFoundException` exception is thrown if the file does not exist.                                                                                                                                   |
| OpenOrCreate | 4     | Specifies that the operating system should open a file if it exists; otherwise, a new file should be created. If the file is opened with `FileAccess.Read`, Read permission is required. If the file access is `FileAccess.Write`, Write permission is required. If the file is opened with `FileAccess`.`ReadWrite`, both Read and Write permissions are required.             |
| Truncate     | 5     | Specifies that the operating system should open an existing file. When the file is opened, it should be truncated so that its size is zero bytes. This requires Write permission. Attempts to read from a file opened with `FileMode.Truncate` cause an `ArgumentException` exception.                                                                                          |
| Append       | 6     | Opens the file if it exists and seeks to the end of the file, or creates a new file. This requires Append permission. `FileMode.Append` can be used only in conjunction with `FileAccess.Write`. Trying to seek to a position before the end of the file throws an `IOException` exception, and any attempt to read fails and throws a `NotSupportedException` exception.                                                                                                                                                                                                                                                                                                                                                                                |


## Writing a Byte To a File
```cs
using System.IO;

class MyClass
{
	static void Main()
	{
		FileStream fout = new FileStream("out.txt", FileMode.Create);
		fout.WriteByte((byte)'A');
		fout.Close();
	}
}
```

## Reading a Byte from a File
```cs
using System.IO;

class MyClass
{
	static void Main()
	{
		FileStream fin = new FileStream("input.txt", FileMode.Open);
		int ch = fin.ReadByte();
		System.Console.Write((char) ch);
		fin.Close();
	}
}
```

## Copy File
```cs
using System.IO;

class MyClass
{
    static void Main()
    {
        FileStream fin = new FileStream("in.txt", FileMode.Open);
        FileStream fout = new FileStream("out.txt", FileMode.Create);
        int ch;

        while ((ch = fin.ReadByte()) != -1)
        {
            fout.WriteByte((byte) ch);
        }
        fin.Close();
        fout.Close();
    }
}
```

## IO using Character Based Stream/Wrapper Class
```cs
using System.IO;

class MyClass
{
    static void Main()
    {
        FileStream fin = new FileStream("in.txt", FileMode.Open);
        FileStream fout = new FileStream("out.txt", FileMode.Create);
		StreamWriter sw = new StreamWriter(fout);
		string data = "Hey How you doing?";
		sw.WriteLine(data);

		StreamReader sr = new StreamReader(fin);
		data = sr.ReadLine();
		System.Console.WriteLine(data);

		
        sw.Close();
        sr.Close();
    }
}
```


```ad-info
They Provide abstraction to facilitate data transfer from and to computer to and from difference devices using same Programming interface without having to worry about underlying hardware.
```


# To Dos
- [x] To Read on different FileMode.types and FileAccess.types
- [x] Some Employee Assignment thing
---

> It is impossible to experience one's death objectively and still carry a tune.
> — <cite>Woody Allen</cite>
---

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: WordCloud

#-----------------#
#- chart data    -#
#-----------------#
data: "wordcount:ead_lecture3"

#-----------------#
#- chart options -#
#-----------------#
options:
  wordField: "word"
  weightField: "count"
  colorField: "count"
  wordStyle:
    rotation: 30
```

Created: 2022-10-25