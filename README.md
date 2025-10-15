# 🏥 MIMIC-III 심부전 환자 사망률 예측 프로젝트

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

중환자실(ICU) 입원 심부전 환자의 병원 내 사망률을 예측하는 머신러닝 프로젝트입니다.

## 📋 프로젝트 개요

본 연구는 **MIMIC-III 임상 데이터베이스**를 활용하여 심부전 환자의 사망 위험을 조기에 예측하고, 의료진의 임상 의사결정을 지원하는 예측 모델을 개발하는 것을 목표로 합니다.

### 🎯 주요 목표

- 11개 다양한 머신러닝 알고리즘 비교 분석
- 최적의 예측 변수 선택 (VIF, Feature Importance, RFE)
- 클래스 불균형 해결 (SMOTE + Undersampling)
- 임상에서 활용 가능한 높은 민감도의 모델 개발
- 오분류 케이스 심층 분석 및 개선

## 📊 데이터셋 정보

- **데이터 소스**: MIMIC-III Database (2001-2012)
- **총 환자 수**: 1,177명
- **변수**: 51개 (인구통계학적, 임상검사, 바이탈사인 등)
- **클래스 분포**: 
  - 생존 (0): 1,017명 (86.5%)
  - 사망 (1): 159명 (13.5%)
- **데이터 분할**: 훈련셋 70% (825명) / 테스트셋 30% (352명)

## 🔬 연구 방법론

### 1. 데이터 전처리
- ✅ 결측치 처리 (25% 이상 결측 변수 제거)
- ✅ 이상치 탐지 및 처리
- ✅ 표준화 (StandardScaler)

### 2. 변수 선택 (Feature Selection)
3가지 방법을 종합하여 **최종 8개 변수** 선택:
- **VIF (Variance Inflation Factor)**: 다중공선성 제거
- **Random Forest Feature Importance**: 변수 중요도 분석
- **RFE (Recursive Feature Elimination)**: 재귀적 특성 제거

#### 최종 선택 변수
1. `Leucocyte` (백혈구)
2. `Lactic acid` (젖산)
3. `Urea nitrogen` (요소질소)
4. `Urine output` (소변량)
5. `Lymphocyte` (림프구)
6. `NT-proBNP` (심부전 바이오마커)
7. `Renal failure` (신부전 여부)
8. `atrialfibrillation` (심방세동 여부)

### 3. 클래스 불균형 처리
**하이브리드 샘플링 기법** 적용:
- **1단계**: RandomUnderSampler (다수 클래스 50% 감소)
- **2단계**: SMOTE (소수 클래스 증강)
- **결과**: 완벽한 1:1 클래스 균형 달성 (각 354명)

### 4. 모델 개발
**11개 머신러닝 알고리즘** 비교:

| 카테고리 | 모델 |
|---------|------|
| **전통적 ML** | Logistic Regression, KNN, SVM, Decision Tree, Random Forest, Gradient Boosting, XGBoost |
| **통계적 판별** | LDA, QDA |
| **확률 기반** | Gaussian Naive Bayes |
| **신경망** | Multi-layer Perceptron |

### 5. 모델 최적화
- **하이퍼파라미터 튜닝**: Optuna (200회 trial)
- **앙상블**: Soft Voting (상위 3개 모델)
- **교차 검증**: 5-Fold Stratified CV

## 📈 주요 결과

### 최고 성능 모델: Logistic Regression

| 지표 | 성능 | 설명 |
|------|------|------|
| **ROC-AUC** | 0.8229 | 우수한 분류 성능 |
| **정확도** | 73.22% | 전체 예측 정확도 |
| **민감도 (Recall)** | 72.09% | 실제 사망 환자 탐지율 |
| **특이도** | 73.38% | 실제 생존 환자 탐지율 |
| **정밀도** | 27.43% | 사망 예측의 정확도 |
| **F1-Score** | 0.3974 | 정밀도-재현율 균형 |

### LDA 모델 (비교 모델)

| 지표 | 성능 |
|------|------|
| **ROC-AUC** | 0.8211 |
| **정확도** | 73.50% |
| **민감도** | 72.09% |
| **특이도** | 73.38% |

### 변수 중요도 (Top 5)

1. **Lactic acid** (젖산): 0.5847 - 위험 증가
2. **Urea nitrogen** (요소질소): 0.5839 - 위험 증가
3. **Renal failure** (신부전): 0.5242 - 위험 감소
4. **Leucocyte** (백혈구): 0.3753 - 위험 증가
5. **Atrialfibrillation** (심방세동): 0.3343 - 위험 증가

## 🔍 오분류 분석

### False Positive (FP): 78건
- 생존 환자를 사망으로 잘못 예측
- 비율: 22.22%
- 평균 예측 확률: 0.6537

### False Negative (FN): 12건 ⚠️
- 사망 환자를 생존으로 잘못 예측 (가장 위험!)
- 비율: 3.42%
- 평균 예측 확률: 0.3758

### 오분류 개선 전략
- 2단계 예측 시스템 구축
- 불확실한 케이스(확률 0.3-0.7) 재검토
- 성능 개선: 7.28% 향상

## 📁 프로젝트 구조

