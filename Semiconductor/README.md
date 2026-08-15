# 🔬 Advanced Semiconductor Packaging & CMP Simulation Portfolio

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![MATLAB](https://img.shields.io/badge/MATLAB-R2025b-0076A8?style=flat&logo=mathworks&logoColor=white)](https://www.mathworks.com/)
[![Simulink](https://img.shields.io/badge/Simulink-Modeling-ED8B00?style=flat&logo=mathworks&logoColor=white)](https://www.mathworks.com/)
[![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=flat&logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-EE4C2C?style=flat&logo=pytorch&logoColor=white)](https://pytorch.org/)

> **차세대 반도체 패키징(HBM, Hybrid Bonding) 및 CMP(Chemical Mechanical Planarization) 공정의 수치해석, 최적화, 제어 및 AI 기반 모니터링 프로젝트입니다.**

---

## 📌 Overview

AI 및 고성능 컴퓨팅(HPC) 시대의 핵심인 **HBM** 및 **Advanced Packaging**을 위한 차세대 CMP 공정 메커니즘 해석과 공정 제어/AI 모니터링을 주제로 한 프로젝트 모음입니다. 본 저장소는 수치 해석(Physics-based), 반응표면 분석(Data-driven Optimization), 폐회로 제어(Control System), 딥러닝 기반 이상 진단(AI Monitoring)을 아우르는 6개의 모듈로 구성되어 있습니다.

---

## 🛠 Tech Stack & Tools

| 구분 | 사용 도구 / 라이브러리 |
| :--- | :--- |
| **Languages & Environment** | Python 3.10+, MATLAB R2025b, Google Colab |
| **Numerical & Modeling** | NumPy, SciPy, SymPy, Control System Toolbox |
| **Optimization & Data** | Pandas, Scikit-learn, CasADi |
| **AI & Computer Vision** | PyTorch, OpenCV, Matplotlib, Seaborn |

---

## 📂 Project Roadmap & Key Modules

---

### 🔰 Level 1. Basic Process Modeling & Defect Analysis

#### 1. Preston-based Wafer MRR & WIWNU Simulation
> **Preston 법칙 기반 CMP 웨이퍼 재료 제거율(MRR) 해석 및 불균일도(WIWNU) 평가**

* **Key Objective:** 압력($P$)과 상대 속도($V$) 분포에 따른 웨이퍼 표면 제거율 메커니즘 수치해석
* **Tech Stack:** `Python (SciPy, Matplotlib)`, `MATLAB`
* **Workflow Steps:**
  * **Step 1:** Preston 방정식 기반 화학적/기계적 연마 수식 모델링 및 공정 변수 설정
  * **Step 2:** 패드 회전 속도 및 압력 매개변수 스윕(Sweep)에 따른 2D/3D MRR 분포 맵 산출
  * **Step 3:** 웨이퍼 반경 방향 선속도 편차 계산 및 WIWNU(Within-Wafer Non-Uniformity) 정량화

#### 2. OpenCV Defect Feature Extraction for Dishing & Erosion
> **하이브리드 본딩 인터커넥트 단차 결함(Dishing/Erosion) 이미지 처리 및 특징 추출**

* **Key Objective:** Cu Hybrid Bonding 시 발생하는 Dishing/Erosion 결함의 정량적 프로파일링
* **Tech Stack:** `Python (OpenCV, Matplotlib, NumPy)`
* **Workflow Steps:**
  * **Step 1:** AFM / SEM 단면 이미지 데이터 노이즈 필터링 및 Binarization 전처리
  * **Step 2:** Canny Edge Detection 및 Contour 알고리즘 기반 패임 영역 자동 검출
  * **Step 3:** 결함 깊이 및 면적 프로파일 2D 시각화 및 결함률 자동 계산 함수 구현

---

### ⚙️ Level 2. Optimization & Process Control

#### 3. Cu Hybrid Bonding CMP Process Optimization via RSM
> **반응표면분석법(RSM)을 활용한 Cu 하이브리드 본딩 CMP 최적 공정 조건 도출**

* **Key Objective:** Dishing 최소화 및 MRR 극대화를 위한 다변량 공정 변수 동시 최적화
* **Tech Stack:** `Python (Scikit-learn, SciPy)`, `MATLAB`
* **Workflow Steps:**
  * **Step 1:** 압력, 패드 속도, 슬러리 Flow Rate를 독립 변수로 하는 2차 회귀 모델 수립
  * **Step 2:** 공정 데이터 피팅 및 Response Surface Contours 그래프 합성
  * **Step 3:** Multi-objective Optimization을 통한 Global Optimal 파라미터 조합 산출

#### 4. Simulink Closed-Loop In-Situ Wafer Thickness Control
> **실시간 두께 실구동 센싱 기반 CMP 폐회로(Closed-Loop) PID 제어기 설계**

* **Key Objective:** 패드 마모 및 연마율 저하 외란 발생 시 목표 웨이퍼 두께 오차 실시간 보정
* **Tech Stack:** `MATLAB / Simulink`
* **Workflow Steps:**
  * **Step 1:** CMP 공정 dynamics(1차 지연 전달함수 및 센서 Noise) 블록 모델링
  * **Step 2:** In-situ Metrology 센서 연동 가변 압력 PID 제어 루프 구축
  * **Step 3:** 외란(Disturbance) 투입 시 정상상태 오차 보정 성능 및 오버슛 평가

---

### 🚀 Level 3. AI-Driven Monitoring & Structural Analysis

#### 5. AI-Driven Real-Time CMP Pad Wear & Defect FDC System
> **딥러닝 기반 CMP 실시간 진동 신호 / 패드 마모 상태 AI 이상 진단(FDC)**

* **Key Objective:** 센서 데이터 기반 CMP 공정 이상 및 패드 조율(Conditioning) 시점 자동 예측
* **Tech Stack:** `Python (PyTorch, Scikit-learn, Seaborn)`
* **Workflow Steps:**
  * **Step 1:** CMP 진동(Acceleration) 센서 타임시리즈 데이터 전처리 및 Feature Engineering
  * **Step 2:** 1D-CNN / ResNet 기반 공정 상태 분류(Normal vs Micro-scratch vs Wear) 모델 구축
  * **Step 3:** Model Training, Confusion Matrix 및 ROC-AUC 성능 평가 지표 검증

#### 6. Thermo-Mechanical Warpage Analysis in Hybrid Bonding
> **하이브리드 본딩 열처리(Annealing) 과정의 열응력 및 웨이퍼 휘어짐(Warpage) 해석**

* **Key Objective:** 이종 재료(Si-Cu-SiO2) 열팽창계수(CTE) 미스매치에 따른 열응력 및 변형 계산
* **Tech Stack:** `Python (SciPy, NumPy)`, `MATLAB`
* **Workflow Steps:**
  * **Step 1:** Bimetallic Strip 수식 기반 열응력 및 모멘트 미분방정식 수립
  * **Step 2:** 열처리 온도 프로파일($25^\circ\text{C} \to 400^\circ\text{C}$)에 따른 수치해석(FDM) 코드 작성
  * **Step 3:** Cu Pad 영역의 유효 응력 집중부 및 Boussinesq 단차 변화 시뮬레이션

---

## 📁 Repository Structure

```text
├── 01_Preston_MRR_Simulation/
│   ├── main_mrr_sim.ipynb
│   └── README.md
├── 02_Defect_Feature_Extraction/
│   ├── dishing_detection.ipynb
│   └── sample_images/
├── 03_Cu_CMP_RSM_Optimization/
│   └── rsm_optimization.ipynb
├── 04_InSitu_Thickness_Control/
│   ├── cmp_control_sim.slx
│   └── params.m
├── 05_AI_Process_Monitoring/
│   ├── train_fdc_model.py
│   └── dataset/
├── 06_ThermoMechanical_Warpage/
│   └── warpage_analysis.py
└── README.md
