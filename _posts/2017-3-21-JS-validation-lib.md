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
```javascript
/**
* validates if a given property<string> is defined in a given object or not
* @param property <string or array[string]>
* @param obj <object>
*
* sample:
* var obj = { user: { value: { algo: { nuevo: { ala: 'wiii' } } } } };
* console.log('should be true obj >>> ', existPropertyInObject('user.value.algo.nuevo.ala', obj));
* console.log('should be false obj >>> ', existPropertyInObject('user.valu.algo.nuevo.ala', obj));
*/
function existPropertyInObject(property, obj){
    var isArray_prop = Array.isArray(property), prop, f_prop;

    if(!isString(property) && /* property es string ? */
        !isArray_prop || /* property es array ? */
        !isStrictObject(obj)){ /* obj es object ? */
        return false;
    }

    if(!isArray_prop){ /* property no es array ? */
        if(property.trim().length > 0){ /* property es string y tiene longitud mayor que cero ? */
            prop = property.trim().split('.');
        } else {
            return false;
        }
    } else {
        if(property.length > 0){
            prop = property;
        } else {
            return false;
        }
    }

    f_prop = prop.shift();

    if(obj[f_prop]){ /* property is defined in object ? */
      if(prop.length === 0){ /* no more items in prop ? */
        return true;
      } else {
        return existPropertyInObject(prop, obj[f_prop]);
      }
    } else {
      return false;
    }
}
```
