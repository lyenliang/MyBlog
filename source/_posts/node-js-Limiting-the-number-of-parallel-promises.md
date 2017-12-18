title: '[node.js] Limiting the number of parallel promises'
author: lyenliang
tags:
  - node.js
categories: []
date: 2017-12-17 19:56:00
---
[Promise.all](http://bluebirdjs.com/docs/api/promise.all.html) is a useful funciton when you want to wait for more than 1 promise running in parallel to complete. However, sometimes you may want to limit the number of parallel promises. For example, you may wish to limit the number of simultaneous downloads from a website.


[cwait](https://github.com/charto/cwait) is a convenient tool which allows you to limit the number of promises running in parallel. 

Here I'll demonstrate how to use `cwait`. First let's assume we have a function `later` that returns a promise which is resolved after a specified timeout. 

    function later (time, val) {
      console.log(`later is triggered. ${val}`)
      return new Promise((resolve, reject) => {
        setTimeout(resolve, time, val)
      })
    }
    
When we create 10 promises with `later`, and execute them with `Promise.all`, it will take about 1 second to finish the execution.

    // echoNumberPromiseAll.js

    const Promise = require('bluebird')

    let totalNumber = 10
    let timeout = 1000 // 1000 ms
    let start, finish

    function later (time, val) {
      console.log(`later triggered. ${val}`)
      return new Promise((resolve, reject) => {
        setTimeout(resolve, time, val)
      })
    }

    let promises = []
    function init () {
      start = new Date()
      for (let i = 0; i < totalNumber; i += 1) {
        promises.push(later(timeout, i))
      }
    }

    init()

    Promise.all(promises)
      .then((result) => {
        console.log(`All done. result: ${result}`)
        finish = new Date()
        console.log(`Execution time: ${finish - start} ms`)
      })
      .catch(err => {
        console.error(`error: ${err}`)
      })


`node echoNumberPromiseAll.js`'s execution result:

    node echoNumberPromiseAll.js
    later triggered. 0
    later triggered. 1
    later triggered. 2
    later triggered. 3
    later triggered. 4
    later triggered. 5
    later triggered. 6
    later triggered. 7
    later triggered. 8
    later triggered. 9
    All done. result: 0,1,2,3,4,5,6,7,8,9
    Execution time: 1012 ms
    
As you can see from the above output, 10 promises are triggered simultaneously. Because the execution time is about 1 second.

Before we can apply `cwait`, we have to convert `Promise.all` to [`Promise.map`](http://bluebirdjs.com/docs/api/promise.map.html) first. 

Here's the converted code:

    // echoNumberPromiseMap.js

    const Promise = require('bluebird')

    let totalNumber = 10
    let timeout = 1000 // 1000 ms
    let start, finish

    let numbers = []

    function later (time, val) {
      console.log(`later triggered. ${val}`)
      return new Promise((resolve, reject) => {
        setTimeout(resolve, time, val)
      })
    }

    function init () {
      start = new Date()
      for (let i = 0; i < totalNumber; i += 1) {
        numbers.push(i)
      }
    }

    function promiseMap (number) {
      return later(timeout, number)
    }

    init()

    Promise.map(numbers, promiseMap)
      .then((result) => {
        console.log(`All done. result: ${result}`)
        finish = new Date()
        console.log(`Execution time: ${finish - start} ms`)
      })
      .catch(err => {
        console.error(`error: ${err}`)
      })

      
 
Then we will be able to apply `cwait` to the above code:

    // echoNumberCwait.js

    const TaskQueue = require('cwait').TaskQueue
    const Promise = require('bluebird')

    let queue = new TaskQueue(Promise, 3)

    let totalNumber = 10
    let timeout = 1000 // 1000 ms
    let start, finish

    let numbers = []

    function later (time, val) {
      console.log(`later triggered. ${val}`)
      return new Promise((resolve, reject) => {
        setTimeout(resolve, time, val)
      })
    }

    function init () {
      start = new Date()
      for (let i = 0; i < totalNumber; i += 1) {
        numbers.push(i)
      }
    }

    function promiseMap (number) {
      return later(timeout, number)
    }

    init()

    Promise.map(numbers, queue.wrap(promiseMap))
      .then((result) => {
        console.log(`All done. result: ${result}`)
        finish = new Date()
        console.log(`Execution time: ${finish - start}`)
      })
      .catch(err => {
        console.error(`error: ${err}`)
      })


In the example above, we limit the number of parallel promises to 3. Here's the execution result of `node echoNumberCwait.js`

    later triggered. 0
    later triggered. 1
    later triggered. 2
    later triggered. 3
    later triggered. 9
    later triggered. 8
    later triggered. 7
    later triggered. 6
    later triggered. 5
    later triggered. 4
    All done. result: 0,1,2,3,4,5,6,7,8,9
    Execution time: 4016 ms
    
The program first executes the promises with `val` equal to 0, 1, and 2. And waits until the 3 promises are completed. Then it executes the promises with `val` equal to 3, 9, and 8. and wait for them to complete ...

So in the end, it takes about 4 seconds to finish the execution. 