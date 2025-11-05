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

본 프로젝트는 **“어떤 고객이 서비스를 해지할 가능성이 높은가?”**론
- 최적화 기법(RandomSearch 포함)을 적용하더라도 기저 성능이 일정 수준 이상이면 성능 개선 폭이 크지 않음을 확인함. 
- 이 문제 설정에서는 복잡한 모델 설계나 고도화된 튜닝보다는, 데이터 전처리와 피처 품질이 성능에 더 큰 영향을 미친다는 점을 확인하였음. 
- MLP 구조를 다양한 프레임워크와 최적화 방법으로 적용하였으나, 성능 변동은 미미했으며 이는 본 문제에서 모델 복잡도보다 데이터 품질과 전처리 과정이 더 중요한 요인임을 의미함

