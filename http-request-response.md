# HTTP 요청·응답과 상태 코드

## 1. HTTP란?
- HyperText Transfer Protocol: 클라이언트(브라우저)와 서버가 데이터를 주고받는 규칙
- **요청(Request)** → 서버 처리 → **응답(Response)** 구조
- 기본적으로 **무상태(Stateless)**: 서버는 이전 요청을 기억하지 않음 → 로그인 유지에는 쿠키·세션·토큰이 필요

## 2. 요청 구조
```http
POST /api/transactions HTTP/1.1
Host: example.com
Content-Type: application/json

{ "type": "expense", "amount": 12000 }
```
| 구성 | 설명 |
|---|---|
| 시작줄 | 메서드 + 경로 + HTTP 버전 |
| 헤더 | 부가 정보 (Content-Type, Authorization 등) |
| 본문(Body) | 전송할 데이터 (GET은 보통 없음) |

## 3. 주요 메서드
| 메서드 | 의미 | 예시 |
|---|---|---|
| GET | 조회 | 거래 목록 보기 |
| POST | 생성 | 거래 등록 |
| PUT | 전체 수정 | 거래 전체 교체 |
| PATCH | 일부 수정 | 금액만 변경 |
| DELETE | 삭제 | 거래 삭제 |

## 4. 상태 코드
| 범위 | 의미 | 자주 쓰는 코드 |
|---|---|---|
| 2xx | 성공 | 200 OK, 201 Created, 204 No Content |
| 3xx | 리다이렉트 | 301 영구 이동, 302 임시 이동, 304 Not Modified |
| 4xx | 클라이언트 오류 | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found |
| 5xx | 서버 오류 | 500 Internal Server Error, 503 Service Unavailable |

## 5. 헷갈리는 코드 정리
- **401**: 인증 안 됨 (로그인 필요)
- **403**: 인증은 됐지만 권한 없음
- **400**: 요청 형식·값이 잘못됨 (입력값 검증 실패)

## 6. 확인 방법
- 브라우저 개발자 도구(F12) → **Network** 탭 → 요청 클릭 → Headers / Response 확인

## 정리
- 프론트엔드와 백엔드는 HTTP로 대화한다.
- 응답 코드를 보면 문제가 클라이언트(4xx)인지 서버(5xx)인지 먼저 구분할 수 있다.
