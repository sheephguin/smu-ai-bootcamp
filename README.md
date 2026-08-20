# 청년안심주택 청약 도우미 RAG 프로젝트

상명대 계절학기 RAG·AI Agent 실습 과정에서 진행한 팀 프로젝트입니다.

## 주제

**2026년 2차 서울시 청년안심주택(공공임대) 청약 도우미**

66페이지 분량의 입주자모집공고문을 사용자가 직접 읽지 않아도, 자연어 질문 한 번으로 일정·자격·임대조건·서류·가점 등 원하는 정보를 바로 찾아주는 RAG 기반 챗봇입니다.

## 파일 구성

| 파일 | 내용 |
|---|---|
| `day2_team_project.ipynb` | PDF 공고문 기반 RAG 파이프라인 (비정형 데이터) |
| `day3_team_project.ipynb` | 테이블 데이터 기반 Text2SQL 조회 시스템 (정형 데이터) |

## 사용한 데이터

**day2 — 비정형 데이터**
- `2026년 2차 청년안심주택 모집공고문.pdf` (서울주택도시공사, 2026.07.31. 공고, 68페이지)
- PyMuPDF(fitz)로 페이지 단위 텍스트 추출 → 500자 단위 청킹(50자 오버랩) → 목차 기준 12개 카테고리(공급일정·신청자격·임대조건·제출서류 등) 메타데이터 태깅 → Qdrant Cloud에 임베딩 적재(363개 청크)

**day3 — 정형 데이터 (CSV 3종)**

| CSV | 내용 |
|---|---|
| `apartment.csv` | 단지별 공급유형·평면·임대보증금·계약금·잔금·월임대료 |
| `preferences.csv` | 청년/신혼부부Ⅰ/신혼부부Ⅱ 신청자격·순위·소득기준·자산기준·가점사항 |
| `service_center.csv` | 공공임대·민간임대·법률지원 등 문의처 및 연락처 |

CSV를 SQLite(로컬)·Supabase(PostgreSQL, 클라우드)에 적재하고, 자연어 질문을 SQL로 변환해 조회하는 Text2SQL 방식으로 구현했습니다.

## 기술 스택

PyMuPDF · LangChain(RecursiveCharacterTextSplitter) · OpenAI Embeddings(text-embedding-3-small) · Qdrant Cloud · SQLite/Supabase · GPT-4o-mini
