# queuer

## Introduction

This is a simple queueing mechanism. It uses interval to check remaining items in the queue. Uses es2015 syntaxes.

## Installation

```
$ npm install --save simple-queuer;
```

## Usage: basic

```
// import the class
import Queuer from 'simple-queuer';

// instantiate
var queuer = new Queuer(10); // the default value is 10.

// add tasks. this will automatically start the queue.
queuer.push(
	function(next){
		setTimeout(()=>{next()}, 1000);
	}
);

```

## Usage: async with promise

```
"use strict";

// import the class
import Queuer from 'simple-queuer';

// instantiate
var queuer = new Queuer(10); // the default value is 10.

function getRandomTimer(){
	return new Promise( (resolve, reject) => {
		let timer = (next) => {
			setTimeout(()=>{
				console.log('timer '+i+' done!')
				resolve(i);
			}, Math.random()*1000);
		}
		queuer.push(timer);
	});
}

// let's create 100 random timers
var promises = [];
for(var i=0; i< 100; i++){
	promises.push(getRandomTimer());
}
Promise
	.all(promises)
	.then((results) => {
		console.log('all timers done!');
	})
;

```