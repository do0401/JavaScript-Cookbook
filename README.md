JavaScript Cookbook
=========================
이 글은 [JavaScript Cookbook](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788909194921&orderClick=LAG&Kc=) 책을 토대로 공부한 내용을 정리한 글입니다.

## `시작하기`
## PART 1. 클래식 자바스크립트

### CHAPTER 1. 간단하지만은 않은 자바스크립트 기본 구성 요소

#### 1.1 자바스크립트 객체(object), 원시(primitive), 리터럴(literal) 구분하기
- 리터럴은 인용 문자열(String), 부동 소수점수(Number), 불리언(Boolean)과 같은 특정한 형식의 값을 나타낸다.
```
"이것은 문자열입니다"
1.45
true
```

- 원시는 데이터 유형의 인스턴스를 나타내며 문자열, 숫자, 불리언, null, undefined 등 다섯 가지 형식이 있다.
```
"이것은 문자열입니다"
null
```

- 원시 데이터 유형 중 문자열, 숫자, 불리언은 상보적인 생성자 객체(constructor object)를 가지고 있다.
- 이 객체들은 내장되어 있는 속성 및 메서드에 접근이 가능해 단순히 값을 할당하고 부차적으로 그 값을 추출하는 것을 넘어서 더 다양한 일처리를 할 수 있게 해준다.
```js
var str1 = "이것은 문자열입니다";
console.log(str1.length); // Stirng 객체의 length 속성 사용
```

#### 1.2 문자열에서 목록 추출하기
- 문자열에서 목록을 추출하기 위해서는 두 가지 동작이 필요하다.
- 먼저 목록을 포함한 문자열을 추출하고, 이 문자열을 목록으로 변환하면 된다.
```js
var start = sentence.indexOf(":");
var end = sentence.indexOf(".", start+1);

var fruits = sentence.substring(start+1, end).split(",");
```
- substring() 메서드와 split() 메서드를 체이닝하여 목록을 추출했다.

#### 1.3 문자열이 존재하는지, 빈 문자열인지 검사하기
- 변수가 정의되었는지 그리고 변수가 null이 아닌지 테스트해야 한다.
- typeof()는 변수가 undefined 되지 않았음을 확인할 때 사용할 수 있다.
```js
if (typeof unknownVariable != 'undefined')...
```

- 그러나 null 변수는 object 객체와 동일한 typeof 값을 갖기 때문에 이것만으로는 충분하지 않다.
- 변수를 나열하는 것만으로도 충분히 null인지 아닌지 테스트해볼 수 있다.
```js
if (typeof unknownVariable != 'undefined' && unknownVariable)...
```

- 변수가 비어있지 않은 문자열인지 여전히 알 수 없으므로 length 테스트를 반환해 변수가 문자열인지 그리고 그 문자열이 비어 있지 않은지 테스트한다.
```js
if ((typeof unknownVariable != 'undefined' && unknownVariable) && unknownVariable.length > 0)...
```

- 만약 변수가 숫자라면, 숫자는 length를 갖고 있지 않으므로 테스트는 실패한다.
- valueOf() 메서드를 사용한다. valueOf() 메서드는 모든 자바스크립트 객체에서 사용할 수 있으며 이 메서드는 객체의 원시(감싸지 않은) 값을 반환한다.
```js
if (((typeof unknownVariable != 'undefined' && unknownVariable) && (typeof unknownVariable.valueOf() == "string")) unknownVariable.length > 0)...
```

#### 1.4 특수 문자 삽입하기
- 문자열에 이스케이프 시퀀스(escape sequences)를 사용하면 된다.
- 예를 들어, 저작권 기호를 삽입하려면 이스케이프 시퀀스 \u00A9를 사용한다.
```js
var resultString = "<p>This page \u00A9 Powers </p>";

// 페이지로 출력
var blk = document.getElementById("result");
blk.innerHTML = resultString;
```

- 자바스크립트에서 이스케이프 시퀀스는 모두 백슬래시(\)로 시작한다.

#### 1.5 패턴을 새 문자열로 대체하기
- String의 replace() 메서드를 정규표현식과 함께 사용하면 된다.
```js
var searchString = "Now is the time, this is the tame";
var re = /t\w{2}e/g;
var replacement = searchString.replace(re, "place");
console.log(replacement); // Now is place, this is the place
```

- 리터럴 정규표현식은 슬래시(/)로 시작하고 슬래시로 끝난다.
- 다른 방법으로는 내장 RegExp 객체를 사용할 수도 있다.
```js
var re = new RegExp('t\\w{2}e', "g");
var replacement = searchString.replace(re, "place");
console.log(replacement); // Now is place, this is the 
```

- RegExp 생성자를 이용하면 정규표현식을 보다 다이내믹하게 만들 수 있다.