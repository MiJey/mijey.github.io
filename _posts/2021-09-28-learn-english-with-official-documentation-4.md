---

layout: post

title: 안드로이드 공식 문서로 영어공부 (4) Lifecycle-aware components

series: “공식 문서로 영어공부”

categories: [기타]

tags: [Android, 영어공부]

filename: 2021-09-28-learn-english-with-official-documentation-4.md

draft: 2021-09-26 01:42:00

date: 2021-09-28 00:14:00

modified: 2021-09-28 00:14:00

---


##### Lifecycle-aware components


###### Handle lifecycles

[https://developer.android.com/topic/libraries/architecture/lifecycle](https://developer.android.com/topic/libraries/architecture/lifecycle)

(1시간 10분 소요)

Lifecycle-aware components perform actions **in response to** a change in the lifecycle status of another component, such as activities and fragments. \
수명 주기 인식 구성요소는 활동과 프래그먼트 같은 다른 구성요소의 수명 주기 상태 변경**에 따라** 작업을 실행합니다.

However, this pattern leads to **a poor organization** of the code and to **the proliferation of errors**. \
하지만 이 패턴으로 인해 코드 **구성이 나빠**지고 **오류가 증가**하게 됩니다.

They are core to how Android works and your application must **respect** them. Not doing so may trigger memory leaks or even application crashes. \
또한 Android 작동 방식의 핵심으로, 애플리케이션은 수명 주기를 **고려해야** 하며, 그렇게 하지 않으면 메모리 누수 또는 애플리케이션 비정상 종료가 발생할 수 있습니다.

Even though this sample looks fine, in a real app, you **end up** having too many calls that manage the UI and other components **in response to** the current state of the lifecycle. \
이 샘플은 괜찮아 보이지만, 실제 앱에서는 수명 주기의 현재 상태**에 따라** UI와 다른 구성요소를 관리하는 호출이 너무 많이 발생**하게 됩니다**.

Managing multiple components places **a considerable amount of code** in lifecycle methods, such as onStart() and onStop(), which makes them difficult to maintain. \
여러 구성요소를 관리하면 onStart() 및 onStop()과 같은 수명 주기 메서드에 **상당한 양의 코드**를 배치하게 되어 유지하기 어려워집니다.

Moreover, **there's no guarantee that** the component starts before the activity or fragment is stopped. \
게다가 활동이나 프래그먼트가 중지되기 전에 구성요소가 시작된다**는 보장도 없습니다**.

The androidx.lifecycle package provides classes and interfaces that help you **tackle** these problems in a **resilient** and isolated way. \
androidx.lifecycle 패키지는 이러한 문제를 **탄력적**이고 단독적인 방법으로 **처리하는** 데 도움이 되는 클래스와 인터페이스를 제공합니다.

The lifecycle events that **are dispatched from** the framework and the Lifecycle class. \
프레임워크 및 Lifecycle 클래스**에서 전달되는** 수명 주기 이벤트입니다. 

**Think of** the states **as** nodes of a graph and events **as** the edges between these nodes. \
상태**를** 그래프의 노드**로**, 이벤트**를** 이 노드 사이의 가장자리**로 생각하세요**.

LifecycleOwner is a single method interface that **denotes** that the class has a Lifecycle. \
LifecycleOwner는 클래스에 Lifecycle이 있음을 **나타내는** 단일 메서드 인터페이스입니다.

This allows the MyLocationListener class to **be self-sufficient**, **meaning that** the logic to react to changes in lifecycle status is declared in MyLocationListener instead of the activity. \
이렇게 하면 MyLocationListener 클래스가 **자립할** 수 있습니다. **즉,** 수명 주기 상태의 변경에 반응하는 로직이 활동 대신 MyLocationListener에서 선언됩니다.

A common use case is to avoid **invoking certain callbacks** if the Lifecycle isn't in a good state right now. \
일반적인 사용 사례에서는 Lifecycle이 현재 정상 상태가 아닌 경우 **특정 콜백 호출**을 피합니다.

All of the **setup and teardown operations** are managed by the class itself. \
모든 **설정과 해제 작업**은 클래스 자체에서 관리합니다.

Try to write **data-driven** UIs **where** your UI controller’s responsibility is to update the views as data changes, or notify user actions back to the ViewModel. \
**데이터 기반** UI를 작성해 보세요. **여기서** 데이터 변경에 따라 뷰를 업데이트하거나 사용자 작업을 다시 ViewModel에 알리는 것은 UI 컨트롤러의 책임입니다.

**Be careful though**, it isn't ViewModel's responsibility to fetch data (for example, from a network). \
**하지만** 데이터를 가져오는 것(예: 네트워크에서 데이터 가져오기)은 ViewModel의 책임이 아닙니다.

Trying to modify the UI after the state is saved **is likely to** cause **inconsistencies** in the navigation state of your application / **which is why** FragmentManager throws an exception if the app runs a FragmentTransaction after state is saved. \
상태를 저장한 후 UI를 수정하려고 하면 애플리케이션의 탐색 상태에 **불일치**가 나타**날 수 있습니다**. / **따라서** 상태가 저장된 후 앱에서 FragmentTransaction을 실행하면 FragmentManager가 예외를 발생시킵니다.

LiveData prevents this edge case **out of the box** / **by refraining from** calling its observer / if the observer's associated Lifecycle isn't at least STARTED. \
LiveData는 관찰자의 관련 Lifecycle이 적어도 STARTED 상태가 아니라면 / 관찰자를 호출**하지 않게 하여** / 이러한 에지 케이스(edge case)를 **처음부터** 방지합니다.



* [https://en.wikipedia.org/wiki/Out_of_the_box_(feature)](https://en.wikipedia.org/wiki/Out_of_the_box_(feature))
* 상자에서 열자마자 바로 사용 가능한 기능 → 별도의 세팅 없이 **처음부터** 제공하는 기능

**Behind the scenes**, it calls isAtLeast() before deciding to invoke its observer. \
**하지만 이면에서는** 관찰자 호출을 결정하기 전에 isAtLeast()를 호출합니다.

This is unlikely to impact your code / but **it is something you need to be aware of as** it doesn't match the call order in the Activity class in API level 26 and lower. \
이로 인해 코드가 영향을 받을 가능성은 없지만, / API 수준 26 이하에서 Activity 클래스의 호출 순서와 일치하지 않**으므로 주의해야 합니다**.


###### ViewModel

[https://developer.android.com/topic/libraries/architecture/viewmodel](https://developer.android.com/topic/libraries/architecture/viewmodel)

(36분 소요)

The framework may decide to destroy or re-create a UI controller **in response to** certain user actions or device events that are completely out of your control. \
프레임워크는 특정 사용자 작업이나 완전히 통제할 수 없는 기기 이벤트**에 대한 응답으로** UI 컨트롤러를 제거하거나 다시 만들도록 결정할 수 있습니다.

The UI controller needs to manage these **calls** and ensure the system **cleans them up** after it's destroyed to avoid potential memory leaks. \
UI 컨트롤러는 비동기 호출을 관리해야 하며, 메모리 누수 가능성을 방지하기 위해 호출이 제거된 후 시스템에서 **호출을 정리**하는지 확인해야 합니다.

UI controllers such as activities and fragments **are primarily intended to** display UI data, react to user actions, or handle operating system communication, such as permission requests. \
활동 및 프래그먼트와 같은 UI 컨트롤러의 **목적은 기본적으로** UI 데이터를 표시하거나, 사용자 작업에 반응하거나, 권한 요청과 같은 운영체제 커뮤니케이션을 처리**하는 것입니다**.

Requiring UI controllers to also be responsible for loading data from a database or network **adds** bloat to the class. \
또한 UI 컨트롤러에 데이터베이스나 네트워크에서 데이터 로드를 책임지도록 요구하면 클래스가 팽창됩니다.



* adds가 해석이 안됨

It's easier and more efficient to **separate out** view data ownership from UI controller logic. \
UI 컨트롤러 로직에서 뷰 데이터 소유권을 **분리하**는 방법이 훨씬 쉽고 효율적입니다.

For example, if you need to display a list of users in your app, make sure to assign responsibility to acquire and keep the list of users to a ViewModel, instead of an activity or fragment, **as illustrated by** the following sample code: \
예를 들어 앱에서 사용자 목록을 표시해야 한다면 다음 샘플 코드**에 설명된 대로** 사용자 목록을 확보하여 활동이나 프래그먼트 대신 ViewModel에 보관하도록 책임을 할당해야 합니다.

Figure 1 illustrates the various lifecycle states of an activity as it **undergoes** a rotation and then is finished. \
그림 1에서는 활동이 회전을 **거친** 다음 끝날 때까지 활동의 다양한 수명 주기 상태를 보여줍니다.

This common **pain point** can be addressed by using ViewModel objects. \
이러한 일반적인 **고충**은 ViewModel 객체를 사용하면 해결할 수 있습니다.

Fragments don't need to know about each other **besides** the SharedViewModel contract. \
프래그먼트는 SharedViewModel 계약 **외에** 서로 알 필요가 없습니다. 


###### LiveData

[https://developer.android.com/topic/libraries/architecture/livedata](https://developer.android.com/topic/libraries/architecture/livedata)

(48분 소요)

Unlike a regular observable, LiveData is lifecycle-aware, meaning it **respects** the lifecycle of other app components, such as activities, fragments, or services. \
관찰 가능한 일반 클래스와 달리 LiveData는 수명 주기를 인식합니다. 즉, 활동, 프래그먼트, 서비스 등 다른 앱 구성요소의 수명 주기를 **고려합니다**.

LiveData **considers** an observer, which is represented by the Observer class, **to be in** an active state if its lifecycle is in the STARTED or RESUMED state. \
Observer 클래스로 표현되는 관찰자의 수명 주기가 STARTED 또는 RESUMED 상태이면 LiveData는 관찰자를 활성 상태**로 간주합니다**.

LiveData notifies Observer objects **when underlying** data changes. \
LiveData는 기본 데이터가 변경**될 때** Observer 객체에 알립니다.

**Always up to date data** \
**최신 데이터 유지**

**Work with** LiveData objects \
LiveData 객체 **사용**

Make sure to store LiveData objects that update the UI in ViewModel objects, **as opposed to** an activity or fragment, for the following reasons: \
활동 또는 프래그먼트**와 달리** ViewModel 객체의 UI를 업데이트하는 LiveData 객체를 저장해야 하며 그 이유는 다음과 같습니다.

In most cases, an app component’s onCreate() method is the **right place** to begin observing a LiveData object for the following reasons: \
대부분의 경우 앱 구성요소의 onCreate() 메서드는 LiveData 객체 관찰을 시작하기 **적합한 장소**이며 그 이유는 다음과 같습니다.

To ensure the system doesn’t make **redundant calls** from an activity or fragment’s onResume() method. \
시스템이 활동이나 프래그먼트의 onResume() 메서드에서 **중복 호출**을 하지 않도록 하기 위해서입니다.

The main responsibility of the ViewModel is to load and manage UI-related data, which makes it **a great candidate** for holding LiveData objects. \
ViewModel은 기본적으로 UI 관련 데이터를 로드하고 관리하는 역할을 하므로 LiveData 객체를 보유하는 데 **적합합니다**.

Applies a function on the value stored in the LiveData object, and **propagates** the result downstream. \
LiveData 객체에 저장된 값에 함수를 적용하고 결과를 다운스트림으로 **전파합니다**.

This mechanism allows lower levels of the app to create LiveData objects that are lazily calculated **on demand**. \
이 메커니즘을 사용하면 앱의 하위 수준에서 **요청이 있을 때** 늦게 계산되는 LiveData 객체를 만들 수 있습니다.

There are **a dozen** different specific transformation that may be useful in your app, but they aren’t provided by default. \
앱에 유용할 **다양한** 관련 변환이 있지만, 이러한 변환은 기본적으로 제공되지 않습니다.

To implement your own transformation you can you use the MediatorLiveData class, which listens to other LiveData objects and processes events **emitted** by them. \
자체 변환을 구현하려면 다른 LiveData 객체를 수신하고 객체에서 **내보낸** 이벤트를 처리하는 MediatorLiveData 클래스를 사용하면 됩니다.


###### Save UI states

[https://developer.android.com/topic/libraries/architecture/saving-states](https://developer.android.com/topic/libraries/architecture/saving-states)

(56분 소요)

Preserving and restoring an activity's UI state **in a timely fashion** across system-initiated activity or application destruction is a crucial part of the user experience. \
시스템에서 시작된 활동 또는 애플리케이션 폐기 과정에서 활동의 UI 상태를 **적시에** 보존하고 복원하는 것은 사용자 환경의 중요한 부분입니다.

Regardless of which approach you take, you should ensure your app meets users expectations **with respect to** to their UI state, and provides a smooth, snappy UI (avoids lag time in loading data into the UI, especially after frequently occurring configuration changes, like rotation). \
어떤 접근 방식을 사용하든 앱은 UI 상태**에 관한** 사용자 기대치를 충족하고 매끄럽고 원활한 UI를 제공해야 합니다. 특히 회전과 같이 자주 발생하는 구성 변경 이후에 UI로 데이터를 로드할 때 지연이 발생하지 않도록 해야 합니다.

**User-initiated** UI state **dismissal** \
**사용자가 시작한** UI 상태 **닫기**

The user's assumption in these complete dismissal cases is that they **have** permanently **navigated away from** the activity, and if they re-open the activity they expect the activity to start from a clean state. \
활동을 완전히 닫은 사용자는 영구적으로 활동**에서 벗어났다**고 가정하며 활동을 다시 열 경우 활동이 완전히 새로 시작될 것으로 예상합니다.

When the user's expectations about UI state do not match default system behavior, you must save and restore the user's UI state to ensure that the system-initiated destruction **is transparent to the user**. \
UI 상태에 관한 사용자 기대치가 기본 시스템 동작과 일치하지 않으면 사용자의 UI 상태를 저장하고 복원하여 시스템에서 시작된 폐기를 **사용자가 인식할 수 있**도록 해야 합니다.

Each of the options for preserving UI state **vary** along the following **dimensions** that impact the user experience: \
UI 상태를 유지하기 위한 각각의 옵션은 사용자 환경에 영향을 주는 다음과 같은 **측정기준**에 따라 **다릅니다**.

Because this process happens on the main thread during a configuration change, long-running serialization can cause dropped frames and **visual stutter**. \
직렬화 프로세스는 구성 변경 시 기본 스레드에서 발생하기 때문에 직렬화가 장기적으로 실행되면 프레임 하락 및 **시각적인 끊김 현상**이 발생할 수 있습니다.

If your activity behaves this way, you can **forego** using onSaveInstanceState() and instead persist everything locally. \
활동이 이런 식으로 작동하면 onSaveInstanceState()를 **사용하지 않**고 대신 모든 항목을 로컬에 유지할 수 있습니다.



* 1.	동사 FORMAL
* If you forego something, you decide to do without it, although you would like it.
* 출처 : Collins Cobuild Advanced Learner's English Dictionary
* 앞서 간다 → 내비두고 간다 → 버린다, 포기한다

**In either of** these scenarios, you should still use a ViewModel to avoid wasting cycles reloading data from the database during a configuration change. \
이러한 시나리오 **중 하나에서** 구성을 변경하는 동안 데이터베이스에서 데이터를 다시 로드하느라 주기를 낭비하지 않으려면 ViewModel을 계속 사용해야 합니다.

**Hook into** saved state using SavedStateRegistry \
SavedStateRegistry를 사용하여 저장된 상태**에 연결**

**Beginning with** Fragment 1.1.0 or its transitive dependency Activity 1.0.0, UI controllers, such as an Activity or Fragment, implement SavedStateRegistryOwner and provide a SavedStateRegistry that is bound to that controller. \
Fragment 1.1.0 또는 전이 종속 항목인 Activity 1.0.0**부터는** Activity 또는 Fragment 같은 UI 컨트롤러가 SavedStateRegistryOwner를 구현하고 컨트롤러에 결합되는 SavedStateRegistry를 제공합니다

To register a SavedStateProvider, call registerSavedStateProvider() on the SavedStateRegistry, passing a key to associate with the provider's data **as well as** the provider. \
SavedStateProvider를 등록하려면 SavedStateRegistry에서 registerSavedStateProvider()를 호출하여 제공자의 데이터**뿐만 아니라** 제공자 자체**와도** 연결할 키를 전달합니다.

Alternatively, you can set a LifecycleObserver on a SavedStateRegistryOwner, which implements LifecycleOwner, and register the SavedStateProvider **once** the ON_CREATE event occurs. \
또는 SavedStateRegistryOwner에서 LifecycleObserver를 설정하여 LifecycleOwner를 구현하고 ON_CREATE 이벤트 발생 **시** SavedStateProvider를 등록할 수 있습니다.

See Guide to App Architecture for more details about how to **leverage** local storage to persist your app model data long term (e.g. across restarts of the device). \
로컬 저장소를 **활용하여** 앱 모델 데이터를 장기적으로(예: 기기 재시작 전체에 걸쳐) 유지하는 방법에 관한 자세한 내용은 앱 아키텍처 가이드를 참고하세요.


###### Saved State module for ViewModel

[https://developer.android.com/topic/libraries/architecture/viewmodel-savedstate](https://developer.android.com/topic/libraries/architecture/viewmodel-savedstate)

(15분 소요)

The SavedStateHandle class is a key-value map that allows you to **write and retrieve** data **to and from** the saved state through the set() and get() methods. \
SavedStateHandle 클래스는 set() 메서드와 get() 메서드를 통해 저장된 상태에 데이터를 **작성하고** 저장된 상태에서 데이터를 **검색할** 수 있게 하는 키-값 맵입니다.

The absolute path **can then be used to** instantiate a new File. \
**그런 다음** 이 절대 경로**를 사용하여** 새 File을 인스턴스화**할 수 있습니다**.


###### Use Kotlin coroutines with lifecycle-aware components

[https://developer.android.com/topic/libraries/architecture/coroutines](https://developer.android.com/topic/libraries/architecture/coroutines)

(39분 소요)

Lifecycle-aware components provide **first-class support** for coroutines for logical scopes in your app along with an interoperability layer with LiveData. \
수명 주기 인식 구성요소는 LiveData와의 상호운용성 레이어와 함께 앱의 논리적 범위에 관한 코루틴을 **가장 잘 지원**합니다.

The **built-in** coroutine scopes described in this topic are contained in the KTX extensions for each corresponding component. \
본 항목에서 설명하는 **기본 제공** 코루틴 범위는 해당하는 각 구성요소의 KTX 확장 프로그램에 포함되어 있습니다.

In the example below, loadUser() is a suspend function declared **elsewhere**. \
아래 예에서 loadUser()는 **다른 곳에서** 선언된 정지 함수입니다.
