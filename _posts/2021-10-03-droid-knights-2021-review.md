---

layout: post

title: Droid Knights 2021 리뷰

categories: [Android]

tags: [Android, DroidKnights2021]

filename: 2021-10-03-droid-knights-2021-review.md

draft: 2021-09-29 16:34:00

date: 2021-10-03 01:08:00

modified: 2021-10-03 01:08:00

---

2021년 9월 25일에 안드로이드 컨퍼런스인 **드로이드나이츠 2021**이 온라인 스트리밍으로 진행되었습니다. Compose와 Hilt 등 평소 궁금했던 것 위주로만 보려고 했는데 다른 세션들도 보다보니 흥미로워서 주요 내용을 정리해보았습니다. 생략된 부분도 있으니 전체 내용이 궁금하시다면 유튜브 다시보기에서 확인해주세요.

공식 홈페이지: [https://sites.google.com/view/dk21/](https://sites.google.com/view/dk21/)

유튜브 다시보기: [https://youtube.com/playlist?list=PLu8dnNjU2FmsROfv5pNAvhRiOFVN_EmnV](https://youtube.com/playlist?list=PLu8dnNjU2FmsROfv5pNAvhRiOFVN_EmnV)


## Track1


### Jetpack Windows Manager 라이브러리와 함께 하는 폴더블 디바이스 지원, 양찬석님

원본 영상: [https://youtu.be/XeKJ4yyxFsA](https://youtu.be/XeKJ4yyxFsA)

폴더블 디바이스를 포함한 라지 스크린 기기를 대응하기 위해 어떤 부분을 살펴보면 좋은지 알 수 있었습니다.



* 폴더블 디바이스, 라지 스크린 기기의 성장 → 많은 수요가 있는 만큼 대응이 필요
* 라지 스크린 최적화
    * 디자인: 가로, 세로, 태블릿 모드 지원
    * 멀티 태스킹: 멀티 윈도우, Multi-Resume, 드래그 & 드롭 지원
    * 입력 모드: 터치 타깃 크기는 최소 48dp, 키보드/마우스 지원
* 라지 스크린 케이스 스터디
    * [https://developer.android.com/large-screens/stories](https://developer.android.com/large-screens/stories)
* 4가지 종류의 디바이스

<table>
  <tr>
   <td>
<strong>디바이스</strong>
   </td>
   <td><strong>기본 오리엔테이션</strong>
   </td>
   <td><strong>대표 화면 크기</strong>
   </td>
  </tr>
  <tr>
   <td>폰
   </td>
   <td>세로
   </td>
   <td>360 x 640 dp
   </td>
  </tr>
  <tr>
   <td>폴더블
   </td>
   <td>가로 / 세로
   </td>
   <td>756 x 945 dp
   </td>
  </tr>
  <tr>
   <td>태블릿
   </td>
   <td>가로
   </td>
   <td>1280 x 800dp
   </td>
  </tr>
  <tr>
   <td>데스크탑
   </td>
   <td>가로
   </td>
   <td>1920 x 1080 dp
   </td>
  </tr>
</table>




* Adaptive layouts: 화면을 그대로 비율만 늘린 것이 아닌 화면 크기별 적절한 레이아웃 제공
    * 텍스트: 큰 화면에서 텍스트 양 옆에 여백 또는 단을 나누어 제공
    * 버튼, 입력폼: 마찬가지로 여백, 컬럼 활용
    * 목록, 내비게이션 바: 화면 하단 대신 양 옆이나 상단으로 옮기기
    * 미디어, 카메라: 테이블 탑 모드 활용
* Jetpack WindowManager
    * 새로운 폼팩터(폴더블 등)와 멀티 윈도우 지원을 위한 라이브러리로 변경
    * WindowMetrics / WindowMetricsCalculator
        * 현재 윈도우 크기 구하기
        * 기존에 크기 구하는 방법들은 모두 문제가 있기 때문에 이걸 사용 권장
    * DisplayFeature
        * 컷아웃, 힌지 등 디스플레이의 물리적 특성을 추상화해서 제공
        * 현재는 폴딩 피쳐만 제공
    * WindowInfoRepository
        * 레이아웃 변경 사항 감지
* 테이블탑 모드를 위한 레이아웃 제공 방법
    * FragmentManager를 이용 새로운 Fragment로 UI 교체
    * Constraint layout, Motion layout에서 제공하는 가이드 라인 위치를 변경
        * 단순한 레이아웃에서만 적용 가능


### 다시 살펴보는 AndroidX, pluu님

원본 영상: [https://youtu.be/QICJtfvsYc8](https://youtu.be/QICJtfvsYc8)

support library와 androidx에서 안드로이드 버전, 하드웨어 지원 여부, 테마 등의 분기처리를 어떻게 하는지 내부 구조까지 함께 소개해주어서 라이브러리에 대한 이해를 높일 수 있었습니다. 어디까지 라이브러리를 믿고 사용하면 되는지, 어디서부터는 개발할 때 신경써서 처리해주어야 하는지 알 수 있었습니다.



* Jetpack과 AndroidX
    * Jetpack: 개발자가 고품질 앱을 손쉽게 작성할 수 있도록 해주는 라이브러리, 도구, 가이드를 모아둔 제품
    * AndroidX: Jetpack이 추구하는 가이드라인을 실체화한 라이브러리
    * 플랫폼 릴리즈와 분리(=unbundled) → 빠른 버그 수정, 새로운 기능 도입
* Support Library의 문제점
    * v4/v7 등이 처음엔 호환성을 지원하는 최소 버전을 의미했지만, 실제 최소 지원 버전이 14로 올라감
    * support-v4 안에 어떤 라이브러리들이 있는지 파악이 어려움
    * 일부 기능만 업데이트 해도 라이브러리 전체의 버전이 올라감
* LayoutInflater
    * 레이아웃 xml 파일을 해당 View 개체로 인스턴스화
    * Theme에 따라 적절한 뷰 선택
        * ex) Button → Button | AppCompatButton | MaterialButton
    * style에 커스텀한 layout inflater를 적용할 수 있음
* Configuration
    * OS 버전과 하드웨어에 따른 분기처리를 도와줌
        * ex) ContextCompat(getDrawble 등), WindowInsetsCompat
    * ViewCompat.setElevation 등 모든 하위 버전을 호환하지는 못하는 경우가 있음
* New Result API
    * 기존 startActivityForResult, onActivityResult 등이 deprecated 됨
    * → registerForActivityResult를 통해 액티비티 시작, 권한 요청, 사진 찍기 등이 가능
* minSdkVersion
    * 대부분 아이스크림 샌드위치부터 제공하지만 몇몇 라이브러리는 더 높은 버전부터 제공하므로 확인 필요
        * browser, camera, compose, security, wear compose 등
* Androidx에서 안되는 것
    * 제조사 혹은 런처에서 제공하는 기능
        * ex) 앱 아이콘의 빨간색 뱃지, 숫자 카운트


### 안드로이드 앱에서 Koin걷어내고 Hilt로 마이그레이션하기, 이기정님

원본 영상: [https://youtu.be/G2gaUnFGGV0](https://youtu.be/G2gaUnFGGV0)

Koin에서 Hilt의 특징과 장단점을 비교하여 설명해주시고, 실제로 Koin에서 Hilt로 마이그레이션을 하면서 생기는 문제점을 공유해주셔서 어떤 경우에 Hilt를 사용하는 것을 고려해야하는지 생각해볼 수 있었습니다.



* Koin
    * 특징
        * Kotlin DSL 사용
        * 런타임에 의존성 주입
        * 빌드 시간에 Stub 파일을 생성하지 않음
        * AAC ViewModel 사용 시 별도의 라이브러리를 통해 의존성 주입이 가능
    * 장점
        * 러닝 커브가 낮음
        * Kotlin 개발 환경에 도입하기 쉬움
        * 별도의 어노테이션을 사용하지 않아 컴파일 시간 단축
        * ViewModel 주입을 쉽게 할 수 있는 별도의 라이브러리 제공
    * 단점
        * 런타임시 컴포넌트가 생성되어 있지 않으면 크래시 발생
        * 런타임 퍼포먼스가 떨어짐
            * 런타임에 서비스 로케이팅을 통해 인스턴스를 동적으로 주입
            * 리플렉션 이용
        * 모듈간 의존성을 신경쓰지 않으면 추후 멀티모듈로 전향시 어려움
            * `koin.get()` 함수를 사용하는 경우 인스턴스가 생성이 되었는지 모름
            * 인스턴스 주입이 필요한 클래스가 많아질수록 런타임시 객체 주입에 대한 검증을 하기 어려워짐
            * → `koin.get()` 함수를 제거하고 각 사용처에 적합하게 koin 모듈 생성
    * → 런타임 세이프한 DI 툴의 필요성 대두(Hilt, Dagger 등)
* Hilt
    * 특징
        * Dagger를 래핑한 DI 라이브러리
        * Dagger에서 관계 스코프 설정을 위한 러닝커브가 높았던 문제를 해결
        * 장점
            * 보일러 플레이트 코드가 줄어듬
            * 설정이 간편
            * 테스트하기 좋음
            * Dependency cycle 없음
* Service Locator vs Dependency Injection

<table>
  <tr>
   <td>
   </td>
   <td>
Hilt(Dependency Injection)
   </td>
   <td>Koin(Service Locator)
   </td>
  </tr>
  <tr>
   <td>종속성
   </td>
   <td>일부 핵심 클래스에 종속성 주입
   </td>
   <td>모든 클래스가 서비스 로케이터에 종속
   </td>
  </tr>
  <tr>
   <td>호출방법
   </td>
   <td>처음 한 번만 호출(명시적 호출 없음)
   </td>
   <td>인젝터를 직접 호출(명시적 호출)
   </td>
  </tr>
  <tr>
   <td>의존 관계
   </td>
   <td>의존 관계 파악이 쉬움
   </td>
   <td>의존 관계 파악이 어려움
   </td>
  </tr>
  <tr>
   <td>Build → 
   </td>
   <td>(DI container, 객체 생성, 주입) generate → run
   </td>
   <td>run (DI container, DI 객체 생성 및 주입)
   </td>
  </tr>
</table>




* Koin vs Dagger2 vs Hilt

<table>
  <tr>
   <td>
   </td>
   <td>
Koin
   </td>
   <td>Dagger2
   </td>
   <td>Hilt
   </td>
  </tr>
  <tr>
   <td>러닝커브
   </td>
   <td>낮음
   </td>
   <td>높음
   </td>
   <td>낮음
   </td>
  </tr>
  <tr>
   <td>Java
   </td>
   <td>X
   </td>
   <td>O
   </td>
   <td>O
   </td>
  </tr>
  <tr>
   <td>Kotlin
   </td>
   <td>O
   </td>
   <td>O
   </td>
   <td>O
   </td>
  </tr>
  <tr>
   <td>에러 검출 시점
   </td>
   <td>런타임
   </td>
   <td>컴파일 타임
   </td>
   <td>컴파일 타임
   </td>
  </tr>
  <tr>
   <td>실제 프로젝트 검증
   </td>
   <td>많은 앱에서 검증됨
   </td>
   <td>많은 앱에서 검증됨
   </td>
   <td>정식 버전(낮은 점유율)
   </td>
  </tr>
</table>




* Koin → Hilt 마이그레이션 적용기
    * 영상 12:20 부터 참고
* 주요 Hilt Annotation Class
    * `@HiltAndroidApp`
        * `Application`을 상속받는 클래스에 `@HiltAndroidApp` 어노테이션을 붙이면 해당 클래스가 다음과 같은 역할을 함
            * Application scope의 컨테이너 역할
            * Hilt의 모든 어노테이션이 붙은 모듈을 생성하도록 트리거하는 역할
    * `@AndroidEntryPoint`
        * `Activity`, `Fragment`, `Service` 등에 해당 어노테이션을 붙이면 다른 `@AndroidEntryPoint` 주석이 있는 클래스에 종속 항목을 제공할 수 있음
        * AAC 뷰모델은 `@HiltViewModel` 사용
    * `@InstallIn`
        * `@Module`과 함께 Hitl 모듈 선언시 사용
        * `@Provides` 또는 `@Binds`로 모듈 선언
    * `@EntryPoint`
* Hilt로 마이그레이션 하면서 생긴 문제들
    * Koin을 통해 주입된 클래스의 의존성을 알기 어려운 경우
        * `koin.get()` 대신 `@Provides`를 통해 koin 인스턴스 주입
        * 모든 `koin.get()`이 `@Provides`로 바뀌어 추적이 가능해지면 `@Inject`로 변경
    * `Fragment.context != Activity.context`
        * `context.getBaseContext()`로 액티비티의 컨텍스트를 가져올 수 있음
    * 생성자에서 기본값 사용 불가
        * BasePresenter의 멤버 변수로 이동
    * 동적 매개변수 주입
        * Koin에서는 런타임에 동적으로 매개변수를 주입할 수 있었지만 Hilt는 안됨
        * `lateinit var` 변수로 빼서 나중에 받을 수 있도록 함
* 마이그레이션하면서 정리한 결론
    * Koin과 Hilt가 공존하는 것은 많은 문제를 야기할 수 있음
    * Koin에서 Hilt로 넘어가는 가이드가 없으니 서비스마다 적절하게 판단
    * 주입에 대한 테스트 코드가 잘 작성되어 있다면 Hilt를 반드시 도입할 필요는 없음
    * Dagger2에서 보일러플레이트를 작성하는데 어려움이 있었다면 Hilt는 필수
    * 동적으로 주입하는 코드가 많다면 Hilt 추천
    * 멀티모듈 사용시 무분별한 주입을 했다면 dependency graph를 명확히 정하자


### 2021 Junior Jetpack, 김민식님

원본 영상: [https://youtu.be/KgpsS2IOLV4](https://youtu.be/KgpsS2IOLV4)

주니어를 대상으로 개인 경험을 공유하고 안드로이드에서 공부해야 할 부분을 전반적으로 추천해주셨습니다.


### AppBundle 괴담, 차영호님

원본 영상: [https://youtu.be/EVYnTe6aXWQ](https://youtu.be/EVYnTe6aXWQ)

다양한 화면 크기와 언어 등을 지원하여 앱 크기가 큰 경우 split apk로 배포할 때 생길 수 있는 문제점과 대응 방법을 알 수 있었습니다. Facebook SoLoader 사례를 통해 버전별 네이티브 라이브러리 압축 방식의 차이점과 생길 수 있는 문제점과 대응 방법을 알 수 있었습니다.



* AppBundle이 나눠서 배포해줄 수 있는 설정들
    * DPI(hdpi, xhdpi 등)
    * 언어(en, ko 등)
    * ABI(Application Binary Interface)
    * Texture Format
    * → `app/build.gradle`에서 원하는 설정을 `enableSplit = true`
* Split APK
    * `.aab` 파일을 구글 플레이스토어에 업로드하면 실제로 유저가 다운로드 받는 것은 `.apk` 파일들의 집합
* Sideloading of split APK files
    * 사이드로딩: 구글 플레이스토어가 아닌 다른 경로로 앱을 다운로드 받는 것
    * Split APK 중 일부를 누락해서 다운받으면 앱이 정상적으로 설치된 것처럼 보이지만 실제로 리소스에 접근할 때 해당 리소스가 없거나(DPI 누락), 네이티브 라이브러리를 로딩하는 순간(ABI 누락) 크래시가 남
* 케이스 스터디
    * 누락된 split apk 찾기
        * `getInstallerPackageName`을 통해 구글 플레이스토어를 통해 설치되었는지 확인할 수 있음
        * `splitNames`로 현재 설치된 split apk를 확인할 수 있음
    * Facebook SoLoader
        * 구형 안드로이드(4.2 젤리빈 이하)에서 네이티브 라이브러리를 문제없이(종속성 관련) 로딩하기 위한 라이브러리
        * React Native, Yoga Layout에서 사용
        * 안드로이드 23(마시멜로우) 부터 네이티브 라이브러리를 압축하지 않고 apk에 포함하면서 SoLoader가 네이티브 라이브러리를 못 찾는 문제가 발생
            * `android.bundle.enableUncompressedNativeLibs = false`로 이전 버전처럼 동작하게 할 수 있지만 저장 공간 등 이점을 잃어버림
        * 어차피 SoLoader가 22(롤리팝) 이하에서만 필요하기 때문에 SoLoader를 직접 수정하여 22 이하일 때만 동작하도록 함


### Jetpack Compose에 있는 것, 없는 것, 안성용님

원본 링크: [https://youtu.be/Wx_arIKIvM8](https://youtu.be/Wx_arIKIvM8)

Jetpack Compose의 장단점을 소개하고 기존 xml 뷰와 비교하며 어디까지 구현이 가능한지 알기 쉽게 설명해주셨습니다. 이제 막 베타 버전이 되어서 도입하기엔 조금 이른 감이 있지만 생각보다 많은 기존 뷰 컴포넌트를 커버할 수 있어서, 기존 앱이 머티리얼 테마 위주로 구현되어 있거나 뷰 계층 구조가 복잡한 경우 컴포즈를 사용해보는 것을 고려해볼만 한 것 같습니다.



* View 보다 Compose가 나은 것
    * 플랫폼 종속성 최소화
        * 뷰: API 마다 최소 버전 제약, Compat API로도 한계가 있음
        * 컴포즈: 라이브러리로 제공되어 플랫폼에 덜 종속적
    * 상속으로 인한 문제 해소
        * 뷰: 상속으로 인해 불필요한 부모의 기능(ex. 버튼에서 텍스트뷰 관련 기능들)을 갖게 됨
        * 컴포즈: composable 함수들로 구성되어 필요한 기능만 작게 유지할 수 있음
    * 중첩 레이아웃 성능
        * 뷰: 뷰그룹에 따라 measure를 여러 번 수행하여 레이아웃이 중첩되지 않도록 신경써주어야 함
        * 컴포즈: measure를 한 번만 수행하도록 강제되어 중첩 레이아웃에서도 성능이 크게 저하되지 않음
    * UI 재사용성
        * 뷰: 중첩 성능 문제로 include 대신 merge를 고려해야 하는 경우가 있음
        * 컴포즈: 재사용이 필요한 부분을 별개의 composable 함수로 분리하면 됨
    * 지연 초기화
        * 뷰: ViewStub 사용이 불편
        * 컴포즈: 조건문으로 간단히 구현 가능
    * Single Source Of Truth
        * 뷰: 렌더링을 위해 데이터와 별개의 상태를 갖게 됨
        * 컴포즈: 별개의 상태를 갖지 않아 SSOT를 유지할 수 있음
    * 데이터 바인딩
        * 뷰: 데이터 바인딩 목적으로 xml과 바인딩 어댑터를 작성해야 함
        * 컴포즈: 별개의 composable 함수로 분리하고 상태만 지정하면 자동으로 바인딩 됨
    * 커스텀 뷰 구현
        * 뷰: 커스텀 뷰를 만들 때도 xml 코드 작성 필요
        * 컴포즈: 코틀린 코드만 작성하면 됨
    * 목록형 UI 구성
        * 뷰: 목록형 UI 작성시 레이아웃 매니저, 어댑터 등 많은 코드를 작성해야 함
        * 컴포즈: 다른 composable 함수와 동일한 방법으로 쉽게 구성 가능
* 비교하기에 애매한 부분들
    * 뷰를 모두 제거하고 컴포즈만 쓰면 APK 크기와 빌드 시간 감소
    * 하지만 뷰와 컴포즈를 함께 쓰면 APK 크기와 빌드 시간이 약간 증가
    * 컴포즈에서도 뷰를 사용할 수 있음
    * Java + XML 코드를 코틀린으로 전환하는 비용
    * 뷰의 유지보수 비용 vs 컴포즈 학습 비용
    * 뷰와 비슷하게 AOT 컴파일 지원 (ProfileInstaller)
        * 컴포즈가 라이브러리라서(?) 미리 로드할 수 없어 AOT의 장점을 못가져옴
        * 이런 부분을 보완하는 ProfileInstaller라는 라이브러리가 있음
            * N 부터 지원해서 M 이하 버전은 이점이 없음
* View 보다 Compose가 아쉬운 점
    * min sdk 제약 (21 이상에서만 가능)
    * 뷰와 컴포즈가 서로 변환되지 않음
    * 머티리얼 테마만 기본으로 지원
    * Xml 보다 프리뷰 성능이 떨어짐 → 생산성 저하
    * Xml을 사용할 때 보다 리뷰할 코드가 늘어남
    * 지원하는 서드파티 라이브러리가 적음
* Compose에 없는 것
    * 테마
        * 머티리얼 테마만 지원(AppCompat 등 지원 안함)
        * 기존 프로젝트에 컴포즈 적용시 테마가 두 벌(xml, kotlin)이 됨
        * → MDC-Android Compose Theme Adapter, AppCompat Compose Theme Adapter 라고 기존 xml 테마를 기반으로 컴포즈 테마를 구성해주는 라이브러리가 있음 (머티리얼이 지원하는 속성이 더 많아서 AppCompat은 의도한 결과가 안나올수도 있음)
        * 커스텀 테마를 사용하고 있는 경우 compose-material에 있는 컴포넌트를 그대로 사용하기 어려워질수도 있음
    * 리소스
        * colorStateList, selector, drawable, animated-selector, nine_patch, GradientDrawable 등 상태에 따라 변경되는 리소스 사용 불가
        * Selector 대신 InteractionSource를 사용해 상태 확인 가능
    * 위젯
        * 대부분의 위젯(ImageView, TextView, Button, CheckBox 등) 지원
            * ViewStub, WebView, CheckedTextView, TextureView, SurfaceView 지원 안함
        * margin
            * Padding, box로 대체
        * foreground
            * 레이아웃 중첩으로 대체
        * visibility
            * 현재는 invisible을 지원하지 않음
        * TextView
            * autoSizeTextType, includeFontPadding, autofillHints 속성 지원 안함
            * EmojiTextView 지원 안함
        * ImageView
            * adjustViewBounds 속성 지원 안함
        * ProgressBar, SeekBar
            * secondaryProgress, thumb 속성 지원 안함
        * Canvas
            * Drawable를 써야하면 natvieCanvas를 사용하면 됨
    * 뷰그룹
        * 대부분의 뷰그룹(LinearLayout, ScrollView, RecyclerView 등) 지원
            * RelativeLayout, MotionLayout, ViewPager, Toolbar, BottomSheet 지원 안함
        * RecyclerView
            * itemDecoration, itemAnimator, fastScrollEnabled 지원 안함
            * GridLayoutManager, StaggeredGridLayoutManager 시험적으로 지원하거나 지원 안함
    * 메시지
        * Toast
            * 지원 안함
            * Context 대신 LocalContext.current을 사용해서 쓸 수는 있음
        * Dialog
            * Title, message, positive/negative button 등 기본 기능 외에는 아직 지원 안함
        * Fragment
            * 더 이상 사용하지 않지만 화면별로 상태를 저장해야하는 경우 rememberSaveable을 사용할 수 있음
            * 화면별 내비게이션 스택 저장은 rememberSaveableStateHolder, SaveableStateProvider 사용
    * 애니메이션
        * Interpolator
            * 대부분 지원하지만 PathInterpolator는 지원하지 않음
        * ViewPropertyAnimator
            * 컴포즈에서는 하드웨어 가속이 기본이라 withLayer 같은 레이아웃 타입을 바꾸는 api는 지원하지 않음
        * Transition
            * exitTransition, enterTransition 등 일부 API를 지원하지 않음
            * beginDelayedTransition은 각각 개별적으로 적용해야 하고 sequential 하게 처리할 수 없음(병렬만 가능)
        * View Animation
            * 지원 안함(alpha, translate, scale, rotate 등 xml 에서 적용하는 애니메이션 불가)
        * Shared Elements
            * 지원 안함
* Compose 전환 준비하기
    * 컴포즈에서 지원하지 않는 기능들을 원래 잘 사용하지 않았다면 전환해볼만 함
    * 사용하는 Jetpack 라이브러리가 컴포즈를 지원하는지 확인
        * ViewPager, ViewPager2, Preference, Emoji 등은 컴포즈 지원 안함
    * ConstraintLayout
        * ConstraintLayout을 사용하는 목적이 중첩을 줄이려는 목적인데 컴포즈에서는 중첩으로 인한 성능저하가 적으니 Constraint Layout을 사용하는 대신 그냥 중첩해서 레이아웃을 구성하는게 생산성 측면에서 나을 수도 있음
    * 외부 라이브러리
        * 컴포즈 지원: Lottie, Coil, Accompanist 등
        * 컴포즈 지원 안함: Picasso, ExoPlayer, FlexboxLayout, Glide, PhotoView 등
            * → Coil 이나 Landscapist로 마이그레이션 검토
        * Accompanist
            * 컴포즈에 없는 기능을 제공하는 라이브러리
                * SwipeRefreshLayout, ViewPager, FlexboxLayout 등을 대체하는 라이브러리 제공
                * Placeholder 같은 새로운 기능도 있음
            * 컴포즈나 외부 라이브러리에서 해당 기능이 추가되면 Accompanist에서는 제거될 수 있음(최근 이미지 로딩 라이브러리가 제거되었다고 함)


### 앱 성능분석 어떻게 시작할까?, 최대순님

원본 영상: [https://youtu.be/1NelJuMzig4](https://youtu.be/1NelJuMzig4)

앱 시작 구간(Startup)을 중점적으로 어떻게 성능 이슈를 측정 및 감지하고 문제가 있는 부분을 분석하는 방법까지 AndroidProfiler를 이용한 예시를 통해 설명해주셔서 로그 찍어보기 같이 단순무식한 방법이 아닌 분석 툴을 사용하는 방법을 알 수 있었습니다.



* 성능 분석이 필요한 이유
    * 빠르고 정확한 기능 전달
    * → 유입 증가, 사용시간 증가, 이탈 감소
* 성능분석 사이클
    * 측정 → 감지 → 분석 → 개선
    * 측정 및 감지
        * 성능 측정 코드 작성(Custom code), 벤치마크 툴, 플레이 콘솔, 파이어베이스, 직접 사용(QA 등)
    * 분석 및 개선
        * Systrace, Android Studio Profiler, Prefetto
* 안드로이드 앱에서의 성능 지표
    * ANR, Crash, Rendering, Startup, Network, File IO 등
* Startup
    * 런처에서 앱을 실행하여 사용자가 서비스와 상호작용 할 수 있게 되기까지 과정
    * Cold Start
        * 살아있는 앱 프로세스가 없는 상태에서 처음 앱을 시작
    * Hot Start
        * 이미 메모리상에 앱이 존재하여 activity만 foreground로 노출
    * Warm Start
        * 기존 실행되었던 프로세스에 의해 일부 정보가 저장되어 있는 상태에서 앱을 시작
* Startup Time 측정 방법들
    * 로그로 찍어보기
        * ActivityTaskManger: Displayed
            * 첫 번째 프레임이 그려진 시간
        * ActivityTaskManger: Fully drawn
            * Activity.reportFullyDrawn()이 호출된 시점
            * 커스텀 설정(네트워크 요청 등)으로 인해 실제로 상호작용 가능한 화면이 그려지기까지 시간
    * Play Console - Android Vital - 앱 시작 시간 확인해보기
    * Firebase Performance - trace - _app_start 확인해보기
        * ContentProvider.onCreate ~ Activity.onResume 까지의 시간
    * 커스텀 측정 방법
        * 세분화된 구간(콜드, 웜, 핫)에서 정확한 측정이 요구되는 경우
            * 핫은 Application 클래스에서 플래그 변수로 간단히 확인 가능
            * 콜드인지 웜인지 구분하는건 런처 액티비티를 찾아서 번들이 있는지 확인
        * 측정하고자 하는 구간에 대한 이해 필요
            * ActivityThred.bindApplication
                * `Process.getStartUptimeMills()`로 가져올 수 있음
            * Init Application
            * Init ContentProvider
                * 컨텐트 프로바이더 init이나 onCreate에서 `SystemClock.uptimeMills()`로 시간 가져오기
                * 프로바이더 끼리의 순서는 보장되지 않으므로 주의
            * ContentProvider.onCreate
            * Application.onCreate
            * Activity.onCreate
            * Activity.onResume
            * First Draw
                * onDrawListener를 등록하여 onDraw가 두번째로 호출되는 시점이 첫 프레임이 그려지고 난 직후임
        * 측정 구간
            * Component Load
                * BindApplication - Application.onCreate Start
            * Application onCreate
                * Application.onCreate Start - End
            * Activity onCreate
                * Activity.onCreate Start - End
            * Activity onResume
                * Activity.onResume Start - End
            * First Draw
                * Activity.onResume End - onDraw 2nd tick
* AndroidProfiler 옵션
    * Sample Java Methods
        * Java-based code 콜스택을 주기적으로 캡쳐
        * 실행시간이 짧은 메서드는 누락될수도 있음
        * 그래도 웬만한 경우는 이걸로 충분
    * Trace Java Methods
        * Java 메서드 실행을 추적
        * 모든 메서드를 추척할 수 있지만 앱이 느려지고 트레이스 파일 자체가 커질 수 있음
    * Sample C/C++ Functions
        * Java, C 콜스택을 캡쳐
    * Trace System Calls
        * 시스템리소스와 사용작용을 추적
        * 이걸로 대략적인 원인을 파악하고 Sample Java Methods로 세부 내용 파악하는 순서로 진행
* 효과적인 성능분석을 위해서는
    * 성능분석 체계와 시스템이 중요
    * 분석보다 측정과 감지
    * 제공하고 있는 서비스에 맞는 분석 체계
    * 분석 사이클 및 효과에 대한 히스토리 관리 필요


## Track2


### 액티비티:코드제로, 정승욱님

원본 영상: [https://youtu.be/lkrEfYO54xU](https://youtu.be/lkrEfYO54xU)



* 목표
    * 액티비티와의 명시적 상호작용 없애기
    * 로직 코드 유닛 테스트
    * 컴포넌트 추상화, 라이프 사이클 처리
* 데이터 바인딩과 Rx, Flow를 써도 남아있는 문제
    * 이미지 버튼 클릭시 액티비티 의존성
        * 저장소 접근 권한 여부 확인
        * 권한 부여 여부 후처리
    * 스트림 처리시 스트림 종료 이슈
        * Flow는 Scope로 처리
        * RxJava는 Scope를 활용하여 Dispose 정의 추가
    * ViewModel init 시 Activity lifecycle 위배
        * Lifecycle init 시 처리 변경 필요
    * 데이터 바인딩은 뷰 콜백 이벤트 처리시 스트림 단절이 생김
* 해결 방법
    * Lifecycle awareness 기반 RxJava 또는 Flow 지향
        * 커스텀 어노테이션(CreatedToDestory, StartedToStop, ResumedToPause)으로 뷰모델 로직이 동작하는 구간을 액티비티의 특정 라이프 사이클 범위로 제한
    * ViewModel에서 모든 로직 처리
        * 데이터 바인딩 활용
        * 피치 못할 외부 컴포넌트는 Usecase 등으로 분리 후 호출
            * ex) 애니메이션 등 뷰의 상세한 정보를 받아야 하는 경우
    * Activity 의존적 컴포넌트들은 래핑
        * 액티비티에 의존적이고 RxJava, Flow를 지원하는 컴포넌트들
            * ActivityResult 처리
            * 뷰 이벤트 콜백: 텍스트 입력, 클릭, 토글 스위치, 백키 클릭 등
            * 이전 화면에서 받은 번들
            * 캐싱을 위해 저장한 번들
            * 액티비티 내비게이션
            * 권한 체크 및 요청
        * 유닛 테스트를 위한 모킹 객체 추가
        * 라이프 사이클에 맞춰 함수를 호출할 때 참조변수를 바인딩하여 호출
            * 단점
                * 화려한 애니메이션에 취약
                * RecyclerView의 아이템 클릭 이벤트 처리는 래핑이 어려움(원래대로 써야함)
    * 위 해결 방법 적용 후에는 액티비티에 DI, XML, 데이터 바인딩 설정만 남음
    * Compose 전환
        * 블로그 참고: [https://jsuch2362.medium.com/](https://jsuch2362.medium.com/)


### 복잡한 RecyclerView, 군더더기 없이 데이터로 표현하기, 김호중님

원본 영상: [https://youtu.be/mqY3GWid7ug](https://youtu.be/mqY3GWid7ug)



* 스크롤 뷰, 리사이클러 뷰 중첩/중복의 문제점
    * 어댑터와 뷰 홀더로 인한 보일러 플레이트 코드 증가
    * 복잡한 계층 구조로 실제 구현 코드 탐색이 어려움 → 유지 보수도 어려움
* 어댑터의 문제점
    * 뷰 홀더의 구현이 어댑터에 의존
    * 뷰 홀더의 타입이 어댑터 내부에서 정의됨
    * 의존성 때문에 뷰 홀더의 재활용이 어려움
        * 비즈니스 로직만 다르고 뷰는 동일한 경우에 재활용하면 좋은데 그게 힘듦
* 중복된 구현의 어댑터 줄이기
    * 뷰 홀더와 어댑터간의 의존 관계 제거
    * 어댑터에 전달할 뷰 타입을 외부에서 정의
        * 뷰 타입을 기준으로 모델과 뷰 홀더를 매핑
            * 모델은 자기 자신의 뷰 타입을 들고 있는 순수 데이터 모델
            * 뷰 홀더는 해당 뷰 타입을 어떻게 보여줄지 정의
        * 어댑터 내부를 구현할 필요 없이 뷰 타입과 뷰 홀더만 주입해주면 됨
        * 어노테이션으로 매번 어댑터에 주입할 필요도 없게 만들 수 있음
* 데이터 바인딩으로 뷰홀더 구현 없애기
    * 비즈니스 로직이 간단한 경우 AutoBindingViewHolder 구현
        * 간단하다 = xml에 데이터 바인딩으로 충분하다
        * 뷰 홀더에 공통적으로 필요한 정보(xml 레이아웃 id, 데이터 모델, 라이프사이클 오너 등)를 생성자로 주입
            * 생성자에서 라이프사이클 오너를 주입받지 못한 경우 생성 시점에서 가장 가까운 라이프사이클 오너(가장 가까운 프래그먼트나 액티비티)를 찾도록 구현
        * Xml에 필요한 정보를 데이터 바인딩
        * 뷰 홀더에 뷰 타입을 매번 주입할 필요가 없도록 데이터 모델이 viewType과 bindingVariableId를 들고 있도록 함
            * viewType: xml 레이아웃 id
            * bindingVariableId: `BR.<xml에 정의된 데이터 모델의 variable name>`
    * 어댑터의 onCreateViewHodler에서
        * 해당 모델이 AutoBindingModel이라면 AutoBindingViewHodler로 뷰 홀더 생성
        * 복잡한 비즈니스 로직이 필요한 경우 별도로 구현한 클래스 생성
* RecyclerView 상태를 ViewModel에 표현하기
    * 요구 사항
        * RecyclerView의 Item List와 함께
        * Adapter와의 의존이 없는 상태로
        * Notify, SubmitList 등의 API 사용
    * 해결 방법
        * 어댑터 인터페이스를 통해 어탭터 의존성을 주입받기
        * → RecyclerViewState라는 이름의 클래스를 만들어 아이템 리스트와 주입받은 어댑터를 들고 있게 하기
            * 어댑터의 의존성을 없애고도 어탭터의 기능을 사용할 수 있음
    * 위 방법을 적용하면
        * RecyclerViewState를 통해 뷰모델에서 바로 아이템 리스트 동기화
            * 뷰모델에서 아이템 리스트가 변경되었을 때 뷰의 상태를 동기화하기 위하여 계층을 통하여 전파할 필요 없이 직접 해당 계층의 리사이클러 뷰에 바뀐 데이터를 동기화할 수 있음
        * 데이터(모델)의 구조가 뷰 계층의 구조와 동일해져 깊은 깊이의 UI도 유지보수가 간편해짐
* 리스트 상태와 컴포즈
    * 컴포즈에서는 MutalbleList만 변경해도 자동으로 UI가 업데이트 됨
        * `mutalbleStateListOf()`에서 내부적으로 `SnapshotStateList`를 만들어주기 때문
        * SnapShot
            * 레이스 컨디션이나 중복 스냅샷을 내부적으로 관리해줌
            * read/write 옵저버 등록 가능
        * SnapShotStateList
            * add() → conditionUpdate → 스냅샷과 비교해서 변경된 것이 있으면 상태 변경 → 스냅샷을 옵저빙하고 있는 composable이 알게 됨
    * Child Composable만 구현하면 리스트(데이터)의 변경을 자동으로 감지하고 UI 업데이트(Lazy Composable)
    * 기존에는 리스트를 업데이트 하기 위해 Adapter, DiffUtil, ViewHolder, Payloads, ViewType 등 많은 데이터를 넘겨주었어야 했는데 컴포즈를 사용하면 그럴 필요 없음!


### 해커 입장에서 생각해보고 안전한 앱 개발하기, 송성현님

원본 영상: [https://youtu.be/xwrSg8RkJx0](https://youtu.be/xwrSg8RkJx0)

공격 시연 영상이 재밌으니 원본 영상을 보시는 것을 추천드립니다.



* 안드로이드 대상 공격 사례
    * 엑시노스 드라이버의 취약점을 이용해 루트 권한 탈취 (옛날 일)
    * 이미지 관련 오픈소스의 double free 취약점을 이용해 gif 파일에 셸 코드를 담아 공격 대상의 기기를 원격으로 조작
* 일반적으로 해커가 자신의 디바이스에서 루트 권한을 탈취하여 앱의 취약점을 공격
    * UID 0 획득하기(루팅)
        * OEM unlock(부트로더 언락)
            * Secure boot chain: 다음에 실행할 이미지를 실행하기 전에 verify
            * 롬에 있는 프라이머리 부트 로더 → 세컨더리 부트 로더 검증 후 로딩 → … → 안드로이드 부트 로더(aboot)가 안드로이드 리눅스 부트 로더 로딩
            * 안드로이드 리눅스 부트 로더 단계에서는 언락하면 무결성이 깨진 커널을 로딩할 수 있음
            * 새로운 커널 패치 시 언락 후 패치 후 다시 로드
        * Install TWRP(커스텀 리커버리)
            * 안드로이드 OS를 업데이트 할 때 제조사에서 설치할 이미지를 검증하는 과정을 건너뛰어 아무 이미지나 다 설치할 수 있음
        * 루팅 툴 설치
            * SuperSU 방식
                * 루트 파일 시스템에 있는 init.rc에 daemonsu.rc를 uid 0로 실행하는 코드 파일을 추가하여 실행하는 앱이 daemonsu를 통해 루트 권한을 획득
            * Magisk 방식
                * init 자체를 패치해서 uid 0 획득
    * SEAndroid 우회하기
        * SEAndroid: 루트 권한이 있어도 사전에 정의되지 않은 행동을 제한
        * SuperSU 방식
            * 허용된 동작들이 정의되어 있는 sepolicy라는 파일을 패치하여 원하는 동작을 추가
        * Magisk 방식
            * init 프로세스 자체를 직접 생성하는 방식이라 init 프로세스 과정에서 sepolicy 파일을 생성
* 앱이 자기자신을 보호하는 방법
    * 디바이스가 루팅되어 있는지 확인
    * 코드 난독화
    * 앱이 실행되는 환경이 에뮬레이터인지 확인
    * 앱이 디버깅되고 있는지 확인
    * 앱 코드가 수정되지 않았는지 확인
    * → 공격을 모두 막을 수 있는 방법은 없음. 그저 시간을 늦출 뿐…
* 결론
    * 모바일 앱의 모든 중요 or 개인 정보는 노출될 수 있음
        * 그것이 메모리에 존재해도, 암호화 되어 있어도, TEE에 보관되어 있어도
    * 중요 or 개인 정보의 사용을 최소화 하자
        * 작은 정보가 큰 문제의 단초가 될 수 있다
        * 반드시 필요한 정보가 아니면 서버에서 내려받지도 말 것
    * 사용자를 항상 의심하자
        * 적절한 권한이 있는 사용자여도 항상 의심하고 검증
    * 오픈 소스 사용을 관리하자
    * 시큐어 코딩 기법을 적용하자
        * 빨리 개발하는게 능사는 아님


### 비디오에 Component View 및 Redux 적용기, 유영혁님

원본 영상: [https://youtu.be/deDauQfNUQA](https://youtu.be/deDauQfNUQA)



* 버즈빌 비디오 서비스 소개
    * 일정 시간 이상 비디오를 보면 리워드를 주는 비디오 광고 서비스
    * 복잡한 기존 비디오 구조
        * 복잡하게 분산된 상태(리워드 상태, 전체 화면, 썸네일, 오디오 등)
        * 복잡한 비즈니스 로직
            * 다수의 상태 접근 필요
            * 컴포넌트 간 강한 결합
    * → 여러 문제점 발생
        * 뷰 의존성이 높아 뷰 수정이 어려움
        * 다양한 상태가 복합된 비즈니스 로직으로 디버깅이 어려움
        * 결합도가 높아 테스트가 어려움
* 리팩토링 전략
    * 효율적인 상태 관리
        * MVI → Redux
    * 수정에 유연한 뷰 구조
        * Composable UI → Component View
* Redux
    * 리액트 기반 프론트엔드에서 주로 사용되는 상태 관리 패턴
    * 3가지 원칙
        * 한 곳(Store)에서 모든 상태 관리
        * 상태는 불변 타입
        * 상태 변화는 순수 함수로 작성
    * 뷰에서 이벤트 전달 → 상태 저장소에서 뷰 업데이트
    * 예시: 비디오 플레이 버튼 클릭
        * View에서 클릭 이벤트 발생 → Action을 생성해서 전달
        * Middleware에서 이벤트 로직 수행 → Reducer로 액션 전달
            * Middleware는 비동기 콜 같은 비순수 함수 작성 가능
            * 필요시 이벤트를 새로 생성해서 Action으로 재전달
        * Reducer는 액션에 따라 순수 함수로 상태를 변경 → Store의 상태 변경
            * 상태 변경은 항상 새로운 객체 생성으로 이루어짐
        * Store의 상태가 변경되면 구독된 모든 컴포넌트에게 newState 콜백이 호출됨
            * 뷰에서는 상태에 리액티브하게 로직 작성
* Component View
    * 뷰를 컴포넌트 단위로 분해
    * ConstraintLayout 기반으로 작성
    * 상태 변경에 리액티브하게 작성
    * 예시: 사운드 버튼 컴포넌트
        * 뷰 코드를 컴포넌트 안으로 숨김
        * newState 콜백을 받아 리액티브하게 뷰 상태 변경
        * 외부에서 컴포넌트를 사용할 때는 컴포넌트를 생성하고 배치(ConstraintLayout 기반)만 하면 됨
* 적용 후기
    * 디버깅 편리
        * 상태 변화는 Reducer에서만 발생 → Reducer만 봐도 상태 변화 추적 가능
    * 자유로운 UI 배치
        * ConstraintLayout에 배치만 잘 해주면 됨
        * 상태에 맞게 ConstraintSet 수정
    * 비즈니스 로직 분리
        * Middleware 또는 Reducer로 모든 Action이 거쳐가고 별도의 결합이 없어 비즈니스 로직 분리가 쉬움
    * 유닛 테스트 구현 편리
        * 비즈니스 로직이 Middleware, Reducer 단위로 분리됨
        * 뷰는 Component View 단위로 분리됨
        * 이벤트(액션) 기반이라 모킹이 쉬움


### Android Native 모듈을 안정적으로 개발하기, 박한범님

원본 영상: [https://youtu.be/3Wt_2ImRhNo](https://youtu.be/3Wt_2ImRhNo)



* 안드로이드 빌드 환경에 대한 설명
* 로그
    * 레벨을 나눠서 적절한 로그만 출력하기
    * 사용자: 프로그램의 실행에 영향을 미치는 핵심 이벤트
        * ex) 네트워크 미연결
    * APP: app layer에서 호출되는 함수들의 목적/기대값
        * ex) 네트워크로 데이터 송신 성공시 패킷 반환
    * SE/QA: 실제 기능을 수행하는 함수들의 목적/기대값
        * ex) 대상 서버 DNS 조회, IP 리턴
    * DEVEL: 주요한 데이터 연산, API 호출 결과 등
        * ex) 실제 메서드 호출 인자와 결과 값
    * Report: 프로그램 실행에 치명적인 오류 값
* 테스트
    * 유닛 테스트
        * Unit != function
        * 일반적인 유닛 구성: 데이터 생성 및 연산
        * 데이터는 유저 인풋과 시스템에 의존성이 큼
        * → 데이터와 로직을 분리하면 테스트가 쉬워짐
        * → 데이터를 생성하는 코드와 데이터를 연산하는 코드 분리
    * 피쳐 테스트
        * 다수의 유닛을 모은 기능 테스트
    * 플래그 세팅으로 테스트 자동화
* 네이티브 코드 안정성 향상 팁
    * 가능한 기능을 모듈로 나눠서 개발
        * 모듈의 특색에 맞는 개발 및 테스트 구성 가능
    * 크래시 제어
        * 크래시 발생 시 제어할 범위 지정(ex. 새로 추가된 함수)
        * Signal Handler 세팅
        * 복귀 지점 설정(크래시 발생 시 복원)
            * sigsetjmp, siglongjmp


### Android Testing Best Practices: 실제 프로젝트에 도움이 되는 테스트 코드 구현, 강사룡님

원본 영상: [https://youtu.be/D_tWlb2deX8](https://youtu.be/D_tWlb2deX8)



* 테스트 코드를 작성하면 좋은 점
    * 코드 수정 및 리팩토링에 부담이 줄어들어 (심리적인) 생산성 증대
    * 효율적으로 버그를 잡을 수 있음
    * 모듈러한 설계에 도움: single responsibility
        * 테스트가 설계를 강제하거나 보장하는건 아니지만, 테스트가 어려운 코드는 단일 책임 등에 문제가 있는 코드일 가능성이 높음
* 테스트 코드를 작성할 수 밖에 없는 이유
    * QA 처럼 사람이 테스트 할 수 있는 범위에는 한계가 있음
    * 협업을 위해 반드시 필요
        * 내가 없을 때 내 코드를 다른 사람이 테스트
            * 미래의 나도 포함..
        * 코드 오너가 아니더라도 코드를 수정할 수 있음
            * 문서로서의 테스트 코드
            * 테스트 코드와 테스트 케이스만 봐도 특정 시스템의 기능과 의도, 올바른 사용법을 파악할 수 있음
* 실기기 테스트
    * 안정성, 호환성, 성능 테스트가 목적
    * 유닛 테스트는 가능한 JVM에서 할 것
        * JVM에서 어려운건 시뮬레이터에서 할 것
    * 실기기 테스트 전 고려할 것
        * 격리된 테스트 환경 구축(Hermetic testing)
            * 로컬에서 먼저 검증 후 외부 서버를 포함한 테스트
        * 클라-서버 프로토콜 테스트
* 테스트 코드를 처음부터 작성한다면
    * 작고 독립적인 부분부터 시작
        * ex) 계산, 변환 로직을 가진 클래스
        * 참고: 테스트 주도 개발
    * 디버깅 과정에서 테스트 코드 적용
        * ex) 문제 상황을 재현하는 테스트 코드 작성(당연히 이 테스트는 fail 함) → 해당 테스트를 통과하도록 코드 수정
    * 의존성 해결 방법(SQLite, Reset/gRPC call 등)
        * 1순위: 의존성 관계에 있는 진짜 코드 사용
            * ex) in-memory DB
        * 2순위: 라이브러리에 의해 제공되는 표준 fake 사용
        * 3순위: 위 방법이 불가능할 때 mock 사용
            * Mock으로는 드러나지 않는 문제가 있을 수 있음
* Mocking Best Practice
    * Type-safe한 matcher 활용(hamcrest, truth 등 + built-in)
    * interaction 보다 state를 체크할 것 (appendix 참조)
    * Android API를 mocking 하지 말 것
        * Robolectric 사용
        * 최근에 안드로이드에서 프래그먼트 독립 생성, 라이프 사이클 제어 등 많은 개선이 있었음 ← 이런거 먼저 적용
* 테스트 코드 유지보수
    * 깨지기 쉬운 테스트(brittle test) → Unchanging Test
    * 테스트는 다음 상황에서도 변경되지 말아야 함
        * 순수한 리팩토링
        * 새로운 기능
        * 버그 픽스
    * 기존의 행위가 바뀐 경우에만 테스트 변경이 필요
* 베스트 프랙티스
    * 퍼블릭 API를 통한 테스트
        * 테스트를 편하게 하려고 private 함수에 접근하면 의도에 맞지 않은 테스트 코드가 생길 수 있음
    * 완결성과 간결성(complete and concise)
        * 완결성: 테스트하고자 하는 것을 정확히 알 수 있는 모든 정보를 갖고 있어야 함
        * 간결성: 불필요한 내용은 감춰야 함
    * 메서드가 아닌 행동(의도)을 테스트하라
        * 나쁜 예: 메서드가 특정 결과를 반환하는지만 체크
        * 좋은 예: 메서드가 어떤 조건(의도)에서 어떤 결과를 반환하는지 체크
    * 테스트에 로직을 포함하지 말 것
        * 테스트 코드 자체에 버그가 생길 가능성을 배제
        * 테스트에서는 하드코딩을 하는게 더 좋을수도
            * ex) baseUrl을 계산해서 넣는 대신 실제 url을 하드코딩으로 넣기
    * DAMP, Not DRY
        * DAMP: Descriptive And Meaningful Phrases
        * DRY: Don’t Repeat Yourself
        * 일반적인 코드는 중복을 피하는게 좋지만 테스트 코드는 반복되더라도 하나의 테스트가 완결성을 가지고, 하나의 테스트 안에 모든 내용이 명확하게 들어가 있는 것이 더 중요함
        * → 중복 코드가 생겨도 명확하게!


### Asynchronous Programming for Android, 권혁신님

원본 영상: [https://youtu.be/Pr-k84Vv1gg](https://youtu.be/Pr-k84Vv1gg)



* 안드로이드에서 비동기 프로그래밍이 필요한 이유
    * Refresh frequency: min 60Hz(약 17ms)
    * 메인 스레드에서 해야하는 일: 뷰 작업(xml 파싱하고 inflate 하기, 뷰 그리기, 유저 인터랙션 받기 등) + 그 외 메인 스레드에서 돌리도록 작성한 코드들
    * 위 작업들을 16ms 안에 못하면 랙 걸리고 심하면 ANR
    * → 메인 스레드에서는 화면 관련된 일만 하고, 나머지는 워커 스레드에서 작업
* RxJava
    * 오퍼레이터를 익히는데 러닝커브가 높음
    * 에러 핸들링
* Coroutine
    * 라이프 사이클 스코프 안에서 실행
    * RxJava 같은 오퍼레이터가 없음
    * 순차적 코드 구조
    * 에러 핸들링은 RxJava 보다 부족(try-catch로 예외처리)
    * Light-weight thread라고 하지만 진짜 스레드는 아님
        * 각 작업마다 스레드가 아닌 오브젝트를 할당하고, 오브젝트 스위칭을 함으로써 컨텍스트 스위칭에서 발생하는 비용을 줄임
            * 여러개의 스레드에서 여러개의 코루틴을 돌리면 컨텍스트 스위칭이 발생할 수 있음
        * 따라서 코루틴의 장점을 살리기 위해선 하나의 스레드에서 여러 개의 코루틴을 만드는게 스레드마다 잡아먹는 메모리도 줄이고 컨텍스트 스위칭도 줄일 수 있음
* Coroutine with Flow
    * RxJava 처럼 오퍼레이터에 대한 학습 필요
        * 아직 RxJava 보다는 오퍼레이터 종류가 적음
    * RxJava 처럼 스트림 처리 가능
    * 코루틴의 라이프 사이클 스코프 처리와 순차적 코드 구조의 장점도 챙길 수 있음