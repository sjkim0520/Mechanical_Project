# 🎛️ HBM Cu Hybrid Bonding CMP Process Optimization using RSM

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Google Colab](https://img.shields.io/badge/Google_Colab-Open_in_Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.x-orange.svg)](https://scikit-learn.org/)
[![SciPy](https://img.shields.io/badge/SciPy-1.x-blue.svg)](https://scipy.org/)
[![Domain](https://img.shields.io/badge/Domain-Semiconductor_Optimization-purple.svg)](#)

> **HBM(High Bandwidth Memory) Cu-to-Cu 하이브리드 본딩 공정의 핵심인 Cu 단차 최소화를 위한 반응표면분석법(RSM) 기반 다변량 공정 최적화 시뮬레이션 프로젝트**

---

## 📌 1. Project Overview (프로젝트 개요)

HBM의 초고밀도 적층을 위한 **Cu 하이브리드 본딩(Hybrid Bonding)** 기술에서는 Cu 배선과 절연체 간의 단차(Dishing)를 수 나노미터($\text{nm}$) 수준으로 제어하는 것이 필수적입니다. 

본 프로젝트는 공정 주요 변수인 **압력($P$), 회전속도($V$), 슬러리 유량($F$)**이 **연마율(MRR)** 및 **Dishing 깊이**에 미치는 복합적 상하작용을 **반응표면분석법(Response Surface Methodology, RSM)**을 통해 모델링합니다. 2차 회귀 방정식(2nd-order Polynomial Model)을 수립하고, Scipy의 최적화 알고리즘을 활용하여 **Dishing을 최소화하면서 MRR을 극대화하는 Global Optimum 공정 파라미터 조합**을 도출합니다.

---

## 🎯 2. Key Objectives (주요 목표)

- **다변량 공정 데이터 세트 합성**: Central Composite Design(CCD) 기반 3변수($P, V, F$) 2차 반응표면 데이터 구축
- **2차 회귀 모델링 (Polynomial Regression)**: 공정 변수 간 교차항($X_i X_j$) 및 제곱항($X_i^2$)을 포함한 다변량 회귀분석
- **복합 목적함수(Multi-Objective Function) 최적화**: Dishing 최소화 및 MRR 극대화를 만족하는 Pareto 최적점 산출
- **Response Surface 2D/3D 시각화**: 최적 공정 마진(Process Window) 확보를 위한 등고선(Contour) 지도 작성

---

## 📐 3. Mathematical Modeling (수학적 모델)

### 3.1 2차 반응표면 회귀 모델 (2nd-Order RSM Model)
$$Y = \beta_0 + \sum_{i=1}^{k} \beta_i X_i + \sum_{i=1}^{k} \beta_{ii} X_i^2 + \sum_{i \lt j} \beta_{ij} X_i X_j + \epsilon$$

* $Y$ : 반응치 ($\text{MRR}$ 또는 $\text{Dishing Depth}$)
* $X_1, X_2, X_3$ : 공정 변수 (압력 $P$, 속도 $V$, 슬러리 유량 $F$)
* $\beta_0, \beta_i, \beta_{ii}, \beta_{ij}$ : 편회귀 계수 (선형, 제곱, 교차작용)

### 3.2 최적화 목적함수 (Multi-Objective Optimization)
Dishing 깊이는 최소화하고 MRR은 극대화하기 위한 가중치 기반 손실 함수(Cost Function) $J(\mathbf{X})$ 정의:

$$\min_{\mathbf{X}} J(\mathbf{X}) = - w_1 \cdot \left( \frac{\text{MRR}(\mathbf{X})}{\text{MRR}_{\max}} \right) + w_2 \cdot \left( \frac{\text{Dishing}(\mathbf{X})}{\text{Dishing}_{\min}} \right)$$

$$\text{Subject to: } P_{\min} \le P \le P_{\max}, \quad V_{\min} \le V \le V_{\max}, \quad F_{\min} \le F \le F_{\max}$$

---

## 👤 4. Author & License

- **Author**: [Seung Ju Kim] / [tmdwn010520@gmail.com] / [www.linkedin.com/in/seung-ju-kim-488881391]
- **License**: MIT License
