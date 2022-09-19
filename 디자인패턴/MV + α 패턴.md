# MV (Model-View)

- **Model** : **데이터** (데이터베이스, 상수, 변수 등)
- **View** : **사용자 인터페이스 → 데이터를 보여주는 화면**
- 그러므로, **데이터와 사용자 인터페이스는 서로 의존성이 생길 수 밖에 없음.**
- **앱 아키텍처 패턴들은 결국 Model과 View의 관계를 어떻게 처리하느냐? 문제**

***

# MVC (MV + Controller)

## 개념

1. **Controller : 모든 입력을 받은 후,** 로직에 따라 **Model 업데이트, View 선택**
2. Controller는 View를 선택할 뿐, **업데이트하지 않음. → View는 Controller를 알지 못함**
3. View 업데이트 방법
    - View가 Model을 직접 이용
    - Model에서 View에 notify
    - View가 Polling하여 Model의 변화 감지
        
        > **polling :** 데이터 통신 방식 중 하나. 하나의 장치(또는 프로그램)가 충돌 회피 또는 동기화 처리 등을 목적으로 다른 장치(또는 프로그램)의 상태를 주기적으로 검사하여 일정한 조건을 만족할 때 송수신 등의 자료처리를 하는 방식.
        > 

## 주의점 · 단점

- Model - View 의존성 커짐

## 활용

### 1. **Laravel : The PHP Frameworkfor Web Artisans.**
- 우리가 웹사이트에 접속했을 때 Laravel에서 생기는 일
1. **Website → Request** 
2. **routes.php : 요청이 들어온 URI를 인덱스처럼 사용하여 관련된 Controller 찾기**
3. **Controller : Model에서 요청을 처리하는 데 필요한 데이터를 가져오거나 저장하는 등의 일을 처리** 
4. **View : Controller로부터 데이터를 받아서 html 생성**

### 2. **Django : The Python web framework that encourages rapid development and clean, pragmatic design.**

- Django는 MTV (Model - Template - View) 패턴을 사용하지만, 각각 MVC와 1:1로 완벽히 대응됨.
- Django Docs에는 이 차이를 이렇게 설명함 → Well, the standard names are debatable.
    
    [https://docs.djangoproject.com/en/4.1/faq/general/#django-appears-to-be-a-mvc-framework-but-you-call-the-controller-the-view-and-the-view-the-template-how-come-you-don-t-use-the-standard-names](https://docs.djangoproject.com/en/4.1/faq/general/#django-appears-to-be-a-mvc-framework-but-you-call-the-controller-the-view-and-the-view-the-template-how-come-you-don-t-use-the-standard-names)
    
- 우리가 웹사이트에 접속했을 때 Django에서 생기는 일
1. **Website → Request**  
2. **urls.py : 요청이 들어온 URI를 인덱스처럼 사용하여 관련된 View(= Controller) 찾기**
3. **View (= Controller) : Model에서 요청을 처리하는 데 필요한 데이터를 가져오거나 저장하는 등의 일을 처리**
4. **Template(= View) : View(= Controller)로부터 데이터를 받아서 html 생성**

## 참고

### **React isn’t an MVC framework.**

- [https://reactjs.org/blog/2013/06/05/why-react.html](https://reactjs.org/blog/2013/06/05/why-react.html)
- **React is a library for building composable user interfaces. It encourages the creation of reusable UI components which present data that changes over time. *→** React is neither MVC or notMVC. It's a library to render the View (with a lots of cool stuff, but still). You can use either MVC patterns, or Flux/Redux, or whatever.*

***

# MVP (MV + Presenter)

## 개념

1. **View : 모든 입력은 View로 전달**
2. **Presenter :** 로직에 따라 **Model 업데이트**
3. **Presenter :**  Model 업데이트 결과를 기반으로 **View 업데이트**
4. Presenter는 View와 Model 인스턴스를 가지고, Model과 View 사이의 매개체 역할을 함

## 특징 · 장점

- Presenter가 Model - View 사이에서 관리 → Model - View 의존성 없음

## 주의점 · 단점

- View와 Presenter는 1:1 관계 → View - Presenter의 의존성 커짐
- 필요한 클래스 개수가 많음

***

# MVVM (MV + ViewModel)

## 개념

> **View Model :** View를 추상화한 계층. View를 위한 Model. View를 나타내기 위한 데이터 처리 담당.
> 
1. **View : 모든 입력은 View로 전달**
2. **View :** **Command 패턴**으로 **View Model**에 입력 전달
3. **View Model :** **Model**에게 데이터 요청 후, 응답 받은 데이터를 가공하여 **저장**
4. **View** : **View Model을 선택**해 **Data Binding**하여 자동 갱신됨
    
   <img width="440" alt="image" src="https://user-images.githubusercontent.com/66233687/191009377-dd00f79b-738b-467a-9211-4cc63949cd08.png">    

## 특징 · 장점

- ViewModel과 View는 1:n 관계 → ViewModel은 View를 참조하지 않음
- Command 패턴과 Data Binding을 이용 → View와 View Model 사이의 의존성을 없앰

> Command 패턴 : 객체의 메서드를 클래스로 만들어 캡슐화 하는 패턴. 어떤 객체(A)에서 다른 객체(B)의 메서드를 실행하려면 그 객체(B)를 참조하고 있어야 하는 의존성이 발생하나, 커맨드 패턴을 적용하면 의존성을 제거할 수 있음
> 

> Data Binding : **화면에 보이는 데이터**와 **웹 브라우저의 메모리 데이터를 일치**시키는 기법. 데이터의 일관성 유지에 탁월
> 

## 활용

### Vue.js : **The ProgressiveJavaScript Framework**

- 양방향 데이터 바인딩
- Model : 데이터. JavaScript 객체 등.
- View : DOM. $el로 설정. Vue 인스턴스 생성당시에 컴파일되어 ViewModel의 메서드등이 바인딩
- ViewModel : Vue 인스턴스가 ViewModel. View에 필요한 기능, 필드을 가지고 Model과 View를 연결

<img width="704" alt="image" src="https://user-images.githubusercontent.com/66233687/191009594-1a1aab96-f23b-41b4-bfd0-e1f492a5a127.png">
