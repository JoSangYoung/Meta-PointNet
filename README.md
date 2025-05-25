📄 [프로젝트 발표자료 보기](Meta-PoinNet.pdf)
📄 [View Project Presentation](Meta-PoinNet.pdf)


# 🔵 Meta-PointNet: 메타러닝 기반 샘플링을 활용한 효율적인 3D 포인트 클라우드 분류

> 📌 적은 수의 포인트만으로도 높은 성능  
> 🧠 PointNet + MAML (Model-Agnostic Meta-Learning) 구조  
> 🧪 ModelNet40 벤치마크에서 검증된 성능

---

## 📌 프로젝트 개요

**Meta-PointNet**은 3D 포인트 클라우드 분류에서 효율적인 샘플링을 위한 메타러닝 기반 프레임워크입니다.  
제안된 모델은 **적은 수의 포인트 또는 무작위 순서의 포인트로도 높은 정확도를 달성**하며, 기존의 고정 샘플링 기법(SampleNet 등)을 능가하는 성능을 보여줍니다.

---

## 🎯 연구 배경 및 목표

- 포인트 클라우드는 LiDAR, RGB-D 센서 등으로부터 얻어지는 3차원 점들의 집합으로, **순서가 없고 불규칙한 구조**를 가짐
- 전통적 샘플링(Farthest Point Sampling 등)은 정적인 기준에 의존 → 유연성 부족
- 본 연구는 **메타러닝(MAML)을 통해 학습 가능한 샘플링 전략**을 도입하여:
  - 적은 포인트로도 분류 성능 유지 또는 향상
  - 포인트 순서 무작위성에 강건한 구조 설계

---

## 🛠️ 핵심 구성요소

| 구성 요소       | 설명                                |
|----------------|-------------------------------------|
| **백본 모델**    | PointNet (순열 불변 구조)             |
| **샘플링 전략**  | 학습 가능한 포인트 선택 메커니즘       |
| **메타러닝 기법**| MAML (Model-Agnostic Meta-Learning) |
| **데이터셋**     | ModelNet40 (3D 객체 분류 벤치마크)     |

---

## 📦 사용 데이터

- **ModelNet40**: 40개 클래스의 3D CAD 모델
- PointNet 및 SampleNet과 동일한 실험 프로토콜
  - Batch size: 32
  - Learning rate: 0.01
  - Optimizer: Adam
  - Decay rate: 0.7

---

## ⚙️ 학습 구조

- **Inner Loop**: 임시 가중치로 task-specific 업데이트 수행
- **Outer Loop**: Inner loop 결과를 기반으로 초기 파라미터 갱신
- 지원 시나리오:
  - 적은 포인트 수 (few-shot classification)
  - 포인트 순서 섞인 데이터 (permutation invariance)

---

## 📊 실험 결과 요약

### ① 포인트 수가 적은 경우

| 포인트 수 | SampleNet | Meta-PointNet |
|-----------|-----------|----------------|
| 1024      | 86.5%     | 86.5%          |
| 512       | 86.8%     | **87.0%** ✅    |
| 256       | 84.1%     | **86.1%** ✅    |
| 128       | 83.9%     | **85.4%** ✅    |

### ② 포인트 순서 섞인 경우

| 포인트 수 / Epoch | SampleNet | Meta-PointNet |
|-------------------|-----------|----------------|
| 1024 / 250        | 81.3%     | **85.6%** ✅    |
| 1024 / 500        | 81.7%     | **85.6%** ✅    |

---

## 🧠 주요 인사이트

- 단순히 포인트 개수를 줄인 것보다, **"어떤 포인트를 선택하느냐"**가 더 중요함
- 메타러닝을 통해 다양한 task에 적응 가능한 샘플링 전략을 학습
- 데이터 순서가 무작위인 상황에서도 일관된 성능을 보장함

---

## 🔍 향후 연구 방향

- PointNet++ 또는 DGCNN과 같은 계층적 구조와 결합
- 분할(segmentation), 객체 감지(detection)로 확장
- 다양한 메타러닝 알고리즘(Reptile, Meta-SGD 등)과 비교

