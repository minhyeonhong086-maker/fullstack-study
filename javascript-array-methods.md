JavaScript 배열 관리

주요 메서드

push(): 배열 마지막에 데이터 추가

splice(): 배열 요소 추가 및 삭제

map(): 각 요소를 변환한 새 배열 생성

filter(): 조건에 맞는 요소로 새 배열 생성

length: 배열의 길이를 확인하는 속성

코드 예제

const students = ["Hong", "Kim"];

students.push("Lee");
students.splice(0, 1);

console.log(students);

정리

배열을 활용하면 학생 목록, 할 일 목록 등 여러 데이터를 효율적으로 관리할 수 있다.
