# 📁 프로젝트 구조 및 파일 설명

## 디렉토리 구조

```
MIMIC3-Heart-Failure-Prediction/
│
├── 📄 README.md                      # 프로젝트 메인 설명서
├── 📓 HF_KNN_최고성능.ipynb          # 메인 분석 노트북 (8,878 lines)
├── 📊 data01.csv                     # MIMIC-III 데이터셋 (1,177 patients × 51 features)
├── 📑 프로젝트PPT.pdf                # 프로젝트 발표 자료
│
├── 📋 requirements.txt               # Python 패키지 의존성
├── 🚫 .gitignore                     # Git 추적 제외 파일
├── ⚖️ LICENSE                        # MIT 라이선스
├── 🤝 CONTRIBUTING.md                # 기여 가이드라인
├── 🚀 GITHUB_SETUP.md                # GitHub 업로드 가이드
└── 📁 PROJECT_STRUCTURE.md           # 이 파일
```

## 파일별 상세 설명

### 📓 HF_KNN_최고성능.ipynb

**메인 분석 노트북 - 총 10개 섹션**

#### 섹션 1-2: 환경 설정 및 데이터 로딩
- 라이브러리 임포트 (pandas, numpy, scikit-learn, xgboost, optuna 등)
- MIMIC-III 데이터셋 로딩 (1,177명)
- 기본 정보 확인 및 변수명 정리 (51개 변수)

#### 섹션 3-4: 탐색적 데이터 분석 (EDA)
- 결측치 분석 및 처리
- 데이터 분포 확인
- 클래스 불균형 확인 (생존 86.5% vs 사망 13.5%)
- 상관분석 및 시각화

#### 섹션 5: 특성 선택 (Feature Selection)
- **VIF 분석**: 다중공선성 제거 (19개 → 8개 변수)
- **Random Forest Importance**: 중요 변수 추출
- **RFE (Recursive Feature Elimination)**: 재귀적 특성 선택
- 최종 8개 변수 선택 (다수결 방식)

#### 섹션 6: 클래스 불균형 처리
- 하이브리드 샘플링 기법:
  - RandomUnderSampler: 다수 클래스 50% 감소
  - SMOTE: 소수 클래스 증강
- 결과: 1:1 완벽한 균형 (각 354명)
- StandardScaler로 데이터 정규화

#### 섹션 7: 모델 개발 및 비교
- **11개 머신러닝 모델** 학습 및 평가:
  1. Logistic Regression (최고 성능: AUC 0.8229)
  2. K-Nearest Neighbors
  3. Support Vector Machine
  4. Decision Tree
  5. Random Forest
  6. Gradient Boosting
  7. XGBoost
  8. Linear Discriminant Analysis
  9. Quadratic Discriminant Analysis
  10. Gaussian Naive Bayes
  11. Multi-layer Perceptron
- Soft Voting 앙상블 (상위 3개 모델)
- ROC 곡선 비교
- 민감도/특이도 시각화

#### 섹션 8: 하이퍼파라미터 최적화
- Optuna 활용 (200회 trial)
- 최고 모델(Logistic Regression) 튜닝
- 교차 검증 (5-Fold Stratified)
- 성능 지표 계산 및 비교

#### 섹션 9: LDA 모델 심층 분석
- Optuna로 LDA 하이퍼파라미터 최적화
- Logistic Regression vs LDA 성능 비교
- 변수 중요도 분석
- 계수 해석 (양의 계수: 위험 증가, 음의 계수: 위험 감소)

#### 섹션 10: 오분류 분석
- False Positive 케이스 분석 (78건)
- False Negative 케이스 분석 (12건) - 가장 위험!
- 개별 오분류 케이스 상세 분석
- 2단계 예측 시스템 구축 (7.28% 성능 향상)
- 변수별 기여도 분석

### 📊 data01.csv

**MIMIC-III 심부전 환자 데이터셋**

- **행**: 1,177명의 환자
- **열**: 51개의 변수
- **구조**: 
  - 식별 변수: `group` (train/test), `ID`
  - 목표 변수: `outcome` (0=생존, 1=사망)
  - 독립 변수: 인구통계학적(2개), 질환(10개), 바이탈사인(6개), 혈액검사(32개)

