# ai_skill

唐超 (Tangchao) 的 Claude Code 自定义 Skill 集合。

## tc-cpp-style

个人 C++ 编码风格 Skill，主要用于 ROS 2 / rclcpp 开发。核心理念：**名字按 ROS 2 写，缩进按个人风格写。**

- **命名规则 → ROS 2 官方约定**：类/类型 `CamelCase`、函数/变量 `snake_case`、成员变量末尾下划线 (`timer_`)、模板参数 `XxxT` (`MessageT`)、`enum class` 成员 `CamelCase`、宏 `ALL_CAPS`。
- **缩进/排版 → 个人风格**：4 空格缩进、Allman 花括号（左括号独占一行）、访问修饰符在类内缩进、构造函数初始化列表与签名同一行、指针/引用的 `*`/`&` 贴变量名 (`int *ptr`、`int &value`)、`int main (int argc, char *argv[])`。

### 安装

把该目录复制到 Claude Code 的 skills 目录即可：

```bash
# 用户级（对所有项目生效）
cp -r tc-cpp-style ~/.claude/skills/

# 或项目级（仅对某个项目生效）
cp -r tc-cpp-style <你的项目>/.claude/skills/
```

重启 Claude Code 会话后，可用 `/tc-cpp-style` 调用，或在编写 C++ 时自动应用。
