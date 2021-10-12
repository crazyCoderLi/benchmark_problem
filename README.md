# Benchmarking problem



## Overview:

By reading the sample code, I wrote a script to evaluate the inference performance of a specific model.

My goal is to write a script that is as general as possible. To evaluate different models, only what you should do is to change the parameters when the class is initialized.

The metrics I have tested mainly include P50_latency, P95_latency, P99_latency, throughput.

I have run the script both on "cuda" and "cpu".

## Design:

![类图](https://github.com/crazyCoderLi/benchmark_problem/blob/main/uml/uml.png)

- Preprocess:
  - Responsible for giving data, it can transform the video into a list of tensors that the model can handle. By changing the parameters, you can control the format of the data.
- BenchmarkingScript:
  - It can load a model from Torch Hub, and run the model inference with metrics testing. It is flexible, you can load different models by giving its source and name.

To see more implementation details, you can [click here](https://github.com/crazyCoderLi/benchmark_problem/blob/main/benchmark.ipynb) to see the source code on colab.



## Results:

| Model         | Device | P50_latency | P95_latency | P99_latency | Throughput (times/sec) |
| ------------- | ------ | ----------- | ----------- | ----------- | ---------------------- |
| slowfast_r50  | cpu    | 5.73        | 5.79        | 5.85        | 0.174                  |
| slowfast_r50  | cuda   | 0.19        | 0.20        | 0.20        | 5.18                   |
| slowfast_r101 | cpu    | 12.50       | 12.60       | 12.82       | 0.08                   |
| slowfast_r101 | cuda   | 0.28        | 0.29        | 0.29        | 3.55                   |

We can see that the model runs on cuda is much faster than on cpu, because the GPU can compute in parallel.

Also we can see that the more complex the model is, the longer latency will be.





