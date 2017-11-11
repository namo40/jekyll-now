---
layout: post
title: "C# 프로젝트에 Sentry 붙이기"
date: 2017-11-11 15:50
categories: C#
permalink: /archivers/sentry_csharp
---
# Sentry 프로젝트 생성하기
* 먼저 Sentry 화면에서 "New Project" 버튼을 누릅니다.
![](/images/sentry_csharp/01.png)

* "C#" 플랫폼을 선택 후, Project의 이름을 정하고 "Create Project" 버튼을 누릅니다.
![](/images/sentry_csharp/02.png)

* 기본적인 설치 사용 방법을 친절하게 안내해 줍니다.
![](/images/sentry_csharp/03.png)

# C# 프로젝트 생성
* Nuget Package 에서 "SharpRaven" 을 찾아서 설치 합니다.

* 테스트 코드 작성
    ```C#
    using SharpRaven;
    using SharpRaven.Data;
    using System;
    
    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
                var ravenClient = new RavenClient("http://****@localhost:9000/3");
    
                AppDomain.CurrentDomain.UnhandledException += (sender, e) =>
                {
                    ravenClient.Capture(new SentryEvent(e.ExceptionObject as Exception));
                };
    
                try
                {
                    throw new Exception("First Exception");
                }
                catch (Exception e)
                {
                    Console.WriteLine("Catch clause caught : {0} \n", e.Message);
                    ravenClient.Capture(new SentryEvent(e));
                }
    
                throw new NotImplementedException();
            }
        }
    }
    ```
    
* 실행 후 Sentry
![](/images/sentry_csharp/04.png)

![](/images/sentry_csharp/05.png)

# PS...
* 기능이 상당히 괜찮아서, Bug Tracker 뿐만 아니라 해당 버그에 대해 담당자 할당 및
이슈 해결 여부 등 사후 관리까지 지원을 해서 참 좋은듯 합니다.
* 적극 추천.

# 참고
* [Sentry 설치](/archivers/sentry_install)
* https://docs.sentry.io/clients/csharp/