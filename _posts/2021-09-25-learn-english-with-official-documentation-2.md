---

layout: post

title: 안드로이드 공식 문서로 영어공부 (2) App architecture

series: “공식 문서로 영어공부”

categories: [기타]

tags: [Android, 영어공부]

filename: 2021-09-25-learn-english-with-official-documentation-2.md

draft: 2021-09-19 14:26:00

date: 2021-09-25 03:24:00

modified: 2021-09-25 03:24:00

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


### Architecture Components


#### UI layer libraries


##### View binding


###### Overview

[https://developer.android.com/topic/libraries/view-binding](https://developer.android.com/topic/libraries/view-binding)

View binding is enabled **on a module by module basis**. \
뷰 결합은 **모듈별로** 사용 설정됩니다.

**To work around** this limitation, view binding supports a tools:viewBindingType attribute, allowing you to tell the compiler what type to use in the generated code. \
이 제한 사항을 **해결하기 위해** 보기 바인딩은 tools:viewBindingType 특성을 지원하므로 생성된 코드에서 사용할 유형을 컴파일러에 알릴 수 있습니다. (구글 번역)


##### Data Binding Library


###### Overview

[https://developer.android.com/topic/libraries/data-binding](https://developer.android.com/topic/libraries/data-binding)

These features of the library **coexist seamlessly** with your existing layouts. \
라이브러리의 이러한 기능은 기존 레이아웃과 **원활하게 공존합니다**.

For example, the binding adapter **can take care of** calling the setText() method / to set the text property or call the setOnClickListener() method / to add a listener to the click event. \
예를 들어 결합 어댑터는 setText() 메서드를 호출하여 / 텍스트 속성을 설정하거나 setOnClickListener() 메서드를 호출하여 / 리스너를 클릭 이벤트에 추가 / **할 수 있습니다**.


###### Get started

[https://developer.android.com/topic/libraries/data-binding/start](https://developer.android.com/topic/libraries/data-binding/start)

The Data Binding Library offers both flexibility and **broad compatibility**—it's a support library, so you can use it with devices running Android 4.0 (API level 14) or higher. \
데이터 결합 라이브러리는 유연성과 **광범위한 호환성**을 모두 제공하는 지원 라이브러리이며 Android 4.0(API 수준 14) 이상을 실행하는 기기에서 사용할 수 있습니다.


###### Layouts and binding expressions

[https://developer.android.com/topic/libraries/data-binding/expressions](https://developer.android.com/topic/libraries/data-binding/expressions)

The expression language allows you to write expressions that handle events **dispatched** by the views. \
표현식 언어를 사용하면 뷰에 의해 **전달된** 이벤트를 처리하는 표현식을 작성할 수 있습니다.

**Let's assume for now that** you have a **plain-old** object to describe the User entity: \
User 항목을 설명하기 위해 **간단한 기존** 객체가 있다고 **가정해 보겠습니다**.

It is also possible to use an object that **follows a set of conventions**, such as the usage of accessor methods in Java, as shown in the following example: \
또한 다음 예에서와 같이 자바의 접근자 메서드 사용과 같이 **일련의 규칙을 준수하는** 객체를 사용할 수도 있습니다.

This class **holds** all the bindings from the layout properties (for example, the user variable) to the layout's views and knows how to assign values for the binding expressions. \
이 클래스는 레이아웃 속성(예: user 변수)에서 레이아웃 뷰까지 모든 결합을 **보유하**며 결합 표현식의 값을 할당하는 방법을 알고 있습니다.

The null **coalescing** operator (??) chooses the left **operand** if it isn't null or the right if the former is null. \
null **병합** 연산자(??)는 왼쪽 **피연산자**가 null이 아니면 왼쪽 피연산자를 선택하고 null이면 오른쪽 피연산자를 선택합니다.

Event attribute names are determined by the name of the listener method **with a few exceptions**. \
이벤트 속성 이름은 **몇 가지 예외를 제외하고** 리스너 메서드의 이름에 따라 결정됩니다.

In your expressions, you can reference methods that **conform to** the signature of the listener method. \
표현식에서 리스너 메서드의 서명과 **일치하는** 메서드를 참조할 수 있습니다.

They are similar to method references, but they let you run **arbitrary** data binding expressions. \
하지만 리스너 결합을 사용하면 **임의의** 데이터 결합 표현식을 실행할 수 있습니다.

If you need to use an expression with **a predicate** (for example, ternary), you can use void as a symbol. \
**조건자**와 함께 표현식(예: 삼항)을 사용해야 한다면 void를 기호로 사용할 수 있습니다.

Imports **make easy to** reference classes inside your layout files. \
가져오기**를 사용하면** 레이아웃 파일 내에서 클래스를 쉽게 참조**할 수 있습니다**.

Variables **allow you to** describe a property that can be used in binding expressions. \
변수**를 사용하면** 결합 표현식에 사용할 수 있는 속성을 설명**할 수 있습니다**.

Includes **let you reuse** complex layouts across your app. \
포함**을 사용하면** 앱 전체에서 복잡한 레이아웃을 재사용**할 수 있습니다**.


###### Work with observable data objects

[https://developer.android.com/topic/libraries/data-binding/observability](https://developer.android.com/topic/libraries/data-binding/observability)

Observability **refers to** the capability of an object to notify others about changes in its data. \
식별 가능성은 객체가 데이터 변경에 관해 다른 객체에 알릴 수 있는 기능**을 의미합니다**.

Some work is involved in creating classes that implement the Observable interface, which **could not be worth the effort** if your classes only have a few properties. \
일부 작업은 Observable 인터페이스를 구현하는 클래스를 생성하는 작업과 관련이 있지만 클래스에 몇 가지 속성만 있다면 **그다지 애쓸 필요가 없습니다**.

Observable fields are **self-contained** observable objects that have a single field. \
식별 가능한 필드는 단일 필드가 있는 **독립적인** 식별 가능한 객체입니다.

A class that implements the Observable interface **allows** the registration of listeners that want to be notified of property changes of on the observable object. \
Observable 인터페이스를 구현하는 클래스를 **사용하면** 식별 가능한 객체의 속성 변경에 관해 알림을 받으려는 리스너를 등록**할 수 있습니다**.

The data class that implements BaseObservable **is responsible for** notifying when the properties change. \
BaseObservable을 구현하는 데이터 클래스는 속성이 변경될 때 알리**는 역할을 합니다**.

You can **opt out of** this functionality by adding the following to your build.gradle file: \
build.gradle 파일에 다음을 추가하여 이 기능**을 선택 해제할** 수 있습니다. (구글 번역)


###### Generated binding classes

[https://developer.android.com/topic/libraries/data-binding/generated-binding](https://developer.android.com/topic/libraries/data-binding/generated-binding)

IDs aren't as necessary as they are without data binding, but **there are still some instances where** access to views is still necessary from code. \
ID는 데이터 결합이 없을 때만큼 필요하지는 않지만 코드에서 계속 뷰에 액세스**해야 하는 상황이 여전히 있습니다**.

Unlike normal views, ViewStub objects **start off** as an invisible view. \
일반 뷰와 달리 ViewStub 객체는 보이지 않는 뷰로 **시작됩니다**.

When they either are made visible or **are** explicitly **told to** inflate, they replace themselves in the layout by inflating another layout. \
이 객체는 가시적으로 표시되거나 확장**을** 명시적으로 **지시받**으면 또 다른 레이아웃을 확장함으로써 레이아웃의 자체 뷰를 대체합니다.

Because the ViewStub essentially disappears from the view hierarchy, the view in the binding object must also disappear to allow to **be claimed by garbage collection**. \
ViewStub이 기본적으로 뷰 계층 구조에서 사라지기 때문에 **가비지 컬렉션을 통한 메모리 회수**가 가능하도록 결합 객체의 뷰도 사라져야 합니다.

Because the views are final, a ViewStubProxy object **takes the place of** the ViewStub in the generated binding class, **giving** you access to the ViewStub when it exists and also access to the inflated view hierarchy when the ViewStub has been inflated. \
뷰가 최종적이므로 ViewStubProxy 객체는 생성된 결합 클래스에서 ViewStub**를 대체하**며, **이에 따라** 개발자는 ViewStub가 존재할 경우 이에 액세스할 수 있고 ViewStub가 확장된 경우 확장된 뷰 계층 구조에도 액세스할 수 있습니다.

When inflating another layout, a binding must **be established for** the new layout. \
또 다른 레이아웃을 확장할 때 새 레이아웃의 결합**을 설정**해야 합니다.

Therefore, the ViewStubProxy must **listen to** the ViewStub OnInflateListener and **establish** the binding when required. \
따라서 ViewStubProxy는 ViewStub OnInflateListener를 **수신 대기하**고 필요할 때 결합을 **설정해**야 합니다.

For example, a RecyclerView.Adapter **operating against** arbitrary layouts doesn't know the specific binding class. \
예를 들어 임의의 레이아웃**에 작동하는** RecyclerView.Adapter는 특정 결합 클래스를 인식하지 못합니다.

You can change your data model in a background thread **as long as** it isn't a collection. \
컬렉션이 아닌 **한** 백그라운드 스레드에서 데이터 모델을 변경할 수 있습니다.


###### Binding adapters

[https://developer.android.com/topic/libraries/data-binding/binding-adapters](https://developer.android.com/topic/libraries/data-binding/binding-adapters)

Binding adapters **are responsible for making** the appropriate framework **calls** to set values. \
결합 어댑터는 적절한 프레임워크를 **호출하여** 값을 설정하는 **작업을 담당합니다**.

For example, the support class DrawerLayout doesn't have any attributes, but **plenty of** setters. \
예를 들어 지원 클래스 DrawerLayout에는 어떤 속성도 없지만 **많은** setter가 있습니다.

The following layout automatically uses the setScrimColor(int) and setDrawerListener(DrawerListener) methods as the setter for the app:scrimColor and app:drawerListener attributes, **respectively**: \
다음 레이아웃은 자동으로 setScrimColor(int) 메서드와 setDrawerListener(DrawerListener) 메서드를 **각각** app:scrimColor 속성과 app:drawerListener 속성의 setter로 사용합니다.

The second parameter determines the type accepted in the binding expression for the **given** attribute. \
두 번째 매개변수는 **지정된** 속성의 결합 표현식에서 허용되는 유형을 결정합니다.

The binding adapters that you define **override** the default adapters provided by the Android framework when there is a conflict. \
개발자가 정의하는 결합 어댑터는 충돌이 발생하면 Android 프레임워크에서 제공하는 기본 어댑터보다 **우선 적용됩니다**.


###### Bind layout views to Architecture Components

[https://developer.android.com/topic/libraries/data-binding/architecture](https://developer.android.com/topic/libraries/data-binding/architecture)

Most of the remaining work **consists in making sure** that you're exposing the correct data. \
데이터 결합 라이브러리를 사용하는 그 밖의 작업은 대부분 적절한 데이터를 노출하고 있는지 **확인하는 것입니다**.

Use an Observable ViewModel for **more control over** binding adapters \
결합 어댑터를 **더 세밀하게 제어**하기 위해 관찰 가능한 ViewModel 사용


###### Two-way data binding

[https://developer.android.com/topic/libraries/data-binding/two-way](https://developer.android.com/topic/libraries/data-binding/two-way)

In order to react to changes in **the backing data**, you can make your layout variable an implementation of Observable, usually BaseObservable, and use a @Bindable annotation, as shown in the following code snippet: \
다음 코드 스니펫에서와 같이 **백업 데이터** 변경에 대응하기 위해 레이아웃 변수를 Observable(대개 BaseObservable) 구현으로 만들고 @Bindable 주석을 사용할 수 있습니다.

However, it doesn't know when or how the attribute changes. **For that**, you need to set a listener on the view. \
하지만 속성이 언제 또는 어떻게 변경되는지는 인식하지 못합니다. 속성의 변경 시기 또는 방식을 알**기 위해서는** 뷰에 리스너를 설정해야 합니다.

**In practice**, this listener includes some **non-trivial** logic, including listeners for one-way data binding. \
**실제로** 이 리스너에는 단방향 데이터 결합을 위한 리스너를 비롯하여 **중요한** 로직이 포함되어 있습니다.

If the variable that's bound to a View object needs to be formatted, translated, or changed **somehow** before being displayed, it's possible to use a Converter object. \
View 객체에 결합된 변수를 표시하기 전에 **먼저** 형식 지정, 변환 또는 변경을 해야 한다면 Converter 객체를 사용하면 됩니다.

Be careful **not to introduce** infinite loops when using two-way data binding. \
양방향 데이터 결합을 사용할 때 무한 루프가 **발생하지 않도록** 주의해야 합니다.
