# Day 2 :: User Interface Testing

소프트웨어 애플리케이션을 개발할 때 자동화된 사용자 인터페이스 테스트는 유용한 도구이다. 사용자 인터페이스 테스트는 빠르게 애플리케이션의 문제를 감지할 수 있으며, 테스트 집합의 성공적인 실행은 앱을 릴리즈하기 전에 개발자에게 신뢰를 제공할 수 있다. iOS 플랫폼에서, 자동화된 사용자 인터페이스 테스트는 자바 스크립트로 작성된 UIAutomation을 사용하여 수행된다. 이것은 Instruments 라는 별도의 애플리케이션을 실행하고, 스크립트를 생성하고 실행하는 것을 포함한다. 이런 작업 방법은 아주 고통스러울 만큼 느리고, 익숙해지기에는 많은 시간이 걸린다.

## UI 테스팅

애플은 Xcode 7에서 앱의 사용자 인터페이스 테스트를 수행할 수 있는 새로운 방법을 소개했다. UI 테스트는 당신이 UI 요소를 찾고 그것들과 상호작용할 수 있으며, 사용 가능한 속성과 상태를 검증할 수 있다. UI 테스트는 완벽하게 Xcode 7 테스트 리포트와 통합되었으며, 단위 테스트와 함께 실행된다. XCTest는 Xcode 5 이후 Xcode의 테스트 프레임워크로 통합되었지만, Xcode 7에서는 새로운 UI 테스트 기능이 포함되어 업데이트되었다. 이것은 당신이 특정 지점에서 당신의 UI 상태를 확인할 수 있도록 주장(assertions)을 만들 수 있다.

### 손쉬운 사용(Accessibility)

UI 테스트가 가능하기 위해서는, 프로임워크에서 UI의 요소별 작업을 수행할 수 있도록 UI 내부에 있는 다양한 요소들에 접근이 가능해야 한다. 당신이 탭(tap)이나 스와이프(swipe) 테스트를 위한 특정 위치를 지정할 수도 있지만, 그것은 다른 크기의 디바이스나 당신의 UI의 요소들의 위치를 아주 조금만 변경해도 테스트 진행률이 떨어질 것이다.

이것은 접근성에 도움이 될 수 있다. 접근성은 장애인 사용자들이 당신의 애플리케이션과 상호작용을 하는 방법을 제공하는 아주 오랫동안 확립된 애플 프레임워크이다. 그것은 당신의 애플리케이션이 장애인 사용자들에게 제공할 수 있는 다양한 접근 가능한 UI 기능에 대한 풍부한 의미의 데이터를 제공한다. 이렇게 상자 밖으로 나온 많은 기능은 당신의 애플리케이션과 함께 작동 할 것이겠지만, 당신은 접근성 API를 사용해서 당신의 UI에 대한 접근성 데이터를 향상 시킬수 있다.(그리고, 향샹 시켜야한다.) 이런 필요성에 대한 많은 경우가 있는데 예를 들자면, 사용자 정의 컨트롤의 경우 접근성으로는 당신의 API가 무엇을 하는지 자동으로 알아낼 수는 없다.

UI 테스트는 다른 크기의 장치 문제에 대한 뛰어난 해결책을 제공하는 접근성을 이용하여 당신의 애플리케이션이 제공하는 기능들과 상호작용을 할 수 있으며, 만약 당신이 당신의 UI의 몇몇 요소들을 재배치 하더라도 당신의 테스트 집합을 다시 쓸 수 있는 기능을 제공한다. 접근성을 구현하는 것은 단순히 UI 테스트 만을 돕는것이 아니라 장애인 사용자들이 당신의 애플리케이션을 사용할 수 있도록 만드는 추가적인 혜택을 제공한다.

### UI 녹화

당신이 몇가지 UI 테스트를 생성하길 원한다면, 접근 가능한 UI를 한 번만 설정하면 된다. 만약 당신이 복잡한 UI를 가지고 있다면 UI 테스트를 작성하는 것은 시간이 많이 걸리고, 지루하며, 어려울 수 있다. 감사하게도 Xcode 7에서 애플은 UI 녹화(UI Recording)를 소개했으며, 이것은 UI 테스트를 새로 만들고 기존에 있는 테스트를 확장할 수 있도록 하였다. 이 기능을 켜면 디바이스 혹은 시뮬레이터에 있는 당신의 앱과 상호작용을 할 때 코드가 자동 생성된다. 우리는 UI 테스트가 어떻게 함께 작동하는지에 대해 알게 되었으니, 이제는 UI 테스트를 사용할 시간이다.

## UI 테스트 만들기

