# ECMAScript Generator Blocks

An ECMAScript proposal to create generator blocks. Essentially placing a scope after a generator would execute the generator compactly. This would be an alternative of using ```for...of``` syntax.

## Syntax

```js
function* Range(start, end)
{
	for (let itr = start; itr < end; ++itr)
	{
		yield { value: itr };
	}
}

Range(0, 10)
{
	console.log(value);
	if (value == 3)
	{
		break;
	}
};
```
Output:
```
0
1
2
3
```

## Return Syntax

```js
function* gen()
{
	yield { a: 1 };
	yield { a: 2 };
	yield { a: 3 };
	return 10;
}

const value = gen()
{
	console.log(a);
	if (a == 2)
	{
		break;
	}
};
console.log(value); // 10
```
Output:
```
1
2
10
```

## Filter and Map

```js
const a = [1, 2, 3, 4, 5];
a.filter = function*(variableName)
{
	var values = [];
	this.forEach(value =>
	{
		if (yield { [variableName ? variableName : 'value']: value })
		{
			values.push(value);
		}
	});
	return values;
};
a.map = function*(operation, variableName)
{
	var values = [];
	this.forEach(value =>
	{
		yield { [variableName ? variableName : 'value']: value })
		values.push(operation(value));
	});
	return values;
};
// Makes more sense with multiline statements
const b = a.filter() { return value < 3; }.map() { return value * 2; }; // [2, 4]
// With optional parenthesis
const c = a.filter{ return value < 3; }.map{ return value * 2; }; // [2, 4]
```

## Filter + Map Combined

```js
const a = [1, 2, 3, 4, 5];
a.filterMap = function*(variableName)
{
	var values = [];
	this.forEach(value =>
	{
		if (yield { [variableName ? variableName : 'value']: value } != undefined)
		{
			values.push(value);
		}
	});
	return values;
};

const b = a.filterMap
{
	if (value < 3)
	{
		return value * 2;
	}
}; // [2, 4]
```
