# 🔍 CMP Dishing & Erosion Defect Feature Extraction using OpenCV

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Google Colab](https://img.shields.io/badge/Google_Colab-Open_in_Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green.svg)](https://opencv.org/)
[![Domain](https://img.shields.io/badge/Domain-Semiconductor_Inspection-red.svg)](#)

> **구리(Cu) 하이브리드 본딩 CMP 공정 중 발생해 수율에 치명적인 영향을 미치는 Dishing 및 Erosion 결함을 AFM/SEM 단면 이미지로부터 자동 검출하고 정량화하는 시뮬레이션 프로젝트**

---

## 📌 1. Project Overview (프로젝트 개요)

차세대 반도체 패키징 기술인 **Cu-to-Cu Hybrid Bonding** 공정에서는 배선 금속(Cu)과 절연체($\text{SiO}_2$ / $\text{SiCN}$) 간 연마 속도 차이로 인해 표면 패임 결함인 **Dishing(단일 배선 패임)** 및 **Erosion(전체 절연체 딤플링)**이 발생합니다.

본 프로젝트는 OpenCV 컴퓨터 비전 기술을 활용하여 이미지 기반 결함 검출 알고리즘을 구축합니다. 단면 높이 데이터(AFM/SEM)로부터 결함 영역을 자동 이진화(Binarization) 및 윤곽선(Contour) 추출을 통해 검출하고, 2D 깊이 프로파일과 **Defect Area Ratio (결함 면적 비율)**를 자동 산출합니다.

---

## 🎯 2. Key Objectives (주요 목표)

- **결함 이미지 전처리**: Gaussian Blur 및 Otsu Thresholding을 활용한 AFM/SEM 명암(Height) 이미지 이진화
- **결함 영역 자동 검출**: Canny Edge Detection 및 Contour Extraction 기반 패임 영역 바운딩
- **2D 단면 프로파일링**: 결함의 최적 깊이(Depth) 및 넓이(Width) 파라미터 2D 그래픽 시각화
- **결함 정량화 지표 자동화**: 전체 배선 영역 대비 패임 결함 면적 비율($\text{Defect Ratio}$) 정량 산출

---

## 📐 3. Mathematical Modeling & Defect Metrics (수학적 모델)

### 3.1 Dishing & Erosion 깊이 정의
$$h_{\text{defect}}(x) = h_{\text{dielectric}}(x) - h_{\text{metal}}(x)$$

* $h_{\text{dielectric}}$ : 기준 절연체 표면 높이 ($\text{nm}$)
* $h_{\text{metal}}$ : 연마 후 Cu 배선 중앙부 표면 높이 ($\text{nm}$)

### 3.2 Thresholding (Otsu Binarization)
이미지 픽셀 강도 $I(x, y)$에 대해 집단 내 분산(In-class Variance)을 최소화하는 최적 임계값 $T^*$ 산출:

$$\sigma_w^2(T) = w_0(T)\sigma_0^2(T) + w_1(T)\sigma_1^2(T)$$
$$\text{Mask}(x, y) = \begin{cases} 1 & \text{if } I(x, y) \le T^* \quad (\text{Defect Area}) \\ 0 & \text{otherwise} \end{cases}$$

### 3.3 Defect Area Ratio (결함 면적 비율)
$$\text{Defect Ratio (\\%)} = \left( \frac{\sum_{(x,y) \in \text{Defect}} 1}{\sum_{(x,y) \in \text{ROI}} 1} \right) \times 100 = \left( \frac{A_{\text{defect}}}{A_{\text{ROI}}} \right) \times 100$$

---

## 👤 4. Author & License

- **Author**: [Seung Ju Kim] / [tmdwn010520@gmail.com] / [www.linkedin.com/in/seung-ju-kim-488881391]
- **License**: MIT License
