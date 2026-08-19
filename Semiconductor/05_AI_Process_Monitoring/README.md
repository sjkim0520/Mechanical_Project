# ⚙️ AI-Driven Real-Time CMP Pad Wear & Defect FDC System

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-EE4C2C.svg?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.x-orange.svg)](https://scikit-learn.org/)
[![Domain](https://img.shields.io/badge/Domain-Semiconductor_FDC-purple.svg)](#)

> **CMP(Chemical Mechanical Planarization) 공정 중 실시간 가속도(진동) 센서 신호를 딥러닝(1D-CNN)으로 분석하여 패드 마모(Pad Wear) 및 마이크로 스크래치(Micro-scratch) 결함을 실시간 진단(FDC)하는 AI 시스템**

---

## 📌 1. Project Overview (프로젝트 개요)

반도체 CMP 공정에서 연마 패드(Pad)의 표면 상태는 웨이퍼 평탄화 품질과 결함 발생률에 직접적인 영향을 미칩니다. 패드가 과도하게 마모되거나 이상 마찰이 발생할 경우, 웨이퍼 표면에 수 나노미터 크기의 **마이크로 스크래치(Micro-scratch)**가 발생하여 수율이 급격히 저하됩니다.

본 프로젝트는 CMP 헤드 및 패드 컨디셔너에 부착된 **가속도(진동) 센서의 실시간 시계열(Time-Series) 데이터**를 수집하고, **1D-CNN(1-Dimensional Convolutional Neural Network)** 딥러닝 모델을 활용하여 공정 상태를 정상(Normal), 패드 마모(Wear), 마이크로 스크래치(Micro-scratch)의 3가지 상태로 실시간 분류하는 **FDC(Fault Detection and Classification)** 시스템을 구축합니다.

---

## 🎯 2. Key Objectives (주요 목표)

- **진동 시계열 데이터 전처리 & 특징 추출**: 고주파 가속도 센서 신호의 푸리에 변환(FFT) 및 통계적 특징량(RMS, Kurtosis 등) 생성
- **1D-CNN 딥러닝 모델 설계**: 시계열 진동 패턴의 국소적 특징(Local Pattern)을 정밀하게 추출하는 1D-Convolution 아키텍처 구축
- **실시간 이상 진단(FDC) 검증**: Multi-class Classification 환경에서 Confusion Matrix 및 ROC-AUC(OvR) 지표를 통한 이상 검출 모델 성능 검증

---

## 📐 3. Mathematical Modeling & Domain Concepts (수학적 모델)

### 3.1 고속 푸리에 변환 (FFT, Fast Fourier Transform)
시간 영역(Time-Domain)의 진동 신호 $x(n)$을 주파수 영역(Frequency-Domain) $X(k)$로 변환하여 마찰 주파수 성분을 추출:

$$X(k) = \sum_{n=0}^{N-1} x(n) \cdot e^{-j 2\pi \frac{k n}{N}}$$

* $N$ : 샘플링 픽셀/데이터 개수
* $x(n)$ : 시간 $n$에서의 진동 가속도 값 ($\text{m/s}^2$)

### 3.2 1차원 합성곱 연산 (1D-Convolution Layer)
시계열 진동 데이터 $X$에 대해 필터(Kernel) $W$를 슬라이딩하며 파형 특성을 압축 추출:

$$y[i] = f \left( \sum_{m=0}^{K-1} X[i + m] \cdot W[m] + b \right)$$

* $K$ : 커널 크기 (Kernel Size)
* $W[m]$ : 학습 가능한 합성곱 가중치
* $f(\cdot)$ : 비선형 활성화 함수 (ReLU)

### 3.3 다중 클래스 교차 엔트로피 손실 (Categorical Cross-Entropy Loss)
3가지 공정 상태(Normal, Micro-scratch, Wear) 분류를 위한 손실 함수:

$$\mathcal{L} = -\sum_{c=1}^{C} y_c \log(\hat{y}_c)$$

* $C$ : 클래스 개수 ($C=3$)
* $y_c$ : 실제 정답 라벨 (One-hot vector)
* $\hat{y}_c$ : Softmax 레이어를 거친 모델의 클래스별 예측 확률 ($\sum \hat{y}_c = 1$)

---

## 💡 초보자를 위한 반도체 FDC & 딥러닝 개념 해설

**1. 반도체 FDC(Fault Detection and Classification)란?**
* **개념**: 공정 장비에 달린 수많은 센서(진동, 압력, 온도 등) 데이터를 실시간으로 감시하다가, 이상 징후가 감지되면 즉시 장비를 멈추고 결함 원인을 분류하는 **반도체 팹(FAB)의 자동 경보 시스템**입니다.
* **왜 진동 센서를 쓰나요?**: 패드가 닳거나 패드 위에 이물질이 끼어 웨이퍼를 긁을 때 발생하느 미세한 마찰음과 진동 변화를 가속도 센서가 가장 빠르게 잡아낼 수 있기 때문입니다.

**2. 왜 2D-CNN이 아니라 1D-CNN을 사용하나요?**
* 이미지 데이터는 가로$\times$세로의 2차원 Grid 구조이므로 `Conv2d`를 사용합니다.
* 반면 센서 데이터는 **시간의 흐름에 따른 1차원 파형(Time-Series)** 형태이므로, 1차원 필터로 시간 축을 따라 훑으며 진동 패턴을 학습하는 `Conv1d`가 연산 속도가 훨씬 빠르고 실시간 진단에 적합합니다.

---

## 👤 4. Author & License

- **Author**: [Seung ju Kim] / [tmdwn010520@gmail.com] / [www.linkedin.com/in/seung-ju-kim-488881391]
- **License**: MIT License
