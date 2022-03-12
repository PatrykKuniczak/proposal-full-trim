## Status
This proposal is a [stage-0 proposal](https://github.com/tc39/proposals/blob/master/stage-0-proposals.md) and waiting for feedback.

## Motivation

We often need to have full validation, i on my last project create this "fullTrim" function for have 100% confident to have good looking records in DB, and when i fetch it in frontend i have good looking description/tilte etc.

This issue is with us from many years, here i have link to Stack Over Flow from 12 years ago:
[Remove blankspaces](https://stackoverflow.com/questions/1981349/regex-to-replace-multiple-spaces-with-a-single-space)


## Use cases


```ts
String.prototype.fullTrim = function () {
    return this.replace(/\s\s+/g, ' ').trim();
}
```

Here is a example where i use it, user clicking too much blank spaces and i trimming it

```ts
console.log("   To    Much     Space    Between   ".fullTrim());
```

The output: "To Much Space Between"


## Description

We don't need any more use regex and replace manual for do this, fullTrim function do it for us 
