# vscode 格式化配置

- setting 搜索 C_Cpp.clang_format_fallbackStyle
- { BasedOnStyle: LLVM, IndentWidth: 4, AccessModifierOffset: -4, PointerAlignment: Left }
- [参考资料](https://blog.csdn.net/core571/article/details/82867932)

- clang-format

> [llvm](https://github.com/llvm/llvm-project)

```conf
# my conf
# .clang-format

---
# 语言: None, Cpp, Java, JavaScript, ObjC, Proto, TableGen, TextProto
Language: Cpp
# BasedOnStyle:  LLVM
# 访问说明符(public、private等)的偏移
AccessModifierOffset: -4
AlignAfterOpenBracket: Align
AlignArrayOfStructures: None
AlignConsecutiveMacros: None
AlignConsecutiveAssignments: None
AlignConsecutiveBitFields: None
AlignConsecutiveDeclarations: None
AlignEscapedNewlines: Right
AlignOperands: Align
AlignTrailingComments: true
AllowAllArgumentsOnNextLine: true
AllowAllConstructorInitializersOnNextLine: true
# 允许函数声明的所有参数在放在下一行
AllowAllParametersOfDeclarationOnNextLine: true
AllowShortEnumsOnASingleLine: true
# 允许短的块放在同一行
AllowShortBlocksOnASingleLine: true
AllowShortCaseLabelsOnASingleLine: false
AllowShortFunctionsOnASingleLine: All
AllowShortLambdasOnASingleLine: All
# 允许短的if语句保持在同一行
AllowShortIfStatementsOnASingleLine: true
# 允许短的循环保持在同一行
AllowShortLoopsOnASingleLine: true
AlwaysBreakAfterDefinitionReturnType: None
AlwaysBreakAfterReturnType: None
AlwaysBreakBeforeMultilineStrings: false
# 总是在template声明后换行
AlwaysBreakTemplateDeclarations: true
AttributeMacros:
    - __capability
# false 表示函数实参要么都在同一行，要么都各自一行
BinPackArguments: false
# false 表示所有形参要么都在同一行，要么都各自一行
BinPackParameters: false
BraceWrapping:
    AfterCaseLabel: false
    AfterClass: false
    AfterControlStatement: Never
    AfterEnum: false
    AfterFunction: false
    AfterNamespace: false
    AfterObjCDeclaration: false
    AfterStruct: false
    AfterUnion: false
    AfterExternBlock: false
    BeforeCatch: false
    BeforeElse: false
    BeforeLambdaBody: false
    BeforeWhile: false
    IndentBraces: false
    SplitEmptyFunction: true
    SplitEmptyRecord: true
    SplitEmptyNamespace: true
BreakBeforeBinaryOperators: None
BreakBeforeConceptDeclarations: true
BreakBeforeBraces: Attach
BreakBeforeInheritanceComma: false
BreakInheritanceList: BeforeColon
BreakBeforeTernaryOperators: true
BreakConstructorInitializersBeforeComma: false
BreakConstructorInitializers: BeforeColon
BreakAfterJavaFieldAnnotations: false
BreakStringLiterals: true
ColumnLimit: 80
CommentPragmas: "^ IWYU pragma:"
CompactNamespaces: false
ConstructorInitializerAllOnOneLineOrOnePerLine: false
ConstructorInitializerIndentWidth: 4
ContinuationIndentWidth: 4
Cpp11BracedListStyle: true
DeriveLineEnding: true
DerivePointerAlignment: false
DisableFormat: false
EmptyLineAfterAccessModifier: Never
EmptyLineBeforeAccessModifier: LogicalBlock
ExperimentalAutoDetectBinPacking: false
FixNamespaceComments: true
ForEachMacros:
    - foreach
    - Q_FOREACH
    - BOOST_FOREACH
IfMacros:
    - KJ_IF_MAYBE
IncludeBlocks: Preserve
IncludeCategories:
    - Regex: '^"(llvm|llvm-c|clang|clang-c)/'
      Priority: 2
      SortPriority: 0
      CaseSensitive: false
    - Regex: '^(<|"(gtest|gmock|isl|json)/)'
      Priority: 3
      SortPriority: 0
      CaseSensitive: false
    - Regex: ".*"
      Priority: 1
      SortPriority: 0
      CaseSensitive: false
IncludeIsMainRegex: "(Test)?$"
IncludeIsMainSourceRegex: ""
IndentAccessModifiers: false
IndentCaseLabels: false
IndentCaseBlocks: false
IndentGotoLabels: true
IndentPPDirectives: None
IndentExternBlock: AfterExternBlock
IndentRequires: false
# 缩进宽度
IndentWidth: 4
IndentWrappedFunctionNames: false
InsertTrailingCommas: None
JavaScriptQuotes: Leave
JavaScriptWrapImports: true
KeepEmptyLinesAtTheStartOfBlocks: true
LambdaBodyIndentation: Signature
MacroBlockBegin: ""
MacroBlockEnd: ""
# 连续空行的最大数量
MaxEmptyLinesToKeep: 2
# 命名空间的缩进: None, Inner(缩进嵌套的命名空间中的内容), All
NamespaceIndentation: None
ObjCBinPackProtocolList: Auto
ObjCBlockIndentWidth: 2
ObjCBreakBeforeNestedBlockParam: true
ObjCSpaceAfterProperty: false
ObjCSpaceBeforeProtocolList: true
PenaltyBreakAssignment: 2
PenaltyBreakBeforeFirstCallParameter: 19
PenaltyBreakComment: 300
PenaltyBreakFirstLessLess: 120
PenaltyBreakString: 1000
PenaltyBreakTemplateDeclaration: 10
PenaltyExcessCharacter: 1000000
PenaltyReturnTypeOnItsOwnLine: 60
PenaltyIndentedWhitespace: 0
# 指针和引用的对齐: Left, Right, Middle
PointerAlignment: Left
PPIndentWidth: -1
ReferenceAlignment: Pointer
ReflowComments: true
ShortNamespaceLines: 1
# 允许排序 #include
SortIncludes: false
SortJavaStaticImport: Before
SortUsingDeclarations: true
SpaceAfterCStyleCast: false
SpaceAfterLogicalNot: false
SpaceAfterTemplateKeyword: true
SpaceBeforeAssignmentOperators: true
SpaceBeforeCaseColon: false
SpaceBeforeCpp11BracedList: false
SpaceBeforeCtorInitializerColon: true
SpaceBeforeInheritanceColon: true
SpaceBeforeParens: ControlStatements
SpaceAroundPointerQualifiers: Default
SpaceBeforeRangeBasedForLoopColon: true
SpaceInEmptyBlock: false
SpaceInEmptyParentheses: false
SpacesBeforeTrailingComments: 1
SpacesInAngles: Never
SpacesInConditionalStatement: false
SpacesInContainerLiterals: true
SpacesInCStyleCastParentheses: false
SpacesInLineCommentPrefix:
    Minimum: 1
    Maximum: -1
SpacesInParentheses: false
SpacesInSquareBrackets: false
SpaceBeforeSquareBrackets: false
BitFieldColonSpacing: Both
Standard: Latest
StatementAttributeLikeMacros:
    - Q_EMIT
StatementMacros:
    - Q_UNUSED
    - QT_REQUIRE_VERSION
TabWidth: 8
UseCRLF: false
UseTab: Never
WhitespaceSensitiveMacros:
    - STRINGIZE
    - PP_STRINGIZE
    - BOOST_PP_STRINGIZE
    - NS_SWIFT_NAME
    - CF_SWIFT_NAME
---


```
