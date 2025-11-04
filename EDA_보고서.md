# 데이터 탐색 결과

## 고객 이탈(churn) 분석
<img width="900" height="500" alt="{0381781B-87DF-486D-894B-AB5FDEF14E7D}" src="https://github.com/user-attachments/assets/b6648a44-dc76-45fe-a558-00a6e789f40a" />

전체 고객 중 이탈 고객의 비율이 유지 교객의 비율보다 약 10% 더 높다.

## Subscription_age & Churn

### 구독 연수
<img width="500" height="350" alt="{AF5B0FC8-107D-43DC-8CB7-0CA5C99A8AE4}" src="https://github.com/user-attachments/assets/500248f6-cec8-43b8-bacf-3c528b99fb5c" />    <img width="350" height="350" alt="{D5FC39D2-EB56-4DDE-888E-E2364D457478}" src="https://github.com/user-attachments/assets/a99f5338-332f-403f-a420-4e9ee779456c" />

보통 인터넷 계약 기간은 1년, 2년, 3년으로 이루어지므로 초기, 중기(약정), 장기(재계약), 충성고객으로 구간화하였다.
| 구간    | 고객 비율 | 이탈률   | 특징                  |
| ----- | ----- | ----- | ------------------- |
| 0~1 years | 27.4% | 높음    | 초기 고객군 — 온보딩 실패 가능성 |
| 1~3 years  | 43.4% | 매우 높음 | 약정 만료 구간, 이탈 집중     |
| 3~5 years  | 16.5% | 낮음    | 재계약 고객 — 안정화 구간     |
| greater than 5 years | 12.7% | 매우 낮음 | 충성 고객층 형성           |

### 구독 연수와 이탈 여부
<img width="600" height="400" alt="{C431BBF1-02C3-49DD-9AED-24BC69E8B77D}" src="https://github.com/user-attachments/assets/ec8b1b86-5170-4173-bef2-b4db59dd70d2" />

```
<분석 결과>
- 전체 고객 중 1~3년 구간이 가장 많으며, 이 구간의 이탈률이 가장 높다.
- 이는 기본 약정 기간(1~3년) 이 만료되는 시점에서 재계약 유도나 서비스 만족도 관리가 미흡함을 알 수 있다.

<문제점>
- 약정 종료 후 갱신 프로세스 부재 → 고객 이탈로 직접 연결
- 신규 고객(0~1년)은 초기 경험 문제로 churn 위험 높음 <br>

<시사점>
- 1~3년차 고객 대상 “재계약 프로모션” 필요
- 0~1년차 고객 대상 온보딩·체험 관리 강화
- 장기 고객(5년 이상) 대상 리워드·혜택 유지로 충성도 유지
```

## Subscription_label & Churn

### 구독 유형
<img width="500" height="350" alt="{B98ECDBE-AC45-4553-BA3D-A80F2735050C}" src="https://github.com/user-attachments/assets/0c8c1df7-2771-4e9c-92ab-c5a42b8dbd45" />  <img width="250" height="200" alt="{61355983-2BD8-437F-AE3F-38959BC9FA40}" src="https://github.com/user-attachments/assets/c4dd67dd-ad50-467c-9a38-95699bd64a52" />

| 구독 유형           | 고객 수    | 특징         | 이탈률 추세              |
| --------------- | ------- | ---------- | ------------------- |
| TV만 구독 (tv)     | 34,954명 | 전체 중 가장 많음 | 유지 > 이탈 (약간의 차이)    |
| Both (tv+movie) | 24,015명 | 복합 구독 고객군  | 유지 고객이 이탈보다 약 2배 많음 |
| None (구독 없음)    | 13,281명 | 단일 서비스 이용  | 이탈 고객 비중 압도적        |
| Movie만 구독       | 2명      | 표본 거의 없음   | 통계적 의미 없음 |


### 구독 유형과 이탈 여부
<img width="600" height="400" alt="{B947130F-F56E-41E9-9D78-B564462D1B93}" src="https://github.com/user-attachments/assets/40276308-1eac-4cbd-9658-9eab4abb1928" />

```
<분석 결과>
- TV만 구독한 고객이 가장 많고, 이탈 고객이 더 많다.
- 복합 구독 고객(Both)은 이탈률이 가장 낮고, 유지 고객이 이탈 고객 보다 반 정도 더 많다.
- 구독 없음(None) 고객은 유지율이 가장 낮고 이탈 고객이 유지 고객에 비해 훨씬 많다.

<문제점>
- 복합 구독 유도 정책 부재
- Movie 단독 상품 수요 및 유입 부족
- 구독 없음 고객군(None)은 서비스 체감도가 낮아 충성도 형성 어려움

<시사점>
- TV+영화 결합 상품(패키지) 프로모션 강화
- Movie 단일 구독 상품 개선 또는 폐합 검토
- 구독 없음 고객 대상 체험/추천 콘텐츠 제공 → 전환 유도
```











