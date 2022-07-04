Struct

Represents a character as a UTF-16 code unit.

A `string` is logically a sequence of `16-bit` values, each of which is an instance of the `char` struct. The `string.Length` property returns the number of `char` instances in the string instance.

Each character is represented by a single char value. That pattern holds true for most of the world's languages.

However, for some languages and for some symbols and emoji, it takes two char instances to represent a single character.

    void PrintChars(string s)
    {
        Console.WriteLine($"\"{s}\".Length = {s.Length}");
        for (int i = 0; i < s.Length; i++)
        {
            Console.WriteLine($"s[{i}] = '{s[i]}' ('\\u{(int)s[i]:x4}')");
        }
        Console.WriteLine();
    }

    PrintChars("🐂");

    // output:
    // "🐂".Length = 2
    // s[0] = '�' ('\ud83d')
    // s[1] = '�' ('\udc02')

The char pairs that map to a single character are called *surrogate* pairs. To understand how they work, you need to understand Unicode and UTF-16 encoding.

## Unicode code points

Unicode is an international encoding standard for use on various platforms and with various languages and scripts.

The Unicode Standard defines over 1.1 million code points. A code point is an integer value that can range from 0 to U+10FFFF (decimal 1,114,111).

Within the full range of code points there are two subranges:

* The **Basic Multilingual Plane (BMP)** in the range U+0000..U+FFFF. This 16-bit range provides 65,536 code points, enough to cover the majority of the world's writing systems.
* **Supplementary code points** in the range U+10000..U+10FFFF. This 21-bit range provides more than a million additional code points that can be used for less well-known languages and other purposes such as emojis.


## UTF-16 code units
16-bit Unicode Transformation Format (UTF-16) is a character encoding system that uses 16-bit code units to represent Unicode code points. .NET uses UTF-16 to encode the text in a string. A char instance represents a 16-bit code unit.

A single 16-bit code unit can represent any code point in the 16-bit range of the Basic Multilingual Plane. But for a code point in the supplementary range, two char instances are needed.

> [character-encoding-introduction](https://docs.microsoft.com/en-us/dotnet/standard/base-types/character-encoding-introduction)

