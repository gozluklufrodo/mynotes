## Pytorch Tensors

- Pytorch tensors are similar to numpy arrays but with a few additional superpowers.
  
  - Ability to perform operations on GPU
  
  - Distribute operations to multiple devices
  
  - Keep track of the graph of computations that created them

A simple one dimensional tensor with ones.

- ```
  import torch
  a = torch.ones()
  
  In [4]: a
  Out[4]: tensor([1., 1., 1.])
  ```

###### Essense of Tensors

- Python lists or tupples are collections of Python objects that are individually allocated into memory. Pytorch tensors or NumPy arrays on the other hand are views over contiguous memory blocks. Pytorch or numpy arrays are unboxed C numeric types not python objects.

```
points = torch.tensor([[5,3,2], [4,3,3]])

In [3]: points
Out[3]: 
tensor([[5, 3, 2],
        [4, 3, 3]])



In [4]: points[0]
Out[4]: tensor([5, 3, 2])
```

Here we created a tensor object and then accessed the first row of that object. Does this mean we have created a new tensor object ? Of cource not, the object is the same in the storage but a view of that storage is returned.

### Tensor element types

1. Numbers in python are objects, but in numpy they are just 32 bit floating point numbres. İn python lists, python convert the number to an object with different capabilities that need more memory.

2. Python interpreter is slow compared to a compiled code.

3. Data types:
   
   1. torch.float32 --> default data type for tensors. 32 bit floating point number
   
   2. torch.float16 --> half precision floating-point number
   
   3. torch.int64 --> or torch.long , singned 64 bit integers

4. Default data type for floating point numbers is torch.float32 and for integers is torch.int64

### Torch Storage

1. Values in tensors are allocated to contiguous chunks of memory managed by **torch.Storage.**

2. **torch.Storage** is a one dimensional array.

3. A pytorch tensor instance is a view of that storage, that can acces to the storage using **offset** and **per dimension strides**.

```
In [49]: points = torch.tensor([[4.0, 1.0], [5.0, 3.0], [2.0, 1.0]])

In [50]: points
Out[50]: 
tensor([[4., 1.],
        [5., 3.],
        [2., 1.]])



In [51]: points.storage()
Out[51]: 
 4.0
 1.0
 5.0
 3.0
 2.0
 1.0
[torch.FloatStorage of size 6]
```

In the code above points tensor has a shape (3,2) but the storage is one dimensional.

If you change the value in storage, it will also changed in the given tensor object.

```
stor = points.storage()
In [61]: stor
Out[61]: 
 4.0
 1.0
 1.0
 3.0
 2.0
 1.0


In [62]: stor[3] = 7

In [63]: points
Out[63]: 
tensor([[4., 1.],
        [1., 7.],
        [2., 1.]])
```

#### Tensor metadata: Size, offset and stride

1. size is the size of tensor in each dimension

```
In [69]: points.size()
Out[69]: torch.Size([3, 2])
```

2. Storage offset is the index in the storage corresponding to the first element of the tensor.

```
In [70]: points.storage_offset()
Out[70]: 0
```

3. Stride is the number of elements in the storage that need to be skipped to obtain the next element along each dimension.

```
In [71]: points.stride()
Out[71]: (2, 1)
```

4. When get a part of the points tensor using index, a new storage will not be allocated, it will still use the same storage but its storage offset and stride will change.

```
second_point = points[1]

In [75]: second_point.storage_offset()
Out[75]: 2


In [76]: second_point.stride()
Out[76]: (1,)
```

If we change respective numbers in the **storage**, then both **second_point** and points **tensors** will also change.

Also, if we change the **second_point** tensor, both **storage** and **points** tensor will also change.

5. If we take transpose, again the storage will not change but the stride and shape will change.

```
In [129]: points_t = points.t()

In [130]: points_t
Out[130]: 
tensor([[4., 5., 2.],
        [1., 3., 1.]])


In [131]: id(points_t.storage()) == id(points.storage())
Out[131]: True


In [133]: points.stride()
Out[133]: (2, 1)

In [134]: points_t.stride()
Out[134]: (1, 2)
```

6. When we take the transpose and create **points_t**, then it will not be a contiguous tensor.

```
In [135]: points_t.is_contiguous()
Out[135]: False
```

7. To make it contiguous again:

```
points_t = points_t.contiguous()
```

In the contiguous tensors number are alligned to the storage row by row.

### Moving Tensors to GPU

1. A tensor can be created in gpu directly.

```
points = torch.tensor([[5,3,2], [4,4,2], [4,3,3]], 
                        dtype=torch.float32, 
                        device="cuda")
```

2. Also it can be moved from cpu to gpu and vice versa.

```
points = points.to("cpu")
```

**Serializing Tensors**

1. To save and load as pickle. Disadvantage of this is that we can only load this with PyTorch.

```
torch.save(points, "test.t")

points = torch.load("test.t")
```

2. Serialize using hdf5.

```
f = h5py.File("file.hdf5", "w")
dset = f.create_dataset("coord", data=points.numpy())
f.close()
```