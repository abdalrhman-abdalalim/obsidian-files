
- Any data in your code stores in memory heap 
- any thing in your code execute by call stack 
- call Stack work with LIFO 

```js 
function one(){
    console.log(1);
}
function two(){
    one();
    console.log(2);
}
function three(){
    two();
    console.log(3);
}
function four(){
    three();
    console.log(4);
}
debugger;
four();
```

#### call Stack 
four -> three -> two -> one .
first one to be executed is one function then two .....

### to create your debugger 
- open inspect in chrome
- open sources 
- open snippet
- create your snippet 
- for debugging use debugger in code and start running

#### What is stack overflow 
- is to exceed size of stack 