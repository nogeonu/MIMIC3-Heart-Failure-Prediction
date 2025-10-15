# 🚀 GitHub 업로드 가이드

이 문서는 프로젝트를 GitHub에 업로드하는 방법을 설명합니다.

## 📋 사전 준비사항

1. **Git 설치 확인**
```bash
git --version
```
Git이 설치되어 있지 않다면 https://git-scm.com/downloads 에서 다운로드하세요.

2. **GitHub 계정**
- https://github.com 에서 계정 생성 (무료)

## 🔧 단계별 업로드 방법

### 1단계: GitHub 저장소 생성

1. GitHub 로그인
2. 우측 상단 `+` → `New repository` 클릭
3. 저장소 정보 입력:
   - **Repository name**: `MIMIC3-Heart-Failure-Prediction` (또는 원하는 이름)
   - **Description**: `심부전 환자 사망률 예측 머신러닝 프로젝트`
   - **Public** 또는 **Private** 선택
   - ⚠️ **README, .gitignore, license 추가하지 마세요** (이미 로컬에 있음)
4. `Create repository` 클릭

### 2단계: 로컬 Git 저장소 초기화

터미널(Mac) 또는 명령 프롬프트(Windows)를 열고 프로젝트 폴더로 이동:

```bash
cd "/Users/nogeon-u/Desktop/건양대_바이오메디컬 /numpy/numpy_project"
```

Git 저장소 초기화:
```bash
git init
```

### 3단계: 파일 추가 및 커밋

```bash
# 모든 파일 추가
git add .

# 첫 커밋 생성
git commit -m "Initial commit: MIMIC-III 심부전 사망률 예측 프로젝트"
```

### 4단계: GitHub 원격 저장소 연결

GitHub에서 생성한 저장소 URL을 복사한 후:

```bash
# 원격 저장소 연결 (YOUR-USERNAME을 실제 GitHub 계정명으로 변경)
git remote add origin https://github.com/YOUR-USERNAME/MIMIC3-Heart-Failure-Prediction.git

# 기본 브랜치 이름 설정
git branch -M main

# GitHub에 푸시
git push -u origin main
```

### 5단계: 확인

브라우저에서 GitHub 저장소로 이동하여 파일이 올라갔는지 확인합니다!

## 📂 업로드된 파일 목록

```
✅ README.md              - 프로젝트 설명서
✅ HF_KNN_최고성능.ipynb   - 메인 노트북
✅ requirements.txt       - 필요 패키지
✅ .gitignore            - Git 제외 파일
✅ LICENSE               - MIT 라이선스
✅ CONTRIBUTING.md       - 기여 가이드
✅ GITHUB_SETUP.md       - 이 파일
⚠️ data01.csv            - 데이터 파일 (용량에 따라 Git LFS 필요할 수 있음)
⚠️ 프로젝트PPT.pdf       - PPT 파일 (용량 확인 필요)
```

## 🔄 이후 업데이트 방법

코드를 수정한 후 GitHub에 업로드:

```bash
# 변경사항 확인
git status

# 변경된 파일 추가
git add .

# 커밋 메시지와 함께 저장
git commit -m "Update: 설명"

# GitHub에 푸시
git push
```

## ⚠️ 주의사항

### 대용량 파일 처리

만약 `data01.csv`나 `프로젝트PPT.pdf`가 100MB 이상이면 Git LFS 사용:

```bash
# Git LFS 설치 (Mac)
brew install git-lfs

# Git LFS 설치 (Windows)
# https://git-lfs.github.com/ 에서 다운로드

# Git LFS 초기화
git lfs install

# 대용량 파일 추적
git lfs track "*.csv"
git lfs track "*.pdf"

# .gitattributes 파일 추가
git add .gitattributes

# 커밋 및 푸시
git add data01.csv 프로젝트PPT.pdf
git commit -m "Add: 대용량 파일 (Git LFS)"
git push
```

### 민감한 데이터 제외

개인정보나 민감한 데이터가 포함된 경우:
1. `.gitignore`에 해당 파일 추가
2. README에 데이터 요청 방법 명시
3. 샘플 데이터만 업로드

## 🎨 저장소 꾸미기 (선택사항)

### 1. 뱃지 추가
README.md 상단에 이미 추가되어 있습니다!

### 2. GitHub Pages 활성화
Settings → Pages → Source에서 `main` 브랜치 선택

### 3. About 섹션 작성
저장소 메인 페이지 우측 상단 ⚙️ → About 편집

### 4. Topics 추가
저장소 메인 페이지에서 Topics 추가:
- `machine-learning`
- `healthcare`
- `heart-failure`
- `mimic-iii`
- `python`
- `jupyter-notebook`

## 🐛 문제 해결

### 오류: "Permission denied"
```bash
# SSH 키 설정 또는 HTTPS 사용
git remote set-url origin https://github.com/YOUR-USERNAME/REPO-NAME.git
```

### 오류: "Large files detected"
```bash
# Git LFS 사용 (위 "대용량 파일 처리" 참조)
```

### 오류: "Failed to push some refs"
```bash
# 원격 저장소 내용 먼저 가져오기
git pull origin main --allow-unrelated-histories
git push
```

## 📞 도움이 필요하신가요?

- GitHub 공식 문서: https://docs.github.com
- Git 튜토리얼: https://git-scm.com/book/ko/v2
- 질문: GitHub Issues에 등록

---

**축하합니다! 이제 프로젝트가 GitHub에 공개되었습니다! 🎉**

