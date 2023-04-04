## [torch 参数更多 ] torch.Tensor.index_copy_

### [torch.Tensor.index_copy_](https://pytorch.org/docs/stable/generated/torch.Tensor.index_copy_.html?highlight=index_copy_#torch.Tensor.index_copy_)

```python
torch.Tensor.index_copy_(dim, index, tensor)
```

### [paddle.Tensor.scatter_](https://www.paddlepaddle.org.cn/documentation/docs/zh/api/paddle/Tensor_cn.html#id17)

```python
paddle.Tensor.scatter_(index, updates, overwrite=True, name=None)
```

两者功能类似，torch 参数更多，具体如下：
### 参数映射
| PyTorch | PaddlePaddle | 备注                        |
|---------|--------------|---------------------------|
| dim     | -            | 索引的维度值。 |
| index   | index          | 选择的需要更新的 Tensor 索引。 |
| tensor  | updates          | 根据 index 来更新 Tensor, 仅参数名不同 |
| -       | overwrite          | 更新输出的方式，True 为覆盖模式，False 为累加模式， 默认即可。 |


### 转写示例
#### 示例 1: 索引的维度为 0
```python
# torch 写法
x.index_copy_(0, index, t)

# paddle 写法
x.scatter_(index, t)
```
#### 示例 2: 索引的维度不为 0
```python
# torch 写法
x.index_copy_(2, index, t)

# paddle 写法
dim = list(x.shape)
for i0 in range(dim[0]):
    for i1 in range(dim[1]):
        x[i0, i1, :] = x[i0: i1].scatter_(index, t[i0: i1])
```