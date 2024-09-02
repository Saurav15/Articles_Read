# Base62 Encoding in JavaScript

## ***What are Encoders?***
Encoders are tools or algorithms that convert data from one format to another.
Base62 encoding converts binary data (like a string or a number) into a set of 62 alphanumeric characters. The character set includes:

* 10 digits: 0-9
* 26 uppercase letters: A-Z
* 26 lowercase letters: a-z

Encoders are essential when you need to transform data into a format that is compatible with systems that might not accept raw or binary data. Here’s how you can explain it:
- Compatibility: Many systems, including databases, URLs, and APIs, expect data to be in a specific text format. For example, binary data (like images, files, or complex data structures) cannot be directly inserted into a URL or passed in a simple text field. Encoders convert this data into a format that fits within these constraints.
- URL-safe: Base62 strings do not contain special characters like +, /, or = found in Base64, making them suitable for URLs.

### **Example Scenario**
- Imagine you are building a web application where users upload images, and those images need to be stored in a database. Directly sending the binary data of the image through an HTTP request might not be feasible because HTTP is text-based, and binary data could be corrupted or misinterpreted. By encoding the image data into a text format (like Base64), you ensure that the data is safely transmitted to the server, where it can then be decoded and processed or stored.


## ***How Base62 Encoding Works ?***
**Step 1: Convert the Input to a Number**
- If the input is a string, convert it into its binary or numerical representation.
- **Example**: *12345*

**Step 2: Repeated Division by 62**
- Divide the number by 62, and keep track of the remainder.
- The remainder corresponds to a character in the Base62 character set.
- Continue dividing the quotient by 62 until the quotient is zero.
```
1. Divide 12345 by 62
    - 12345 ÷ 62 = 199 (quotient), remainder = 7
    - The remainder 7 maps to the character '7' in Base62.
2. Divide 199 by 62:
    - 199 ÷ 62 = 3 (quotient), remainder = 13.
    - The remainder 13 maps to the character 'D' in Base62.
3. Divide 3 by 62:
    - 3 ÷ 62 = 0 (quotient), remainder = 3
    - The remainder 3 maps to the character '3' in Base62
```

**Step 3: Map Remainders to Characters**
- Each remainder is mapped to the corresponding Base62 character (0-61 maps to 0-9, A-Z, a-z).
```
 Result: The Base62-encoded string is read in reverse order of remainders, so the result is '3D7'.
```


## ***How Base62 Decoding Works ?***
**Step 1: Convert characters to numbers:**
Base62-encoded string: '3D7.
- '3' -> 3
- 'D' -> 13
- '7' -> 7

**Step 2: Convert characters to numbers:**
- 3×62<sup>2</sup>  + 13×62<sup>1</sup>  + 7×62<sup>0</sup>
- 3×3844+13×62+7 = 11532+806+7 = 12345

So, the original number was 12345.