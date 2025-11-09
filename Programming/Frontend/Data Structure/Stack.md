
```js
class Stack {

  constructor() {

    this.items = [];

    this.count = 0;

  }

  

  push(ele) {

    this.items[this.count] = ele;

    this.count++;

  }

  

  pop() {

    if (!this.isEmpty()) {

      this.items.length = this.count - 1;

      this.count--;

    }

  }

  

  print() {

    return this.items;

  }

  

  isEmpty() {

    return this.count == 0;

  }

  

  Top() {

    return this.items[this.count - 1];

  }

}
```