# Personal collection
1. Relation between SIMD(a technique), ISPC(a tool for SIMD) and AVX(a concrete implementation of SIMD):
   ISPC是一种利用高级编程接口来方便开发者编写利用SIMD技术的工具，SIMD是一类并行计算的技术，而AVX2是SIMD指令集中针对现代处理器的一个具体实现，特别强调了增强的并行处理能力和更宽的数据处理能力。ISPC通过编译器优化使得开发者能够更容易地利用包括AVX2在内的SIMD指令集来提升程序的性能。
2. SIMD is different from multi-thread. The former runs in the same core while the latter run in multiple CPU cores
> What does it mean? Then, how to implement it efficiently.
>> SIMD code is **not** paralleled until it is called, then a gang of instances are created.
3. add `foreach` in ISPC code, you get data-parallel
   * a more proper way: *stream programming model*
4. benefit of *stream programming*
   * compiler help rewrite the code, e.g. `foo(input, tmp); bar(tmp, output)` convert to `output[i] = bar(foo(input[x]));`
   * you need kernel like `bar` and `foo` above
   * use a lot of opertaor
   * `scatter` and `gather`
5. Amdahl's law: Even small fraction of your code need to run sequentially due to the dependency, say 1%, the speedup is 40x even with 64 processors
6. Trade off footprint for removing dependency!空间换时间
   * one brilliant example about `math first` / `barrier` / `lock` / `trade off` in `Perform Gauss-Seidel sweeps over grid until convergence`
1. SPMD execution model: 多个处理器执行同一程序，但是每个处理器处理的数据集是不同的。这种模型通常用于数据并行计算，其中大量的数据需要被处理，并且可以将数据分割成多个部分，每个部分由一个处理器独立处理。
   * message passing model
   * data-parallel programming model
   * shared address space model