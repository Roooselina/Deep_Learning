# 딥러닝 이해 (3학년 1학기)

PyTorch로 MLP, CNN, 전이학습을 실습한 과제와 기말 프로젝트 기록입니다.

| 폴더 | 내용 | 노트북에 기록된 결과 |
|---|---|---|
| `과제1/` | MNIST MLP 분류 (TensorBoard, torchsummary 사용) | 두 노트북의 Test Accuracy 97.83%, 96.35% |
| `과제2/` | `ImageFolder` 기반 CNN 학습, ResNet18·VGG16 전이학습 비교 (고양이/개, X-ray) | 고양이/개 최고 모델 VGG16(특징 추출부 고정) 정확도 0.9794 (출력에 평가 분할이 표기되지 않음) |
| `딥러닝 기말 프로젝트/` | 신선 식품과 부패 식품 이진 분류, Grad-CAM 시각화 | 아래 표 |

## 기말 프로젝트: 신선/부패 식품 분류

`Final_Project.ipynb`의 흐름입니다.

1. Food-101 데이터로 ResNet50을 먼저 학습(15 epoch, 셀 4~9)
2. 신선/부패 데이터의 `train` 폴더를 `random_split`으로 학습·검증으로 나누고, 별도 `test` 폴더로 평가
3. 학습 범위를 바꿔 비교하고, ROC·PR 곡선과 임계값별 정밀도·재현율을 계산
4. ResNet50 `layer4[-1]`, VGG16 `features[28]`에 Grad-CAM 적용

테스트 데이터 24,204장 기준(노트북 셀 21, 22, 27 출력):

| 설정 | Test Accuracy | 오탐(정상→부패) | 미탐(부패→정상) |
|---|---|---|---|
| ResNet50, `layer4` + FC 학습 | 0.9582 | 450 | 561 |
| ResNet50, FC만 학습 | 0.8793 | 1,356 | 1,566 |
| VGG16, 마지막 분류층만 학습 | 0.8864 | 666 | 2,084 |

- 데이터 출처와 이용 조건은 노트북에 적혀 있지 않습니다. 데이터는 저장소에 없습니다.
- 학습은 원격 Linux 서버(Conda, Python 3.10)에서 진행된 출력이 남아 있습니다.
- 결과는 이 테스트 폴더 한정이며, 반복 실행이나 다른 데이터에서의 검증은 하지 않았습니다.

## 모델 가중치

`best_model.pth`, `best_transfer_model2.pth`, `best_transfer_VGG_model3`는 용량이 커서 Google Drive에 올렸습니다.

https://drive.google.com/drive/folders/1vBbMgQS0EpqxYdTKLrOIqf96Xey-TlnE?usp=drive_link

`과제2/`의 `.pt` 파일은 저장소에 Git LFS 없이 포함되어 있습니다.

## 그 밖의 파일

`딥러닝 이해 기말과제.docx`(보고서), `딥러닝 이해 제안 발표.pptx`, `딥러닝 이해 최종 발표.pptx`
