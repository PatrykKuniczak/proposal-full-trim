## Status

This proposal is a [stage-0 proposal](https://github.com/tc39/proposals/blob/master/stage-0-proposals.md) and waiting for feedback.

## Motivation

We often need to have full validation, i on my last project create this "fullTrim" function for have 100% confident to have good looking records in DB, and when i fetch it in frontend i have good looking description/tilte etc.

This issue is with us from many years, here i have link to Stack Over Flow from 12 years ago:
<a href="https://stackoverflow.com/questions/1981349/regex-to-replace-multiple-spaces-with-a-single-space" target="_blank">Remove blankspaces</a>

## Use cases

This function remove multiple blankspaces from string and replace it with 1 space, and 1 was trimming whole string after replacing, for remove spaces from end and start.

```ts
String.prototype.fullTrim = function () {
    return this.replace(/ +/g, ' ').trim();
}

interface String {
    fullTrim(): string
}
```

Here is a example where i use it, user clicking too much blank spaces and i trimming it

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

When we need to set a min and max lenght of string we can fullTrim it and maybe user can save on DB or something longer text then type on form or other input, because users type good looking text for human not for computer, the usless blankspaces on DB can be trimmed and when user try to watch this later, developer can fetch this from DB and reformat for good looking again, but saving space in DB, that's what we deploying our apps, usless blankspace is trimmed and computer reading code well, but developer have good looking code on his IDE.

If this idea is good, we can extend this with optional argument, which can work like this:
<a href="https://github.com/Kingwl/proposal-string-trim-characters" target="_blank">Trim Characters</a> but for whole word.

## Comparison

Other popular languages don't have it, but i watching on Stack for Java, Js, Python the similar question is the same "How to remove multiple spaces", this means many people have this issue when coding.
