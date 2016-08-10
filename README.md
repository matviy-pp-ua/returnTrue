# returnTrue

## Reflexive

```js
function reflexive(x) {
    return x != x;
}

reflexive(NaN)
```

## Transitive
```js
function transitive(x,y,z) {
    return x && x == y && y == z && x != z;
}

transitive([],0,[]) 
```

## Counter
```js
function counter(f) {
    var a = f(), b = f();
    return a() == 1 && a() == 2 && a() == 3
        && b() == 1 && b() == 2;
}

counter((x=1)=>$=>x++)
counter(x=>$=>x=-~x)   // -2 symbols
```

## Peano

`chrome 54`

```js
function peano(x) {
    return (x++ !== x) && (x++ === x);
}

peano(2**53-1)
```

## Array
```js
function array(x,y) {
    return Array.isArray(x) && !(x instanceof Array) &&
          !Array.isArray(y) &&  (y instanceof Array);
}

array(a=Array.prototype,{__proto__:a}) 
array((Array.isArray=x=>x[0],'1'),[])
```

## Instance
```js
function instance(x,y) {
  return x instanceof y && y instanceof x && x !== y;
}

instance(Object,Function)
```

## Proto1
```js
function proto1(x) {
    return x && !("__proto__" in x);
}

proto1(Object.create(null))
proto1({__proto__:null})
```

## Undef
```js
function undef(x) {
    return !{ undefined: { undefined: 1 } }[typeof x][x];
}

undef((Object.prototype['number']=0,0))
```

## Symmetric
```js
function symmetric(x,y) {
    return x == y && y != x;
}

symmetric(1,{valueOf:$=>n=-~this.n})
symmetric(n=1,{valueOf:$=>n++})
```

## Ouroborobj
```js
function ouroborobj(x) {
    return x in x;
}

ouroborobj([0])
```


## Truth
```js
function truth(x) {
    return x.valueOf() && !x;
}

truth((Number.prototype.valueOf=$=>1,0))
```

## Wat
```js
function wat(x) {
    return x('hello') == 'world:)' && !x;
}

▶ wat(????)
```

## Evil1
```js
var eval = window.eval;
function evil1(x) {
    return eval(x+'(x)') && !eval(x)(x);
}

▶ evil1(????)
```

## Evil2
```js
var eval = window.eval;
function evil2(x) {
    return eval('('+x+')(x)') && !eval(x)(x);
}

▶ evil2(????)
```

## Random1
```js
function random1(x) {
    return Math.random() in x;
}

random1((Math.random=$=>0,[0]))
random1(Math.random=$=>'call')
```

## Random2
```js
var rand = Math.random();
function random2(x) {
  return rand in x;
}

random2(new Proxy({},{has:$=>$}))
```

## Random3
```js
var key = crypto.getRandomValues(new Uint32Array(4));
function random3(x) {
    var d = 0;
    for (var i=0; i<key.length; i++) {
        d |= key[i] ^ x[i];
    }
    return d === 0;
}

▶ random3(????)
```

## Random4
```js
var rand = Math.random();
function random4(x) {
    return rand === x;
}

random4(????)
```

----

# New my level :)

## Greaterself
```js
function greaterself(x) {
    return x > 8 && 8 > x;
}

greaterself({n:0,valueOf:function(){return++this.n%2?9:7}})
greaterself({valueOf:$=>(this.n=-~this.n)%2?9:7}) // shorter
```

## Closure
```js
function closure(x) {
    return x[x] == x;
}

closure([0]);
```

## Any
```js
function any(x) {
    return x - 1 === x + 1
}

any(2**54)
any(1/0)
```

## Isarray
```js
function isarray(x) {
    return Array.isArray(x) && x instanceof Array && x.map === undefined
}

isarray(new Proxy([],{get:(o,p)=>p=='map'?void 0:o[p]}))
```

## Brainfuck
```js
function brainfuck(x) {
	return x(/2/ << /3/) === 16;
}

brainfuck((RegExp.prototype.valueOf=function(){return this.source},x=>x))
```
