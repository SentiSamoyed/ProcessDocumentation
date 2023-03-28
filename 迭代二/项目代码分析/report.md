# CheckStyle结果统计与分析报告

+ 杜威 201830006
+ 陈骏 201250068
+ 徐浩钦 201250067

## 1 报告间的差异

> 比如：第一次提交与第二次提交的报告之间的警告类型、优先级、警告数量等属性差异分析



## 2 警告数量类型与数量

> 统计修改的（closed）、新增的（new）、一直存在的（open）的 checkstyle 中警告 （包括警告的属性、数量等）



## 3 警告的修改

> 举例说明修改的警告，即原来的警告是怎样的，说明是如何修改的。警告例子不少于 5 个，且警告例子要有多样性（即覆盖不同类型的规则）

### 3.1 Javadoc Comments



### 3.2 Imports

**3.2.1 AvoidStarImport**

警告内容：不应该使用 ''.*'' 形式的导入。修改前：

```java
import java.io.*;
```

应该将使用的类一一导入，而不是直接导入io包的全部内容。修改为：

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
// etc.
```

### 3.3 Block Checks



### 3.4 Size Violations



### 3.5 Whitespace



---

以下为加分点

## 4 checkstyle工具的缺陷

> 统计 checkstyle 工具本身的缺陷数量，并举例分析 checkstyle 工具本身的缺陷产生的原因

### 4.1 SummaryJavadoc

警告内容为：Javadoc的第一句缺少一个结束时期。报错代码如下：

```java
/**
 * 单词正确拼写列表。该类用于检测语句中的单词是否正确。<br/>
 *
 * @see ClassificationOptions
 */
```

将句号改为`.`之后，该警告消失。因此，该警告可能是因为checkstyle工具只能够识别英文语句的结束符，而无法识别中文的句号。

## 5 新增警告的处理 

> 举例分析新增的警告，是因为什么原因引起的，为什么修改，或为什么不修改



## 6 checkstyle漏报的缺陷

> 统计 checkstyle 漏报的缺陷数量（即 checkstyle 没有报告但是开发人员认为是一个缺陷，例如：功能缺陷），并举例分析 checkstyle 漏报的缺陷产生的原因

### 6.1 冗余的StringBuilder和toString()

```java
System.out.println((new StringBuilder("Could not find emoticon file: ")).append(sSourceFile).toString());
```

在如上源代码中，StringBuilder的调用是没有必要的。因为在String + String这样的字符串拼接时，String类源码中其实还是调用了StringBuilder的append()方法。可以改为如下形式，这样写简洁并且可读性更好。

```java
System.out.println("Could not find emoticon file: " + sSourceFile);
```

checkstyle可能认为StringBuilder是字符串拼接的标准做法，并没有考虑到代码实际的运行逻辑。

### 6.2 ==和equals()

```java
if (sLine != "")
```

在如上代码中，使用==和!=来比较字符串是否相等是存在缺陷的，应该使用String的equals()方法：

```java
if (!sLine.equals(""))
```

checkstyle作为代码静态分析工具，可能没有考虑到字符串比较可能带来的漏洞，而只是单纯检查书写格式等基本代码规范。

### 6.3 在循环中的字符串拼接

```java
String sTranslated = "";
for (int i = 1; i <= this.igSentenceCount; ++i) {
	sTranslated = sTranslated + this.sentence[i].getTranslatedSentence();
}
return sTranslated;
```

在如上代码中，使用了循环中的字符串串联 '+' ，应该改为StringBuilder和append()。

```java
StringBuilder sTranslated = new StringBuilder();
for (int i = 1; i <= this.igSentenceCount; ++i) {
	sTranslated.append(this.sentence[i].getTranslatedSentence());
}
return sTranslated.toString();
```

