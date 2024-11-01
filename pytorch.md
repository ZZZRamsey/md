## 读取一个pth文件

`.pth` 文件通常用于存储 PyTorch 模型的权重和其他状态信息。这些文件可以包含整个模型的状态字典（state dict）、优化器的状态字典、损失值以及其他任意 Python 对象。

如果你想要读取一个 `.pth` 文件来加载一个模型以便进行推理或者继续训练，你可以使用 `torch.load()` 函数。下面是一个基本的例子来说明如何读取 `.pth` 文件：

#### 步骤 1: 导入必要的库

```python
import torch
from your_model_module import YourModelClass  # 从定义模型的模块导入模型类
```

#### 步骤 2: 加载模型的 state_dict

```python
model_path = "path_to_your_model.pth"  # 替换为你的.pth文件路径
model_state_dict = torch.load(model_path)
```

#### 步骤 3: 创建模型实例并加载权重

```python
model = YourModelClass()  # 创建模型实例
model.load_state_dict(model_state_dict)  # 将 state_dict 加载到模型中
model.eval()  # 设置模型为评估模式
```

#### 完整示例:

```python
import torch
from your_model_module import YourModelClass

def load_model(model_path):
    model_state_dict = torch.load(model_path)
    model = YourModelClass()
    model.load_state_dict(model_state_dict)
    model.eval()
    return model

# 使用方法
model = load_model("path_to_your_model.pth")
```

如果模型是在 GPU 上训练的，而你正在使用 CPU 进行推理，你需要确保模型和数据都在相同的设备上。可以通过以下方式将模型移动到 CPU：

```python
device = torch.device('cpu')
model.to(device)
```

如果你的模型定义在一个单独的模块中，请确保已经正确地导入了模型类。如果模型定义在当前脚本中，则不需要额外导入。



## 查看tensor大小

1. **使用 `.size()` 方法**：
   - 这个方法返回一个 `torch.Size` 对象，它是一个类似于元组的对象，表示张量的各个维度的大小。
2. **使用 `.shape` 属性**：
   - 这是一个只读属性，同样返回一个 `torch.Size` 对象，表示张量的形状。



## 查看网络结构

要根据 `.pth` 文件可视化 PyTorch 模型的网络结构，你可以采用多种方法。这里我将介绍几种常见的方法：

1. **使用 `torchsummary` 库**
2. **使用 `torchviz` 库**
3. **使用 `netron` 工具**

### 方法 1: 使用 `torchsummary` 库

`torchsummary` 是一个非常方便的库，可以直接打印出模型的结构以及每层的输出尺寸。

#### 安装 `torchsummary`:

```bash
pip install torchsummary
```

#### 示例代码:

```python
import torch
from torchsummary import summary
from your_model_module import YourModelClass

# 加载模型
model_path = "path_to_your_model.pth"
model = YourModelClass()
model.load_state_dict(torch.load(model_path))
model.eval()

# 打印模型结构
summary(model, input_size=(3, 224, 224))  # 假设输入尺寸为 (3, 224, 224)
```

### 方法 2: 使用 `torchviz` 库

`torchviz` 可以生成模型的图形表示，这需要安装 `torchviz` 和 `graphviz`。

#### 安装依赖:

```bash
pip install torchviz graphviz
```

#### 示例代码:

```python
import torch
from torchviz import make_dot
from your_model_module import YourModelClass

# 加载模型
model_path = "path_to_your_model.pth"
model = YourModelClass()
model.load_state_dict(torch.load(model_path))
model.eval()

# 创建一个随机输入
x = torch.randn(1, 3, 224, 224)  # 假设输入尺寸为 (1, 3, 224, 224)

# 通过模型传递数据
y = model(x)

# 生成图形
g = make_dot(y, params=dict(list(model.named_parameters()) + [('x', x)]))
g.view()
```

### 方法 3: 使用 `netron` 工具

Netron 是一个跨平台的工具，可以用来查看和探索神经网络模型。

[pytorch快速上手（10）-----netron查看神经网络结构图_netron画神经网络图-CSDN博客](https://blog.csdn.net/All_In_gzx_cc/article/details/125805032)

#### 安装 Netron:

- 下载并安装 Netron: https://lutzroeder.github.io/netron/
- 或者使用 Docker 安装: `docker pull lutzroeder/netron`

#### 将 `.pth` 转换成 `.onnx` 格式:

```python
import torch
from your_model_module import YourModelClass

# 加载模型
model_path = "path_to_your_model.pth"
model = YourModelClass()		# 一般pth中只有state_dict，要转化需要有模型定义
model.load_state_dict(torch.load(model_path))
model.eval()

# 导出模型到 ONNX 格式
dummy_input = torch.randn(1, 3, 224, 224)  # 假设输入尺寸为 (1, 3, 224, 224)
output_onnx = "path_to_output_model.onnx"

torch.onnx.export(
    model,
    dummy_input,
    output_onnx,
    export_params=True,        # 存储模型参数
    opset_version=11,          # ONNX版本
    do_constant_folding=True,  # 是否执行常量折叠优化
    input_names=['input'],     # 输入节点名称
    output_names=['output'],   # 输出节点名称
    dynamic_axes={
        'input': {0: 'batch_size'},  # 可变批次大小
        'output': {0: 'batch_size'}
    }
)

# 使用 Netron 查看 ONNX 文件
# 如果使用的是 Docker 版本，可以在命令行执行:
# docker run --rm -it -p 8080:8080 lutzroeder/netron path_to_output_model.onnx
```

以上就是几种不同的方法来可视化 PyTorch 模型的网络结构。选择哪种方法取决于你的具体需求和个人偏好。

#### 可选：简化模型

如果你希望进一步简化模型，可以使用一些工具如 `ONNX-Simplifier`。这是一个额外的步骤，不是必须的。

```python
!pip install onnx-simplifier
from onnxsim import simplify

# 加载 ONNX 文件
onnx_model = onnx.load(output_onnx)

# 简化模型
model_simplified, check = simplify(onnx_model)

assert check, "Simplified ONNX model could not be validated"

# 保存简化后的模型
onnx.save(model_simplified, output_onnx)
```





## 追踪模式

追踪模式（Tracing Mode）是 PyTorch 中的一种特性，它允许你记录模型的前向传播过程，以便在后续的运行中可以重放这个过程。这对于模型的序列化、优化和部署非常有用。

在 PyTorch 中，追踪模式主要用于以下几个方面：

1. **模型序列化**：通过追踪模式，你可以将模型的前向传播过程记录下来，并将其序列化为一个可以被加载和执行的脚本模块。这使得你可以在没有原始 Python 代码的情况下运行模型。
2. **模型优化**：追踪模式可以帮助你分析模型的性能，并进行优化。例如，你可以通过追踪模式找出模型中的瓶颈，并针对性地进行优化。
3. **模型部署**：在部署模型时，追踪模式可以帮助你将模型转换为一种更高效的格式，以便在不同的平台和设备上运行。

追踪模式的工作原理是，当你调用 `torch.jit.trace` 函数时，它会记录模型的前向传播过程，并生成一个可以被序列化和执行的脚本模块。这个脚本模块包含了模型的结构和参数，以及前向传播的逻辑。

在追踪模式下，模型的前向传播过程被记录为一系列的操作，这些操作可以被解释器执行。这意味着，在追踪模式下，模型的前向传播过程是不可变的，你不能在运行时改变模型的结构或参数。
