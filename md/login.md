# 로그인 바 구현

[네이버 로그인 구현 화면](https://betteree.github.io/homework/login/login.html)

## 1. 로고 중앙 정렬 문제

하지만 로고가 중앙에 위치하지 않는 문제를 해결해야 했습니다. 이 문제의 원인은 `logo-box`의 `width`와 `display` 속성의 설정에 있었습니다.

로고의 `width`를 `100%`로 설정했지만, 부모 요소인 `login-bar`의 너비가 명시적으로 설정되지 않아서 로고가 예상과 다르게 표시되었습니다. 이러한 문제는 사용자 경험을 저하시킬 수 있으므로 신속히 해결해야 했습니다.

### 해결 방법

부모 요소에 `text-align: center;` 속성을 추가하여 모든 자식 요소가 중앙 정렬되도록 수정했습니다. 이를 통해 로고가 항상 화면의 중앙에 위치하도록 보장할 수 있었습니다.

```css
.login-bar {
  width: 100%;
  text-align: center;
}

.logo-box {
  display: inline-block;
}

.logo-box img {
  width: 100%;
  max-width: 200px;
}
```

<br>

## 2. 포커스 시 스타일 문제

아이디나 비밀번호를 눌렀을 때 색깔이 바뀌는 것을 고민했습니다.

### 해결 방법

&:focus 선택자를 발견하여 이를 적절한 위치에 추가하여 포커스 상태에서의 스타일을 적용했습니다.

```css
&:focus {
  border-color: #03cf5d;
  background-color: #e9f0fd;
  outline: none;
}
```

<br>

## 3. 로그인 상태 유지 체크박스 기능

버튼누르는 것을 인식하고 눌리는 순간 다른 형태로 변화하는 것은 js 에서만 다루어보아서 어떻게 할지 막막하고 고민이 되었습니다

### 해결 방법

focus를 이용하여 포커스가 맞추어 지는 순간 check 표시로 변환되도록 했습니다.

```css
.checked {
  width: 24px;
  height: 24px;
  background-image: url("./../../assets/login/unchecked.svg");
  background-size: contain;
  background-repeat: no-repeat;
  cursor: pointer;
  &:focus {
    background-image: url("./../../assets/login/checked.svg");
  }
}
```

<br>

## 4. 마진 문제

데스크탑 환경에서는 박스가 500px로 고정되었어야 했는데, 입력박스는 말 그대로 width 를 지정하면 되지만 로그인상태 유지나 ip보안은 width를 지정하니 아예 면적이 줄어 중앙 양쪽으로 정렬되지 않는 사태가 일어났습니다.

### 해결방법

입력 폼과 로그인 버튼, 그 외 것들을 한꺼번에 묶어 width를 줄이고 센터로 정렬했습니다.
그 후 기능들은 width:100%으로 맞춤으로써 데스크 탑에서도 정렬이 무너지지 않도록 했습니다.

```css
@media (min-width: 768px) {
  .block-form {
    width: 100%; /* 블록 폼의 전체 너비를 100%로 설정 */
    max-width: 500px;
    margin: 0 auto;
    .login {
      display: flex;
      justify-content: center;
      flex-flow: row wrap;

      .login-pw,
      .submit {
        width: 100%;
      }
    }

    .check-box {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      justify-content: space-between;
      width: 100%;
    }
    .ip-check {
      display: block;
      margin-left: auto;
      color: #121212;
      font-size: 16px;
    }
  }
}
```

<br>

## 5. 키보드 접근성

키보드를 통해서도 아이디 서식이나 체크박스에 접근이 가능하도록 하는 것이었는데
문제를 해결하지 못했습니다.
