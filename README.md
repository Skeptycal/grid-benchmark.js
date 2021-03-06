# I benchmarked 8 different ways of representing a 2d grid in JavaScript

**Motivation**: Find the fastest way for representing a 2d collision bitmap for a fast-paced JavaScript game ([LineRage](https://chrome.google.com/webstore/detail/oplmlhhgdcliikihbehklkagmeophnlh)).

There are many ways to represent a bitmap-style grid in Javascript. I compiled a collection of implementations and benchmarked them.

* Some were obvious but I thought were inefficient. Array full of arrays (`grid_array_2d`) turned out is the fastest overall despite having to create that many more objects.
* Some I suspected would be most efficient. `grid_array_1d` turned out to be mediocre due to the extra math required for determining the 2d -> 1d index mapping.
* Some I had no idea how they would compare. The hash-based structs almost compete with `grid_array_2d`, and might actually be better for sparse grids.
* Some I was hoping would yield surprising results, like `grid_canvas` which was completely disappointing.

Needless to say, the results were very surprising to me.

If there are any corrections or additions, please fork and request a pull. Excuse the ghetto benchmarking code, I could not find a good standard benchmarking library that did what I needed.

**Update**: Anyone want to port the benchmarks to [Benchmark.js](https://github.com/mathiasbynens/benchmark.js)? ([Issue 1](https://github.com/shazow/grid-benchmark.js/issues#issue/1))

## Results

YMMV, but I found generally the same trends across machines and browsers. These particular results are from my Macbook Pro on Chrome 8.0.552.231.

size = [1200,800]

### grid_array_1d

    create: 11ms
    write: 57ms
    read: 45ms
    total: 114ms


### grid_array_1d_bitwise

    create: 1ms
    write: 89ms
    read: 65ms
    total: 156ms

### grid_array_2d

    create: 12ms
    write: 48ms
    read: 38ms
    total: 101ms

### grid_array_2d_lazy

    create: 6ms
    write: 78ms
    read: 38ms
    total: 123ms

### grid_canvas

    create: 2ms
    write: 1702ms
    read: 4727ms
    total: 6433ms

### grid_hash

    create: 177ms
    write: 55ms
    read: 35ms
    total: 270ms

### grid_hash_2d

    create: 25ms
    write: 50ms
    read: 39ms
    total: 116ms

### grid_hash_lazy_2d

    create: 0ms
    write: 86ms
    read: 45ms
    total: 134ms
