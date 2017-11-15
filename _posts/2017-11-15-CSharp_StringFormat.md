---
layout: post
title: "C# 양수, 음수 기호를 남기고 그룹 구분 기호 표시하기"
date: 2017-11-15 18:00
categories: C#
permalink: /archivers/csharp_stringformat_0
---
# C# 양수, 음수 기호를 남기고 그룹 구분 기호 표시하기
문뜩 친구가 +1,015 혹은 -1,015 의 형태로 출력을 하고 싶다길래

찾아 보았습니다.

* Source
```C#
string format = "{0:+#,##0;-#,##0;#,##0}";
Console.WriteLine(format, -1015);
Console.WriteLine(format, 0);
Console.WriteLine(format, 1015);
```

* Result
```
-1,015
0
+1,015
```

; 라는 구분자를 이용해 조건식을 처리하는거 같네요.
