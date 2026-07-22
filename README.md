# 니트로사민 불순물 규제 모니터링

국내(식약처) · 미국(FDA) · 유럽(EMA)의 니트로사민류 불순물 **허용섭취한도(AI limit)** 를 통합 비교하고,
자사 사용 원료와 대조하며, 규제 변경(신규/변경)을 감지하는 웹 대시보드입니다.

## 주요 기능
- 3개 규제기관 기준을 나란히 비교하는 카드 (AI limit · CPCA 분류 · 공개일)
- 자사 원료 현황표(엑셀) 업로드 → 해당되는 불순물 자동 리스트업
- 직전 갱신 대비 **신규/변경** 하이라이트 + 최근공개(14일) 배지
- 불순물명 · CAS · 원료 검색/필터

## 구조
- `index.html` — 의존성 없는 단일 정적 페이지. 브라우저에서 **Supabase(PostgREST)** 를 직접 조회해 렌더링합니다.
- 페이지에 포함된 Supabase 키는 **공개용(publishable) 키** 이며, 읽기 전용 RLS 정책으로 보호됩니다.
- 규제 사이트 자동 수집 · 통합 · 적재 · 변경감지 · 메일 알림은 **로컬 자동화 스크립트**가 담당하고, 결과만 Supabase에 저장합니다. (이 저장소에는 포함되지 않음)

## 배포
Vercel 정적 호스팅. `index.html` 이 루트(`/`)에서 서빙됩니다. 별도 빌드 단계가 없습니다.

## 데이터 출처
- 식약처 nedrug (1일 섭취허용량)
- FDA CDER Nitrosamine Impurity Acceptable Intake Limits
- EMA Appendix 1: Acceptable intakes established for N-nitrosamines
