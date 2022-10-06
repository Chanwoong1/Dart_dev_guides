# Dart Tour

[dart.dev](https://dart.dev/guides/language/language-tour)

Dart 공홈에 있는 가이드 따라가보기

이 페이지는 다른 언어로 프로그래밍하는 법을 이미 알고 있다는 가정 아래, 변수와 연산자부터 클래스와 라이브러리에 이르기 까지 주된 Dart 특징들을 어떻게 사용하는지 보여준다. 이 언어의 짤막한 소개를 보려면 다음 [샘플 페이지](https://dart.dev/samples)를 보자.

```
참고로, DartPad를 사용한다면 대부분의 Dart 언어 기능을 개인 환경 설정 없이 사용할 수 있다.

그 외에 Android Studio, Visual Studio Code 등을 사용해도 된다.
```

# Contents

- [A basic Dart program](#a-basic-dart-program)
- [Important concepts](#important-concepts)
- [Keywords](#keywords)
- [Variables](#variables)
	- [Default value](#default-value)
	- [Late variables]
	- [Final and const]
- [Built-in types]
	- [Numbers]
	- [Strings]
	- [Booleans]
	- [Lists]
	- [Sets]
	- [Maps]
	- [Runes and grapheme clusters]
	- [Symbols]
- [Functions]
	- [Parameters]
	- [The main() function]
	- [Functions as first-class objects]
	- [Anonymous functions]
	- [Lexical scope]
	- [Lexical closures]
	- [Testing functions for equality]
	- [Return values]
- [Operators]
	- [Arithmetic operators]
	- [Equality and relational operators]
	- [Type test operators]
	- [Assignment operators]
	- [Logical operators]
	- [Bitwise and shift operators]
	- [Conditional expressions]
	- [Cascade notation]
	- [Other operators]
- [Control flow statements]
	- [If and else]
	- [For loops]
	- [While and do-while]
	- [Break and continue]
	- [Switch and case]
	- [Assert]
- [Exceptions]
	- [Throw]
	- [Catch]
	- [Finally]
- [Classes]
	- [Using class members]
	- [Using constructors]
	- [Getting an object’s type]
	- [Instance variables]
	- [Constructors]
	- [Methods]
	- [Abstract classes]
	- [Implicit interfaces]
	- [Extending a class]
	- [Extension methods]
	- [Enumerated types]
	- [Adding features to a class: mixins]
	- [Class variables and methods]
- [Generics]
	- [Why use generics?]
	- [Using collection literals]
	- [Using parameterized types with constructors]
	- [Generic collections and the types they contain]
	- [Restricting the parameterized type]
	- [Using generic methods]
- [Libraries and visibility]
	- [Using libraries]
	- [Implementing libraries]
- [Asynchrony support]
	- [Handling Futures]
	- [Declaring async functions]
	- [Handling Streams]
- [Generators]
- [Callable classes]
- [Isolates]
- [Typedefs]
- [Metadata]
- [Comments]
	- [Single-line comments]

## A basic Dart program

아래 코드는 Dart의 가장 기본 기능을 많이 사용한다.

```Dart
// Define a function.
void printInteger(int aNumber)
{
	print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
void main()
{
	var number = 42;  // Declare and initialize a variable.
	printInteger(number); // Call a function.
}
```

이 프로그램은 모든 Dart app에 적용되는 것들을 사용한다.

**//**

한 줄을 주석 처리할때 사둉한다. Dart는 여러 줄의 문서 주석도 지원한다. 더 자세한 정보는 [Comments](#comments).

**void**

사용된 적이 없는 값을 나타내는 특수한 타입이다. 함수인 printInteger()와 main()는 명시적인 값을 반환하지 않아서 void형을 가진다.

**int**

정수를 나타낼 수 있는 다른 타입이다. String, List, bool과 같이 [기본 내장](#built-in-types)된 타입이다.

**42**

리터럴 한 숫자이다. 컴파일 시간이 고정되어있다.

**print()**

출력을 표시하는 편리한 방법이다.

'...' (or "...")

문자열 리터럴.

**\$variableName(or \${expression})**

문자열 보간: 문자열 리터럴 내부의 변수 또는 표현식의 해당 문자열을 포함한다. 더 많은 정보는 [String](#string)으로.

main()

앱을 실행이 시작되는 특별하며 필수적인 최상위 함수이다. 더 많은 정보는 [The main() function](#the-main()-function)

var

특별한 타입 없이 변수를 선언하는 방법. 이 변수 (int)의 타입은 초기화 값(42)에 의해 결정된다.

## Important concepts

Dart를 배울 때, 다음 사실과 개념을 명심하자:

- 변수에 넣을 수 있는 모든 것은 객체이며 모든 객체는 클래스의 구성이다. 짝수, 함수들, null도 다 객체이다. null([sound null safety](#sound-null-safety)를 알고싶다면)을 활성화 하는 것을 제외하고, 모든 객체는 [Object](#object)클래스에서 상속된다.
- Dart는 강력한 타입화를 하지만, Dart는 타입을 유추할 수 있으므로 형식 주석은 선택사항이다. 코드를 보면, number는 int 타입으로 유추할 수 있다.
- 만약 [null safety](#null-safety)를 활성화한다면, nullable하다고 하지 않는 한 변수를 포함할 수 없다. null이 들어갈 지도 모르는 변수에 끝에 물음표(?)를 달아주면 nullable로 만들 수 있다. 예를 들어, 변수의 타입이 **int?** 형이라면, 정수이거나 **null**이 될 수 있다. 만약 절대 null이 들어갈 수 없다면, 너는 !를 사용해서 표현할 수 있다.
예시: **int x = nullableButNotNullInt!**
- 모든 타입이 허용된다고 명시적으로 말하고 싶다면, Object?라고 쓸 수 있고([null safety](#null-safety)를 활성화 한 경우), 다른 타입을 실행하기 전에 확인할 수 있다. 런타임까지 타입 검사를 연기해야 하는 경우 [특수 타입인 dynamic](#special-type-dynamic)을 사용한다.
- Dart는 **List\<int\>** 또는 **List\<Object>** 와 같은 일반적인 타입들을 지원한다.
- Dart는 최상위 함수(main()과 같은)와 클래스 혹은 객체에 연결된 함수(static, instance, methods, respectively)를 지원한다. 함수 내에서 함수를 만들 수 있다.
- 마찬가지로, Dart는 최상위 변수와 클래스 또는 객체에 연결된 변수를 지원한다. instance변수는 field혹은 properties라고 한다.
- java와 다르게, Dart는 **public, protected, private**를 키워드로 갖기 않는다. 만약 식별자가 밑줄(_)을 사용한다면, 해당 라이브러리에 대해 private가 된다. 더 자세한 사항은 [Libraries and visibility](#libraries-and-visibility)에서.
- 식별자는 문자 혹은 _로 시작할 수 있고, 그 뒤에 문자와 숫자의 조합으로 사용할 수 있다.
- Dart는 표현식(런타임 값이 있음)과 명령문(런타임 값이 없음) 모두 가진다. 예를 들어, [조건식](#conditional-expression) **condition ? expr1 : expr2**는 **expr1** 또는 **expr2**의 값을 가진다. [if-else](#if-else-statement)와 비교해보면, if-else문은 값이 없다. 명령문에는 종종 하나 혹은 그 이상의 표현식을 담지만, 표현식은 명령문을 직접 포함할 수 없다.
- Dart 툴들은 두 종류의 문제를 보고할 수 있다: warnings와 errors. Warnings는 단지 너의 코드가 작동하지 않을 수 있다고 알리지만, 프로그램의 실행을 막지는 않는다. Errors는 컴파일타임 혹은 런타임일 수 있다. 컴파일 에러는 코드 실행을 막으며; 런타임 에러는 코드 실행 동안 [예외](#exception)가 발생한다.

## Keywords
다음 표는 Dart언어가 특별히 취급하는 단어들을 나열한다.
|||||
|--|--|--|--|
|[abstract](#abstract-classes) 2|[else](#if-and-else)|[import](#using-libraries) 2|[show](#importing-only-part-of-a-library) 1|
|[as](#type-test-operators) 2|[enum](#enumerated-types)|[in](#for-loops)|[static](#class-variables-and-methods) 2|
|[assert](#assert)|[export](https://dart.dev/guides/libraries/create-library-packages) 2|[interface](#implicit-interfaces) 2|[super](#extending-a-class)|
|[async](#asynchrony-support) 1|[extends](#extending-a-class)|[is](#type-test-operators)|[switch](#switch-and-case)|
|[await](#asynchrony-support) 3|[extension](#extension-methods) 2|[late](#late-variables) 2|[sync](#generators) 1|
|[break](#break-and-continue)|[external](https://spec.dart.dev/DartLangSpecDraft.pdf#External%20Functions) 2|[library](#libraries-and-visibility) 2|[this](#constructors)|
|[case](#switch-and-case)|[factory](#factory-constructors) 2|[mixin](#adding-features-to-a-class:-mixins) 2|[throw](#throw)|
|[catch](#catch)|[false](#booleans)|[new](#using-constructors)|[true](#booleans)|
|[class](#instance-variables)|[final](#final-and-const)|[null](#default-value)|[try](#catch)|
|[const](#final-and-const)|[finally](#finally)|[on](#catch) 1|[typedef](#typedefs) 2|
|[continue](#break-and-continue)|[for](#for-loops)|[operator](#operators) 2|[var](#variables)|
|[covariant](https://dart.dev/guides/language/sound-problems#the-covariant-keyword) 2|[Function](#functions) 2|[part](https://dart.dev/guides/libraries/create-library-packages#organizing-a-library-package) 2|[void](#built-in-types)|
|[default](#switch-and-case)|[get](#getters-and-setters) 2|[required](#named-parameters) 2|[while](#while-and-do-while)|
|[deferred](#lazily-loading-a-library) 2|[hide](#importing-only-part-of-a-library) 1|[rethrow](#catch)|[with](#adding-features-to-a-class:-mixins)|
|[do](#while-and-do-while)|[if](#if-and-else)|[return](#functions)|[yield](#generators) 3|
|[dynamic](#important-concepts) 2|[implements](#implicit-interfaces) 2|[set](#getters-and-setters) 2||
||||

이 단어들은 식별자로 쓰일 수 없지만, 필요한 경우 첨자로 표시된 키워드들은 식별자가 될 수 있다..
- 1은 **contextual keywords** 로, 특정 장소에서만 의미가 있는 문맥 키워드이다. 이들은 어디서나 유효한 식별자다.
- 2는 **built-in identifiers** 로, 이 키워드들은 대부분의 장소에서 유효한 식별자로 쓰이지만, 클래스 또는 타입 이름 혹은 import prefixes와 같은 곳에서는 쓰일 수 없다.
- 3은 제한된 예약어로 [asynchrony support](#asynchrony-support)과 관련되어 있다. 함수 내부에서 **async** , **async \*** **sync \*** 로 표현된 것이 있을 때, **await** 또는 **yield** 를 식별자로 사용할 수 없다.

## Variables

다음은 변수 생성과 초기화를 하는 예다.
```Dart
var name = 'Bob';
```
변수는 참조를 저장한다. 호출된 변수는 'Bob'이라는 값을 가진 **String** 객체에 **name** 에 대한 참조가 포함되어 있다.

**name** 변수의 타입은 **String** 으로 추측되지만, 해당 타입을 지정하여 변경할 수 있다. 만약 한 객체가 단일 타입으로 제한되지 않았다면, **Object(or 필요하다면 dynamic)** 타입으로 한다.

```Dart
Object name = 'Bob';
```

다른 옵션은 명확하게 추측되는 타입을 선언해주는 것이다.

```Dart
String name = 'Bob';
```

- note : 이 페이지는 지역변수의 타입 선언 대신 **var** 사용의 [style guide recommendation](#https://dart.dev/guides/language/effective-dart/design#types)을 따른다.

### Default value

nullable 형식인 초기화하지 않은 변수는 초기값으로 **null** 을 가진다. (만약 [null safety](https://dart.dev/null-safety)를 설정하지 않았다면, 모든 변수는 nullable 타입을 가진다.) 수치형 타입인 변수들도 처음에는 null이다, 왜냐하면 모든 경우에서 Dart에서는 객체들이기 때문이다.

```Dart
int? lineCount;
assert(lineCount == null);
```

- note : 위 코드는 **assert()** 를 호출을 무시한다. 반면 development 동안 조건이 false가 되면 예외가 발생한다. 자세한 내용은 [Assert](#assert) 참고.

만약 null safety를 허용한다면, non-nullable 변수들의 값들을 사용하기 전에 무조건 초기화해주어야한다.

```Dart
int lineCount = 0;
```

선언된 지역변수를 초기화할 필요는 없지만, 사용하기 전에 값들을 가정할 필요가 있다. 예를들어 아래 코드는 Dart가 **lineCount** 가 **print()** 에 전달될 때 non-null을 감지할 수 있기 때문에 유효한 코드이다.

```Dart
int lineCount;

if (weLikeToCount) {
	lineCount = countLines();
}
else {
	lineCount = 0;
}

print(lineCount);
```

최상위 및 클래스 변수들이 느리게 초기화된다; 이 초기화 코드는 변수가 처음 사용될 때 실행된다.

### Late variables
Dart 2.12에서는 **late** 라는 수정자를 추가했다. 이건 두가지의 사용 사례가 있다.
- non-nullable 변수를 선언할 때.
- 게으른 변수 초기화

종종 