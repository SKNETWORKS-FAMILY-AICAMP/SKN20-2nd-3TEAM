![header](https://capsule-render.vercel.app/api?type=blur&height=200&color=gradient&text=SKN20-2nd-3TEAM&reversal=false&fontColor=35007f&fontSize=50)

# <img src="https://raw.githubusercontent.com/Tarikul-Islam-Anik/Telegram-Animated-Emojis/main/Animals%20and%20Nature/Lion.webp" alt="Lion" width="25" height="25" /> Team Member
<table>
  <tr>
    <th>강민지</th>
    <th>김지은</th>
    <th>김효빈</th>
    <th>안채연</th>
    <th>홍혜원</th>
  </tr>
    <td><a href="https://github.com/mminguu"><img src="https://img.shields.io/badge/GitHub-mminguu-green?logo=github"></a></td>
    <td><a href="https://github.com/carookim"><img src="https://img.shields.io/badge/GitHub-carookim-yellow?logo=github"></a></td>
    <td><a href="https://github.com/kimobi"><img src="https://img.shields.io/badge/GitHub-kimobi-blue?logo=github"></a></td>
    <td><a href="https://github.com/hochaeyeon"><img src="https://img.shields.io/badge/GitHub-hochaeyeon-lightblue?logo=github"></a></td>
    <td><a href="https://github.com/newhione"><img src="https://img.shields.io/badge/GitHub-newhione-pink?logo=github"></a></td>
  </tr>
</table>
  
---

# 인터넷 고객 이탈(Churn) 분석 및 예측

## 1. Project Overview
### 1.1. 배경
전 세계적으로 인터넷 서비스 제공업체(Internet Service Providers, ISP) 간의 경쟁이 치열해지고 있다.
새로운 고객을 확보하는 것도 중요하지만, 기존 고객을 유지(Retention) 하는 것이
매출 성장과 장기적인 수익성 확보에 더 큰 영향을 미친다.

서비스 품질 저하, 요금 불만, 약정 만료 등으로 인해 고객이 서비스를 해지하는 현상을 “Churn(이탈)” 이라고 하며,
통신사는 이러한 이탈 징후를 조기에 포착하고 대응하는 것이 매우 중요하다.

본 프로젝트는 **“어떤 고객이 서비스를 해지할 가능성이 높은가?”** 라는 문제를 다루며,
고객의 계약 상태, 이용 패턴, 서비스 품질, 요금 수준 등의 데이터를 분석하여
이탈을 유발하는 주요 요인을 파악하고, ISP의 고객 유지 전략(Retention Strategy) 수립에 필요한 인사이트를 제공하는 것을 목표로 한다.
### 1.2. 목표
- 이탈 고객(`Churn=1`) 과 유지 고객(`Churn=0`) 간의 특성 차이 분석
- 계약 상태(Contract Type), 서비스 이용 연수(Subscription Age), 요금 수준(Bill Avg), 데이터 사용량(Download/Upload), 서비스 품질(Service Failure, Over Limit) 등의 요인이
이탈에 미치는 영향 파악
- 통계적 검정 및 시각화를 통해 이탈에 유의미한 변수 도출
- EDA를 통해 도출된 결과를 기반으로 머신러닝 및 딥러닝 수행 및 성능 비교

---
  
## 2. Data Description & Preprocessing

| 구분          | 설명                       |
| ----------- | ------------------------ |
| **총 데이터 수** | 71,892개 고객 데이터           |
| **총 변수 수**  | 11개 변수                 |
| **분석 단위**   | 고객(user_id) 단위           |
| **타깃 변수**   | `churn` (0 = 유지, 1 = 이탈) |

### 2.1. 데이터셋 설명
| 컬럼명                           | 설명                                 | 데이터 타입 | 전처리 내용                                   |
| -------------------------------- | ------------------------------------ | ------------ | --------------------------------------------- |
| `id`                             | 고객 ID                              | int          | 삭제                                          |
| `bill_avg`                       | 최근 3개월 평균 청구 금액(단위: $)   | float        | 로그 변환(`bill_avg_log`) 수행               |
| `service_failure_count`          | 최근 3개월 동안 고객센터 신고 건수    | int          | 이상치 탐지 및 분포 확인                     |
| `download_avg`                   | 최근 3개월 평균 다운로드 사용량(GB)  | float        | 결측치 381행 제거 후, 로그 변환(`download_avg_log`) 수행          |
| `upload_avg`                     | 최근 3개월 평균 업로드 사용량(GB)    | float        | `download_avg`의 결측 행과 동일 구간에서 결측치 발생 -> 자동 제거 후, 로그 변환(`upload_avg_log`) 수행 |
| `download_over_limit`            | 지난 9개월 동안 다운로드 한도 초과 횟수 | int        | 이상치 탐지 및 분포 확인                     |
| `remaining_contract`             | 남은 약정 기간(년 단위, null이면 계약 없음) | float   | 파생 변수 `contract_type` 생성 후 삭제        |
| `subscription_age`               | 서비스 이용 기간(년 단위)            | float        | -0.02 값 제거 후, 파생 변수 `subscription_age_group` 생성 후 삭제 |
| `is_tv_subscriber`               | TV 구독 여부 (1=구독, 0=미구독)      | int          | `subscription_label` 통합 후 삭제             |
| `is_movie_package_subscriber`    | 영화 패키지 구독 여부 (1=구독, 0=미구독) | int       | `subscription_label` 통합 후 삭제             |
| `churn`                          | 이탈 여부 (1=이탈, 0=유지)           | int          | Target 변수                                  |

### 2.2. 파생 변수 설명
| 파생 컬럼명                       | 생성 기준                                                | 값의 의미                                                                                   |
| ---------------------------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **`contract_type`**          | `remaining_contract` 값 기반으로 분류                       | `0: no_contract` → 계약 없음<br>`1: expired` → 계약 만료<br>`2: active` → 현재 약정 유지 중            |
| **`subscription_age_group`** | `subscription_age`를 구간화하여 그룹 생성                      | `0~1년`: 초기 고객<br>`1~3년`: 중기(약정)<br>`3~5년`: 장기(재계약)<br>`5년 이상`: 충성 고객                    |
| **`subscription_label`**     | `is_tv_subscriber`와 `is_movie_package_subscriber` 결합 | `0: none` (구독 없음)<br>`1: tv` (TV만 구독)<br>`2: movie` (영화만 구독)<br>`3: both` (TV+영화 결합 구독) |

본 프로젝트에서는 분석 목적과 모델 구조에 따라 데이터를 세 가지 형태로 구분하여 활용하였다.

**EDA 및 트리 기반 모델**(Decision Tree, Random Forest, XGBoost 등) 에서는
범주형 변수를 구간화·라벨링한 데이터를 사용하였다.
트리 계열 모델은 범주형 피처를 직접 처리할 수 있으므로
`contract_type`, `subscription_age_group`, `subscription_label`을
라벨 인코딩(Label Encoding) 방식으로 변환하였다.

**회귀 및 비트리 기반 모델**(Logistic Regression, SVM 등) 에서는
모델이 연속형 입력에 민감하기 때문에,
`subscription_age`는 연속형 변수로 유지하고,
`contract_type`과 `subscription_label`은 원-핫 인코딩(one-hot encoding) 하였다.

또한, 모델의 안정성과 예측 성능 향상을 위해
`bill_avg`, `download_avg`, `upload_avg`에 대해 로그 변환(Log Transformation) 을 적용한 버전과
변환하지 않은 원본 버전 두 가지를 비교 실험하였다.
이를 통해 로그 변환이 데이터의 분포 왜곡(skewness) 완화와 모델 성능 개선에 미치는 영향을 검증하였다.

---

## 3. EDA
EDA 결과 **고객의 이탈(Churn)**은 **요금, 서비스 품질, 계약 상태, 구독 조합, 구독 연수**에 의해 명확히 구분되는 패턴을 보였다.

- 요금(bill_avg): 낮을수록 이탈률 상승 → 저요금제 고객의 충성도 낮음
- 데이터 사용량(download_avg, upload_avg): 낮을수록 이탈률 높음 → 사용률 낮은 고객은 서비스 몰입도 낮음
- 서비스 품질(service_failure_count, download_over_limit): 불만(장애·초과)이 많을수록 churn 증가 → 품질 경험이 이탈의 직접 요인
- 계약 상태(contract_type): active 상태 고객은 유지율 높고, expired 고객은 대부분 이탈
- 구독 조합(subscription_label): 복합 구독(both) 고객의 이탈률이 가장 낮고, 단일 또는 미구독(none) 고객은 이탈률 높음
- 구독 연수(subscription_age_group): 연수가 길수록 churn 감소 → 장기 고객의 충성도 상승
- 
특히 **(Active 계약 × 복합 구독 × 장기 이용) 고객이 이탈률이 가장 낮은 핵심 유지 고객군(retention segment) 으로 확인**되었다.

---

## 4. Feature Engineering
- 파생 변수 추가 및 중요 변수 선정
- 로그 변환 변수 활용 여부 결정
- 중요 변수 시각화 (Feature Importance, Correlation Heatmap)

---

## 5. Modeling & Evaluation