### 📑 프로젝트PPT.pdf

**프로젝트 발표 자료**

구성 (예상):
1. 연구 배경 및 목적
2. 데이터 소개
3. 연구 방법론
4. 모델 개발 과정
5. 결과 및 성능 평가
6. 오분류 분석
7. 결론 및 향후 계획

### 📋 requirements.txt

**필수 Python 패키지**

카테고리별 패키지:
- 데이터 분석: numpy, pandas, scipy
- 머신러닝: scikit-learn, xgboost, imbalanced-learn
- 최적화: optuna
- 통계: statsmodels
- 시각화: matplotlib, seaborn
- 개발환경: jupyter

### 🚫 .gitignore

**Git 추적 제외 파일**

제외 항목:
- Python 캐시 파일 (`__pycache__`, `*.pyc`)
- 가상환경 (`venv/`, `env/`)
- Jupyter 체크포인트 (`.ipynb_checkpoints/`)
- IDE 설정 (`.vscode/`, `.idea/`)
- OS 파일 (`.DS_Store`, `Thumbs.db`)
- 대용량 출력 파일 (`*.png`, `*.pdf` - 선택적)

### ⚖️ LICENSE

**MIT 라이선스**

- 상업적/비상업적 사용 가능
- 수정 및 배포 자유
- 원저작자 표시 필수
- 무보증

### 🤝 CONTRIBUTING.md

**기여 가이드라인**

포함 내용:
- 이슈 생성 방법
- Pull Request 절차
- 코드 스타일 (PEP 8)
- 커밋 메시지 규칙

### 🚀 GITHUB_SETUP.md

**GitHub 업로드 완벽 가이드**

단계별 설명:
1. GitHub 저장소 생성
2. Git 초기화
3. 파일 커밋
4. 원격 저장소 연결
5. 푸시
6. 문제 해결

## 코드 통계

### Jupyter Notebook 분석

- **총 라인 수**: 8,878 lines
- **섹션 수**: 10개 (+ 하위 섹션)
- **셀 개수**: 약 65개
- **주요 라이브러리**: 15+개
- **모델 개수**: 11개
- **시각화**: 20+개

### 주요 함수 및 클래스

```python
# 데이터 로딩
pd.read_csv()

# 특성 선택
variance_inflation_factor()  # VIF
RandomForestClassifier()     # Feature Importance  
RFE()                        # Recursive Feature Elimination

# 샘플링
RandomUnderSampler()
SMOTE()

# 모델링
11개 분류 모델

# 최적화
optuna.create_study()
optuna.optimize()

# 평가
accuracy_score(), roc_auc_score(), confusion_matrix()
```

## 실행 시간 예상

- **전체 노트북**: 약 15-20분 (CPU 기준)
- **섹션 5 (특성 선택)**: 2-3분
- **섹션 7 (11개 모델)**: 5-7분
- **섹션 8 (Optuna 200 trials)**: 3-5분
- **섹션 9 (LDA Optuna)**: 2-3분

## 메모리 사용량

- **데이터셋**: ~10MB
- **피크 메모리**: ~500MB-1GB
- **권장 RAM**: 8GB 이상

## 의존성 그래프

```
프로젝트
├── 데이터 (data01.csv)
│   └── 1,177 patients × 51 features
│
├── 전처리
│   ├── 결측치 처리
│   ├── 특성 선택 (8개 변수)
│   └── SMOTE (708명 균형)
│
├── 모델링
│   ├── 11개 기본 모델
│   ├── 앙상블
│   └── Optuna 최적화
│
└── 결과
    ├── 최고 모델: Logistic Regression (AUC 0.82)
    ├── 비교 모델: LDA (AUC 0.82)
    └── 오분류 분석 및 개선
```

## 업데이트 이력

- **v1.0** (2024-10): 초기 프로젝트 완성
  - 11개 모델 비교
  - LDA 심층 분석
  - 오분류 분석 및 개선

---

**📌 Note**: 이 구조는 프로젝트의 현재 상태를 반영합니다. 업데이트 시 이 문서도 함께 수정해주세요.

