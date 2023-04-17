# CheckStyle 结果统计与分析报告

[TOC]

## 1 报告间的差异

### 1.1 警告数量

第一次报告中的警告数量为 5439，最后一次报告中的警告数量为 1534。在利用 checkstyle 对代码进行修改后，警告数量大幅减少，代码风格更符合规范。

### 1.2 警告类型

在最后一次报告中，第一次报告中最长出现的 Coding, Block Checks 类型错误全部被改正了。最后仍然存在的警告类型一般是两种：变量命名警告、本行字符数超过 100 个警告。经过讨论后决定暂不修改变量名。

| 警告类型                                         | 修改前数量 | 修改后数量 |
| ------------------------------------------------ | ---------- | ---------- |
| indentation.IndentationCheck                     | 1557       | 1          |
| blocks.NeedBracesCheck                           | 352        | 0          |
| whitespace.WhitespaceAroundCheck                 | 504        | 0          |
| whitespace.WhitespaceAfterCheck                  | 592        | 0          |
| naming.AbbreviationAsWordInNameCheck             | 74         | 71         |
| naming.LocalVariableNameCheck                    | 434        | 427        |
| sizes.LineLengthCheck                            | 520        | 423        |
| blocks.LeftCurlyCheck                            | 428        | 0          |
| naming.ParameterNameCheck                        | 242        | 242        |
| javadoc.RequireEmptyLineBeforeBlockTagGroupCheck | 143        | 0          |
| javadoc.SummaryJavadocCheck                      | 353        | 352        |
| RightCurlySame                                   | 61         | 0          |
| imports.CustomImportOrderCheck                   | 20         | 1          |
| imports.AvoidStarImportCheck                     | 12         | 0          |
| whitespace.OperatorWrapCheck                     | 20         | 0          |
| ArrayTypeStyleCheck                              | 121        | 0          |
| coding.OverloadMethodsDeclarationOrderCheck      | 5          | 0          |
| naming.MethodNameCheck                           | 4          | 2          |
| coding.VariableDeclarationUsageDistanceCheck     | 13         | 4          |
| blocks.EmptyCatchBlockCheck                      | 3          | 0          |
| whitespace.EmptyLineSeparatorCheck               | 6          | 0          |
| naming.MemberNameCheck                           | 6          | 6          |
| javadoc.NonEmptyAtclauseDescriptionCheck         | 1          | 0          |
| javadoc.JavadocTagContinuationIndentationCheck   | 3          | 3          |
| coding.MultipleVariableDeclarationsCheck         | 3          | 0          |
| coding.MissingSwitchDefaultCheck                 | 1          | 0          |
| AvoidEscapedUnicodeCharactersCheck               | 1          | 1          |

## 2 警告数量类型与数量

> 统计修改的（closed）、新增的（new）、一直存在的（open）的 checkstyle 中警告 （包括警告的属性、数量等）

| 警告类型                            | closed | open | new |
| ----------------------------------- | ------ | ---- | --- |
| Indentation                         | 1556   | 1    | 0   |
| NeedBraces                          | 352    | 0    | 0   |
| WhitespaceAround                    | 504    | 0    | 0   |
| WhitespaceAfter                     | 592    | 0    | 0   |
| AbbreviationAsWordInName            | 3      | 71   | 0   |
| LocalVariableName                   | 7      | 427  | 0   |
| LineLength                          | 97     | 423  | 0   |
| LeftCurly                           | 428    | 0    | 0   |
| ParameterName                       | 0      | 242  | 0   |
| RequireEmptyLineBeforeBlockTagGroup | 143    | 0    | 0   |
| SummaryJavadoc                      | 353    | 0    | 0   |
| RightCurlySame                      | 61     | 0    | 0   |
| CustomImportOrder                   | 19     | 1    | 0   |
| AvoidStarImport                     | 12     | 0    | 0   |
| OperatorWrap                        | 20     | 0    | 0   |
| ArrayTypeStyle                      | 121    | 0    | 0   |
| OverloadMethodsDeclarationOrder     | 5      | 0    | 0   |
| MethodName                          | 2      | 2    | 0   |
| VariableDeclarationUsageDistance    | 9      | 4    | 0   |
| EmptyCatchBlock                     | 3      | 0    | 0   |
| EmptyLineSeparator                  | 6      | 0    | 0   |
| MemberName                          | 0      | 6    | 0   |
| NonEmptyAtclauseDescription         | 1      | 0    | 0   |
| JavadocTagContinuationIndentation   | 0      | 3    | 0   |
| MultipleVariableDeclarations        | 3      | 0    | 0   |
| MissingSwitchDefault                | 1      | 0    | 0   |
| AvoidEscapedUnicodeCharacters       | 0      | 1    | 0   |

