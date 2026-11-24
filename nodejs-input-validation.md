Node.js 입력값 검증

주요 개념

trim(): 문자열 앞뒤 공백 제거

Number(): 숫자로 변환

Number.isInteger(): 정수 여부 확인

if: 조건에 따른 실행 처리

return: 함수 실행 종료

코드 예제

const input = "3";
const number = Number(input);

if (!Number.isInteger(number) || number < 1) {
    console.log("잘못된 입력입니다.");
} else {
    console.log("정상적인 입력입니다.");
}

정리

사용자 입력값을 검증하면 잘못된 데이터 처리와 프로그램 오류를 예방할 수 있다. 학생 관리 프로그램의 등록 및 삭제 기능에도 활용할 수 있다.
