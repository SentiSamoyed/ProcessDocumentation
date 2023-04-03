# CheckStyle结果统计与分析报告

+ 杜威 201830006
+ 陈骏 201250068
+ 徐浩钦 201250067

## 1 报告间的差异

### 1.1 警告数量

第一次报告中的警告数量为 5439，最后一次报告中的警告数量为 1534。在利用 checkstyle 对代码进行修改后，警告数量大幅减少，代码风格更符合规范。

### 1.2 警告类型

在最后一次报告中，第一次报告中最长出现的 Coding, Block Checks 类型错误全部被改正了。最后仍然存在的警告类型一般是两种：变量命名警告、本行字符数超过 100 个警告。经过讨论后决定暂不修改变量名。

## 2 警告数量类型与数量

> 统计修改的（closed）、新增的（new）、一直存在的（open）的 checkstyle 中警告 （包括警告的属性、数量等）



## 3 警告的修改

> 举例说明修改的警告，即原来的警告是怎样的，说明是如何修改的。警告例子不少于 5 个，且警告例子要有多样性（即覆盖不同类型的规则）

### 3.1 Javadoc Comments

#### 3.1.1 RequireEmptyLineBeforeBlockTagGroup

警告内容：Javadoc tag @param等tag前面应该有一行空行。修改前：

~~~java
/**
   * Description
   * @param param_test 参数一
   */
~~~

应该在描述内容和tag中间添加空行。修改后：

~~~java
/**
   * Description
   * 
   * @param param_test 参数一
   */
~~~

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

#### **3.2.1 AvoidStarImport**

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

#### 3.2.2 CustomImportOrder

##### 3.2.2.1

警告内容：导入语句字典序错误。修改前：

~~~java
import java.io.FileNotFoundException;
import java.io.FileInputStream;
import java.io.FileOutputStream;
~~~

应该根据字典序排列导入顺序。修改后：

~~~java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
~~~

##### 3.2.2.2

警告内容：导入组之前的额外空行。修改前：

~~~java
import java.io.OutputStreamWriter;

import uk.ac.wlv.utilities.FileOps;
~~~

应该删去空行。修改后：

~~~java
import java.io.OutputStreamWriter;
import uk.ac.wlv.utilities.FileOps;
~~~

### 3.3 Block Checks

#### 3.3.1 NeedBraces

警告内容：if/else/for结构必须使用大括号{}。修改前：

~~~java
if (resources == null && !resources.initialise(options))
    return false;
~~~

给仅有一条语句的if/else/fro block添加大括号。修改后：

~~~java
if (resources == null && !resources.initialise(options)) {
	return false;
}
~~~

#### 3.3.2 EmptyCatchBlock

警告内容：空catch块。修改前：

~~~java
catch (NumberFormatException numberformatexception) {
}
~~~

修改后：

~~~java
catch (NumberFormatException numberformatexception) {
	numberformatexception.printStackTrace();
}
~~~

### 3.4 Whitespace

#### 3.4.1 OperatorWrap

警告内容：‘+’应该另起一行

~~~java
 wWriter.write("\t" + iMultiOptimisations +
          "\t" + this.bgReduceNegativeEmotionInQuestionSentences +
          "\t" + this.bgMissCountsAsPlus2 +
		// etc.
);
~~~

将'+'另起一行。修改后：

~~~java
wWriter.write("\t" + iMultiOptimisations
		+ "\t" + this.bgReduceNegativeEmotionInQuestionSentences
		+ "\t" + this.bgMissCountsAsPlus2
 		+ "\t" + this.bgYouOrYourIsPlus2UnlessSentenceNegative
		+ "\t" + this.bgExclamationInNeutralSentenceCountsAsPlus2
 		+ "\t" + this.bgUseIdiomLookupTable
		+ "\t" + this.igMoodToInterpretNeutralEmphasis
		// etc.
);
~~~

### 3.5 Miscellaneous

#### 3.5.1 ArrayTypeStyle

警告内容：数组大括号位置错误。修改前：

~~~java
int igNegClass[];
~~~

将C风格数组修改为Java风格

~~~java
int[] igNegClass;
~~~

### 3.6 Coding

#### 3.6.1 VariableDeclarationUsageDistance

警告内容：变量‘wTermStrengthWriter’声明及第一次使用距离4行（最多：3行）。若需存储该变量的值，请将其声明为final的。3行为google_checks定义。修改前：

~~~java
BufferedWriter wResultsWriter = new BufferedWriter(new FileWriter(sOutFileName));
BufferedWriter wTermStrengthWriter = new BufferedWriter(new FileWriter((new StringBuilder(String.valueOf(FileOps.s_ChopFileNameExtension(sOutFileName)))).append("_termStrVars.txt").toString()));
if (igPosClass == null || igPosClass.length < igPosCorrect.length) {
	igPosClass = new int[igParagraphCount + 1];
	igNegClass = new int[igParagraphCount + 1];
	igTrinaryClass = new int[igParagraphCount + 1];
}
options.printClassificationOptionsHeadings(wResultsWriter);
~~~

