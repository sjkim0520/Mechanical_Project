<div align="center">

# 🎛️ CMP 폐회로(Closed-Loop) 웨이퍼 두께 제어 시뮬레이션

### Closed-Loop Wafer Thickness Control for CMP — Python / Google Colab Edition

![Field](https://img.shields.io/badge/Field-Process%20Control%20%7C%20Semiconductor-blue)
![Tech](https://img.shields.io/badge/Tech-PID%20%7C%20In--situ%20Metrology%20%7C%20Disturbance%20Rejection-orange)
![Tool](https://img.shields.io/badge/Tool-Python%20(numpy%2C%20scipy%2C%20matplotlib)-yellow)
![Level](https://img.shields.io/badge/Level-Beginner%20Friendly-brightgreen)
![Duration](https://img.shields.io/badge/Duration-1%20Week-lightgrey)

**1차 지연 공정모델 + In-situ 두께 센서 + PID 제어기를 파이썬 시뮬레이션 루프로 직접 구현하고,<br>패드 마모 외란 속에서도 목표 두께에 정확히 도달하는 적응형 제어기를 설계하는 미니 프로젝트**

> 이 버전은 MATLAB/Simulink 없이 **Google Colab에서 Python만으로** 동일한 폐회로 제어 시스템을 구현하도록 재구성한 버전입니다.

</div>

---

## 📌 프로젝트 개요

CMP(화학기계연마) 공정에서는 연마가 진행되는 동안 웨이퍼 두께가 계속 얇아지며, 목표 두께에 정확히 도달한 뒤 멈추는 것이 수율과 직결됩니다. 최신 CMP 장비는 편심전류(eddy current) 센서 등으로 연마 중에도 실시간으로 두께를 측정하는 **In-situ Metrology** 시스템을 갖추고, 이 측정값을 바탕으로 압력을 실시간으로 조절하는 **피드백 제어(closed-loop control)**를 수행합니다.

이 프로젝트는

1. CMP 공정을 "압력 → 연마율(1차 지연) → 누적 제거두께(적분)"로 이어지는 제어계로 수식화하고,
2. 이를 파이썬 시간영역 시뮬레이션 루프(In-situ 센서 노이즈 + PID 제어기 + 압력 포화)로 직접 구현하며,
3. 패드 마모(pad wear)로 연마율이 서서히 저하되는 현실적인 외란 속에서도 목표 두께에 정확히 도달하는 **게인 스케줄링 기반 적응형 PID**를 설계·검증하는

3단계로 구성됩니다.

## 🎯 연구 연관성

- 실시간 피드백 제어 시스템을 가상으로 구축해, 연마 진행에 따른 웨이퍼 두께 오차를 실시간으로 보정하는 제어기 설계 역량을 기릅니다.
- 1차 지연 전달함수, PID 제어, 외란 보상이라는 공정제어의 핵심 개념을 코드로 직접 구현하며 체득합니다.
- 반도체 공정에서 널리 쓰이는 In-situ Metrology 개념과, 센서 노이즈를 포함한 폐회로 시스템 설계·검증 워크플로우를 경험합니다.

## 🛠 사용 기술 스택

| 분류 | 도구 |
|---|---|
| 실행 환경 | Google Colab (권장) 또는 Jupyter Notebook |
| 언어 | Python 3 |
| 핵심 라이브러리 | `numpy`, `pandas`, `matplotlib`, `scipy.signal` |

```bash
pip install numpy pandas matplotlib scipy
```

## 🗂 폴더 구조

```
04_InSitu_Thickness_Control/
├── README.md                                       # 본 파일
├── requirements.txt                                  # 필요 패키지 목록
├── Step1_전달함수모델링과_센서노이즈.ipynb          
├── Step2_폐회로_PID_시뮬레이션.ipynb               
└── Step3_패드마모외란과_적응형PID.ipynb              
```

## 🗓 일정

| 단계 | 주제 | 핵심 활동 | 노트북 |
|---|---|---|---|
| **Step1** | 수학적 모델링 | CMP 공정을 1차 지연 전달함수 $G(s)=K/(\tau s+1)$로 근사(`scipy.signal.TransferFunction`), 적분기와 결합해 "압력→제거두께" 플랜트 완성, In-situ 센서 노이즈를 가우시안 백색잡음으로 모델링 | `Day1_2_전달함수모델링과_센서노이즈.ipynb` |
| **Step2** | 폐회로 PID 시뮬레이션 구현 | PID 제어기 클래스와 플랜트 클래스를 직접 구현, 오일러 적분법으로 목표두께-오차-PID-포화-플랜트-센서노이즈-피드백 폐회로를 시간영역에서 시뮬레이션, Type-1 시스템 이론(P 제어만으로 정상상태오차 0) 검증 | `Day3_4_폐회로_PID_시뮬레이션.ipynb` |
| **Step3** | 외란 보상 &amp; 적응형 PID 검증 | 패드 마모(지수적 연마율 저하) 외란을 모델에 추가, 오차 크기 기반 게인 스케줄링으로 적응형 PID 구현, 고정게인 PID와 성능(정착시간/오버슈트/정상상태오차) 비교, 임계값 파라미터 스윕 | `Day5_7_패드마모외란과_적응형PID.ipynb` |

## 🧮 핵심 수학 개념 (초급자용 요약)

1. **1차 지연 전달함수** — 공정의 응답 지연을 근사하는 표준 모델: $G(s)=\dfrac{K}{\tau s+1}$. $K$는 정상상태 이득, $\tau$는 목표값의 63.2%에 도달하는 시간(시간상수)
2. **적분형(Type-1) 플랜트** — 두께는 연마율의 시간 적분이므로 전체 플랜트는 $G_p(s)=\dfrac{K}{s(\tau s+1)}$. 이 적분기 덕분에 P 제어만으로도 목표 두께에 정상상태오차 0으로 도달 가능
3. **PID 제어** — $u(t)=K_pe(t)+K_i\displaystyle\int e(t)\,dt+K_d\dfrac{de}{dt}$, 오차 $e(t)=$ 목표두께 $-$ 측정두께
4. **패드 마모 외란 모델** — 문헌에서 보고된 지수적 연마율 저하 경향을 반영: $K_{eff}(t)=K_0\,e^{-t/T_{wear}}$
5. **게인 스케줄링(Gain Scheduling)** — 오차 크기에 따라 제어기 게인을 전환하는 적응형 제어 기법: 오차가 크면 공격적(빠른) 게인, 오차가 작으면 보수적(느린, 오버슈트 방지) 게인

## 📚 참고문헌 &amp; 초급자용 학습 자료 (출처 명시)

**1차 지연 공정모델 / PID 제어 이론**
1. Enwerem, C., &amp; Okoro, I. (2022). *Optimal Controller Tuning Technique for a First-Order Process with Time Delay*. arXiv:2210.08187. https://arxiv.org/pdf/2210.08187 — 1차 지연(FOPTD) 공정모델과 PID 튜닝의 기본 개념을 다룬 논문.

**In-situ Metrology / CMP 폐회로 제어**
2. SURAGUS. *CMP Process Monitoring and Endpoint Detection*. https://suragus.com/thickness-measurement-before-etching-processes/ — 편심전류(eddy current) 기반 In-situ 센서가 실시간 두께 측정과 압력 존별 피드백 제어에 어떻게 쓰이는지 설명하는 무료 기술 자료.
3. US Patent US20110189925A1, *High Sensitivity Real Time Profile Control Eddy Current Monitoring System*. https://patents.google.com/patent/US20110189925A1/en — 실시간 두께 측정값으로 캐리어 헤드 압력을 조절하는 "Real Time Profile Control(RTPC)" 개념을 설명하는 공개 특허문헌.
4. Kim, H. et al. *In-situ CMP copper endpoint control system*. IEEE (2001). https://www.academia.edu/44444540/In_situ_CMP_copper_endpoint_control_system — 편심전류 센서와 광학 반사율 센서를 결합한 실제 In-situ CMP 제어 시스템 설계 사례.

**패드 마모(Pad Wear) 외란 모델링**
5. US Patent 6,169,931, *Method and system for modeling, predicting and optimizing chemical mechanical polishing pad wear and extending pad life*. https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/6169931 — 패드 컨디셔닝 없이 연마를 지속하면 재료제거율이 시간에 따라 지수적으로 감소한다는 사실을 명시한 공개 특허문헌.
6. JEES Semicon Blog. *CMP Process Step-by-Step: How Wafer Polishing Works*. https://jeez-semicon.com/blog/cmp-process-step-by-step-how-wafer-polishing-works/ — 패드 글레이징(glazing)이 재료제거율 저하(removal rate drift)의 주요 원인이라고 설명하는 초급자용 개론 자료.

**프로그래밍 참고 문서**
7. SciPy 공식 문서 — `scipy.signal.TransferFunction`: https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.TransferFunction.html
8. SciPy 공식 문서 — `scipy.signal.step`: https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.step.html
9. NumPy 공식 문서 — `numpy.random.normal`: https://numpy.org/doc/stable/reference/random/generated/numpy.random.normal.html

> 💡 **읽는 순서 추천**: 2번(SURAGUS 개론) → 6번(패드 마모 개론) → 1번(1차지연 PID 이론) → 3, 4, 5번(심화 특허/사례) → 7~9번(SciPy/NumPy 공식 문서) 순으로 읽는 것을 추천합니다.

## ▶️ 실행 방법

1. Google Colab에서 `notebooks/` 폴더의 `.ipynb` 파일들을 업로드하거나 GitHub 저장소를 연결해 엽니다.
2. 첫 코드 셀부터 순서대로 실행하며, `# TODO` 표시가 있는 빈칸 코드를 직접 채워 넣습니다.
3. Day1~2 → Day3~4 → Day5~7 순서로 진행하는 것을 권장하지만, 각 노트북은 필요한 클래스/함수를 자체적으로 다시 정의하고 있어 독립적으로도 실행 가능합니다.

## 🏆 포트폴리오 어필 포인트

- ✅ **공정 제어 시스템 설계** — 1차 지연 공정모델을 시간영역 시뮬레이션으로 구현하고, PID 제어기·플랜트를 객체지향(class) 구조로 설계하는 실무형 코딩 역량
- ✅ **In-situ 두께 제어** — 실시간 센서 피드백(노이즈 포함)을 반영한 폐회로 제어 시스템 설계 역량
- ✅ **PID 및 외란 보상 알고리즘** — 패드 마모와 같은 현실적 외란 속에서도 목표값에 정확히 도달하는 게인 스케줄링 기반 적응형 PID 설계·검증 역량

---

<div align="center">

*이 자료는 공정제어 교과서 수준의 학습용 예시값(K, tau, PID 게인 등)을 기반으로 제작된 시뮬레이션이며, 실제 CMP 장비의 사양이나 성능 데이터를 포함하지 않습니다.*

</div>