우리는 새로운 UI 테스트 툴이 어떻게 동작하는지 설명하기 위해서 이것을 사용하여 UI 테스트 집합을 구축해 보겠다. 만약 당신이 따라 해 보기를 원하거나 결과를 보고 싶다면 [GitHub](https://developer.apple.com/accessibility/)의 완성된 데모 애플리케이션을 이용할 수 있다.

### 셋업

당신이 새로운 프로젝트를 Xcode7에서 생성한다면 당신은 UI 테스트를 포함 시킬지를 선택할 수 있다. 이것은 UI 테스트를 위해 당신이 필요로 하는 모든 구성을 설정해 준다.

![Creating a new project with UI Tests](images/Day2-1.png)

이번 예제 프로젝트 셋업은 정말로 간단하지만, Xcode7 에서 UI 테스트가 어떻게 동작하는지를 설명하는 데는 충분하다.

![The structure of the demo app](images/Day2-2.png)

스위치와 상세 뷰 컨트롤러를 연결하는 버튼을 포함하는 메뉴 뷰 컨트롤러가 있다. 스위치가 "off" 상태였을때, 버튼은 비활성화되어야 하며 네비게이션 기능은 불가능해야 한다. 상세 뷰 컨트롤러는 레이블의 값을 증가하는 간단한 버튼을 포함하고 있다.

### UI 레코딩 사용하기

UI를 설정하고 동작하게 되면, 우리는 코드의 어떤 변경도 기능적으로 영향을 주지 않는 몇 가지 UI 테스트를 작성할 수 있다.

#### XCTEST UI 테스팅 API

우리가 녹화를 시작하기 전에 우리는 우리가 주장하고 싶은 것을 결정해야 한다. 우리가 우리의 UI에 대해 확실한 무언가를 주장하기 위해서는 3가지 새로운 부분을 포함하도록 확장된 XCTest 프레임워크를 사용할 수 있다.

**XCUIApplication.** 이것은 당신이 테스트 중인 애플리케이션을 위한 대리(Proxy)이다. 이것은 당신이 애플리케이션을 실행하여 그것에 테스트할 수 있도록 허용해 준다. 그것이 항상 새로운 프로세스를 시작하는 것에 주목할 가치가 있다. 이것은 시간이 조금 더 필요하지만, 그것은 당신의 애플리케이션이 테스트를 하기 위해 실행 될때 깨끗하다는 것을 의미하며, 당신이 고려해야 할 변수가 적다는 것을 의미하기도 한다.

** XCUIElement.** 이것은 당신이 테스트 중인 애플리케이션의 UI 요소를 위한 대리(Proxy)이다. 요소들은 유형들(types)과 식별자들(identifiers)을 가지고 있으며, 당신이 애플리케이션에서 요소들을 찾을 수 있도록 결합 할수도 있다. 이 요소들은 당신의 애플리케이션을 표현하는 구조(tree) 모두 자리잡고 있다.

** XCUIElementQuery.** 당신이 요소들을 찾기를 원할 때 당신은 요소 쿼리를 사용 한다. 모든 XCUIElement 은 쿼리에 의해서 뒷받침 된다. 이러한 쿼리는 XCUIElement 구조를 검사하고 반드시 일치하는 하나를 결정해야 한다. 그렇지 않으면 당신의 테스트는 요소에 접근을 하려고 할 때 실패할 것이다. 이 예외는 이것이 속성에 존재하는지 당신이 체크 하려고 할 때 확인할 수 있다. 이것은 주장(assertions)에 유용한다. 당신은 명백하게 접근할 수 있는 요소들을 찾기를 원할 때  XCUIElementQuery를 보다 일반적으로 사용할 수 있다. 쿼리는 결과의 집합을 반환한다.

이제 우리는 API를 탐험할 수 있는 방법을 알게 되었고 몇 가지 테스트 작성을 시작할 수 있다.

#### 테스트 1 - 스위치가 꺼져 있을 때 상세 화면으로 이동하지 못함을 보장한다.

먼저 우리는 테스트를 포함하는 함수를 정의해야 한다.

```swift
func testTapViewDetailWhenSwitchIsOffDoesNothing() {

}
```

함수를 정의 했다면, 우리는 마우스 커서를 괄호 안으로 이동하고 Xcode 창의 맨 아래에 있는 녹화버튼을 누릅니다.

![Preparing to record the actions for the first test](images/Day2-3.png)

이제 애플리케이션이 실행 될 것이다. 메인 뷰 컨트롤러의 스위치를 "off"로 바꾸고 "View Detail" 버튼을 누릅니다. 아래 코드가 `testTapViewDetailWhenSwitchIsOffDoesNothing`의 내부에 보여야 한다.

```swift
  let app = XCUIApplication()
  app.switches["View Detail Enabled Switch"].tap()
  app.buttons["View Detail"].tap()
```

이제 녹화 버튼을 다시 클릭해서 녹화를 중지해야 한다. 우리는 실제로 애플리케이션이 상세 뷰 컨트롤러를 표시하지 않은 것을 볼 수 있지만, 테스트는 현재 상태를 알 수 있는 방법이 없다. 우리는 아무것도 변경되지 않은 것을 주장(assert)해야 한다. 우리는 네비게이션 바의 타이틀을 검사 함으로써 이것을 알 수 있다. 이것이 모든 사례에 적합하지는 않겠지만, 지금은 잘 동작 한다.

```swift
XCTAssertEqual(app.navigationBars.element.identifier, "Menu")
```

일단 이 라인을 추가하고 다시 테스트를 실행해도 여전히 테스트를 통과해야 한다. 예를 들어 "Menu" 문자열을 "Detail" 로 변경하고 시도하면 테스트는 실패할 것이다. 여기에 동작에 대한 설명을 추가한 몇 가지 코멘트와 최종 테스트의 결과 있다.

```swift
func testTapViewDetailWhenSwitchIsOffDoesNothing() {
  let app = XCUIApplication()

  // Change the switch to off.
  app.switches["View Detail Enabled Switch"].tap()

  // Tap the view detail button.
  app.buttons["View Detail"].tap()

  // Verify that nothing has happened and we are still at the menu screen.
  XCTAssertEqual(app.navigationBars.element.identifier, "Menu")
}
```

#### 테스트 2 - 스위치가 켜져 있을 때 상세 화면으로 이동을 보장한다.

두 번째 테스트는 첫 번째 테스트와 비슷하기 때문에 상세히 이야기하지는 않습니다. 여기에서 유일한 차이점은 스위치가 활성화되어 있는 것이며, 그래서 애플리케이션은 상세 화면을 로드 할 수 있어야 하며, 그리고 XCTAssertEqual는 이를 확인할 수 있어야 한다.

```swift
func testTapViewDetailWhenSwitchIsOnNavigatesToDetailViewController() {
  let app = XCUIApplication()

  // Tap the view detail button.
  app.buttons["View Detail"].tap()

  // Verify that navigation occurred and we are at the detail screen.
  XCTAssertEqual(app.navigationBars.element.identifier, "Detail")
}
```

#### 테스트 3 - 증가 버튼은 레이블의 값을 증가시키는 것을 보장한다.

이번 테스트는 사용자가 증가 버튼을 클릭했을 때 레이블의 값이 1씩 증가 하는지 확인하는 것이다. 이번 테스트의 처음 두 줄은 이전 테스트와 아주 비슷하기 때문에 이전 테스트에서 복사해서 붙여넣을 수 있다.

```swift
  let app = XCUIApplication()

  // Tap the view detail button to open the detail page.
  app.buttons["View Detail"].tap()
```

다음으로 우리는 버튼에 접근해야 할 필요가 있다. 우리가 변수로서 이것을 저장할 수 있도록 몇 번 이 버튼을 누릅니다. 수동으로 이 버튼을 찾기 위해서 코드를 수동으로 입력하고 디버깅하는 것 보다, 녹화를 시작하고 버튼을 클릭한다. 이렇게 하면 다음과 같은 코드가 제공됩니다.

```swift
app.buttons["Increment Value"].tap()
```

우리는 녹화를 중단하고 이렇게 변경한다.

```swift
let incrementButton = app.buttons["Increment Value"]
```

이 방법은 우리가 버튼을 찾기 위해서 수동으로 코드를 입력할 필요가 없습니다. 우리는 이것과 같은 방법으로 값 레이블을 찾을 수 있다.

```swift
let valueLabel = app.staticTexts["Number Value Label"]
```

이제 우리는 애플리케이션의 UI와 상호 작용을 할 수 있는 흥미로운 UI 요소를 가지고 있다. 이 테스트에서 우리는 10번 버튼을 누른 후에 그에 따라서 업데이트된 레이블을 확인한다. 우리가 녹화기를 통해서 이것을 10번 녹화할 수 있지만, 우리는 이 요소를 저장하기 때문에, 간단하게 반복문(for loop)에 넣을 수 있다.

```swift
for index in 0...10 {
  // Tap the increment value button.
  incrementButton.tap()

  // Ensure that the value has increased by 1.
  XCTAssertEqual(valueLabel.value as! String, "\(index+1)")
}
```

이 세 가지 테스트는 포괄 적인 테스트 집합(test suite)과는 거리가 멀지만, 좋은 시작점을 제공할 것이며, 당신은 쉽게 확장할 수 있을 것이다. 버튼을 활성화 하거나, 스위치를 "off" 하고 네비게이트를 하거나, 다시 돌아가는 것들에 대한 테스트 케이스를 왜 추가하려고 하지 않으십니까?  

#### 레코딩이 잘 못 되었을 때

녹화하는 동안 당신이 요소를 누를 때, 때때로 올바르지 않은 것처럼 보이는 코드가 생성되는 것을 알게 될 수도 있다. 이것은 보통 당신이 접근성이 표시되지 않는 요소들과 상호 작용할 때 발생한다. 만약 이런 경우 Xcode의 Accessibility Inspector를 사용하여 찾을 수 있다.

![Opening the Accessibility Inspector](images/Day2-4.png)

만약 당신이 "CMD+F7"을 쳤고 그것을 실행했다면, 시뮬레이터에서 당신의 마우스로 요소 위를 이동하면 커서 아래에 있는 요소에 대한 포괄 적인 정보를 확인할 수 있다. 이것은 왜 접근성이 요소를 찾지 못했는지에 대한 실마리를 제공할 것이다.

일단 당신이 이슈를 확인했다면, 인터페이스 빌더를 열고 "identity inspector"에서 접근성 제어판(Accessibility panel)을 찾을 수 있다. 이것은 당신이 접근성을 활성화하거나, 힌트, 식별자 및 특성 레이블을 설정할 수 있다. 이것들은 당신의 인터페이스에 접근할 수 있는 접근성을 활성화할 수 있는 강력한 도구이다.

![Xcode Accessibility panel in the identity inspector.](images/Day2-5.png)

#### 테스트가 실패할 때

만약 테스트가 실패하고 당신이 그 이유를 확실하게 알지 못하는 경우 그것을 수정하는 몇 가지 방법이 있다. 우선 당신은 Xcode의 Report Navigator의 테스트 리포트를 확인할 수 있다.

![Test Report Failure](images/Day2-6.png)

당신이 이 화면을 띄우고 테스트의 특정 단계 위로 마우스를 이동시키면 테스트 작업의 오른쪽에 작은 눈 모양의 아이콘이 표시됩니다. 만약에 당신이 이 눈 모양을 클릭하면 당신은 정확한 그 시점의 앱의 상태의 스크린 샷이 표시됩니다. 이것은 당신이 시각적으로 당신 UI의 상태를 확인할 수 있도록 하며, 정확하게 무엇이 잘못되었는지 찾을 수 있다.

단위 테스트와 마찬가지로 당신은 UI 테스트에 문제점을 찾거나, 디버깅할 수 있는 브레이크 포인트를 추가할 수 있다. 당신은 뷰의 계층구조를 측정하거나 접근 속성의 검열을 사용하여 왜 당신의 테스트가 실패하는지 알 수 있다.

## 왜 UI 테스팅을 사용해야 하는가?

자동화된 UI 테스트는 당신이 당신의 애플리케이션을 변경할 수 있는 자신감을 주면서 품질 보증을 향상할 수 있는 가장 좋은 방법이다. 우리는 Xcode에서 UI 테스트를 준비하고 실행하는 것이 얼마나 간단 한지와, 접근성 기능을 추가하는 것이 단지 당신의 앱을 테스트하는 것만을 돕는 것이 아니라 장애가 있는 사용자가 당신의 앱을 사용하는 것을 돕는 추가적인 혜택도 가지고 있음을 경험했다.

Xcode의 UI 테스트의 가장 새로운 기능 중에 하나는 지속적인 통합 서버에서도 여러분의 테스트를 실행할 수 있다는 것이다. Xcode 봇이 이렇게 지원을 하며, UI 테스트가 실패하면 [커멘드 라인의 의미로부터](https://krausefx.com/blog/run-xcode-7-ui-tests-from-the-command-line) 당신은 즉시 정보를 얻을 수 있다.

## 더 읽을거리

Xcode의 새로운 UI 테스트 기능에 대한 보다 많은 정보는 WWDC session 406, [UI Testing in Xcode](https://developer.apple.com/videos/wwdc/2015/?id=406)을 보기를 권한다. 당신은 아마 [Testing in Xcode Documentation](https://developer.apple.com/library/prerelease/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/Introduction.html#//apple_ref/doc/uid/TP40014132)과 [Accessibility for Developers Documentation](https://developer.apple.com/accessibility/)에 대해서도 흥미를 느낄 것이다. 이글에서 설명한 프로젝트들을 실행해보고 싶다면 [GitHub](https://github.com/shinobicontrols/iOS9-day-by-day/tree/master/02-User-Interface-Testing)에 있으니 잊지 말기 바란다.
