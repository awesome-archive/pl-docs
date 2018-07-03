﻿# 关于本系列

　　本系列文章暂定名为《基本笔记》（ *Elementary Notes* ），全名可能叫《关于计算机科学的入门者基本笔记》（ *Elementary Notes on Computer Science for Beginners* ）之类，不过暂时没有定论；这暂时不是很重要。

　　这些文章的原始的写作动机都一样：为了避免回答一些“经”问题的无谓的重复劳动。这也是对有些人建议我写书的一个粗浅的回应——尽管我对出版的事项或者盈利的计划并不是很感兴趣。

　　鉴于问题的系统和复杂性，解答也需要相称的体量和体裁，故不使用列表式的 [FAQ](https://zh.wikipedia.org/wiki/FAQ) 的类似[某些经典读物](https://zh.wikipedia.org/wiki/%E5%85%B3%E4%BA%8E%E6%89%98%E5%8B%92%E5%AF%86%E5%92%8C%E5%93%A5%E7%99%BD%E5%B0%BC%E4%B8%A4%E5%A4%A7%E4%B8%96%E7%95%8C%E4%BD%93%E7%B3%BB%E7%9A%84%E5%AF%B9%E8%AF%9D)的对话体的形式。

　　这个系列构思已久，但一直因为种种原因（主要是懒）和其它文章一起拖着。这也是使用顺序的、自顶向下的方式论述的原因（虽然事实上在我脑子以外并没有什么提纲）；当然，也需要注意到提交到版本库的好处是可以可追溯地不断更新补充内容的这个好处。

　　作为[目录](contents.md)外的第一篇文字，本文主要讲述一些不适合自然地放在篇目内的其它内容。

　　以下的体例是工具书类型的说明文字。其它章节请视为正文。

## 体例说明

　　本节指定体例规则。

　　除非另行指定，适用[版本库指定的全局规则(en-US)](../../Readme.md)。

### 编辑标记

　　遵从技术写作的习惯，这里该给一些定义和对应的说明；不过，完整的内容暂时空缺。

**TODO** 补充内容。

　　其它如有不完善之处使用同上标记。

**WIP** ←这是一个 WIP 标记。

**注意** ←这是一个注意的标记(notice) 。

### 缩进

　　和代码要求的缩进不同，以空格引起使用等宽字体时视觉上对齐为准体现缩进，以摆脱对特定文本处理工具的依赖。

　　编辑标记可以使用全角或半角空格和所属段落保持一致。

### 排版体例

**TODO** 提升和归并本节规则至全局规则。

　　**强调**以 [Markdown](https://zh.wikipedia.org/wiki/Markdown) 的强调实现，视觉效果上为**粗体**。注意，是[粗体](https://zh.wikipedia.org/wiki/%E7%B2%97%E9%AB%94)，而不是[黑体](https://zh.wikipedia.org/wiki/%E9%BB%91%E4%BD%93_%28%E5%AD%97%E4%BD%93%29) 。*斜体* 的使用包括一些次要的强调（这也是在 Markdown 中的本来含义），通常是局部的术语(terminology) 。一些其它的惯例用法，如西文书名，也适用斜体。

　　全角空格的用法同中文书面文法惯例。中西文混排的半角空格应被考虑，如遗漏则可考虑[提交问题(en-US)](https://github.com/FrankHB/pl-docs/issues)；但是，需要注意特别的用法：正文的半角括号 () 和左边没有空格，但和右边有一个空格，表示紧接左侧作为专有的术语或者 ISO-639 语言代码标注。此外，为了避免 Markdown 渲染的一些兼容性问题，斜体文字周围可能插入冗余半角空格。除有意的对齐外的任何情况下，插入的半角空格不多余连续一个。

　　注意空格的用法和一些其它规则，如[《中文文案排版指北》](https://github.com/mzlogin/chinese-copywriting-guidelines/blob/Simplified/README.md)不同。

### 参考和引用

　　关于被认为是事实进行论述但并非[原创研究](https://zh.wikipedia.org/wiki/%E5%8E%9F%E5%89%B5%E7%A0%94%E7%A9%B6)的材料，通常原则上应给出参考资料来源以佐证出处和可信性。不过因为体裁并非论文，这点并不强制——这通常意味着**有可以补充的余地**，但为了阅读或者写作上的体验暂不全部给出。

　　引用的出处可能通过链接给出，而不是文末的标号；当然，链接不一定表示引用，可能只是一个相关的解释；请读者根据上下文内容自行判断。

### 外来语

　　有时，一个术语(terminology) 对应的外来语（通常为英文）会在上下文中首次出现时给出以便进一步查证。这里的“首次”的范围指本系列文章（但通常不算作为例子的体例）。基本使用体例为半角括号标注，另见本节文字和排版体例的说明。标注时一般应保证词性对应。在之后的下文中仍可视情况重复标注外来语。

　　外来语可能对应概念(concept) 的原文。作者期望这样有助于更精确的辨义，但恕无法担保理解偏差的存在。在一些并非一一对应的场合——如接口(interface) 和界面(interface) 或者属性(attribute) 和属性(property) ——这样的情形，这种注释性质的原文往往是必要的，但仍有赖于读者的独立思考和正确理解。

　　专名（包括下文中的缩写）须循例使用。如有必要区分，在保持含义准确的前提下，引入注释的术语使用原型单数，且不因为位置（如在标题中）转写其中的字母为大写形式。

### 缩写(abbreviation) 和（首字母）缩略语(acronym)

　　首字母缩略语在引入西文外来语的同时给出，如：图形用户界面(GUI, graphical user interface) 。下文优先使用缩略语。

　　其它形式的缩写的使用不在此进行特殊约定，以无歧义和通顺为基本要求。

## 对预期读者的要求

　　作为基础性的(elementary) 的读物，本系列不对读者的阅读能力要求进行预设，但就现实论，至少得**理解中文**白话；对英文的了解有助于回避特定的一些歧义，不过不是严格意义上必须的。

　　高中程度的知识背景是被建议的，但也不是必须的；对本科课程的了解可能会有一些帮助，不过，计算机方面的课程也许正好除外——特别是考虑当这些课程内容掺杂过多流行的谬误而被需要纠正的时候。

　　读者不被要求具有其它学术意义上的训练。不过，作者希望能读者能**独立思考**。

　　因为许多概念的关联性超过文章写作意图，释义恕不能详尽。作者期望读者能适时地**勤于搜索**。作为基础性和识字相差无几的技能，如何实现搜索不是本文关心的问题，尽管可能文章涉及特定话题的更有效率的搜索建议。

## 价值观(value) 和方法论(methodology)

　　基于可行性，文章不排除任意的预设的对特定的价值的观点和立场。相反，必要时文章内容强调、肯定或否定特定的价值；这当然不代表读者和作者的需要观念一致。一致的观念是共识(concensus) ，它表示关于某个逻辑陈述具有唯一的真值——要么都肯定，要么都否定。

　　文章内容从作者预期和读者之间具有的共识为基础出发，明示或默示地断言一些内容是事实(fact) ，不需另行说明；另一些取决于价值判断([value judgement(en-US)](https://en.wikipedia.org/wiki/Value_judgment)) 。[两者的差异](https://en.wikipedia.org/wiki/Fact–value_distinction)是一个基本的哲学范畴问题，不过这里需要注意核心问题主要就是：是否需另行说明。

　　考虑未形成共识的情况，确认一件事实的判断属于价值判断。但一经承认为共识，则不需价值判断断定其事实地位。因此，一般讨论的价值判断中，排除已确认为共识的事实判断。

　　价值判断的总体（结果）是价值观，也指代价值判断的伦理准则。（注意英文中“价值观”和“价值”都是 value 。）而另外一些认识是和价值范畴独立的；其中普遍的一部分被称为方法论。这种划分蕴含了“是”和“应是”是两类有关但有所区别的问题。读者被期望适时区分这两种情况，即便作者没有强调。

　　因为价值判断的不同体现了立场的差异，从作为共识的事实中剔除这些差异有助于表达和理解问题的效率并影响之后的决策。形式系统(formal system) 中的公理(axiom) 作为“事实”具有类似的价值：避免之后无法休止的废话。

　　基于现实考虑，作为讨论的基础，不得不假设存在一些预设的共识，尽管无法精确地描述它包括哪些，因为不这样做会遇到现实困难。举个现实的用例：若读者打算不认同作者的声称的所有论述（即不存在共识），那么就不需要继续往下看了，省得浪费时间。这里，“浪费时间”是作者认为的对价值的否定行为，理由是时间作为资源体现了价值。若某个读者的价值判断准则对此无所谓，那么作者自然不需要皇帝不急太监急了。但是，判断读者是不是在乎“浪费时间”，在本文的作者看来就是一种浪费时间（这点不需要是共识，但不影响结论），接受判断的必要性引起了逻辑上的不自洽。因此，本文作者不打算推测读者的价值判断的准则；这个系列的文章中显式或隐式的关于“事实”的断言，指的都是共识的子集。除了预设的共识以及各方都明确断言过的对某个判断的肯定，形成共识的唯一方法为已经是共识的证明(proof) ，这通过公理、已经是默认的其它前提通过已经是默认的逻辑规则推理得到，其中“已经是默认”意为不言自明。作者期望读者能充分理解这一点。
