---
layout: post
title: "Daily Reading Note #1"
date: 2017-01-17 23:16:40 +0800
comments: true
categories: 
---
这里记录了每天阅读代码记录的新知识。

### List.keymember?/3
用来检查 Keyword List 中有没有对应的 key / value：
```elixir
iex> List.keymember?([a: 1, b: 2], :a, 0)
true
iex> List.keymember?([a: 1, b: 2], 2, 1)
true
iex> List.keymember?([a: 1, b: 2], :c, 0)
false
```

### :code.where_is_file/1
可以从 load_paths 中找到 beam 文件
```elixir
iex> :code.where_is_file('Elixir.Kernel.beam')
'/usr/local/bin/../lib/elixir/ebin/Elixir.Kernel.beam'
```
### Code.prepend_path/1
将一个路径加入 Elixir 的 load_paths

### Code.eval_string/3
执行一段代码，并返回结果，以及结果 binding
```elixir
iex> Code.eval_string "b = a + 1", [a: 1], file: __ENV__.file, line: __ENV__.line
{2, [a: 1, b: 2]}
```
### Keyword.get_values/2
获取关键字列表中某个 key 对应的所有值，很适合用来获取参数
```elixir
iex> Keyword.get_values [path: "a", path: "b/c"], :path
["a", "b/c"]
```
### :binary.last/1` 或 `String.last/1
获取字符串的最后一个字符

### Kernel.struct/2
适合留下 struct 合法的 key，丢弃不合法的 key
```elixir
iex> defmodule User do
...>  defstruct name: nil
...> end
...> struct %User{name: "qhwa"}, %{name: "Billy", age: 10}
%User{name: "Billy"}
```
### Code.ensure_loaded?/1
可以判断一个 Module 是否已经加载进来了
### Path.wildcard/1
等于 Ruby 的 `Dir.glob`
### Path.basename/2
和 Ruby 一样，可以用来去掉扩展名
### Kernel.function_exported?/3
判断一个模块是否暴露了方法名
```elixir
iex> function_exported? Kernel, :struct, 2
true
```
`Code.get_docs/2`
如果编译时有 `--docs` 选项（默认是有的），可以从模块中得到文档。返回 `{line, text}`
```elixir
iex> Code.get_docs Code, :moduledoc
{2,
 "Utilities for managing code compilation, code evaluation and code loading.\n\nThis module complements Erlang's [`:code` module](http://www.erlang.org/doc/man/code.html)\nto add behaviour which is specific to Elixir. Almost all of the functions in this module\nhave global side effects on the behaviour of Elixir.\n"}
```
### Enum.at/1
### module.__info__(:compile)
能获取一些编译信息
```elixir
iex> Code.__info__(:compile)
[options: [:debug_info], version: '6.0.1', time: {2017, 1, 5, 10, 33, 52},
 source: '/Users/jose/OSS/elixir/lib/elixir/lib/code.ex']
```

### Kernel.Typespec.beam_specs/1
可以获取一个模块的类型信息
```elixir
iex> Kernel.Typespec.beam_specs(Code)
 ...
```

### 如何在管道中用 `||`
```elixir
a |> func() |> Kernel.||([]) |> IO.inspect
```
