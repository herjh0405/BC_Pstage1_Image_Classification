# 😷 Boostcamp AI Tech P-Stage 1 - Image Classification

2021.08.23 ~ 2021.09.03 [Wrap-up Report](https://bit.ly/38EbbIw) [개인 회고록](https://www.notion.so/0905f6ffe6b5404d8ed6d5562bf27c78)

## 📑 Summary
### Mask status Classification

>    COVID-19의 확산으로 우리나라는 물론 전 세계 사람들은 경제적, 생산적인 활동에 많은 제약을 가지게 되었습니다. 우리나라는 COVID-19 확산 방지를 위해 사회적 거리 두기를 단계적으로 시행하는 등의 많은 노력을 하고 있습니다. 과거 높은 사망률을 가진 사스(SARS)나 에볼라(Ebola)와는 달리 COVID-19의 치사율은 오히려 비교적 낮은 편에 속합니다. 그럼에도 불구하고, 이렇게 오랜 기간 동안 우리를 괴롭히고 있는 근본적인 이유는 바로 COVID-19의 강력한 전염력 때문입니다.  
>    감염자의 입, 호흡기로부터 나오는 비말, 침 등으로 인해 다른 사람에게 쉽게 전파가 될 수 있기 때문에 감염 확산 방지를 위해 무엇보다 중요한 것은 모든 사람이 마스크로 코와 입을 가려서 혹시 모를 감염자로부터의 전파 경로를 원천 차단하는 것입니다. 이를 위해 공공 장소에 있는 사람들은 반드시 마스크를 착용해야 할 필요가 있으며, 무엇 보다도 코와 입을 완전히 가릴 수 있도록 올바르게 착용하는 것이 중요합니다. 하지만 넓은 공공장소에서 모든 사람들의 올바른 마스크 착용 상태를 검사하기 위해서는 추가적인 인적자원이 필요할 것입니다.  
>    따라서, 우리는 카메라로 비춰진 사람 얼굴 이미지 만으로 이 사람이 마스크를 쓰고 있는지, 쓰지 않았는지, 정확히 쓴 것이 맞는지 자동으로 가려낼 수 있는 시스템이 필요합니다. 이 시스템이 공공장소 입구에 갖춰져 있다면 적은 인적자원으로도 충분히 검사가 가능할 것입니다.

### Labeling
* 마스크 착용 여부 : 착용 / 잘못된 착용(턱스크 or 코스크) / 미착용
* 성별 : 남 / 여
* 연령 : 30대 미만 / 30대 이상 ~ 60대 미만 / 60대 이상

총 18개의 label 분류  

<img src='https://user-images.githubusercontent.com/54921730/132083902-edabcce7-4ff7-4517-a1a5-f840fa86b57b.png' width=900 height=700/>

## 👨‍🔬Result
<img src='https://user-images.githubusercontent.com/54921730/132083921-9799aecc-9185-4779-943b-289e4c4f757e.png' alt='132083921-9799aecc-9185-4779-943b-289e4c4f757e' width=900/>  

* 주어진 데이터는 공개가 불가하여 내 사진과 팀원 사진, 저작권 공개된 사진을 이용해서 실험
* 학습 데이터와 비슷한 경우 역시나 잘 맞춤
  * 하지만 실제 결과와 비슷하게 마스크로 눈과 코를 가린 경우 맞추기 힘들어 함 
* 특이한 점은 학습 데이터에 전혀 없던 아주 어린 아이도 맞췄다는 사실과, 수염기른 데이터가 없다보니 마스크로 인식한 점이다.

* License - https://pixabay.com/, MyImage, 캠퍼 조현동

## 👋 Introduction Team

---

<img src="https://raw.githubusercontent.com/herjh0405/Img/master/img/KakaoTalk_20210902_105117185.png" alt="KakaoTalk_20210902_105117185"/>

|                            허정훈                            |                            임성민                            |                            조현동                            |                            황원상                            |                            오주영                            |                            이준혁                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| [![Avatar](https://avatars.githubusercontent.com/u/54921730?v=4)](https://github.com/herjh0405) | [![Avatar](https://avatars.githubusercontent.com/u/49228132?v=4)](https://github.com/mickeyshoes) | [![Avatar](https://avatars.githubusercontent.com/u/61579014?v=4)](https://github.com/JODONG2) | [![Avatar](https://avatars.githubusercontent.com/u/49892621?v=4)](https://github.com/WonsangHwang) | [![Avatar](https://avatars.githubusercontent.com/u/69762559?v=4)](https://github.com/Jy0923) | [![Avatar](https://avatars.githubusercontent.com/u/49234207?v=4)](https://github.com/kmouleejunhyuk) |
|        [주영교 신자](https://herjh0405.tistory.com/)         |   [오주영<br/>그는 신이야](https://velog.io/@mickeyshoes)    | [zi존부캠](https://shimmering-form-67a.notion.site/WEEK-e0a8cfccd85a43fca143a14641de8e30) |                         이팀의 멘토                          |                           정훈찡❤                            | [최고의<br/>모델러<br/>허정훈](https://dreaming-lee.notion.site/boostcamp-archive-44d6ea71b8bf4c0e9dc8d37e57ebbf5f) |
|              `데이터분석` `CV`<br>  `음성인식`               |                `CV` `모델 서빙` <br> `백엔드`                |                        `CV` `AutoML`                         |                             `CV`                             |                   `CV` `Generative Model`                    |                             `CV`                             |

## 😄Data Preprocessing
### Face Crop

* `cvlib` - By cvlib.detect_face, crop face+cloth coordinate(x, y, w, h)

## 👨🏾‍💻Model
### Backbone

* `ResNet18`(https://pytorch.org/hub/pytorch_vision_resnet/) - model fine-tuning

### Loss

* `Focal loss` (gamma = 2)

### Optimizer

* `Adam`

### Albumentation

* `Resize `
* `GaussianBlur`
* `Normalize`
* `HorizontalFlip`

### Wandb log
![image-20210902192217807](https://raw.githubusercontent.com/herjh0405/Img/master/img/image-20210902192217807.png)

## 💯Performance
### Public

* F1 Score : 0.763
* Accuracy : 79.206%

### Private

* F1 Score : 0.744
* Accuracy : 78.333%

## 💻Hardware

* Ubuntu 18.04.5 LTS
* Intel(R) Xeon(R) Gold 5120 CPU @ 2.20GHz 중 논리코어 8개
* Ram 90GB
* Tesla V100 32GB

## 🎮Getting Started

### File Structure

```text
pro_hun/
├── base
│  └── baseline.ipynb		# Introduction & EDA Baseline
├── data_preprocessing
│  ├── data_labeling.py		# Data labeling(18 classes&Error Fix)
│  ├── data_split.py		# Apply StratifiedKFold
│  └── image_crop.py		# Crop face by cvlib
├── experiment
│  └── model_test.ipynb		# check submission distribution
├── model
│  ├── loss.py			# Focal loss
│  ├── metric.py		# Acc, F1_score
│  └── model.py
├── requirements.txt
├── test.py
├── train.py
└── utils
  └── util.py			# For smooth processing
```

### Dependencies

* torch==1.7.1
* torchvision==0.8.2
* cvlib==0.2.6
* opencv-python==4.5.3.56
* albumentations==1.0.3
* matplotlib==3.2.1
* numpy==1.19.5
* Pillow==8.3.1
* pandas==1.1.5
* scikit-learn==0.24.2
* tqdm==4.62.2
* wandb==0.12.1

### Install Requirements
```
$ pip install -r requirements.txt
```
### Data Preprocessing

* labeling, crop, split, 

```
$ python data_preprocessing/data_labeling.py
$ python data_preprocessing/image_crop.py
$ python data_preprocessing/data_split.py
```

### Training

```
$ python train.py [-lr] [-bs] [--epoch] [--train_path] [--model_save] [--image_data] [--image_dir]
```

* `-lr` : learning rate, default=0.0001
* `-bs` : batch size, default=128
* `--epoch` : Epoch size, default=10
* `--train_path` : train_directory_path
* `--model_save` : model_save_path
* `--image_data` : CSV according to image type(Original, Crop, All), default='train_with_all.csv'
* `--image_dir` : Directory according to image type, default='ori_image_all'

### Evaluation
```
$ python test.py [--test_path] [--result_save] [--image_dir]
```

* `--test_path` : test_directory_path
* `--result_save` : submission_save_path
* `--image_dir` : Directory according to image type, default='crop_image'

## Acknowledgements
본 프로젝트는 Victor Huang 의 PyTorch Template Project 을 기반으로 하여 개발되었습니다.

## License
This project is licensed under the MIT License. See LICENSE for more details.



















