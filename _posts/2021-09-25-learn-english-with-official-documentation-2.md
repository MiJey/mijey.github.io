---

layout: post

title: 안드로이드 공식 문서로 영어공부 (2) App architecture

series: “공식 문서로 영어공부”

categories: [기타]

tags: [Android, 영어공부]

filename: 2021-09-25-learn-english-with-official-documentation-2.md

draft: 2021-09-19 14:26:00

date: 2021-09-25 03:24:00

modified: 2021-09-27 16:36:00

---


## App architecture


### Introduction

[https://developer.android.com/topic/architecture](https://developer.android.com/topic/architecture)

Android provides a set of libraries and components to help you **put together** your app **according to** best practices. \
Android는 권장사항**에 따라** 앱을 **구성하는** 데 도움이 되는 라이브러리와 구성요소 세트를 제공합니다.

Learn the basics of **putting together** a robust app with the Guide to app architecture. \
앱 아키텍처 가이드에서 강력한 앱을 **만드는** 기본사항을 배웁니다.


### Guide to app architecture

[https://developer.android.com/jetpack/guide](https://developer.android.com/jetpack/guide)

**Given** that a properly-written Android app contains multiple components and that users often interact with multiple apps in a short period of time, / apps need to adapt to different kinds of **user-driven** workflows and tasks. \
올바르게 작성된 Android 앱은 여러 구성요소를 포함하며, 사용자는 짧은 시간 내에 여러 앱과 상호작용할 때도 많다는 점을 **고려하면**, / 앱은 **사용자 중심의** 다양한 워크플로 및 작업에 맞게 조정될 수 있어야 합니다.

This **app-hopping behavior** is common on mobile devices, so your app must handle these flows correctly. \
휴대기기에서는 이렇게 **앱을 바꾸는 동작**이 일반적이므로, 앱에서 이러한 흐름을 올바르게 처리해야 합니다.

**Given** the conditions of this environment, it's possible for your app components to be launched individually and **out-of-order**, and the operating system or user can destroy them at any time. \
이러한 환경 조건을 **고려해 볼 때** 앱 구성요소는 개별적이고 **비순차적으로** 실행될 수 있으며, 운영체제나 사용자가 언제든지 앱 구성요소를 제거할 수 있습니다.

The most important principle to follow is **separation of concerns**. \
따라야 할 가장 중요한 원칙은 **관심사 분리**입니다.

Keep in mind that **you don't own implementations** of Activity and Fragment; rather, these are just **glue classes** that represent the contract between the Android OS and your app. \
Activity 및 Fragment **구현은 소유의 대상이 아니**며 Android OS와 앱 사이의 계약을 나타내도록 **이어주는 클래스**일 뿐입니다.

Another important principle is that you should **drive** your UI **from** a model, preferably a persistent model. \
또 하나의 중요한 원칙은 모델**에서** UI**를 도출**해야 한다는 것입니다. 가급적 지속적인 모델을 권장합니다.

Your app continues to work in cases when a network connection is **flaky** or not available. \
네트워크 연결이 **취약**하거나 연결되어 있지 않아도 앱이 계속 작동합니다.

**By basing your app on** model classes with the well-defined responsibility of managing the data, your app is more testable and consistent. \
데이터 관리 책임이 잘 정의된 모델 클래스를 **기반으로 앱을 만들면** 쉽게 테스트하고 일관성을 유지할 수 있습니다.

In this section, we demonstrate how to structure an app using Architecture Components **by working through an end-to-end use case**. \
이 섹션에서는 **종합적인 사용 사례를 들어** 아키텍처 구성요소를 사용하여 앱을 구성하는 방법을 보여줍니다.

**That being said,** this recommended architecture is a good starting point for most situations and workflows. \
**하지만** 이 권장 아키텍처는 대부분의 상황 및 워크플로에 유용한 출발점이 될 것입니다.

Notice that each component depends only on the component **one level below it**. \
각 구성요소가 **한 수준 아래의** 구성요소에만 종속됨을 볼 수 있습니다.

**Regardless of whether** the user comes back to the app several minutes after they've last closed it or several days later, they instantly see a user's information that the app persists locally. \
사용자가 앱을 마지막으로 닫은지 몇 분 후 또는 며칠 후에 다시 사용**하는지와 관계없이** 앱이 로컬에 보존하는 사용자의 정보가 바로 표시됩니다.

If this data is **stale**, the app's repository module starts updating the data in the background. \
이 데이터가 **오래된** 경우 앱의 저장소 모듈이 백그라운드에서 데이터 업데이트를 시작합니다.

This is where the LiveData architecture component **comes in**. \
여기에서 LiveData 아키텍처 구성요소가 **사용됩니다**.

Given that ViewModel objects **are intended to outlast** the corresponding View objects that they update, you shouldn't include direct references to View objects within your implementation of ViewModel. \
ViewModel 객체가 업데이트하는 관련 View 객체보다 **오래 지속되게 의도되었**으므로 ViewModel 구현 내의 View 객체에 직접 참조를 포함하면 안 됩니다.

We've left out the network error case **for the sake for simplicity**. \
**편의를 위해** 네트워크 오류 사례는 생략했습니다.



* 검색해보면 for the sake **of** simplicity 라고 나오는데, 공식 문서에 오타가 있는건가?

This design is **suboptimal** for the following reasons: \
이 디자인은 다음과 같은 이유로 **최적의 방법이 아닙**니다.

**To address these shortcomings,** we add a new data source to our UserRepository, which caches the User objects in memory: \
**이러한 단점을 해결하기 위해** 메모리에 UserRepository 객체를 캐시하는 User에 새로운 데이터 소스를 추가해 보겠습니다.

Details omitted for brevity. \
간결함을 위해 자세한 내용은 생략합니다. (구글 번역)

**By relying on** our current implementation in this situation, we need to fetch the data again from the network. \
이 상황에서 현재 구현**에 의존하면** 네트워크에서 데이터를 다시 가져와야 합니다.

The app would show inconsistent data, which is confusing **at best**. \
앱에서 일치하지 않는 데이터를 표시하여 **(기껏해야, 잘해봤자)** 혼란스러워집니다.

This is where the Room persistence library **comes to the rescue**. \
여기에서 Room 지속성 라이브러리가 **필요합니다**.

At compile time, it validates each query **against** your data schema, so broken SQL queries result in compile-time errors instead of runtime failures. \
컴파일 시 데이터 스키마**에 대해** 각 쿼리의 유효성을 검사하므로 SQL 쿼리가 잘못되면 런타임 실패가 아닌 컴파일 시간 오류가 발생합니다.

Single source of truth \
단일 소스 저장소



* 단일 진실 공급원
* https://en.wikipedia.org/wiki/Single_source_of_truth

For example, if our backend has another endpoint that returns a list of friends, the same user object could come from two different API endpoints, maybe even using different **levels of granularity**. \
예를 들어 백엔드에 친구 목록을 반환하는 다른 엔드포인트가 있다면, 2개의 다른 API 엔드포인트에서 서로 다른 **세분화 수준**을 사용하여 동일한 사용자 객체를 제공할 수 있습니다.

If the UserRepository were to return the response from the Webservice request **as-is**, without checking for consistency, our UIs could show confusing information because the version and format of data from the repository would depend on the endpoint most recently called. \
일관성 확인 없이 UserRepository가 Webservice 요청으로부터 응답을 **있는 그대로** 반환했다면 저장소의 데이터 버전과 형식이 가장 최근에 호출된 엔드포인트에 종속되므로 UI에서 혼란스러운 정보를 표시할 수 있습니다.

Using this model, the database **serves as** the single source of truth, and other parts of the app access it using our UserRepository. \
이 모델을 사용하면 데이터베이스가 단일 정보 소스 **역할을 하**며 앱의 다른 부분은 UserRepository를 사용하여 데이터베이스에 액세스합니다.

**Regardless of whether** you use a disk cache, we recommend that your repository **designate** a data source as the single source of truth for the rest of your app. \
디스크 캐시 사용 **여부와 상관없이** 저장소에서 데이터 소스를 나머지 앱의 단일 소스 저장소로 **지정하**는 것이 좋습니다.

From the UI's perspective, the fact that there's a request **in flight** is just another data point, similar to any other piece of data in the User object itself. \
UI 관점에서 보면 **진행 중인** 요청이 있다는 사실은 User 객체의 다른 데이터 부분과 유사한 다른 데이터 포인트에 불과합니다.

You can test the UserRepository using a JUnit test, **as well**. \
UserRepository**도** JUnit 테스트를 사용하여 테스트할 수 있습니다.

Test DAO classes using **instrumentation tests**. \
**계측 테스트**를 사용하여 DAO 클래스를 테스트합니다.

You can also **associate** this rule with Espresso as an **idling resource**. \
이 규칙을 **유휴 리소스**로 Espresso와 **연결할** 수도 있습니다.

There are many ways to solve a problem, **(whether) be it** communicating data between multiple activities or fragments, **retrieving** remote data and persisting it locally for offline mode, or **any number of** other common scenarios that nontrivial apps encounter. \
문제를 해결하는 방법은 여러 가지가 있습니다. 즉, 여러 활동이나 프래그먼트 간에 데이터를 교환하거나, 원격 데이터를 **가져와서** 오프라인 모드에서 사용하도록 데이터를 로컬에 보존**하는 등** 앱에 발생하는 어려운 문제와 관련된 **다양한** 일반적인 시나리오가 있습니다.

Remember that not all of your users enjoy **constant, high-speed connectivity**. \
모든 사용자가 **끊김 없고 속도가 빠른 연결**을 사용하지는 않는다는 점에 유의하세요.

After creating the NetworkBoundResource, we can use it to write our **disk- and network-bound implementations** of User in the UserRepository class: \
NetworkBoundResource를 만든 후에는 UserRepository 클래스에서 User의 **디스크 및 네트워크 결합 구현**을 작성하는 데 사용할 수 있습니다.
