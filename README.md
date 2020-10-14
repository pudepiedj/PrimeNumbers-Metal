# PrimeNumbers-Metal

Compute prime numbers with Metal GPU API and compare its performance to CPU results.

COMMENT from pudepiedj. I found this while looking for an implementation of prime-number generation using the GPU and Metal for an XCodeProject.
It works well but on my system the CPU/GPU code provided generates errors with the GPU falsely identifying some numbers as prime. As far as I can tell all such numbers are the squares of primes, the first being 17884441 = 4229^2; the next is 4231^2 and so on.
This error arises from a mistake in the upper bound of the test in the gpuTest/computerPrimeNumbers.metal file where at about line 33 the loop needs to be modified so that the upper bound is included. This is easily done by simply adding 2. (I note that the CPU test uses a Double here instead of FloatType and doesn't succumb to the same problem.)

for (UIntType i = 3;  i <= sqrt((FloatType)num) + 2;  i+=2)

```
Current Device Name: iPhone 8

'GPU Test' : Current numbers range: 1 ... 500_000
'GPU Test' : 0.177096962928772 sec

'CPU Test' : Current numbers range: 1 ... 500_000
'CPU Test' : 0.490992069244385 sec

[2, 3, 5, 7, 11, 13, 17, 19, 23, ....  499973, 499979]

Checking....
Tasks were completed successfully:
GPU test is 2.77 times faster than CPU test
```

## Metal Shader

See GPU test sources - [this](https://github.com/dneprDroid/PrimeNumbers-Metal/tree/master/PrimeNumbers-Metal/gpuTest).

