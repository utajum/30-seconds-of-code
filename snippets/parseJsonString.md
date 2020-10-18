---
title: parseJsonString
tags: array,json,object,string,intermediate
---

`JSON.parse` throws a `SyntaxError` if the string to parse is not a valid JSON.

- We create a utility function `parseJsonString` that we use instead of JSON.parse.
- We use `try...catch` in the function body.
- If parsing is successful `parseJsonString` returns the parsed data.
- If parsing is successful but the value is falsy `parseJsonString` returns `defaultReturnVal` (`false` and `null` can be parsed even though they are not strings).
- If parsing is unsuccessful `parseJsonString` returns `defaultReturnVal`

```js
const parseJsonString = (dataToParse, defaultReturnVal) => {
  try {
    return JSON.parse(dataToParse) || defaultReturnVal;
  } catch (error) {
    return defaultReturnVal;
  }
};
```

```js
parseJsonString('{"foo":"bar"}', {}); // {foo:"bar"}
parseJsonString('{"broken json string', {}); // {}
parseJsonString("", {}); // {}
parseJsonString("", null); // null
parseJsonString("[1,2,3]", []); // [1,2,3]
```

It can be shortened even more like so

```js
const parsedJsonData = (() => {
  try {
    return JSON.parse('{"foo":"bar"}') || {};
  } catch (error) {
    return {};
  }
})();

console.log(parsedJsonData); // {foo:"bar"}
```
