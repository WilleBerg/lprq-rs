# lprq-rs
lprq-rs is a Rust implementation of the [LPRQ](https://dl.acm.org/doi/abs/10.1145/3572848.3577485).
It is a very fast concurrent lock-free queue, outperforming most, if not all, other Rust concurrent queues.

## Usage
```rust
use lprq_rs::LPRQueue;

fn main() {
    let q: LPRQueue<i32> = LPRQueue::new();
    q.enqueue(1);
    assert_eq(q.dequeue(), Some(1));
}
```

## Performance
lprq-rs was benchmarked using the [rusty-benchmarking-framework](https://github.com/dcs-chalmers/rusty-benchmarking-framework).

It performs a lot better than all other concurrent queues benchmarked after 6 threads for τ = 0.5 and 0.7.
The poor performance for for τ = 0.3 is probably due to no optimisation for the empty queue, however
that is planned to be implemented.

![Benchmark results](todo)

Here are results from three different benchmarks using varying tau (τ) values to control the enqueue/dequeue ratio. 

**Benchmark Setup:** Threads are synchronized to start simultaneously, with each thread alternating between enqueue and dequeue operations based on a random number r ∈ [0,1) - enqueueing when r > τ, dequeueing otherwise. Additional random operations simulate realistic workloads between each queue operation.

For implementation details, see the [rusty-benchmarking-framework](https://github.com/dcs-chalmers/rusty-benchmarking-framework).

