---
title: MachineLearning DAY1
author: JinYeong
layout: post
tags: [MachineLearning, 머신러닝]
comments: true
---

## 1. 파일로드
- `pd.read_csv()` : text 파일, csv 파일을 불러오기 -> 데이터프레임 저장
- `sep` : 구분자
- `head` : 제목
- `names` : 이름부여
- `encoding` : 인코딩 방식 지정

## 2. 파일 저장
- `df.to_csv()` : 데이터프레임 -> csv 파일 저장
- `sep` : 구분자

## 3. 데이터프레임 생성, 각 속성 조회
- `DataFrame(데이터, index, column, dtype=float32)`
- `df.T` : 전치행렬
- `df.axes` : 행과 열의 이름을 추출
- `df.dtypes` : 데이터 타입 추출(column 단위)
- `df.shape` : 행과 열의 수(차원)
- `size` : 원소 개수
- `values` : numpy 형태 배열로 출력

## 4. 데이터 프레임의 행, 열 데이터 추출
- `df.index` : 행 인덱스 추출
- `df.ix[2]` : 2번째 데이터 추출
- `df.loc, df.iloc` : 데이터 추출
- `df.head(), df.tail()` : 상/하위 데이터 추출

- `df. columns` : 열 인덱스 추출
- `df['열이름']` : 열 추출, [[참조열이 2개 이상]]

## 5. 인덱스 설정
- `reindex` : index 재설정
- `data_range` : 시계열 데이터 함수

## 6. 데이터프레임 합치기
- `pd.concat` 함수
- 위아래 합치기 : axis=0
- 좌우 합치기 : axis=1
- 합집합 : `join=outer`
  ex) pd.concat([df1,df2], join='outer')
- 교집합 : `join=inner`
- ignore_index = True : 기존 index 무시하고 새롭게 0부터 index가 지정

- `pd.merge()`
- how = 'left', inner, outer
- on = 'key'

## 7. 결측치 처리
- NaN(None)
- 결측치 유무 : `isnull(), notnull()`
- `df.isnull().sum()` => 각 컬럼별 NaN의 개수
- `df['A'].isnull().sum()` => 'A' 컬럼 NaN의 개수
- `sum()` : 컬럼 단위 합, sum(1) or sum(axis=1) : 행 단위 합
  ex) df.isnull().sum(1) => 행별 결측값 개수
      df.isnull().sum()  => 열별 결측값 개수
      
## 8. 결측값 대체
- `df.fillna()` : 결측값을 특정값으로 대체
  ex) df.fillna('missing') : na를 missing으로 대체
- 결측값이 있는 행 제거 : dropna(axis=0)
- 결측값이 있는 행 제거 : dropna(axis=1)

- `df.replace(np.nan, 10)` : na를 10으로 대체

## 9. 중복값 확인
- `df.duplicated(['기준열'])` : 중복인 경우 => True

- `unique()` : 유일값 찾기, 각 열을 구성하는 컬럼에 대한 유일한 값들만 추출
  ex) A,A,B,B,C => A,B,C
- `value_counts()` : 유일한 값별로 개수 세기
  ex) A,A,B,B,C => A가 2개, B가 2개, C가 1개
  
## 10. 정규화와 표준화
- 정규화 = (각 값-최소값) / (최대값-최소값) => 0~1사이의 수
- 표준화 = (각 값-평균) / 표준편차, 모집단이 정규분포를 따르는 경우, 평균이 0, 표준편차가 1인 표준정규분포로 만드는 작업
* 표준화 작업 3가지 코드
- 넘파이 : (x-mean())/std()
- 싸이파이 : zscore()
- 싸이킷런 : StandScaler().fit_transform()

## 11. 이상치 & 특이값 처리
- 1) 제거 -> 표준화 => 분석, 모델링
- 2) 평균값 등으로 대체 -> 표준화 => 분석, 모델링

- 이상치가 포함된 데이터의 표준화 => RobustScaler()함수
(x-median)/IQR

## 12. 이항변수화
- `Binarizer()` : 연속형 변수값에 대해 기준(threshold)이하 => 0, 초과 => 1
                동전을 던짐(시행), 성공(앞면,1) 또는 실패(뒷면,0) => 베르누이 시행
                성공확률이 p인 베르누이 시행을 n번 수행
                성공하는 횟수를 X라 하면, 확률 변수 X는 모수 n과 p인 이항분포를 따른다고 함
                
## 13. 데이터 재구조화
- 1) `pivot, pivot_table`
     pivot(인덱스, 컬럼, 값)
     pivot_table(데이터, 인덱스, 컬럼, 값)
- 2) `stack, unstack`
     stack : 위/아래로 데이터를 쌓는 것
     unstack : 옆으로 늘어놓는 것
     
## 14. 데이터 정렬
- 1) 데이터프레임 정렬 : `df.sort_values(by, axis, ascending, inplace)`
- 2) 튜플, 리스트 정렬 : `sorted, sort(reverse)`

## 15. 데이터 삭제
- `df.drop(['c1', 'c2', ...])`
- `del df['c1']`

## 16. 넘파이
- 넘파이 배열 : `np.array()`
- 크기 : `shape`
- 타입 : `dtype`

---
