---
name: tc-cpp-style
description: 唐超 (tc) 的 C++ 编码风格，适用于**所有项目**中的任何 C++ 代码。在编写、补全、生成或修改 C++ 代码时使用——包括类、函数、头文件 (.hpp)、main() 入口，以及 ROS 2 节点 (rclcpp) 等。命名规则遵循 ROS 2 官方约定（类/类型 CamelCase、函数/变量 snake_case、成员变量末尾下划线、模板参数 XxxT、enum class 成员 CamelCase）；缩进与排版遵循个人风格：4 空格缩进、Allman 花括号、访问修饰符在类内缩进、构造函数初始化列表与签名同一行、指针/引用的 * 与 & 贴变量名 (int *ptr、int &value)、int main (int argc, char *argv[])。
---

# 唐超 (tc) 的 C++ 编码风格

编写或修改**任何** C++ 代码时都应遵循此风格——**适用于所有项目**，不限于某一个工作区。

本风格是**两部分的组合**——一句话概括：**名字按 ROS 2 写，缩进按你写。**

- **命名规则 → ROS 2 官方约定**（见第 3 节）：类、函数、变量、成员、模板参数等的
  命名，参照 ROS 2 (rclcpp) 源码，例如
  `/opt/ros/humble/include/rclcpp/rclcpp/timer.hpp`。
- **缩进与排版 → 个人风格**（见第 2 节）：缩进、花括号、访问修饰符位置、指针/引用
  写法等，样例基准文件
  `/home/tangchao/ros2_project/chapt3_ws/src/example_topic_rclcpp/src/topic_publisher_01.cpp`。

> ROS 2 的 **API 用法**（继承 `rclcpp::Node`、`SharedPtr` 成员、`RCLCPP_*` 日志、
> `init`/`spin`/`shutdown` 流程）在 ROS 2 项目中照常适用；非 ROS 2 项目忽略这部分即可。
> 命名与排版规则对**所有** C++ 项目都适用。

---

## 风格速览

**命名遵循 ROS 2 官方约定（见第 3 节）。** 排版方面，让代码成为「tc 风格」的标志性
特征：

1. **4 空格缩进**，绝不用 Tab。
2. **Allman 花括号**——每个左花括号 `{` 都独占一行（类、函数、`main`、控制流都一样）。
3. **访问修饰符缩进**：`public:`/`private:` 在类内缩进 4 空格；成员和方法再缩进
   4 空格（共 8 空格）。
4. **构造函数初始化列表与签名同一行**：`TopicPublisher01(std::string name) : Node(name)`。
5. **指针 / 引用的 `*`、`&` 贴变量名**：`int *ptr`、`int &value`、`char *argv[]`。
6. **`main` 写法**：`int main (int argc, char *argv[])`——`main` 后有一个空格。
7. **多用空行**分隔代码块（`public:` 之后、方法之间）。

## 1. 语言与文件基础

- **C++17**。优先使用 `auto`、智能指针 (`std::make_shared`)、`std::bind`/lambda
  作回调、范围 `for`、`nullptr`。
- **文件名**：`snake_case`（下划线小写）。源文件 `.cpp`，头文件 `.hpp`。
- **许可证头 (license header)**：不使用——tc 的学习代码不写许可证头，不要添加。
- 日志 / 字符串字面量里可以用中文（例如 `"%s节点已经启动"`）。

## 2. 排版（遵循个人风格）

- **缩进：4 空格，不用 Tab。**
- **花括号：Allman 风格。** 类、结构体、函数、方法、`main`、命名空间、控制流
  (`if`/`for`/`while`/`switch`) 的左花括号都独占一行。
- **访问修饰符** (`public:` / `private:` / `protected:`) 在类内缩进 **4 空格**；
  类的成员和方法缩进 **8 空格**。
- **构造函数初始化列表**：`: Base(args)` 与构造函数签名保持**同一行**；函数体的
  `{` 放到下一行。
- **指针 / 引用**：`*` 和 `&` 贴着**变量名**写，而不是类型——
  `int *ptr`、`int &value`、`char *argv[]`、`const std::string &name`。
- **`main` 签名**：`int main (int argc, char *argv[])`——`main` 后有一个空格。
- 多用空行分隔逻辑块。

## 3. 命名（遵循 ROS 2 官方约定）

命名规则参照 ROS 2 (rclcpp) 源码。下表的依据可以在
`/opt/ros/humble/include/rclcpp/rclcpp/timer.hpp` 等头文件中直接看到。

