# Spread syntax

    console.log(1,[2,3],4)
    // 1 [2, 3] 4

    console.log(1, ...[2,3], 4)
    // 1 2 3 4

    console.log({"a":1, "b":2})
    // {a: 1, b: 2}

    console.log({...{"a":1, "b":2}})
    // {a: 1, b: 2}

    const state = {"a": 1, "b": 2}
    const copy_state = ...state
    const state2 = {...state, "b": 3, "d": 4} // {a: 1, b: 3, d: 4}

    const {a} = state; // 1
    const {x} = state; // undefined

[array](http://es6.ruanyifeng.com/#docs/array)

[Object Rest/Spread](https://github.com/tc39/proposal-object-rest-spread)

[Spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

