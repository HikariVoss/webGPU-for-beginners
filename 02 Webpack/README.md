# WebGPU for Beginners 02: Webpack

## First make a fairly complex webapp

First make the html file, which contains and input, a submit button and div for the ouputs, then make the main.js script. After making the main script which contains all the functions, split it into several scripts. This doesn't really make sense to do which such a simple app however later in the tutorial we will be making very large apps, where it does make a lot of sense to split them up into multiple files, which is where webpack comes in. Webpack is a opensource javascript module bundler, which packs many modules into a few bundled assets.

<details>
<summary>code</summary>

### naive implementation
```js
const hex_lookup = [
    "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "a", "b", "c", "d", "e", "f"
];

function dec_to_binary(number) {
    var digits = [];

    while (number > 0) {
        var digit = String(number % 2);
        number = (number - (number % 2))/ 2;
        digits.push(digit);
    }

    return digits.reverse().join("");
}

function group_binary(number) {
    var digits = [];

    const number_split = number.split("").reverse();
    var group_count = (number_split.length - (number_split.length % 4)) / 4 + 1;
    if (number_split.length % 4 == 0) {
        group_count -= 1;
    }

    var group = []

    for (let i = 0; i < number_split.length; i++) {
        group.push(number_split[i]);
        if (group.length == 4) {
            digits.push(group.reverse().join(""));
            group = [];
        }
    }

    for (let i = number_split.length; i < 4 * group_count; i++) {
        group.push("0");
        if (group.length == 4) {
            digits.push(group.reverse().join(""));
            group = [];
        }
    }

    return digits.reverse();
}

function binary_to_hex(number) {
    var result = 0;

    for (let i = 0; i < 4; i++) {
        result += Number(number[i]) * 2**(3 - i);
    }

    return result;
}

const decimal_input = document.getElementById("decimalInput");
const conversion_button = document.getElementById("convert-button");
const binary_step = document.getElementById("binary-raw");
const grouped_binary_step = document.getElementById("binary-grouped");
const grouped_hex_step = document.getElementById("hexadecimal-grouped");
const hex_output = document.getElementById("hexadecimal");

const click = () => {

    binary = dec_to_binary(Number(decimal_input.value));
    binary_step.innerText = "binary: " + binary;
    
    tempStr = "grouped: ";
    grouped_binary = group_binary(binary);
    for (let i = 0; i < grouped_binary.length; i++) {
        tempStr += grouped_binary[i] + " ";
    }
    grouped_binary_step.innerText = tempStr;

    tempStr = "hex (grouped): ";
    for (let i = 0; i < grouped_binary.length; i++) {
        tempStr += String(binary_to_hex(grouped_binary[i])) + " ";
    }
    grouped_hex_step.innerText = tempStr;

    tempStr = "final: 0x";
    for (let i = 0; i < grouped_binary.length; i++) {
        tempStr += String(hex_lookup[binary_to_hex(grouped_binary[i])]);
    }
    hex_output.innerText = tempStr;
}

conversion_button.addEventListener("click", click);
```

</details>

After splitting the main.js file into the seperate files we can get to using Webpack

## Learning how to use Webpack

Following the same process as for 01 of this series, initialise npm. 
After that do the following:
1. run `npm i webpack webpack-cli`
2. add `"build": "webpack --config webpack.config.js"` in `"scripts"`
3. in the root folder make a `webpack.config.js` file
Inside the `webpack.config.js` file:
```js
const path = require("path")
module.exports = {
    entry: "./src/hex-verter/main.js",
    output: {
        filename: "main.js",
        path: path.resolve(__dirname, "dist")
    }
}
```
I spent a while trying to get this too work, turns out I forgot quotations around path in `const path = require("path")`