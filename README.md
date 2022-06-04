**Write a JavaScript function to get the successor of a string.**

*Note*: The successor is calculated by incrementing characters starting from the rightmost alphanumeric (or the rightmost character if there are no alphanumerics) in the string. Incrementing a digit always results in another digit, and incrementing a letter results in another letter of the same case. If the increment generates a carry, the character to the left of it is incremented. This process repeats until there is no carry, adding an additional character if necessary.

<!-- begin snippet: js hide: false console: true babel: false -->

<!-- language: lang-js -->

    console.log(successor("abcd"));     // "abce"
    console.log(successor("THX1138"));  // "THX1139"
    console.log(successor("<>"));       // "<>"
    console.log(successor("1999zzz"));  // "2000aaa"
    console.log(successor("ZZZ9999"));  // "AAAA0000"

    function successor(str) {
      if (str.charAt(str.length - 1).match(/[a-z]|[0-9]/i) === null)
        // if not digit or letter
        return str;
      var lastCharCode = str.charCodeAt(str.length - 1) + 1; // increment last character

      if (lastCharCode == 123 || lastCharCode == 91 || lastCharCode == 58) {
        var newStr = str.slice(0, str.length - 1);
        lastCharCode == 58 ? (lastCharCode -= 10) : (lastCharCode -= 26); // go back 26 if its Z or z, 10 if 0
        var lastChar = String.fromCharCode(lastCharCode);

        return newStr.length > 0
          ? successor(newStr) + lastChar
          : (lastChar == "0" ? "1" + lastChar : lastChar + lastChar);
      }
      // in case of first number is 9 : add 1 in first position
      return str.slice(0, str.length - 1) + String.fromCharCode(lastCharCode);
    }

<!-- end snippet -->