## 3 警告的修改

> 举例说明修改的警告，即原来的警告是怎样的，说明是如何修改的。警告例子不少于 5 个，且警告例子要有多样性（即覆盖不同类型的规则）

### 3.1 Javadoc Comments

#### 3.1.1 RequireEmptyLineBeforeBlockTagGroup

警告内容：Javadoc tag @param 等 tag 前面应该有一行空行。修改前：

```java
/**
   * Description
   * @param param_test 参数一
   */
```

应该在描述内容和 tag 中间添加空行。修改后：

```java
/**
   * Description
   *
   * @param param_test 参数一
   */
```

#### 3.1.2 NonEmptyAtclauseDescription

警告内容：@标签应有非空说明。修改前

```java
  /**
   * 获取习语的情感值。<br>
   *
   * @param sPhrase 习语
   * @return 情感值
   * @deprecated
   */
```

修改后：

```java
  /**
   * 获取习语的情感值。<br>
   *
   * @param sPhrase 习语
   * @return 情感值
   * @deprecated 已弃用
   */
```

### 3.2 Imports

#### 3.2.1 AvoidStarImport

警告内容：不应该使用 ''.\*'' 形式的导入。修改前：

```java
import java.io.*;
```

应该将使用的类一一导入，而不是直接导入 io 包的全部内容。修改为：

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
// etc.
```

#### 3.2.2 CustomImportOrder

**3.2.2.1**

警告内容：导入语句字典序错误。修改前：

```java
import java.io.FileNotFoundException;
import java.io.FileInputStream;
import java.io.FileOutputStream;
```

应该根据字典序排列导入顺序。修改后：

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
```

**3.2.2.2**

警告内容：导入组之前的额外空行。修改前：

```java
import java.io.OutputStreamWriter;

import uk.ac.wlv.utilities.FileOps;
```

应该删去空行。修改后：

```java
import java.io.OutputStreamWriter;
import uk.ac.wlv.utilities.FileOps;
```

### 3.3 Block Checks

#### 3.3.1 NeedBraces

警告内容：if/else/for 结构必须使用大括号{}。修改前：

```java
if (resources == null && !resources.initialise(options))
    return false;
```

给仅有一条语句的 if/else/fro block 添加大括号。修改后：

```java
if (resources == null && !resources.initialise(options)) {
	return false;
}
```

#### 3.3.2 EmptyCatchBlock

警告内容：空 catch 块。修改前：

```java
catch (NumberFormatException numberformatexception) {
}
```

修改后：

```java
catch (NumberFormatException numberformatexception) {
	numberformatexception.printStackTrace();
}
```

### 3.4 Whitespace

#### 3.4.1 OperatorWrap

警告内容：‘+’应该另起一行

```java
 wWriter.write("\t" + iMultiOptimisations +
          "\t" + this.bgReduceNegativeEmotionInQuestionSentences +
          "\t" + this.bgMissCountsAsPlus2 +
		// etc.
);
```

将'+'另起一行。修改后：

```java
wWriter.write("\t" + iMultiOptimisations
		+ "\t" + this.bgReduceNegativeEmotionInQuestionSentences
		+ "\t" + this.bgMissCountsAsPlus2
 		+ "\t" + this.bgYouOrYourIsPlus2UnlessSentenceNegative
		+ "\t" + this.bgExclamationInNeutralSentenceCountsAsPlus2
 		+ "\t" + this.bgUseIdiomLookupTable
		+ "\t" + this.igMoodToInterpretNeutralEmphasis
		// etc.
);
```

### 3.5 Miscellaneous

#### 3.5.1 ArrayTypeStyle

警告内容：数组大括号位置错误。修改前：

```java
int igNegClass[];
```

将 C 风格数组修改为 Java 风格

```java
int[] igNegClass;
```

### 3.6 Coding

#### 3.6.1 VariableDeclarationUsageDistance

警告内容：变量‘wTermStrengthWriter’声明及第一次使用距离 4 行（最多：3 行）。若需存储该变量的值，请将其声明为 final 的。3 行为 google_checks 定义。修改前：