| 实体 | 约定 | ROS 2 实例 |
|---|---|---|
| 类 / 结构体 | `CamelCase`（大驼峰，即 PascalCase） | `TimerBase`、`WallTimer`、`GenericTimer` |
| 类型别名 (using / typedef) | `CamelCase` | `SharedPtr`、`UniquePtr`、`VoidCallbackType` |
| 模板参数 | `CamelCase`，通常以 `T` 结尾 | `MessageT`、`AllocatorT`、`CallbackT`、`NodeT` |
| `enum class` 枚举值 | `CamelCase`（**不是**全大写） | `MutuallyExclusive`、`Reentrant`、`Enable` |
| 函数 / 方法 | `snake_case`（下划线小写） | `create_publisher()`、`get_logger()`、`execute_callback()` |
| 布尔查询方法 | `is_` / `has_` 前缀 | `is_ready()`、`is_canceled()`、`is_steady()` |
| 变量 / 函数参数 | `snake_case` | `period`、`callback`、`in_use_state` |
| 成员变量 | `snake_case_`（**末尾下划线**） | `clock_`、`callback_`、`timer_handle_` |
| 命名空间 | `snake_case` | `rclcpp`、`rclcpp::function_traits` |
| 宏 / C 级常量 | `ALL_CAPS`（全大写下划线） | `RCLCPP_INFO`、`RCL_RET_OK` |

要点提醒：

- **函数和方法一律 `snake_case`**——这是 ROS 2 风格的显著特征（例如
  `time_until_trigger()`、`exchange_in_use_by_wait_set_state()`）。
- **成员变量一律加末尾下划线**：`publisher_`、`count_`、`timer_`。
- 注意区分两类「枚举 / 常量」：C++ 的 `enum class` 枚举值用 `CamelCase`；而来自 C 层
  (rcl / rmw) 的宏常量用 `ALL_CAPS`，例如 `RCL_STEADY_TIME`。

## 4. include 顺序

标准库 / 第三方库头文件在前，ROS / 项目头文件在后，中间空一行：

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"
```

## 5. 头文件 (.hpp)

- 用**头文件保护宏** (include guard)，不用 `#pragma once`：全大写路径，包名与文件名
  之间用双下划线，末尾再加一个下划线。
- **命名空间内容要缩进** 4 空格（个人风格）：

```cpp
#ifndef EXAMPLE_TOPIC__TOPIC_PUBLISHER_01_HPP_
#define EXAMPLE_TOPIC__TOPIC_PUBLISHER_01_HPP_

#include "rclcpp/rclcpp.hpp"

namespace example_topic
{

    class TopicPublisher01 : public rclcpp::Node
    {
        public:

            TopicPublisher01(std::string name);
            ~TopicPublisher01() = default;

        private:

            /*  */

    };

}  // namespace example_topic

#endif  // EXAMPLE_TOPIC__TOPIC_PUBLISHER_01_HPP_
```

## 6. ROS 2 节点写法（在 ROS 2 项目中适用）

- 继承 `rclcpp::Node`；在初始化列表里把节点名传给 `Node(...)`。
- 实体存为带末尾下划线的 `SharedPtr` 成员：
  `rclcpp::Publisher<T>::SharedPtr publisher_;`、
  `rclcpp::TimerBase::SharedPtr timer_;`。
- 用 `this->create_publisher<>()`、`create_subscription<>()`、
  `create_wall_timer()` 等创建实体。
- 用 `RCLCPP_INFO/WARN/ERROR(this->get_logger(), ...)` 打日志，不用 `std::cout`。
- 标准 `main`：`init` → `spin(std::make_shared<NodeType>(...))` → `shutdown`。

## 7. 注释

- `//` 写行注释，`/* ... */` 写块注释。空白区段里放 `/*  */` 占位是可以的。
- 注释要解释**为什么**，而不是显而易见的**做了什么**。

---

## 标准模板（照这个形状写）

一个完整的发布者 (publisher)。**命名是 ROS 2 风格**（类 `CamelCase`、方法
`snake_case`、成员末尾下划线），**排版是个人风格**（4 空格缩进、缩进的
`public:`/`private:`、与签名同一行的初始化列表、Allman 花括号、指针/引用贴变量名、
`main` 的写法）。

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

class TopicPublisher01 : public rclcpp::Node
{
    public:

        TopicPublisher01(std::string name) : Node(name)
        {
            RCLCPP_INFO(this->get_logger(), "%s节点已经启动", name.c_str());
            publisher_ = this->create_publisher<std_msgs::msg::String>("chatter", 10);
            timer_ = this->create_wall_timer(
                500ms, std::bind(&TopicPublisher01::timer_callback, this));
        }

        ~TopicPublisher01() = default;

    private:

        void timer_callback()
        {
            auto message = std_msgs::msg::String();
            message.data = "Hello, world! " + std::to_string(count_++);
            RCLCPP_INFO(this->get_logger(), "发布消息：%s", message.data.c_str());
            publisher_->publish(message);
        }

        rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
        rclcpp::TimerBase::SharedPtr timer_;
        size_t count_ = 0;
};

int main (int argc, char *argv[])
{
    rclcpp::init(argc, argv);
    auto node = std::make_shared<TopicPublisher01>("topic_publisher_01");
    rclcpp::spin(node);
    rclcpp::shutdown();
    return 0;
}
```
