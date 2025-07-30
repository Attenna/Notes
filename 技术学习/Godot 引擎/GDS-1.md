# 变量 
```python
var a = 1
var avc = 1
var a1 = 1
var _a = 11
var 1a//error
```

```python
var a = 1
var b = 1.1
var c = "hello"
var d = true
var e = false#允许有布尔值
var x :String = "hello"#字符串可以拼接
var y :float = 1.1
var z :bool = false#布尔值可以和数据进行转换，true代表非0
```
# 函数
```python
func _enter_tree():
	_a = a+1
	print(a)
	print(_a)
	pass#类似python，缩进敏感
```