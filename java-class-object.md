# Java 클래스와 객체 기초

## 1. 클래스와 객체
- **클래스**: 객체를 만들기 위한 설계도
- **객체(인스턴스)**: 설계도로 만든 실체

```java
public class Student {
    // 필드(상태)
    private String name;
    private int score;

    // 생성자
    public Student(String name, int score) {
        this.name = name;
        this.score = score;
    }

    // 메서드(행동)
    public boolean isPassed() {
        return score >= 60;
    }

    // Getter
    public String getName() {
        return name;
    }
}
```
```java
Student s = new Student("홍길동", 85);
System.out.println(s.getName() + " 합격: " + s.isPassed());
```

## 2. 접근 제어자
| 제어자 | 접근 범위 |
|---|---|
| public | 어디서나 |
| protected | 같은 패키지 + 자식 클래스 |
| (default) | 같은 패키지 |
| private | 같은 클래스 안에서만 |

## 3. 캡슐화
- 필드는 `private`, 접근은 메서드로 → 잘못된 값이 들어오는 것을 막음
```java
public void setScore(int score) {
    if (score < 0 || score > 100) throw new IllegalArgumentException("0~100만 가능");
    this.score = score;
}
```

## 4. static
- 객체가 아니라 **클래스에 속한** 필드·메서드
```java
Math.max(3, 5); // 객체 생성 없이 호출
```

## 5. JavaScript와 비교
| 항목 | Java | JavaScript |
|---|---|---|
| 타입 | 정적 타입 (선언 필요) | 동적 타입 |
| 실행 | 컴파일 후 JVM에서 실행 | 인터프리터/JIT |
| 클래스 | 필수 구조 | 선택 (ES6 class) |

## 정리
- 클래스 = 상태(필드) + 행동(메서드)
- 캡슐화로 데이터를 안전하게 지킨다.
