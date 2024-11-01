## numpy数组大小

可以使用.size or .shape 查看numpy数组的的大小 or 形状

在NumPy中，`shape`和`size`是数组的两个不同属性，它们提供了关于数组结构的不同信息：

- **`shape`**
  `shape`属性返回一个元组，表示数组的维度大小。每个元素代表对应维度上的长度。例如，一个具有形状`(3, 4)`的数组是一个2D数组，它有3行和4列。对于一维数组，`shape`将只有一个元素，例如`(10)`表示一个长度为10的数组。
- **`size`**
  `size`属性返回数组中元素的总数。它是`shape`中所有维度长度的乘积。例如，如果一个数组的`shape`是`(3, 4)`，那么它的`size`将是`3 * 4 = 12`。



```python
 mean_vel = np.zeros_like(mean_pos)
```

该函数用于创建一个与`mean_pos`具有相同形状的全零数组。

diag 从一维数组创建对角矩阵，或者提取二维数组的对角线上的元素

sqrt 对数组每个元素取平方根

square 对数组的每个元素平方

 `np.r_` 将 `std_pos` 和 `std_vel` 连接成一个一维数组。（这两个数组都是一维数组）



## numpy数组特性

在 NumPy 中，当您使用比较操作符（如 `>`, `<`, `==`, `!=`, `>=`, `<=`）在数组上时，这些操作会应用到数组中的每一个元素上。即使数组中只有一个元素，这个操作仍然有效。

在您的代码片段中：

```
remain_inds = scores > self.args.track_high_thresh
```

`scores` 可能是一个 NumPy 数组，而 `self.args.track_high_thresh` 是一个浮点数。当您执行 `scores > self.args.track_high_thresh` 时，NumPy 会将这个阈值与 `scores` 数组中的每一个元素进行比较。如果 `scores` 数组中确实只包含一个元素，那么这将是一个简单的元素级别的比较。

比较的结果是一个布尔数组（`numpy.ndarray` 类型），其中的元素是 `True` 或 `False`，表示原数组中对应位置的元素是否满足比较条件。

<img src="C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20240725164837124.png" alt="image-20240725164837124" style="zoom:50%;" />

例如，如果 `scores` 是一个包含单个元素的数组，比如 `[4.5]`，而 `self.args.track_high_thresh` 是 `4.0`，那么 `scores > self.args.track_high_thresh` 将返回 `[True]`，因为 `4.5 > 4.0`。

这种行为称为“广播”（Broadcasting），它是 NumPy 中处理不同形状的数组之间算术和比较运算的一种机制。在这种情况下，标量值被“广播”到数组的形状，使得每个元素都能与之进行比较。



## numpy逻辑运算

```python
inds_second = np.logical_and(inds_low, inds_high)
```

该函数使用了numpy库，通过logical_and函数对两个布尔型数组inds_low和inds_high进行按位与操作，返回一个新的布尔型数组inds_second，其中的每个元素都对应着inds_low和inds_high对应位置上均为True的情况



## 布尔索引

在NumPy中，布尔索引是一种非常强大的特性。当你用一个布尔型数组（例如`inds_second`）来索引另一个数组（例如`bboxes`）时，它会选取原数组中对应于布尔数组中值为`True`的位置的元素。

具体到这段代码：

```
dets_second = bboxes[inds_second]
```

- `bboxes`是一个二维数组，存储了边界框的信息。
- `inds_second`是一个与`bboxes`形状相同的布尔型数组，其中`True`表示对应的边界框应该被选中，而`False`表示不选中。

执行上述代码后，`dets_second`将包含`bboxes`中所有对应`inds_second`中`True`值的行。这是因为NumPy的布尔索引机制允许你基于条件直接选择数组中的元素或行，而无需循环或显式迭代，从而提供了高效的数据筛选方式。



## np.where

```python
 pairs = np.where(pdist < 0.15)
```

此函数返回一个np数组pairs，其中包含pdist中所有距离小于0.15的元素的索引位置格式为（索引，元素）

