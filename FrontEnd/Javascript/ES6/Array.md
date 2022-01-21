## Array

### dump Array

    console.log("my object: %o", myObj)

### To check if an array is either empty or not

    if (Array.isArray(arr) && arr.length) {
        // array exists and is not empty
    }

## [map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

    // callback 函数只会在有值的索引上被调用；那些从来没被赋过值或者使用 delete 删除的索引则不会被调用
    Array(3).map(x => console.log(x)) // 无输出，因为没有没赋过值

    // 匿名函数
    Array(3).fill(1).map(
        (item, index) => {
            console.log(`item: ${item}, index: ${index}`)
        }
    )

    // callback 函数会被自动传入三个参数：数组元素，元素索引，原数组本身
    function pp(item, index, arr) {
        console.log(`item: ${item}, index: ${index}, arr: ${arr}`)
    }

    Array(3).fill(1).map(pp)

    // Array 如果想要生成数组时，需要注意数据类型
    Array(3).length // 3
    Array("3").length // 1

## [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

    const array1 = [1, 2, 3];
    console.log(array1.includes(2)); // true

## [every](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

    // every 方法为数组中的每个元素执行一次 callback 函数，直到它找到一个会使 callback 返回 false 的元素。如果发现了一个这样的元素，every 方法将会立即返回 false

    // 若收到一个空数组，此方法在一切情况下都会返回 true
    Array(0).every(x => x === 0) // true

    // callback 只会为那些已经被赋值的索引调用
    Array(3).every(x => x === 0) // true

    [1,2].fill(0).every(x => x === 1) // false

## [slice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

slice() 方法返回一个新的数组对象，这一对象是一个由 begin 和 end 决定的原数组的浅拷贝（包括 begin，不包括end）

    const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

    console.log(animals.slice(2));
    // expected output: Array ["camel", "duck", "elephant"]

    console.log(animals.slice(2, 4));
    // expected output: Array ["camel", "duck"]

## [concat](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

    const array1 = ['a', 'b', 'c'];
    const array2 = ['d', 'e', 'f'];
    const array3 = array1.concat(array2);

    console.log(array3);
    // expected output: Array ["a", "b", "c", "d", "e", "f"]

## from

    Array.from({length: 5}, (v, i) => i);
    // [0, 1, 2, 3, 4]

    Array.from({length: 3}, (v, i) => i + 1);
    // [1, 2, 3]

## reduce

    The final result of running the reducer across all elements of the array is a single value.
