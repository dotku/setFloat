# setNumber
A solution for react onChange/onChangeText for number.

## Story

Simple parseFloat or parseInt would easily get `NaN` on input value, which might not be user friendly, that's why setNumber comes.

## Design

### setFloat

In general we handle on number and dot as float number needs, so it would be regex with `/\d|\./` to validate the number from string. 
Baside of that, we have few corner cases: 

1. Leading 0 is not allowed for number more then 1.
2. It is not allow double 0 in the beginning of the string input. 
3. It is not allow double dots ("..") among the number characters.

Here is the function:

```js
function setFloat(v, fun): void {
  if (v.length > 1 && v[0] === "0" && v[1] !== ".") v = v.slice(1);
  if (v.match(/\./g)?.length > 1) return;
  if (/\d|\./.test(v[v.length - 1])) {
    fun(v);
  }
}
```

Usage for a react app:

```
const [profit, setProfit] = useState(0);
return <input onChangeText((v) => setFloat(v, setProfit)) value={profit} />
```


### setIntger

1. It shouldn't be more then one dot in the string.
2. It only accepts numberic charaters.

### setSciNumber

Scientific number might be complicate, there could be a sperical char for a certain value, eg "e" prepresents times ten, "1e2" would be "100".

