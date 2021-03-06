# Cipher decoder ring:

## Live demo:

[Deployed  cipher decoder ring temp placeholder ](https://vercel.app/)  

## Application summary:

A two-way cipher encoding/decoding app for three different ciphers (Caesar, Polybius, and Substitution), as well as accompanying self-implemented test cases for each of the ciphers using Mocha and Chai. Each function takes in a string that satisfies a specific set of criteria and returns an encoded or decoded string based on the user's selection.

## Screenshots:

![Application screenshot](https://raw.githubusercontent.com/Thinkful-Ed/project-decoder-ring/master/docs/home.png)

## Tech stack:

This application was created using JavaScript, BootStrap, HTML, CSS, Mocha, and Chai.

## Caesar Shift:

![Caesar shift](https://github.com/Thinkful-Ed/project-decoder-ring/blob/master/docs/caesar.png?raw=true)

The Caesar Shift is a type of substitution cipher originally used by Julius Caesar to protect messages of military significance. It relies on taking the alphabet and "shifting" letters to the right or left, based on the typical alphabetic order.

For example, if you were to "shift" the alphabet to the right by 3, the letter "A" would become "D".

#### caesar()

The `caesar()` function in the `src/caesar.js` file has three parameters:

- _input_ is a string that refers to the inputted text to be encoded or decoded.
- _shift_ is an integer refers to how much each letter is "shifted" by. A positive number means shifting to the right (i.e. "A" becomes "D") whereas a negative number means shifting to the left (i.e. "M" becomes "K"). If there is no _shift_ value, the function will return `false`.
- _encode_ is a boolean that refers to whether you should encode or decode the message. By default, it is set to `true`. Encoding is case-insensitive (e.g., both "a" or "A" would be encoded to the same result).

The following should also hold true:

- If a letter is shifted so that it goes "off" the alphabet (e.g. a shift of 3 on the letter "z"), it will wrap around to the front of the alphabet (e.g. "z" becomes "c").
- Spaces, as well as other non-alphabetic symbols, will be maintained before and after encoding or decoding.

#### Examples

```js
caesar("thinkful", 3); //> 'wklqnixo'
caesar("thinkful", -3); //> 'qefkhcri'
caesar("wklqnixo", 3, false); //> 'thinkful'

caesar("This is a secret message!", 8); //> 'bpqa qa i amkzmb umaaiom!'
caesar("BPQA qa I amkzmb umaaiom!", 8, false); //> 'this is a secret message!'

caesar("thinkful"); //> false
caesar("thinkful", 99); //> false
caesar("thinkful", -26); //> false
```

## Polybius Square:

|       | **1** | **2** | **3** | **4** | **5** |
| ----- | ----- | ----- | ----- | ----- | ----- |
| **1** | A     | B     | C     | D     | E     |
| **2** | F     | G     | H     | I/J   | K     |
| **3** | L     | M     | N     | O     | P     |
| **4** | Q     | R     | S     | T     | U     |
| **5** | V     | W     | X     | Y     | Z     |

The Polybius Square is a cipher that is achieved by arranging a typical alphabet into a grid. Each letter is represented through a coordinate.

In this app, the grid will be arranged as above and coordinates will be read by comparing the first digit to the number on the top of the table and the second digit to that on the left. For example, in the above table, the letter "B" would be represented by the numerical pair "21".

```
"thinkful" -> "4432423352125413"
```

When decoding the message, each pair of numbers is translated using the coordinates.

### polybius()

The `polybius()` function in the `src/polybius.js` file has two parameters:

- _input_ is a string that refers to the inputted text to be encoded or decoded. The input may only contain spaces and letters.
- _encode_ is a boolean that refers to whether you should encode or decode the message. By default it is set to `true`. Encoding is case-insensitive (e.g., both "a" or "A" would be encoded to the same result).

The following should also hold true:

- When decoding, the number of characters in the string _excluding spaces_ should be even. Otherwise, the function will return `false`.
- Spaces in the message will be maintained before and after encoding or decoding.
- The letters "I" and "J" share a space. When encoding, both letters can be converted to `42`, but when decoding, both letters will be shown as `"(i/j)"`.

#### Examples

```js
polybius("thinkful"); //> "4432423352125413"
polybius("Hello world"); //> '3251131343 2543241341'

polybius("3251131343 2543241341", false); //> "hello world"
polybius("4432423352125413", false); //> "th(i/j)nkful
polybius("44324233521254134", false); //> false
```

## Substitution Cipher:

![Substitution cipher](https://github.com/Thinkful-Ed/project-decoder-ring/blob/master/docs/substitution.jpeg?raw=true)

The Substitution Cipher requires a standard alphabet and a substitution alphabet. Letters from the standard alphabet will be transposed to the standard alphabet. This cipher requires that the recipient have the substitution alphabet; otherwise, it will be difficult for them to decode the message.

For example, in the image above, the word "HELLO" would be translated as follows:

- "H" becomes "R".
- "E" becomes "M".
- "L" becomes "W".
- "O" becomes "L".

This would result in the code "RMWWL". To decrypt this code, you would simply take the result and transpose back from the substitution alphabet to the standard alphabet.

### substitution()

The `substitution()` function in the `src/substitution.js` file has three parameters:

- _input_ is a string that refers to the inputted text to be encoded or decoded; only letters and spaces may be included.
- _alphabet_ is a string that refers to substitution alphabet.
- _encode_ is a boolean that refers to whether you should encode or decode the message. By default, it is set to `true`.

The following should also hold true:

- Spaces in the message should be maintained before and after encoding or decoding.
- Encoding/decoding is case-insensitive (e.g., both "a" or "A" would be encoded to the same result).
- The `alphabet` parameter must be a string of exactly 26 characters. Otherwise, it will return `false`.
- All of the characters in the `alphabet` parameter _must be unique._ Otherwise, it will return `false`.

#### Examples

```js
substitution("thinkful", "xoyqmcgrukswaflnthdjpzibev"); //> 'jrufscpw'
substitution("You are an excellent spy", "xoyqmcgrukswaflnthdjpzibev"); //> 'elp xhm xf mbymwwmfj dne'
substitution("jrufscpw", "xoyqmcgrukswaflnthdjpzibev", false); //> 'thinkful'

substitution("thinkful", "short"); //> false
substitution("thinkful", "abcabcabcabcabcabcabcabcyz"); //> false
```

## Installation:

- Run `npm install` to install the dependencies needed for this project.

To run the tests, you can run the following command:

```bash
npm test
```

To watch how the code you write affects the application website, you can run the following command, which will start a server and take over your terminal window:

```bash
npm start
```

To stop the server and regain control of your terminal, you can press `Ctrl + C`.