---

## 👤 연구자 정보

**조상영 SangYeong Jo**  
2022 UNIST AI 대학원  
딥러닝 기반 3D 비전 최종 프로젝트

---

## 📎 키워드

`Point Cloud` · `메타러닝` · `Few-Shot 학습` · `3D 객체 분류` · `PointNet` · `MAML` · `샘플링 최적화` · `ModelNet40`



---
# 🔵 Meta-PointNet: Meta-Learning-Based Sampling for Efficient 3D Point Cloud Classification

> 📌 Few-shot meta-learning + point cloud sampling = higher performance with fewer points  
> 🧠 Implemented with PointNet backbone + MAML framework  
> 🧪 Validated on ModelNet40 benchmark

---

## 🧭 Overview

**Meta-PointNet** is a meta-learning-based framework that improves 3D point cloud classification performance by learning to sample more informative subsets of points.  
The model demonstrates **higher classification accuracy using fewer or shuffled point sets**, outperforming baseline methods like SampleNet in low-data regimes.

---

## 🎯 Motivation

Point clouds are unordered sets of 3D points obtained from RGB-D or LiDAR sensors.  
Due to their irregular structure, they require efficient sampling to reduce computational cost without sacrificing accuracy.

Traditional sampling methods (e.g., Farthest Point Sampling) offer fixed heuristics. In contrast, **Meta-PointNet introduces a task-adaptive sampling mechanism via meta-learning**:

- Learn to sample the most informative points using MAML
- Perform well even under data scarcity or permutation noise

---

## 🛠️ Key Components

| Component       | Description                                      |
|----------------|--------------------------------------------------|
| **Backbone**    | PointNet (permutation-invariant architecture)    |
| **Sampler**     | Learnable point selection mechanism              |
| **Meta-Learning** | Model-Agnostic Meta-Learning (MAML)             |
| **Benchmark**   | ModelNet40 (standard for 3D object classification) |

---

## 📦 Dataset

- **ModelNet40**
- Consists of 40 categories of 3D CAD models
- Standard preprocessing and splitting used
- Protocol aligns with PointNet and SampleNet:
  - Batch size: 32
  - Learning rate: 0.01
  - Optimizer: Adam
  - Decay rate: 0.7

---

## ⚙️ Training Protocol

Meta-learning via MAML:
- **Inner Loop**: Fast adaptation on task-specific sampled support sets
- **Outer Loop**: Update the shared initialization based on inner loop performance

Supports:
- Few-shot point cloud classification
- Robustness to permutation of point order

---

## 📊 Experimental Results

### Performance with Fewer Points

| # Points | SampleNet | Meta-PointNet |
|----------|-----------|----------------|
| 1024     | 86.5%     | 86.5%          |
| 512      | 86.8%     | **87.0%** ✅    |
| 256      | 84.1%     | **86.1%** ✅    |
| 128      | 83.9%     | **85.4%** ✅    |

### Performance with Shuffled Points

| # Points / Epochs | SampleNet | Meta-PointNet |
|-------------------|-----------|----------------|
| 1024 / 250        | 81.3%     | **85.6%** ✅    |
| 1024 / 500        | 81.7%     | **85.6%** ✅    |

---

## 🧠 Insights

- Meta-PointNet achieves better performance with **less than half the points**
- Learns robust and generalizable sampling strategies via meta-learning
- Demonstrates that **sampling itself can be meta-learned**, not just classification

---

## 🔍 Future Work

- Integrate Meta-PointNet with hierarchical backbones (e.g., PointNet++, DGCNN)
- Apply to segmentation or object detection tasks
- Explore alternative meta-learning algorithms (e.g., Reptile, Meta-SGD)

---

## 🙋 Author

**SangYeong Jo**  
Deep Learning for 3D Vision – Final Project (2022.06)  
UNIST AI Graduate School

---

## 📎 Keywords

`Point Cloud` · `Meta-Learning` · `Few-Shot Learning` · `3D Classification` · `Sampling` · `PointNet` · `MAML` · `ModelNet40`