```java
BufferedWriter wResultsWriter = new BufferedWriter(new FileWriter(sOutFileName));
BufferedWriter wTermStrengthWriter = new BufferedWriter(new FileWriter((new StringBuilder(String.valueOf(FileOps.s_ChopFileNameExtension(sOutFileName)))).append("_termStrVars.txt").toString()));
if (igPosClass == null || igPosClass.length < igPosCorrect.length) {
	igPosClass = new int[igParagraphCount + 1];
	igNegClass = new int[igParagraphCount + 1];
	igTrinaryClass = new int[igParagraphCount + 1];
}
options.printClassificationOptionsHeadings(wResultsWriter);
```

将 BufferedWriter 在调用前声明。修改后：

```java
BufferedWriter wResultsWriter = new BufferedWriter(new FileWriter(sOutFileName));
BufferedWriter wTermStrengthWriter = new BufferedWriter(new FileWriter((new StringBuilder(String.valueOf(FileOps.s_ChopFileNameExtension(sOutFileName)))).append("_termStrVars.txt").toString()));
options.printClassificationOptionsHeadings(wResultsWriter);
```

#### 3.6.2 OverloadMethodsDeclarationOrder

警告内容：所有的重载方法都应该相邻放置。在相同类型的重载方法之间放置非重载方法是违反的。修改前：

```java
public boolean setSentiment(String sWord, int iNewSentiment) {
	...
}

// 其他非重载方法
...

public void setSentiment(int iWordID, int iNewSentiment) {
    ...
}
```

修改后：

```java
public boolean setSentiment(String sWord, int iNewSentiment) {
	...
}

public void setSentiment(int iWordID, int iNewSentiment) {
    ...
}
```

#### 3.6.3 MissingSwitchDefault

警告内容：Switch 块未定义 default。修改前：

```java
switch (iLastCharType) {
        case 1:
          this.codeWord(sWordAndPunctuation);
          break;
        case 2:
          this.codePunctuation(sWordAndPunctuation);
          break;
      }
```

修改后：

```java
switch (iLastCharType) {
        case 1:
          this.codeWord(sWordAndPunctuation);
          break;
        case 2:
          this.codePunctuation(sWordAndPunctuation);
          break;
        default:
          throw new IllegalStateException("Unexpected value: " + iLastCharType);
      }
```

## 4 checkstyle 工具的缺陷

> 统计 checkstyle 工具本身的缺陷数量，并举例分析 checkstyle 工具本身的缺陷产生的原因

### 4.1 SummaryJavadoc

警告内容为：Javadoc 的第一句缺少一个结束时期。报错代码如下：

```java
/**
 * 单词正确拼写列表。该类用于检测语句中的单词是否正确。<br/>
 *
 * @see ClassificationOptions
 */
```

将句号改为`.`之后，该警告消失。因此，该警告可能是因为 checkstyle 工具只能够识别英文语句的结束符，而无法识别中文的句号。

### 4.2 WhitespaceAround

