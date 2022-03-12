## Status

This proposal is a [stage-0 proposal](https://github.com/tc39/proposals/blob/master/stage-0-proposals.md) and waiting for feedback.


## Motivation

We often need to have full validation, i'm on my last project create this "fullTrim" function because i have 100% confidence to have good looking records in DB, and when i fetch it on frontend, i have good looking description/tilte etc.

This issue is with us from many years, here i have link to Stack Over Flow from 12 years ago: 
[Remove blankspace](https://stackoverflow.com/questions/1981349/regex-to-replace-multiple-spaces-with-a-single-space)


## Use cases

This function remove multiple blankspaces from string and replace it with 1 space, and trimming whole string after replacing, for remove spaces from end and start.

```ts
String.prototype.fullTrim = function () {
    return this.replace(/ +/g, ' ').trim();
}

interface String {
    fullTrim(): string
}
```

Here is a example where i use it, user making too much blank spaces and i trimming it

```ts
console.log("   To    Much     Space    Between   ".fullTrim());
```

The output:

```js
"To Much Space Between"
```


### Performance

```js
str.replace( /  +/g, ' ' )       ->  380ms  // I use this
str.replace( /\s\s+/g, ' ' )     ->  390ms
str.replace( / {2,}/g, ' ' )     ->  470ms
str.replace( / +/g, ' ' )        ->  790ms
str.replace( / +(?= )/g, ' ')    -> 3250ms
```

This test's is not from my own, i have this from this "Remove blankspaces" link from above.


## Description

We don't need any more use regex and replace manual for do this, fullTrim function do it for us.

When we need to set a min and max lenght of string we can fullTrim it, sometimes user need save on DB longer text and this blankspace it's a garbage, max limit is 500, user type 502 and make 3 blankspace from mistake and here fullTrim can help.

Second issue is: Users type good looking text for human not for computer, the usless blankspaces on DB can be trimmed and save space on DB, when user try to watch this later, developer can fetch this from DB and reformat for good looking again, that's the reason why we deploying our apps, usless blankspace is trimmed and computer reading code well, but developer have good looking code on his IDE.

If this idea is good, we can extend this with optional argument, which can work like this:
[Trim Characters](https://github.com/Kingwl/proposal-string-trim-characters)


## Comparison

Other popular languages don't have it, but i watching on Stack for Java, Js, Python and the question is similar "How to remove multiple spaces", this means many people have this issue when coding.
