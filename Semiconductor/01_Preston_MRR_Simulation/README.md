# 🧪 CMP Process Mathematical Modeling & WIWNU Analysis

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Domain](https://img.shields.io/badge/Domain-Semiconductor%20Process-green.svg)](#)

> **CMP(Chemical Mechanical Planarization) 공정의 물리적/기계적 메커니즘 수치 해석 및 Preston 방정식 기반 WIWNU(Wafer Within-Wafer Non-Uniformity) 최적화 시뮬레이션**

---

## 📌 1. Project Overview (프로젝트 개요)

반도체 제조 공정 중 **CMP(Chemical Mechanical Planarization)**는 웨이퍼 표면의 국소적/전역적 평탄화를 달성하는 핵심 공정입니다. 

본 프로젝트는 CMP의 기본 물리 법칙인 **Preston's Law ($MRR = k_p \cdot P \cdot V$)**를 바탕으로, 공정 변수(압력 $P$, 상대 속도 $V$)에 따른 재료 제거율(Material Removal Rate)을 시뮬레이션합니다. 또한 플래튼과 캐리어의 회전 속도 동기화($\omega_p$ vs $\omega_c$)에 따른 웨이퍼 반경 방향 선속도 차이를 해석하여, 반도체 현업의 핵심 품질 지표인 **WIWNU (Within-Wafer Non-Uniformity)**를 최소화하는 최적 공정 조건을 정량 도출합니다.

---

## 🎯 2. Key Objectives (주요 목표)

- **공정 변수 물리 해석**: 압력($1 \sim 5 \text{ psi}$) 및 회전 속도($30 \sim 120 \text{ rpm}$) 변화에 따른 MRR Response Surface 해석
- **운동학(Kinematics) 모델링**: 회전체 오프셋 운동 및 반경 방향 위치 $r$에 따른 상대속도 $V(r, \theta)$ 계산
- **WIWNU 정량 평가**: 웨이퍼 반경 방향 측정 지점 기준 표준편차 및 불균일도 지표 산출
- **공정 최적화 조건 입증**: $\omega_p = \omega_c$ (Synchronous Condition) 조건에서 기계적 균일도 극대화 검증

---

## 📐 3. Mathematical Modeling (수학적 모델)

### 3.1 Preston's Law (재료 제거율)
$$MRR = k_p \cdot P \cdot V$$

* $MRR$ : Material Removal Rate ($\text{nm/min}$)
* $k_p$ : Preston Coefficient ($\approx 1.5 \times 10^{-13} \text{ Pa}^{-1}$)
* $P$ : Applied Down Force / Pressure ($\text{psi} \rightarrow \text{Pa}$)
* $V$ : Relative Velocity between Wafer and Pad ($\text{m/s}$)

### 3.2 Kinematic Relative Velocity (운동학적 상대속도)
$$V(r, \theta) = \sqrt{(\omega_p R_{offset})^2 + ((\omega_p - \omega_c) r)^2 + 2 \omega_p R_{offset} (\omega_p - \omega_c) r \cos\theta}$$

* **Synchronous Condition ($\omega_p = \omega_c$)**:
  $$V(r) = \omega_p \cdot R_{offset} = \text{Constant}$$
  *(회전 속도가 동기화되면 웨이퍼 상의 모든 위치에서 상대 속도가 동일해져 균일도 극대화)*

### 3.3 WIWNU (Wafer Within-Wafer Non-Uniformity)
$$\text{WIWNU (\%)} = \left( \frac{\sigma_{MRR}}{\mu_{MRR}} \right) \times 100$$

* $\sigma_{MRR}$ : 반경별 측정 지점들의 MRR 표준편차
* $\mu_{MRR}$ : 반경별 측정 지점들의 MRR 평균값

---

## 👤 4. Author & License

- **Author**: [Seung Ju Kim] / [tmdwn010520@gmail.com] / [LinkedIn 또는 개인 블로그 링크]
- **License**: MIT License
