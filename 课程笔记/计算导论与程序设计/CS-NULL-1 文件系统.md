# Reading from and Writing to Text Files

加上文件指针，就可以做到从文件里读，从文件里写。

---

## Reading from a Text File

```c
int fputc ( int ch, FILE *fp );
```

### Write a character to the file 写入文件的字符流程

- Create a new file buffer (open with mode `w` / `w+`)
    
- Load file block to the file buffer (open with mode `a` / `a+` / `r+`)
    
- Internally, the character is converted to `unsigned char` just before being written.
    
- Move the file position indicator forward 1 byte.
    
- Returns `EOF` (End of File) if a write error occurs.
    

### 示例：写字符到文件

```c
#include <stdio.h>

int main() {
	FILE *fp = fopen("out.txt", "w");
	if (!fp) {
		return -1;
	}
	
	printf("Input something (Ctrl+D to end):\n");
	char ch;
	while ((ch = getchar()) != EOF) {
		fputc(ch, fp);
	}
	fclose(fp);
	return 0;
}
```

---

## Read from a Text File

```c
int fgetc(FILE *fp);
```

- `fgetc(stdin)` 相当于 `getchar()`
    
- `fputc(ch, stdout)` 相当于 `putchar(ch)`
    

标准流：

- 标准输入流：`stdin`
    
- 标准输出流：`stdout`
    

### 示例：读取文件内容并打印

```c
#include <stdio.h>

int main() {
	FILE *fp = fopen("out.txt", "r");
	if (!fp) {
		return -1;
	}
	
	char ch;
	while ((ch = fgetc(fp)) != EOF) {
		putchar(ch);
	}
	fclose(fp);
	return 0;
}
```

---

## 有 open 就要有 close，这是好习惯

malloc 和 free 一样，开了就要关。C++ 同理。  
资源管理必须配对，避免内存泄漏或文件句柄泄露。

---

## Read a Line from File

```c
char *fgets(char *str, int n, FILE *stream);
```

- 从指定的 `stream` 中读取最多 `n-1` 个字符（最后一个字符留给 `\0`）
    
- 直到遇到换行符、EOF 或读取了 `n-1` 个字符
    
- 常用于按行读取文本文件
    

### 示例：读取并打印一行

```c
char buffer[100];
fgets(buffer, 100, fp);
printf("%s", buffer);
```

---

## Write a Line to File

```c
int fputs(const char *str, FILE *stream);
```

- 将字符串写入指定的文件流中
    
- 不会自动在末尾添加换行符
    

### 示例：写入字符串

```c
fputs("Hello, world!\n", fp);
```

---

## Compress App 示例片段

```c
char c = 0;
char ch = 0;
int count = 0;

while (!feof(fpSrc) && (c = fgetc(fpSrc)) != EOF) {
	// 执行压缩逻辑，比如统计连续字符数量等
}
```

---

## 软件工程（Software Engineering）

1. 需求分析（Requirements Analysis）
    
2. 初步设计（Preliminary Design）
    
3. 详细设计（Detailed Design）
    

**思考题：** 百度的大模型、自动驾驶为何失败？

- 你是不是真的热爱你在做的事？
    
- 不要幻想“有人能替我干”。
    
- 劳动者欺骗资本家，是必然的？值得思考。
    

---

## Reading from and Writing to Binary Files

```c
size_t fread(void *buffer, size_t size, size_t count, FILE *stream);
size_t fwrite(const void *buffer, size_t size, size_t count, FILE *stream);
```

- `fread()` 从文件中读取二进制数据
    
- `fwrite()` 向文件写入二进制数据
    
- `size` 是每个元素的大小，`count` 是要读/写的元素个数
    

---

## 顺序读写 vs 随机读写

### 顺序读写（Sequential Access）：

- 文件内容从头到尾读取或写入
    
- 常用于大多数普通文件操作
    

### 随机读写（Random Access）：

```c
int fseek(FILE *stream, long offset, int origin);
long ftell(FILE *stream);
void rewind(FILE *stream);
```

- `fseek()` 设定文件位置指示器（类似跳转）
    
- `ftell()` 获取当前文件指针位置
    
- `r7ewind()` 重置文件指针到文件开始位置
    

---

## 文件打开模式（File Open Modes）

|Text Mode|Binary Mode|Meaning|
|---|---|---|
|`"r"`|`"rb"`|只读|
|`"w"`|`"wb"`|只写（覆盖原文件）|
|`"a"`|`"ab"`|追加写入|
|`"r+"`|`"rb+"`|读写，文件必须存在|
|`"w+"`|`"wb+"`|读写，创建新文件|
|`"a+"`|`"ab+"`|读写，追加到文件末尾|
