在Bash脚本中，变量是非常重要的组成部分，用于存储数据并在脚本的不同部分之间传递信息。以下是Bash脚本中变量使用的一些关键点：

1. **变量声明与赋值**：
   - 变量在Bash中不需要事先声明类型，它们默认是字符串类型。
   - 变量赋值的基本语法是 `variable_name=value`，注意等号两边不能有空格。
   - 如果变量值中包含空格或特殊字符，应该用引号包围，例如 `my_var="Hello World"`。
2. **变量引用**：
   - 引用变量使用 `$` 符号，例如 `echo $my_var`。
   - 对于可能未定义的变量，可以使用 `${variable_name:-default}` 形式来提供默认值。
3. **环境变量**：
   - 环境变量可以在整个系统中访问，可以通过 `export` 命令将普通变量提升为环境变量。
   - 例如，`export PATH=$PATH:/new/path`。
4. **数组变量**：
   - Bash 支持一维数组和关联数组（键值对形式）。
   - 创建数组：`my_array=(element1 element2)` 或者 `declare -A assoc_array=(["key"]="value")`。
5. **局部变量与全局变量**：
   - 默认情况下，变量在脚本的整个作用域内都是可见的，除非使用 `local` 关键字在函数内部声明局部变量。
6. **命令替换**：
   - 可以将命令的输出赋值给变量，例如 `output=$(command arg)`。
7. **算术运算**：
   - 使用 `$((expression))` 进行算术运算，例如 `count=$((count + 1))`。
8. **特殊变量**：
   - Bash 提供了一些特殊变量，如 `$0`（脚本名称）、`$1`, `$2`, ...（命令行参数）、`$#`（参数个数）和 `$?`（上一个命令的退出状态）。
9. **字符串操作**：
   - 可以使用 `${variable#pattern}` 和 `${variable##pattern}` 来删除变量值开头的匹配模式。
   - 使用 `${variable%pattern}` 和 `${variable%%pattern}` 来删除变量值结尾的匹配模式。
10. **读取用户输入**：
    - 使用 `read` 命令从标准输入读取一行并将其存储到变量中，例如 `read -p "Enter your name: " name`。

这些是Bash脚本中变量使用的基本概念，掌握它们可以帮助你编写功能丰富且灵活的脚本。



```bash
echo "请输入model_name："
read name 		# 获取用户输出

save_model(){
    local model_name="$1"		# 取第一个参数
    local save_path="$save_dir/$model_name"

    if [ ! -d "$save_path" ]; then
        mkdir -p "$save_path"
        echo "文件夹 $model_name 在 $save_dir 下创建成功。"
    else
        echo "文件夹 $model_name 已经存在。"
    fi

    rsync -avP "$output_model" "$output_log" "$save_path"	# 在rsync命令中传参
}

save_model "$name"
```

```bash
 if [ ! -d "$save_path" ]; then
```

`! -d "$save_path"` 这个表达式的含义是检查 `$save_path` 是否不是一个已存在的目录。这里的 `!` 表示逻辑非，即如果 `$save_path` 不是目录，则条件为真。整个 `if` 语句的意思是：“如果 `$save_path` 不是一个存在的目录，则执行随后的命令。”

也就是 -d 会返回一个布尔值？

可以这样理解，在 Shell 脚本中，`-d` 是一个测试操作符，用于判断给定的文件是否为一个目录。它返回的结果不是布尔值（如 `True` 或 `False`），而是通过退出状态码表示。如果 `$save_path` 指向的是一个存在的目录，则 `-d` 的测试成功，返回 0；否则返回非 0 值。在 `if` 语句中，非 0 值被当作“假”处理，0 被当作“真”。



```bash
mkdir -p "$save_path"
```

这段 Shell 脚本函数使用 `mkdir -p` 命令来创建由 `$save_path` 变量指定的目录。`-p` 选项表示**即使父目录不存在也递归创建所有必要的上级目录**。简而言之，就是确保 `$save_path` 指定的路径作为目录存在