```
MIMIC3-Heart-Failure-Prediction/
├── 📄 README.md                       # 프로젝트 설명서 (이 파일)
├── 📋 requirements.txt                # 필요 패키지 목록
├── ⚖️ LICENSE                         # MIT 라이선스
├── 🚫 .gitignore                      # Git 제외 파일
│
├── 📁 src/                            # 소스 코드
│   └── 📓 HF_KNN_최고성능.ipynb       # 메인 분석 노트북
│
├── 📁 data/                           # 데이터 파일
│   └── 📊 data01.csv                  # MIMIC-III 데이터셋
│
├── 📁 docs/                           # 문서
│   ├── 📑 프로젝트PPT.pdf             # 프로젝트 발표 자료
│   ├── 🤝 CONTRIBUTING.md             # 기여 가이드
│   ├── 🚀 GITHUB_SETUP.md             # GitHub 업로드 가이드
│   ├── 📁 PROJECT_STRUCTURE.md        # 프로젝트 구조 설명
│   └── ⚡ QUICKSTART.md               # 빠른 시작 가이드
│
└── 📁 assets/                         # 이미지 및 결과물 (향후 추가)
    ├── roc_curve.png
    ├── confusion_matrix.png
    └── feature_importance.png
```

## 🚀 설치 및 실행 방법

### 1. 환경 설정

```bash
# 저장소 클론
git clone https://github.com/nogeonu/MIMIC3-Heart-Failure-Prediction.git
cd MIMIC3-Heart-Failure-Prediction

# 가상환경 생성 (선택사항)
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 필요 패키지 설치
pip install -r requirements.txt
```

### 2. Jupyter Notebook 실행

```bash
jupyter notebook src/HF_KNN_최고성능.ipynb
```

### 3. 실행 순서

1. **섹션 1-2**: 라이브러리 임포트 및 데이터 로딩
2. **섹션 3-4**: 탐색적 데이터 분석 (EDA)
3. **섹션 5**: 변수 선택 (VIF, Feature Importance, RFE)
4. **섹션 6**: 클래스 불균형 처리 (SMOTE)
5. **섹션 7**: 11개 모델 학습 및 비교
6. **섹션 8**: 최적 모델 하이퍼파라미터 튜닝
7. **섹션 9**: LDA 모델 분석 및 비교
8. **섹션 10**: 오분류 분석 및 개선

## 📊 주요 시각화

### ROC Curve 비교
11개 모델의 ROC 곡선을 한눈에 비교하여 최적 모델을 선택합니다.

### Confusion Matrix
- True Negative: 230건
- False Positive: 78건
- False Negative: 12건
- True Positive: 31건

### Feature Importance
각 변수가 사망률 예측에 미치는 영향을 시각화합니다.

## 💡 주요 발견사항

### 1. 임상적 의의
- **ROC-AUC 0.82+**: 임상에서 활용 가능한 우수한 성능
- **민감도 72%**: 실제 고위험 환자의 72%를 정확히 탐지
- **특이도 73%**: 저위험 환자를 과다 치료하지 않음

### 2. 주요 위험 인자
- **젖산 수치 증가**: 조직 저산소증 지표
- **요소질소 증가**: 신기능 저하
- **백혈구 증가**: 감염 또는 염증 반응
- **심방세동**: 심장 리듬 이상

### 3. 보호 요인
- **신부전 진단**: 역설적으로 더 집중적인 관리로 인한 효과
- **소변량 증가**: 신기능 정상 지표
- **림프구 수치**: 면역 기능 지표

## 🔧 기술 스택

- **언어**: Python 3.9+
- **데이터 분석**: pandas, numpy, scipy
- **시각화**: matplotlib, seaborn
- **머신러닝**: scikit-learn, xgboost, imbalanced-learn
- **최적화**: optuna
- **통계**: statsmodels
- **개발 환경**: Jupyter Notebook

## 📚 참고문헌

1. Johnson, A.E.W., et al. (2016). MIMIC-III, a freely accessible critical care database. *Scientific Data*, 3, 160035.
2. Chawla, N.V., et al. (2002). SMOTE: Synthetic Minority Over-sampling Technique. *JAIR*, 16, 321-357.
3. Guyon, I., et al. (2002). Gene Selection for Cancer Classification using Support Vector Machines. *Machine Learning*, 46, 389-422.

## 👥 기여자

- **프로젝트 책임자**: [Your Name]
- **소속**: 건양대학교 바이오메디컬학과
- **기간**: 2024

## 📄 라이선스

이 프로젝트는 MIT 라이선스를 따릅니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 📞 문의

프로젝트에 대한 질문이나 제안사항이 있으시면 다음으로 연락주세요:
- **Email**: your.email@example.com
- **GitHub Issues**: [프로젝트 Issues 페이지](https://github.com/your-username/MIMIC3-Heart-Failure-Prediction/issues)

## 🙏 감사의 말

이 연구는 MIMIC-III 데이터베이스를 제공해주신 MIT Laboratory for Computational Physiology와 PhysioNet에 감사드립니다.

---

**⭐ 이 프로젝트가 도움이 되셨다면 Star를 눌러주세요!**

