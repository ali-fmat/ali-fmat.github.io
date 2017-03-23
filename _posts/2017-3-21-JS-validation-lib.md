---
layout: post
title: Javascript(ES5) validation library
---
Estas son algunas funciones, que podrían ser de utilidad para aquellos que desarrollan con Javascript y requieren de hacer validaciones en determinados lugares de sus proyectos.

#### isObjectStrict
```javascript
function isStrictObject(value){
  // fuente: https://www.toptal.com/javascript/interview-questions
  return (value !== null) && (typeof(value) === 'object') && (toString.call(value) !== '[object Array]');
}
```

#### iObject
```javascript
function isObject(value){
  return (value !== null) && (typeof(value) === 'object');
}
```

#### isString
```javascript
function isString(value){
  return typeof(value) === 'string';
}
```

#### isFunction
```javascript
function isFunction(value){
  return typeof(value) === 'function';
}
```

#### isBoolean
```javascript
function isBoolean(value){
  return typeof(value) === 'boolean';
}
```

#### existPropertyInObject
