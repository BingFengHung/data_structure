# Set 集合
集合由一組 `無序` 且 `唯一` 的項目組成。

這個資料結構使用了與有限集合相同的數學概念，在數學中，集合也有聯集、交集、差集等基本操作。


- add
- remove
- has
- clear
- size 
- values

這邊主要使用到 JavaScript 的物件來進行實現。

```js
class Set {
	constructor() {
		this.items = {};
	}

	add(value) {
		if (!this.has(value)) {
			this.items[value] = value;
			return true;
		}
		return false;
	}

	remove(value) {
		if (this.items.has(value))) {
			delete this.items[value];
			return true;
		}
	}

	has(value) {
		return this.items.hasOwnProperty(value);
		// or 
		// return value in this.items
	}

	clear() {
		this.items = {};
	}

	size() {
		return Object.keys(this.items).length;
	}

	values() {
		return Object.keys(this.items);
	}

	union(otherSet) {
		let unionSet = new Set();

		var values = this.values();

		for(let i = 0; i < values.length; i++) {
			unionSet.add(values[i])
		}

		values = otherSet.values();
		for(let i = 0; i < values.length; i++) {
			unionSet.add(values[i]);
		}

		return unionSet;
	}

	intersection(otherSet) {
		let intersectionSet = new Set();

		let values = this.values();

		for(let i = 0; i < values.length; i++) {
			if (otherSet.has(values[i])) {
				intersectionSet.add(values[i]);
			}
		}
	}

	difference(otherSet) {
		let differenceSet = new Set();

		let values = this.values();

		for(let i = 0; i < values.length; i++) {
			if (!otherSet.has(values[i])) {
				differenceSet.add(values[i])
			}
		}
	}

	subst(otherSet) {
		if (this.size() > otherSet.size()) 
		   return false;
		else {
			let values = this.values();
			for(let i = 0; i < values.length; i++) {
				if (!otherSet.has(values[i]))
				   return false;
			}
		}

		return true;
	}
}
```