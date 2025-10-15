# ⚡ 빠른 시작 가이드

5분 안에 프로젝트를 실행해보세요!

## 1️⃣ 환경 설정 (3분)

### 터미널 열기
- **Mac**: `Cmd + Space` → "터미널" 입력
- **Windows**: `Win + R` → "cmd" 입력

### 프로젝트 폴더로 이동
```bash
cd "/Users/nogeon-u/Desktop/건양대_바이오메디컬 /numpy/numpy_project"
```

### 필요 패키지 설치
```bash
pip install -r requirements.txt
```

## 2️⃣ Jupyter Notebook 실행 (1분)

```bash
jupyter notebook
```

브라우저가 자동으로 열리면 `HF_KNN_최고성능.ipynb` 클릭!

## 3️⃣ 코드 실행 (1분)

Jupyter Notebook에서:
1. 상단 메뉴: `Cell` → `Run All` 클릭
2. 또는 각 셀을 순차적으로 실행: `Shift + Enter`

## 🎯 주요 결과 확인

### 섹션 7: 11개 모델 성능 비교
- 최고 모델: **Logistic Regression (AUC: 0.8229)**
- ROC 곡선 비교
- 민감도/특이도 시각화

### 섹션 9: LDA 모델 분석
- Logistic Regression vs LDA 비교
- 변수 중요도 그래프

### 섹션 10: 오분류 분석
- False Positive: 78건
- False Negative: 12건
- 개선 방안 제시

## 📊 결과 요약

| 모델 | ROC-AUC | 정확도 | 민감도 |
|------|---------|--------|--------|
| Logistic Regression | 0.8229 | 73.22% | 72.09% |
| LDA | 0.8211 | 73.50% | 72.09% |
| Random Forest | 0.7779 | 81.77% | 46.51% |

**최종 선택 변수 (8개)**:
1. Leucocyte (백혈구)
2. Lactic acid (젖산)
3. Urea nitrogen (요소질소)
4. Urine output (소변량)
5. Lymphocyte (림프구)
6. NT-proBNP (심부전 마커)
7. Renal failure (신부전)
8. Atrialfibrillation (심방세동)

## ⚠️ 문제 해결

### "ModuleNotFoundError"
```bash
pip install 패키지명
```

### "Kernel died"
- Jupyter 재시작: `Kernel` → `Restart Kernel`

### 메모리 부족
- 일부 셀만 실행하거나
- 가상환경에서 실행

## 📞 도움말

더 자세한 내용은 다음 문서를 참조하세요:
- **전체 설명**: `README.md`
- **파일 구조**: `PROJECT_STRUCTURE.md`
- **GitHub 업로드**: `GITHUB_SETUP.md`

---

**Happy Coding! 🚀**

