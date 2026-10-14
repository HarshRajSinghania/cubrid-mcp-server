# 문제 해결 (한국어)

> 🌐 [TROUBLESHOOTING.md](https://github.com/cubrid-lab/cubrid-mcp-server/blob/main/docs/TROUBLESHOOTING.md)의 번역입니다. 영어 원문이 표준이며, 페이지 번역은 경고 수준의 동기화 규칙을 따릅니다.

## 연결 실패

**증상:** 클라이언트가 서버에 연결하지 못하거나 도구 호출이 타임아웃됩니다.

- CUBRID 서버가 실행 중인지, `CUBRID_HOST`/`CUBRID_PORT`가 맞는지 확인하세요.
- 방화벽이 33000 포트를 막고 있지 않은지 확인하세요.
- `CUBRID_USER`/`CUBRID_PASSWORD`/`CUBRID_DATABASE`가 올바른지 확인하세요.

## 권한 오류

**증상:** `SELECT` 문에서 권한 오류.

CUBRID 사용자에게 권한이 없습니다. CUBRID는 **테이블 단위**로 권한을 부여합니다 — 스키마 전체 `db.*` 부여는 없습니다. 사용자를 만들고 모델이 읽을 각 테이블에 `SELECT`를 부여하세요. [보안 모델](SECURITY_MODEL.md#계층-1--데이터베이스-권한-필수) 참고.

## 읽기 전용 거부

**증상:** 쓰기 문장이 거부됩니다.

의도된 동작입니다. `execute_query`는 읽기 전용입니다. 쓰기가 필요하면 `CUBRID_MCP_WRITE=1`로 옵트인하고 `execute_write`를 사용하세요.

## 감사 로그가 안 남음

`CUBRID_MCP_AUDIT_LOG=1`을 설정하세요(옵트인, 기본 꺼짐). 멀티커넥션에서는 연결별로 `CUBRID_<NAME>_MCP_AUDIT_LOG`로 켭니다. 기록은 **stderr**의 JSON 라인입니다 — stdout에는 절대 나오지 않습니다. [보안 모델](SECURITY_MODEL.md#계층-4--감사-로그-옵트인) 참고.