警告内容为：‘{’ is not followed by whitespace.Empty Blocks may only be represented as {} when not part of a multi-block statement(4.1.3)。

```java
if (sData.length > iTextCol) {// TODO
	Paragraph paragraph = new Paragraph();
    // code
}
```

将// TODO 换行或添加空格，该警告消失，因此 checkstyle 工具不能识别紧跟语句的注释

### 4.3 WhitespaceAfter

警告内容为：';'后应有空格。修改前：

```java
iFileTrinary = Integer.parseInt(sData[0].trim());// 以制表符分割的第一个字符串
```

逻辑同 4.2，checkstyle 不能有效识别注释

## 5 新增警告的处理

> 举例分析新增的警告，是因为什么原因引起的，为什么修改，或为什么不修改

### 5.1 CustomImportOrder

由于将 import \_.\*转化为具体的类之后，未考虑其字典序，在修正 import 顺序为字典序之后，该警告消失。

### 5.2 ParamterName&&LocalVariableName

由于 SentiStrength 源码的变量声明没有采用驼峰命名法，将变量类型以缩写（String->s，int->i，float->f）添加在变量名称前面，整体项目中风格统一，不进行修改。

### 5.3 AbbreviationAsWordInName

由于变量声明中存在多于一个的连续大写字母，如 ID 等，认为是专有名词缩写，不进行修改。

### 5.4 LineLength

由于代码的逻辑过于复杂，块嵌套，变量命名复杂导致一行代码内容较长。修改逻辑与命名会影响代码可读性，不进行修改。

## 6 checkstyle 漏报的缺陷

> 统计 checkstyle 漏报的缺陷数量（即 checkstyle 没有报告但是开发人员认为是一个缺陷，例如：功能缺陷），并举例分析 checkstyle 漏报的缺陷产生的原因

### 6.1 冗余的 StringBuilder，toString()和 String.valueof

```java
String sTempFile = (new StringBuilder(String.valueOf(sInputFile))).append("_temp").toString();
```

在如上源代码中，StringBuilder 的调用是没有必要的。因为在 String + String 这样的字符串拼接时，String 类源码中其实还是调用了 StringBuilder 的 append()方法。同时 sInputFile 本身就是 String 类，不需要再显式调用 String.valueof，可以改为如下形式，这样写简洁并且可读性更好。

```java
String sTempFile = sInputFile + "_temp";
```

checkstyle 可能认为 StringBuilder 是字符串拼接的标准做法，并没有考虑到代码实际的运行逻辑。

### 6.2 ==和 equals()

```java
if (sLine != "")
```

在如上代码中，使用==和!=来比较字符串是否相等是存在缺陷的，应该使用 String 的 equals()方法：

```java
if (!sLine.equals(""))
```

checkstyle 作为代码静态分析工具，可能没有考虑到字符串比较可能带来的漏洞，而只是单纯检查书写格式等基本代码规范。

### 6.3 在循环中的字符串拼接

```java
String sTranslated = "";
for (int i = 1; i <= this.igSentenceCount; ++i) {
	sTranslated = sTranslated + this.sentence[i].getTranslatedSentence();
}
return sTranslated;
```

在如上代码中，使用了循环中的字符串串联 '+' ，应该改为 StringBuilder 和 append()。

```java
StringBuilder sTranslated = new StringBuilder();
for (int i = 1; i <= this.igSentenceCount; ++i) {
	sTranslated.append(this.sentence[i].getTranslatedSentence());
}
return sTranslated.toString();
```

### 6.4 重复的异常捕捉

```java
try {
      BufferedWriter wWriter = new BufferedWriter(new FileWriter(sOutFilenameAndPath));
      wWriter.write("Correct+\tCorrect-\tPredict+\tPredict-\tText\n");
      for (int i = 1; i <= igParagraphCount; i++) {
        if (bgSupcorpusMember[i]) {
          wWriter.write((new StringBuilder(String.valueOf(igPosCorrect[i]))).append("\t").append(igNegCorrect[i]).append("\t").append(igPosClass[i]).append("\t").append(igNegClass[i]).append("\t").append(paragraph[i].getTaggedParagraph()).append("\n").toString());
        }
      }
      wWriter.close();
    } catch (FileNotFoundException e) {
      e.printStackTrace();
      return false;
    } catch (IOException e) {
      e.printStackTrace();
      return false;
    }
}
```

上述代码中，FileNotFoundException 和 IOException 的异常捕获之后的逻辑完全相同，且 FileNotFoundException 为 IOException 的子类，因此 FileNotFoundException 是完全多余的，CheckStyle 作为代码静态分析工具，不对异常的冗余逻辑进行检查。

### 6.5 EmptyBlock

```java
for (int i = 1; i <= igParagraphCount; i++) {
	boolean _tmp = bgSupcorpusMember[i];
	// TODO 此处循环只做了局部变量的声明，没有进行其他操作
}
```

上述代码中，for 循环体内仅作了局部变量的声明，没有任何其他操作，其实是一个空循环块，CheckStyle 对 EmptyBlock 的检查仅检查块内是否有语句，不检查语句是否为变量声明。

### 6.5 函数返回

```java
  public void run10FoldCrossValidationMultipleTimes(int iMinImprovement, boolean bUseTotalDifference, int iReplications, int iMultiOptimisations, String sOutFileName) {
    try {
      BufferedWriter wWriter = new BufferedWriter(new FileWriter(sOutFileName));
      BufferedWriter wTermStrengthWriter = new BufferedWriter(new FileWriter(FileOps.s_ChopFileNameExtension(sOutFileName) + "_termStrVars.txt"));
      options.printClassificationOptionsHeadings(wWriter);
      writeClassificationStatsHeadings(wWriter);
      options.printClassificationOptionsHeadings(wTermStrengthWriter);
      resources.sentimentWords.printSentimentTermsInSingleHeaderRow(wTermStrengthWriter);
      run10FoldCrossValidationMultipleTimes(iMinImprovement, bUseTotalDifference, iReplications, iMultiOptimisations, wWriter, wTermStrengthWriter);
      wWriter.close();
      wTermStrengthWriter.close();
    } catch (IOException e) {
      e.printStackTrace();
      return;
    }
  }
```

return 作为 void 函数的最后一条语句时是冗余的，CheckStyle 并不对此进行检查

### 6.6 index0f(" ") >= 0 和 contains(" ")

```java
if (sLine.indexOf(" ") >= 0)
```

在上述代码中用 indexof 的效率是不如 contains 的，应该使用 contains，这种缺陷源于 CheckStyle 仅作代码格式的检查。

### 6.7 字符集参数设定

```java
rReader = new BufferedReader(new InputStreamReader(new FileInputStream(sFilename), "UTF8"));
```

Java 在传递编码格式时可以使用 Java 的 StandardCharsets，而不通过字符串指定。可修改为：

```java
rReader = new BufferedReader(new InputStreamReader(new FileInputStream(sFilename), StandardCharsets.UTF_8));
```

### 6.8 大量嵌套 if-else 语句

```java
if (sData[0].equals("EmotionParagraphCombineMethod")) {
	if (sData[1].contains("Max")) {
		this.igEmotionParagraphCombineMethod = 0;
    }
    if (sData[1].contains("Av")) {
    	this.igEmotionParagraphCombineMethod = 1;
   	}
 	if (sData[1].contains("Tot")) {
      	this.igEmotionParagraphCombineMethod = 2;
 	}
} else if (sData[0].equals("EmotionSentenceCombineMethod")) {
    if (sData[1].contains("Max")) {
        this.igEmotionSentenceCombineMethod = 0;
	}
	if (sData[1].contains("Av")) {
   		this.igEmotionSentenceCombineMethod = 1;
    	}
	if (sData[1].contains("Tot"))
        this.igEmotionSentenceCombineMethod = 2;
	}
} else if (sData[0].equals("IgnoreNegativeEmotionInQuestionSentences")) {
    this.bgReduceNegativeEmotionInQuestionSentences = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("MissCountsAsPlus2")) {
    this.bgMissCountsAsPlus2 = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("YouOrYourIsPlus2UnlessSentenceNegative")) {
    this.bgYouOrYourIsPlus2UnlessSentenceNegative = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("ExclamationCountsAsPlus2")) {
    this.bgExclamationInNeutralSentenceCountsAsPlus2 = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("UseIdiomLookupTable")) {
    this.bgUseIdiomLookupTable = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("Mood")) {
    this.igMoodToInterpretNeutralEmphasis = Integer.parseInt(sData[1]);
} else if (sData[0].equals("AllowMultiplePositiveWordsToIncreasePositiveEmotion")) {
    this.bgAllowMultiplePositiveWordsToIncreasePositiveEmotion = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("AllowMultipleNegativeWordsToIncreaseNegativeEmotion")) {
    this.bgAllowMultipleNegativeWordsToIncreaseNegativeEmotion = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("IgnoreBoosterWordsAfterNegatives")) {
    this.bgIgnoreBoosterWordsAfterNegatives = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("MultipleLettersBoostSentiment")) {
            this.bgMultipleLettersBoostSentiment = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("BoosterWordsChangeEmotion")) {
            this.bgBoosterWordsChangeEmotion = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("NegatingWordsFlipEmotion")) {
	this.bgNegatingWordsFlipEmotion = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("NegatingWordsFlipEmotion")) {
    this.bgNegatingPositiveFlipsEmotion = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("NegatingWordsFlipEmotion")) {
    this.bgNegatingNegativeNeutralisesEmotion = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("CorrectSpellingsWithRepeatedLetter")) {
    this.bgCorrectSpellingsWithRepeatedLetter = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("UseEmoticons")) {
    this.bgUseEmoticons = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("CapitalsAreSentimentBoosters")) {
    this.bgCapitalsBoostTermSentiment = Boolean.parseBoolean(sData[1]);
} else if (sData[0].equals("MinRepeatedLettersForBoost")) {
    this.igMinRepeatedLettersForBoost = Integer.parseInt(sData[1]);
} else if (sData[0].equals("WordsBeforeSentimentToNegate")) {
    this.igMaxWordsBeforeSentimentToNegate = Integer.parseInt(sData[1]);
} else if (sData[0].equals("Trinary")) {
    this.bgTrinaryMode = true;
} else if (sData[0].equals("Binary")) {
    this.bgTrinaryMode = true;
    this.bgBinaryVersionOfTrinaryMode = true;
} else {
    if (!sData[0].equals("Scale")) {
        rReader.close();
        return false;
    }
    this.bgScaleMode = true;
}
```

CheckStyle 对变量声明之后的第一次调用距离报错，同时对于 if-else 中重复出现的条件，如上例中的`sData[0].equals("NegatingWordsFlipEmotion")`，即一定为 true 或一定为 false 的条件也并不报错，但对大量嵌套的 if-else 并不报错，对于上面复杂的 if-else，使用 switch 语句是更好的选择。

### 6.9 Unused import statement

CheckStyle 对没有使用的 import 的类不报 Warning。

## 7 CheckStyle 与其他工具(PMD)的对比

PMD 是一款非编译型的，免费的针对 Java 的源码静态分析工具，根据自带的或用户自定义的 XML 规则进行分析。其中，PMD 自带的规则包括 bestpractices 等六种规则，对源码分析共产生 2825 个错误。

| <span style="display:inline-block;width:90px">规则</span> | <span style="display:inline-block;width:70px">警告类型</span> | <span style="display:inline-block;width:70px">警告内容</span> | <span style="display:inline-block;width:70px">警告数量</span> | 警告原由                                                                                 |
| --------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| bestpractices                                             | Error                                                         | AvoidReassigningParameters                                    | 9                                                             | 函数体内对传入参数进行赋值                                                               |
|                                                           |                                                               | SystemPrintln                                                 | 272                                                           | 使用了 System.out/err.prinln 函数，PMD 认为程序信息应该由日志打印                        |
|                                                           | Warning                                                       | AvoidPrintStackTrace                                          | 62                                                            | PMD 推荐使用 LoggerCall 而不是 Java 自带的异常捕获                                       |
|                                                           |                                                               | ForLoopCanBeForeach                                           | 4                                                             | 对于仅用下标来获取数组元素的可以使用 Foreach 方法                                        |
|                                                           |                                                               | LiteralsFirstInComparisons                                    | 166                                                           | 字符串直接进行比较可能会出现 NullPointerException 异常                                   |
|                                                           |                                                               | MethodReturnsInternalArray                                    | 2                                                             | 函数返回对象的成员变量数组                                                               |
|                                                           |                                                               | PositionLiteralsFirstInCaseInsensitiveComparisons             | 1                                                             | PMD6.24.0 修改为 deprecated，PM7.0.0 之后替换为 LiteralsFirstInComparisons               |
|                                                           |                                                               | PositionLiteralsFirstInComparisions                           | 42                                                            | 同 PositionLiteralsFirstInCaseInsensitiveComparisons                                     |
|                                                           |                                                               | UnusedAssignment                                              | 47                                                            | 变量赋值后未使用就再次赋值                                                               |
|                                                           |                                                               | UnusedLocalVariables                                          | 5                                                             | 未使用的局部变量                                                                         |
|                                                           |                                                               | UnusedPrivateField                                            | 3                                                             | 未使用的私有变量                                                                         |
|                                                           | WeakWarning                                                   | UnusedImports                                                 | 3                                                             | 未使用的导入                                                                             |
|                                                           |                                                               | UseVarargs                                                    | 6                                                             | 使用了可变长参数                                                                         |
| codestyle                                                 | Error                                                         | LocalVariableNamingConventions                                | 1                                                             | 局部变量命名不规范                                                                       |
|                                                           |                                                               | MethodNamingConventions                                       | 4                                                             | 方法命名不规范                                                                           |
|                                                           |                                                               | VariableNamingConventions                                     | 1                                                             | 变量命名不规范                                                                           |
|                                                           | Warning                                                       | AtLeastOneConstructor                                         | 2                                                             | 类至少有一个构造函数                                                                     |
|                                                           |                                                               | CommentDefaultAccessModifier                                  | 8                                                             | 成员变量声明默认值                                                                       |
|                                                           |                                                               | ConfusingTernary                                              | 14                                                            | if 判断优先判断的是否定情况                                                              |
|                                                           |                                                               | DefaultPackage                                                | 8                                                             | PMD6.25.0 修改为 deprecated，PM7.0.0 之后 removed                                        |
|                                                           |                                                               | FieldDeclarationsShouldBeAtStartOfClass                       | 13                                                            | 成员变量的声明应该在类的最开始                                                           |
|                                                           |                                                               | LinguisticNaming                                              | 4                                                             | 方法命名与成员变量不符合                                                                 |
|                                                           |                                                               | LocalVaribaleCouldBeFinal                                     | 154                                                           | 局部变量可以声明为 final                                                                 |
|                                                           |                                                               | LongVariable                                                  | 235                                                           | 变量名过长                                                                               |
|                                                           |                                                               | MethodArgumentCouldBeFinal                                    | 283                                                           | 方法参数可以声明为 Final                                                                 |
|                                                           |                                                               | OnlyOneReturn                                                 | 165                                                           | 一个函数方法应该只有一个 Return                                                          |
|                                                           |                                                               | PrematureDeclaration                                          | 15                                                            | 变量声明应该在用到之前，过早声明可能会报错                                               |
|                                                           |                                                               | ShortVariable                                                 | 34                                                            | 变量名过短                                                                               |
|                                                           |                                                               | UnnecessaryConstructor                                        | 4                                                             | 不需要的构造函数                                                                         |
|                                                           |                                                               | UseUnderscoresInNumericLiterals                               | 6                                                             | 使用下划线分隔大数字                                                                     |
|                                                           | WeakWarning                                                   | ShortClassName                                                | 2                                                             | 过短的类名                                                                               |
|                                                           |                                                               | UnnecessaryImport                                             | 3                                                             | 没有必要的导入                                                                           |
|                                                           |                                                               | UselessParentheses                                            | 8                                                             | 无效的括号                                                                               |
| design                                                    | Warning                                                       | AvoidCatchingGenericException                                 | 18                                                            | 避免捕获父类异常，应该为更具体的异常                                                     |
|                                                           |                                                               | CognitiveComplexity                                           | 44                                                            | 函数逻辑过于复杂                                                                         |
|                                                           |                                                               | CollapsibleIfStatements                                       | 2                                                             | 可以合并的嵌套 if 条件                                                                   |
|                                                           |                                                               | CyclomaticComplexity                                          | 46                                                            | 过于复杂的条件判断                                                                       |
|                                                           |                                                               | DataClass                                                     | 1                                                             | 仅包含数据的类，没有方法                                                                 |
|                                                           |                                                               | ExcessiveClassLength                                          | 2                                                             | 类的长度过长，承担职责过多                                                               |
|                                                           |                                                               | ExcessiveMethodLength                                         | 7                                                             | 函数长度过长                                                                             |
|                                                           |                                                               | ExcessivePublicCount                                          | 2                                                             | 公共成员变量过多                                                                         |
|                                                           |                                                               | FinalFieldCouldBeStatic                                       | 6                                                             | final 修饰的成员变量可以声明为 static                                                    |
|                                                           |                                                               | GodClass                                                      | 1                                                             | 类职责过多                                                                               |
|                                                           |                                                               | LawOfDemeter                                                  | 164                                                           | 违反迪米特法则                                                                           |
|                                                           |                                                               | ModifiedCyclomaticComplexity                                  | 46                                                            | PM7.0.0 之后 removed，由 CyclomaticComplexity 实现                                       |
|                                                           |                                                               | NPathComplexity                                               | 19                                                            | 函数的路径复杂度过高                                                                     |
|                                                           |                                                               | NcssCount                                                     | 14                                                            | 违背 Non-Comment Source Statement 矩阵                                                   |
|                                                           |                                                               | NcssMethodCount                                               | 6                                                             | PM7.0.0 之后 removed，由 NcssCount 实现                                                  |
|                                                           |                                                               | SingularField                                                 | 1                                                             | 仅依赖函数参数决定的成员变量应该修改为局部变量                                           |
|                                                           |                                                               | StdCyclomaticComplexity                                       | 46                                                            | PM7.0.0 之后 removed，由 CyclomaticComplexity 实现                                       |
|                                                           |                                                               | TooManyFields                                                 | 6                                                             | 类的成员变量过多                                                                         |
|                                                           |                                                               | TooManyMethods                                                | 8                                                             | 类的函数过多                                                                             |
|                                                           |                                                               | UesUtilityClass                                               | 2                                                             | 使用工具类                                                                               |
| documentation                                             | Warning                                                       | CommentRequired                                               | 69                                                            | 成员变量需要注释进行解释                                                                 |
|                                                           |                                                               | CommentSize                                                   | 41                                                            | 注释的大小不合适                                                                         |
|                                                           |                                                               | UncommentedEmptyConstructor                                   | 4                                                             | 未注释的空构造方法                                                                       |
|                                                           |                                                               | UncommentedEmptyMethodBody                                    | 1                                                             | 未注释的空函数                                                                           |
| errorprone                                                | Error                                                         | ConstructorCallsOverridableMethod                             | 1                                                             | 在构造函数内调用重写方法                                                                 |
|                                                           |                                                               | ReturnEmptyArrayRatherThanNull                                | 1                                                             | 返回空数组而不是 Null                                                                    |
|                                                           |                                                               | ReturnEmptyCollectionRatherThanNull                           | 1                                                             | 返回空集合而不是 Null                                                                    |
|                                                           |                                                               | BrokenNull                                                    | 2                                                             | null 的检查逻辑非法                                                                      |
|                                                           | Warning                                                       | AssignmentInOperand                                           | 14                                                            | 在判读语句中进行赋值                                                                     |
|                                                           |                                                               | AvoidDuplicateLiterals                                        | 5                                                             | 字符串变量操作过多，可以声明为局部变量                                                   |
|                                                           |                                                               | AvoidLiteralsInIfCondition                                    | 62                                                            | 避免在 if 条件中使用复杂的变量                                                           |
|                                                           |                                                               | CloseResource                                                 | 38                                                            | Java 的 IO 流需要 close 进行关闭                                                         |
|                                                           |                                                               | CompareObjectsWithEquals                                      | 1                                                             | 使用 equals 而不是==来进行判断                                                           |
|                                                           |                                                               | NullAssignment                                                | 2                                                             | 使用 null 进行赋值                                                                       |
|                                                           |                                                               | TestClassWithoutTestCases                                     | 1                                                             | Test 类没有具体 test 方法                                                                |
|                                                           |                                                               | UnnecessaryCaseChange                                         | 4                                                             | 不需要的条件传唤                                                                         |
|                                                           |                                                               | UseEqualsToCompareStrings                                     | 1                                                             | 使用 equals 而不是==来比较字符串                                                         |
|                                                           |                                                               | UseLocaleWithCaseConversions                                  | 26                                                            | 使用 toLowerCase 最好显示指明转换规则                                                    |
|                                                           | Suggestions                                                   | DataflowAnomalyAnalysis                                       | 369                                                           | PMD6.27.0 修改为 deprecated，PM7.0.0 之后 removed，由 bestpractice/UnusedAssignment 实现 |
| performance                                               | Error                                                         | AvoidFileStream                                               | 45                                                            | fileStream 会导致 JVM 的垃圾回收机制暂停，影响效率                                       |
|                                                           | Warning                                                       | AppendCharacterWithChar                                       | 9                                                             | 单个字符使用单引号而不是双引号                                                           |
|                                                           |                                                               | AvoidInstantiatingObjectsInLoops                              | 25                                                            | 避免在循环中重复创建对象                                                                 |
|                                                           |                                                               | RedundantFieldIntializer                                      | 50                                                            | Java 对于基础类型会以默认值进行赋值，如 boolean 会以 false 赋值                          |
|                                                           |                                                               | UseIndexOfChar                                                | 20                                                            | 对于单个字符使用 indexOf 时以字符而不是字符串传入效率更高                                |
|                                                           |                                                               | UseStringBufferForStringAppends                               | 6                                                             | 较长的字符串拼接使用 StringBuffer 而不是+                                                |

综合对比，CheckStyle 更注重代码样式的优化，对于代码效率关注较少，而 PMD 在 codestyle 之外，还关注了 performance 之类的优化，这一点从报错数量上可以显然的看出来，但 PMD 中存在大量的重复报错，例如一处代码会同时产生 CompareObjectsWithEquals 和 UseEqualsToCompareStrings 两个错误。同时，CheckStyle 对于代码样式的优化能力比 PMD 更好，CheckStyle 对于 Style 的报错数目是多于 PMD 的 codestyle 部分且更加细化的。
