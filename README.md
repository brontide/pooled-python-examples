# High Throughput Python

This code is designed to highlight ways to improve your python code using the standard libraries by
taking advantage of multiprocessing or multithreading.  We will come up with some example use-cases
and then show the development of code to speed development.

We will be concentrating on jobs which are inherently CPU bound.

Presumtions

* We will be using python 3
* We are programming for unix-like platforms
* You have a working understanding of python

## Case 1: Hashing fixed sized blocks

One of the necessary evils of hashing is that is can be slow and is inherently a serial operation.
While the hashing of each blob of data can not be sped up, we may be able to improve the speed
by allowing multiple blobs to be hashed in parallel.

The first part of this case we will develop a fixed input set for testing all of our scenarios.

### Developing an input set

```python


def generate_data(*, blob_size=10 * 1024 * 1024, count=1000):
    # Returns an array of random data
    with open('/dev/urandom', 'rb') as rand_in:
        return [ rand_in.read(blob_size) for x in range(count) ]


```
