---

layout: post

title: 안드로이드 공식 문서로 영어공부 (1) App Bacis

series: “공식 문서로 영어공부”

categories: [기타]

tags: [Android, 영어공부]

filename: 2021-08-31-learn-english-with-official-documentation-1.md

draft: 2021-08-31 20:56:00

date: 2021-09-19 14:12:00

modified: 2021-09-19 14:12:00

---


## App Basics


### Introduction

[https://developer.android.com/guide](https://developer.android.com/guide)

If you'**re brand new to** Android and **want to jump into** code, start with the Build Your First App tutorial. \
Android를 **처음 접하고** 바로 코드 작성에 **들어가고 싶다**면 첫 앱 빌드 가이드로 시작하세요.

Codelabs: Short, **self-paced** tutorials that each cover a discrete topic. \
Codelab: 각각 별개의 주제를 다루는 짧은 **자기 주도형** 가이드입니다.


### Build your first app


#### Overview

[https://developer.android.com/training/basics/firstapp](https://developer.android.com/training/basics/firstapp)

The system **determines** which layout to use **based on** the screen size of the current device. \
시스템은 현재 기기의 화면 크기**에 따라** 사용할 레이아웃을 **결정합니다**.

If **any of** your app's features need specific hardware, such as a camera, \
앱에 특정 하드웨어가 필요한 기능(예: 카메라)이 **(무언가)** 있다면

you can query at runtime **whether** the device has that hardware **or** not, / and then disable the **corresponding features** if it doesn't. \
런타임 시 기기에 하드웨어가 **있는지 (없는지)** 쿼리하고 / 없는 경우 **(해당) 기능**을 사용 중지할 수 있습니다.

You can specify that your app requires certain hardware / **so that** Google Play won't allow the app to be installed on devices without them. \
앱에 필요한 특정 하드웨어를 지정하여 / Google Play에서 하드웨어가 없는 기기에 앱을 설치하지 못**하도록 할** 수 있습니다.


#### Build a simple user interface

[https://developer.android.com/training/basics/firstapp/building-ui](https://developer.android.com/training/basics/firstapp/building-ui)

To **make room for** the Layout Editor, hide the Project window. \
Layout Editor**를 위한 공간을 확보**하려면 Project 창을 숨깁니다.

**To do so**, select View > Tool Windows > Project, or just click Project on the left side of the Android Studio screen. \
**이렇게 하려면**, View > Tool Windows > Project를 선택하거나 간단히 Android 스튜디오 화면 왼쪽에 있는 Project를 클릭합니다.

**To do so**, use the Zoom buttons in the Layout Editor toolbar. \
편집기에서 확대**하려면**, Layout Editor 툴바의 Zoom 버튼을 사용합니다.

**Locate** the hint property and then click  (Pick a Resource), which is to the right of the text box. \
hint 속성을 **찾아**서 텍스트 상자 오른쪽에 있는 (Pick a Resource)를 클릭합니다.

To create a layout that's responsive to different screen sizes, / you need to make the text box stretch to fill all the horizontal space that remains / after the button and margins **are accounted for**. \
다양한 화면 크기에 반응하는 레이아웃을 만들려면 / 버튼과 여백**을 고려한** 후 / 텍스트 상자를 늘려 남은 가로 공간을 채워야 합니다.



* account synonym
    1. [noun] description, report, version, story, narration, narrative, statement, news, explanation, exposition, interpretation, communiqué, recital
    2. [noun] financial record, book, ledger, journal, balance sheet, financial statement, results
    3. **[verb] consider, regard as, reckon, hold to be, think, think of as, look on as, view as, see as, take for, judge, adjudge, count, deem, rate, gauge**

A chain is a **bidirectional** constraint between two or more views that allows you to **lay out** the chained views in unison. \
체인은 둘 이상의 뷰 간에 존재하는 **양방향** 제약 조건입니다. 체인을 사용하면 체인으로 연결된 뷰를 일관성 있게 **배치할** 수 있습니다.

Therefore, / the text box stretches to fill the horizontal space that remains / after the button and all the margins **are accounted for**. \
따라서, / 버튼과 모든 여백**을 고려한** 후 / 남은 가로 공간을 채우기 위해 텍스트 상자가 확장됩니다.

If your layout didn't **turn out** as expected, click See the final layout XML below to see what your XML should look like. \
레이아웃이 예상했던 대로 **표시되지** 않으면 아래의 See the final layout XML을 클릭하여 XML이 어떻게 보이는지 확인하세요.


#### Start another activity

[https://developer.android.com/training/basics/firstapp/starting-activity](https://developer.android.com/training/basics/firstapp/starting-activity)

**To clear the error,** click the View declaration, place your cursor on it, and then press Alt+Enter, or Option+Enter on a Mac, to perform a Quick Fix. \
**오류를 해결하려면** View 선언을 클릭하고 커서를 그 위에 둔 채로 Alt+Enter(Mac의 경우 Option+Enter)를 눌러 빠른 수정을 실행합니다.

**Take note** of the details in this method. \
이 메서드의 세부정보를 **확인하세요**.

They're required for the system **to recognize** the method **as compatible with** the android:onClick attribute. \
시스템에서 메서드를 android:onClick 속성과 **호환되는 것으로 인식하는 데** 필요합니다.

In MainActivity, add the EXTRA_MESSAGE constant and the sendMessage() code, **as shown**: \
MainActivity에서 **다음과 같이** EXTRA_MESSAGE 상수와 sendMessage() 코드를 추가하세요.

**Expect** Android Studio **to encounter** Cannot resolve symbol errors again. \
Android 스튜디오에서 Cannot resolve symbol 오류가 다시 **발생할 것입니다**.

**To clear the errors,** press Alt+Enter, or Option+Return on a Mac. Your should end up with the following imports: \
**오류를 해결하려면** Alt+Enter(Mac의 경우 Option+Return)를 누르세요. 그러면 다음 항목을 가져오게 됩니다.

An error still remains for DisplayMessageActivity, but that's okay. You fix it in the next section. Here's what's going on in sendMessage(): \
여전히 해결되지 않은 DisplayMessageActivity 관련 오류는 다음 섹션에서 해결할 수 있습니다. sendMessage()에서 이루어지는 작업은 다음과 같습니다. \
(어감 차이가 재밌어서 넣음)

The Class parameter of the app component, **to which** the system **delivers** the Intent, is, in this case, the activity to start. \
이 경우 시스템에서 Intent를 전송하는 앱 구성요소의 Class 매개변수는 시작할 활동입니다.



* [https://youtu.be/-Rla6eF24ZU](https://youtu.be/-Rla6eF24ZU)
* [ which 관계대명사 ] - Part 3 [ in which, to which, from which ] - 영어회화, 라이브 아카데미

**It's a good practice to** define keys for intent extras with your app's package name as a prefix. \
앱의 패키지 이름을 접두사로 사용해 인텐트 extras의 키를 정의**하는 것이 좋습니다.**

**Leave** all other properties set to their defaults and click Finish. \
다른 모든 속성은 기본값으로 **그대로 두고** Finish를 클릭합니다.

Autoconnect adds left and right constraints **in order to** place the view in the horizontal center. \
자동 연결은 수평 중앙에 뷰를 배치**하기 위해** 왼쪽과 오른쪽 제약 조건을 추가합니다.

Optionally, **you can make some adjustments to the text style** if you expand textAppearance in the Common Attributes panel of the Attributes window, and change attributes such as textSize and textColor. \
선택사항으로 Attributes 창의 Common Attributes 패널에서 textAppearance를 확장하고 textSize 및 textColor와 같은 속성을 변경하면 **텍스트 스타일을 조정할 수 있습니다.**


### App fundamentals

[https://developer.android.com/guide/components/fundamentals](https://developer.android.com/guide/components/fundamentals)

An Android package, which is an archive file with an .apk suffix, contains the contents of an Android app that are required at runtime and it is the file that **Android-powered** devices use to install the app. \
Android 패키지는 접미사가 .apk인 아카이브 파일입니다. 한 개의 APK 파일에는 Android 앱의 모든 콘텐츠가 들어 있으며, **Android로 구동하는** 기기가 앱을 설치할 때 바로 이 파일을 사용합니다.

Each Android app **lives** in its own security sandbox, protected by the following Android security features: \
각 Android 앱은 자체적인 보안 샌드박스에 **속하며**, 이는 다음과 같은 Android 보안 기능으로 보호됩니다.

By default, the system assigns each app a unique Linux user ID (the ID is used only by the system and **is unknown to** the app). \
기본적으로 시스템이 각 앱에 고유한 Linux ID를 할당합니다(이 ID는 시스템만 사용할 수 있으며 앱에서는 **인식하지 못함**).

The system sets permissions for all the files in an app **so that** only the user ID assigned to that app can access them. \
시스템은 앱 안의 모든 파일에 대해 권한을 설정**하여** 해당 앱에 할당된 사용자 ID만 이에 액세스할 수 있도록 합니다.

This creates a very secure environment **in which** an app cannot **access** parts of the system **for which** it is not **given** permission. \
이렇게 하면 대단히 안전한 환경이 구성되어 앱이 시스템에서 권한을 부여받지 못한 부분에는 액세스할 수 없게 됩니다.

It's possible to **arrange for** two apps to share the same Linux user ID, **in which case** they are able to access each other's files. \
두 개의 앱이 같은 Linux 사용자 ID를 공유하도록 **설정할** 수도 있습니다. **이 경우** 두 앱은 서로 파일에 액세스할 수 있게 됩니다.

For example, an email app might have one activity that shows a list of new emails, another activity to **compose an email**, and another activity for reading emails. \
예를 들어 이메일 앱이라면 새 이메일 목록을 표시하는 액티비티가 하나 있고, **이메일을 작성하**는 액티비티가 또 하나, 그리고 이메일을 읽는 데 쓰는 액티비티가 또 하나 있을 수 있습니다.

Although the activities work together to form **a cohesive user experience** in the email app, each one is independent of the others. \
여러 액티비티가 함께 작동하여 해당 이메일 앱에서 **짜임새 있는 사용자 환경**을 구성하는 것은 사실이지만, 각자 서로 독립되어 있습니다.

Music playback is something the user **is directly aware of**, \
음악 재생은 사용자가 **바로 인식할** 수 있는 작업입니다.

**It is tempting to think of** a content provider as an abstraction on a database, \
콘텐츠 제공자를 데이터베이스에 대한 추상화**로 생각하기 쉽습니다**.

Thus an app can decide how it wants to map the data (it contains to a URI namespace), / **handing out** those URIs **to** other entities / which can **in turn** use them to access the data. \
따라서 앱에서 (URI 네임스페이스에 넣을) 데이터를 매핑할 방식을 결정하고, / 해당 URI를 다른 엔터티**에 전달할** 수 있습니다. / 이를 전달받은 엔터티는 URI를 사용하여 데이터에 액세스합니다.



* in turn
    * ‘차례로, 결국’ 이라는 직역보다는 문맥에 맞게 번역
* The sweat then cools, which **in turn** lowers your body temperature.
    * 땀이 식으면, **이번에는** 체온을 낮추게 된다. (NE능률)
* Such heating dries out the air, which **in turn** dries out the human body. 
    * 이러한 난방은 공기를 건조**하게 해서** 인체 **또한** 건조**하게 합니다**. (YBM 올인올 영한사전)
* The nuclear reactions **in turn** created helium. 
    * **이어서** 핵 반응은 헬륨을 생성시켰다. (NE능률)

For example, if you want the user to capture a photo with the device camera, there's probably another app that **does that** / and your app can use it instead of developing an activity to capture a photo yourself. \
예를 들어 사용자가 기기 카메라로 사진을 캡처하기를 바라는 경우, **그런 작업을 수행하는** 다른 앱이 있을 가능성이 높습니다. / 그러면 사진을 캡처하는 액티비티를 직접 개발하는 대신 여러분의 앱에서 그 앱을 사용하면 됩니다.

The manifest **does a number of things** in addition to declaring the app's components, such as the following: \
매니페스트는 앱의 구성 요소를 선언하는 것 이외에도 **많은 역할을 합니다**. 예를 들면 다음과 같습니다.

Declares API libraries the app needs **to be linked against** (other than the Android framework APIs), such as the Google Maps library. \
앱이 **링크되어야 하는** API 라이브러리(Android 프레임워크 API 제외)(예: Google Maps라이브러리)를 선언합니다.



* against가 의미하는 바가 와닿지 않아서 찾아봄
* [https://ell.stackexchange.com/questions/138537/linked-against-vs-linked-with](https://ell.stackexchange.com/questions/138537/linked-against-vs-linked-with)
* 기술 문서에서는 자주 쓰이는 구문인듯 하고, 완전히 한 몸 처럼 연결되는 라이브러리(ex. 프레임워크 라이브러리)가 아니라 부분적으로 연결되는 라이브러리(ex. 서드파티 라이브러리)에 쓰이는 듯
* against라는 단어 자체가 물리적으로는 가깝고 의미적으로는 반대되는 것을 수식할 때 쓰이는 듯

**As discussed above,** in Activating components, you can use an Intent to start activities, services, and broadcast receivers. \
**위에서 설명한 바와 같이,** 활성화 상태의 구성 요소에서는 Intent를 사용하여 액티비티, 서비스 및 Broadcast Receiver를 시작할 수 있습니다.

You can also use an implicit intent, which describes the type of action to perform and, **optionally**, the data **upon which** you’d like to **perform** the action. \
또한 암시적 인텐트를 사용할 수도 있습니다. 암시적 인텐트는 수행할 작업의 유형을 설명하고, **원한다면** 작업을 **수행할 대상인** 데이터를 설명할 수도 있습니다.

To learn more about best practices and designing **robust**, production-quality apps, see Guide to App Architecture. \
모범 사례와 **안정적인** 프로덕션 품질의 앱을 설계하는 방법에 대한 자세한 내용은 앱 아키텍처 가이드를 참조하세요.

How Android restricts app access to **certain APIs** with a permission system that requires the user's consent for your app to use those APIs. \
Android가 **특정 API**에 대한 앱의 액세스를 제한하기 위해 권한 시스템을 사용하는 방법으로, 해당 API를 사용하려면 앱에 대해 사용자의 승인이 필요합니다.