将BufferedWriter在调用前声明。修改后：

~~~java
BufferedWriter wResultsWriter = new BufferedWriter(new FileWriter(sOutFileName));
BufferedWriter wTermStrengthWriter = new BufferedWriter(new FileWriter((new StringBuilder(String.valueOf(FileOps.s_ChopFileNameExtension(sOutFileName)))).append("_termStrVars.txt").toString()));
options.printClassificationOptionsHeadings(wResultsWriter);
~~~

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

### 4.2 WhitespaceAround

警告内容为：‘{’ is not followed by whitespace.Empty Blocks may only be represented as {} when not part of a multi-block statement(4.1.3)。

~~~java
if (sData.length > iTextCol) {// TODO
	Paragraph paragraph = new Paragraph();
    // code
}
~~~

将// TODO 换行或添加空格，该警告消失，因此checkstyle工具不能识别紧跟语句的注释

### 4.3 WhitespaceAfter

警告内容为：';'后应有空格。修改前：

~~~java
iFileTrinary = Integer.parseInt(sData[0].trim());// 以制表符分割的第一个字符串
~~~

逻辑同4.2，checkstyle不能有效识别注释

## 5 新增警告的处理 

> 举例分析新增的警告，是因为什么原因引起的，为什么修改，或为什么不修改

### 5.1 CustomImportOrder

由于将import _.*转化为具体的类之后，未考虑其字典序，在修正import顺序为字典序之后，该警告消失。

### 5.2 ParamterName&&LocalVariableName

由于SentiStrength源码的变量声明没有采用驼峰命名法，将变量类型以缩写（String->s，int->i，float->f）添加在变量名称前面，整体项目中风格统一，不进行修改。

### 5.3 AbbreviationAsWordInName

由于变量声明中存在多于一个的连续大写字母，如ID等，认为是专有名词缩写，不进行修改。

### 5.4 LineLength

由于代码的逻辑过于复杂，块嵌套，变量命名复杂导致一行代码内容较长。修改逻辑与命名会影响代码可读性，不进行修改。

## 6 checkstyle漏报的缺陷

> 统计 checkstyle 漏报的缺陷数量（即 checkstyle 没有报告但是开发人员认为是一个缺陷，例如：功能缺陷），并举例分析 checkstyle 漏报的缺陷产生的原因

### 6.1 冗余的StringBuilder，toString()和String.valueof

```java
String sTempFile = (new StringBuilder(String.valueOf(sInputFile))).append("_temp").toString();
```

在如上源代码中，StringBuilder的调用是没有必要的。因为在String + String这样的字符串拼接时，String类源码中其实还是调用了StringBuilder的append()方法。同时sInputFile本身就是String类，不需要再显式调用String.valueof，可以改为如下形式，这样写简洁并且可读性更好。

```java
String sTempFile = sInputFile + "_temp";
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

### 6.4 重复的异常捕捉

~~~java
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
~~~

上述代码中，FileNotFoundException和IOException的异常捕获之后的逻辑完全相同，且FileNotFoundException为IOException的子类，因此FileNotFoundException是完全多余的，CheckStyle作为代码静态分析工具，不对异常的冗余逻辑进行检查。

### 6.5 EmptyBlock

~~~java
for (int i = 1; i <= igParagraphCount; i++) {
	boolean _tmp = bgSupcorpusMember[i];
	// TODO 此处循环只做了局部变量的声明，没有进行其他操作
}
~~~

上述代码中，for循环体内仅作了局部变量的声明，没有任何其他操作，其实是一个空循环块，CheckStyle对EmptyBlock的检查仅检查块内是否有语句，不检查语句是否为变量声明。

### 6.5 函数返回

~~~java
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
~~~

return作为void函数的最后一条语句时是冗余的，CheckStyle并不对此进行检查

### 6.6 index0f(" ") >= 0 和 contains(" ")

```java
if (sLine.indexOf(" ") >= 0) 
```

在上述代码中用indexof的效率是不如contains的，应该使用contains，这种缺陷源于CheckStyle仅作代码格式的检查。

### 6.7 字符集参数设定

~~~java
rReader = new BufferedReader(new InputStreamReader(new FileInputStream(sFilename), "UTF8"));
~~~

Java在传递编码格式时可以使用Java的StandardCharsets，而不通过字符串指定。可修改为：

```java
rReader = new BufferedReader(new InputStreamReader(new FileInputStream(sFilename), StandardCharsets.UTF_8));
```

### 6.8 大量嵌套if-else语句

~~~java
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
~~~

CheckStyle对变量声明之后的第一次调用距离报错，同时对于if-else中重复出现的条件，如上例中的`sData[0].equals("NegatingWordsFlipEmotion")`，即一定为true或一定为false的条件也并不报错，但对大量嵌套的if-else并不报错，对于上面复杂的if-else，使用switch语句是更好的选择。

### 6.9 Unused import statement

CheckStyle对没有使用的import的类不报Warning。