# Spring Boot 프로젝트 구조와 MVC 흐름

## 1. Spring Boot란?
- Spring 프레임워크를 **설정 최소화** 로 바로 실행할 수 있게 만든 도구
- 내장 톰캣 서버 포함 → `main` 메서드 실행만으로 웹 서버 시작

## 2. 기본 폴더 구조
```
src/main/java/com/example/demo
├─ DemoApplication.java      # 시작점 (@SpringBootApplication)
├─ controller/               # 요청 받기
├─ service/                  # 비즈니스 로직
├─ repository/               # DB 접근
└─ domain(entity)/           # 데이터 모델
src/main/resources
├─ application.properties    # 설정 (포트, DB 연결 등)
├─ templates/                # Thymeleaf 화면
└─ static/                   # CSS, JS, 이미지
```

## 3. 계층별 역할
| 계층 | 어노테이션 | 역할 |
|---|---|---|
| Controller | @Controller / @RestController | 요청을 받고 응답 반환 |
| Service | @Service | 핵심 로직, 트랜잭션 |
| Repository | @Repository | DB 조회·저장 |

## 4. 요청 흐름
```
브라우저 → DispatcherServlet → Controller → Service → Repository → DB
                                   ↓
                      View(Thymeleaf) 또는 JSON 응답
```

## 5. 예시 코드
```java
@RestController
@RequestMapping("/api/students")
public class StudentController {

    private final StudentService studentService;

    public StudentController(StudentService studentService) { // 생성자 주입
        this.studentService = studentService;
    }

    @GetMapping
    public List<Student> list() {
        return studentService.findAll();
    }
}
```

## 6. @Controller vs @RestController
- @Controller: 화면(View 이름)을 반환
- @RestController: 객체를 **JSON** 으로 반환 (= @Controller + @ResponseBody)

## 7. 의존성 주입(DI)
- 객체를 직접 `new` 하지 않고 Spring이 만들어 넣어줌 → 결합도 감소, 테스트 쉬움
- 생성자 주입 방식이 권장된다.

## 정리
- Controller는 얇게, 로직은 Service에 모은다.
