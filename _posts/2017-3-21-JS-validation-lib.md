---
layout: post
title: Javascript(ES5) validation library
---
Estas son algunas funciones, que podrían ser de utilidad para aquellos que desarrollan con Javascript y requieren de hacer validaciones en determinados lugares de sus proyectos.

#### isDefined
```javascript
function isDefined(value){
  if(value === null || value === undefined){
    return false;
  }
  
  return true;
}
```

#### iObject
```javascript
function isObject(value){
  return isDefined(value) && (typeof(value) === 'object');
}
```

#### isObjectStrict
```javascript
function isStrictObject(value){
  // fuente: https://www.toptal.com/javascript/interview-questions
  return isObject(value) && (toString.call(value) !== '[object Array]');
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

#### isEmpty
```javascript
function isEmpty(value){
  var index, item;

  if(isObject(value)){
    for(index in value){
      item = value[index];
      if(isDefined(item)){
        return false;
      }
    }
    
    return true;
  }

  if(isString(value)){
    return value.trim().length === 0;
  }

  return !isDefined(value);
}
```

#### existPropertyInObject
```javascript
/**
* validates if a given property<string> is defined in a given object or not
* @param property <string>
* @param obj <object>
*
* sample:
* var obj = { test: { test: { test: { test: { test: 'test' } } } } };
* console.log('should be true obj >>> ', existPropertyInObject('test.test.test.test.test', obj));
* console.log('should be false obj >>> ', existPropertyInObject('test.tests.test.test.test', obj));
*/
function existPropertyInObject(property, obj){
  var prop, index, c_prop, o_prop;
  
  if(!isString(property) || /* property es string ? */
     !isObject(obj)){ /* obj es object ? */
    return false;
  }
  
  if(isEmpty(property) || isEmpty(obj)){
    return false;
  }

  prop = property.trim().split('.');
  o_prop = obj;
  
  for(index in prop){
    c_prop = prop[index];
    o_prop = o_prop[c_prop];
    
    if(!isDefined(o_prop)){
      return false;
    }
  }
  return true;
}
```

Tests done for this method:
var obj = { test: { test: { test: { test: { test: undefined } } } } };

console.log('(null,null) should be false', existPropertyInObject(null, null));
console.log('() should be false', existPropertyInObject());
console.log('(undefined,null) should be false', existPropertyInObject(undefined, null));
console.log('(null,undefined) should be false', existPropertyInObject(null, undefined));
console.log('("",undefined) should be false', existPropertyInObject('', undefined));
console.log('("","") should be false', existPropertyInObject('', ''));
console.log('({},undefined) should be false', existPropertyInObject({}, undefined));
console.log('({},{}) should be false', existPropertyInObject({}, {}));
console.log('(1,{}) should be false', existPropertyInObject(1, {}));
console.log('("",{}) should be false', existPropertyInObject('', {}));
console.log('("test",{}) should be false', existPropertyInObject('test', {}));
console.log('("",obj) should be false', existPropertyInObject('', obj));
console.log('("test",obj) should be true', exist('test', obj));
console.log('("test.test",obj) should be true', exist('test.test', obj));
console.log('("test.test.test",obj) should be true', exist('test.test.test', obj));
console.log('("test.test.test.test",obj) should be true', exist('test.test.test.test', obj));
console.log('("test.test.test.test.test",obj) should be false', exist('test.test.test.test.test', obj));
console.log('("test.test.test.test.tests",obj) should be true', exist('test.test.test.test.tests', obj));
console.log('("test.test.test.test.tests",obj) should be true', exist('test.test.test.test.tests', obj));
console.log('("test.test.test.tests.tests",obj) should be false', exist('test.test.test.tests.tests', obj));
console.log('("test.test.tests.test.tests",obj) should be false', exist('test.test.tests.test.tests', obj));
console.log('("test.tests.test.test.tests",obj) should be false', exist('test.tests.test.test.tests', obj));
console.log('("tests.test.test.test.tests",obj) should be false', exist('tests.test.test.test.tests', obj));
