---
layout: post
title: "C# 7.1 사용해보기"
date: 2017-11-21 11:30
categories: C#
permalink: /archivers/csharp_use_ver_7_1
---
# C# 7.1 사용해보기
Visual Studio 2017을 설치해서 C# 프로젝트를 생성하면 기본적으로 C# 7.0으로 버전이 설정이 되어있습니다.

그래서 C# 7.1 기능을 이용하면 에러가 발생합니다.

C# 7.1을 이용하려면 먼저 프로젝트에서 언어 버전을 선택해야 하는데 그에 대해 알아봅시다.

## 언어 버전 설정하기
* 프로젝트 - 속성 - [고급] 선택
	![](/images/csharp_7_1/01.png)

* 언어 버전 선택
	![](/images/csharp_7_1/02.png)

## C# 7.1 기능 이용하기
* Async Main
	Async 를 드디어 main에서도 적용이 가능하게 되었습니다.
	```C#
	static async Task<int> Main(string[] args)
	{
		return await DoAsyncWork();
	}
	```

* Default literal expressions
	var 혹은 Generic 같은 타입의 경우 기본 값을 자동으로 유추하는데 사용 할 수 있습니다.
	```C#
	public static T Get<T>()
    {
        var temp = default(T);

        var s = default(string);
        var d = default(dynamic);
        var i = default(int);
        var n = default(int?); // n is a Nullable int where HasValue is false.

        return temp;
    }
	```

## 참고
* Welcome to C# 7.1 https://blogs.msdn.microsoft.com/dotnet/2017/10/31/welcome-to-c-7-1/
* Default Value Expresions https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions