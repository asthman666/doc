### `Promise` is one of the JavaScript's standard, built-in objects.

The `Promise` object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

The `.then()` method takes up to two arguments; the first argument is a callback function for the resolved case of the promise, and the second argument is a callback function for the rejected case.

Handling a rejected promise in each `.then()` has consequences further down the promise chain. Sometimes there is no choice, because an error must be handled immediately. In such cases we must throw an error of some type to maintain error state down the chain. On the other hand, in the absence of an immediate need, it is simpler to leave out error handling until a final .catch() statement. A .catch() is really just a .then() without a slot for a callback function for the case when the promise is resolved.

    interface Promise<T> {
        /**
        * Attaches callbacks for the resolution and/or rejection of the Promise.
        * @param onfulfilled The callback to execute when the Promise is resolved.
        * @param onrejected The callback to execute when the Promise is rejected.
        * @returns A Promise for the completion of which ever callback is executed.
        */
        then<TResult1 = T, TResult2 = never>(onfulfilled?: ((value: T) => TResult1 | PromiseLike<TResult1>) | undefined | null, onrejected?: ((reason: any) => TResult2 | PromiseLike<TResult2>) | undefined | null): Promise<TResult1 | TResult2>;

        /**
        * Attaches a callback for only the rejection of the Promise.
        * @param onrejected The callback to execute when the Promise is rejected.
        * @returns A Promise for the completion of the callback.
        */
        catch<TResult = never>(onrejected?: ((reason: any) => TResult | PromiseLike<TResult>) | undefined | null): Promise<T | TResult>;
    }

    interface Promise<T> {
        /**
        * Attaches a callback that is invoked when the Promise is settled (fulfilled or rejected). The
        * resolved value cannot be modified from the callback.
        * @param onfinally The callback to execute when the Promise is settled (fulfilled or rejected).
        * @returns A Promise for the completion of the callback.
        */
        finally(onfinally?: (() => void) | undefined | null): Promise<T>
    }

The termination condition of a promise determines the "settled" state of the next promise in the chain. A "resolved" state indicates a successful completion of the promise, while a "rejected" state indicates a lack of success. The return value of each resolved promise in the chain is passed along to the next .then(), while the reason for rejection is passed along to the next rejection-handler function in the chain.

    promise1
        .then(value => { return value + ' and bar'; })
        .then(value => { return value + ' and bar again'; })
        .then(value => { return value + ' and again'; })
        .then(value => { return value + ' and again'; })
        .then(value => { console.log(value) })
        .catch(err => { console.log(err) });

The promises of a chain are nested like Russian dolls, but get popped like the top of a stack. The first promise in the chain is most deeply nested and is the first to pop.

    (promise D, (promise C, (promise B, (promise A) ) ) )

## Creating a Promise around an old callback API

A Promise can be created from scratch using its constructor. This should be needed only to wrap old APIs.

In an ideal world, all asynchronous functions would already return promises. Unfortunately, some APIs still expect success and/or failure callbacks to be passed in the old way. The most obvious example is the setTimeout() function:

    setTimeout(() => saySomething("10 seconds passed"), 10*1000);

Mixing old-style callbacks and promises is problematic. If saySomething() fails or contains a programming error, nothing catches it. setTimeout is to blame for this.

Luckily we can wrap setTimeout in a promise. Best practice is to wrap problematic functions at the lowest possible level, and then never call them directly again:

    const wait = ms => new Promise(resolve => setTimeout(resolve, ms));

    wait(10*1000).then(() => saySomething("10 seconds")).catch(failureCallback);

Basically, the promise constructor takes an executor function that lets us resolve or reject a promise manually. Since setTimeout() doesn't really fail, we left out reject in this case.

> [Global_Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)

> [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

> [Using_promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

> [async_function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)