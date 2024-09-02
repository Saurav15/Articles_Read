-# Hashing
A hash function is a function that takes an input (or ‘message’) and returns a fixed-size string of bytes. The output, typically a number, is called the hash code or hash value. The main purpose of a hash function is to efficiently map data of arbitrary size to fixed-size values, which are often used as indexes in hash tables.

### Links to read it:
https://blog.algomaster.io/p/design-a-url-shortener?ref=dailydev
https://www.designgurus.io/blog/url-shortening




# Basic calculation explaination: 
## **1. Original String (Input Data)**
Let's say you start with a string:
```
"https://example.com/some/very/long/path"
```
- Characters in the string: Each character in this string is typically represented by 1 byte (8 bits) in ASCII encoding.
- Length in bytes: This string has 41 characters, so it’s 41 bytes (or 328 bits) long.

## **2. Hashing the String**
Next, you apply a hash function, like MD5, to the string.
- Hashing process: A hash function takes input data of any length and outputs a fixed-size string of bytes.
- MD5 Hash Output: MD5 always produces a 128-bit hash, regardless of the input size.
```
128 bits=16 bytes
```
For example, the MD5 hash of your string might look like this in ***hexadecimal***:
```
5d41402abc4b2a76b9719d911017c592
```
This is a 32-character hexadecimal string, but it's still 16 bytes because **each hex character represents 4 bits**.

## **3. Encoding the Hash**
- Base64 Encoding Process: Base64 encodes data using a set of 64 characters. Each Base64 character represents 6 bits because 2<sup>6</sup> = 64
    - **Converting bytes to Base64:**
        ```
        128 bits / 6 bits per Base64 character ~= 21.33 characters.
        ```
    - However, Base64 encoding rounds up to ensure the output is a multiple of 4 characters, adding padding (=) if necessary.
- Encoded String Length:
    - Without padding: The Base64 string would be 22 characters.
    - With padding: Often, you'll see = padding to make the output length a multiple of 4 characters, so the total would be 24 characters.

For example, the Base64 encoded version of the MD5 hash might look like this:
```
XUFAKrxLKna5cZ2REBfFkg==
```



### ***Flow Summary***
Let’s summarize the bit/byte transformations:
```
- Original String: 41 caracters → 328 bits (41 bytes).
- Hashing: Fixed 128 bits → 16 bytes.
- Base64 Encoding: Encodes 128 bits to 144 bits (due to padding) → 24 characters (18 bytes).
- Short Key: You extract 6 characters from Base64 (36 bits) → 4.5 bytes.
```