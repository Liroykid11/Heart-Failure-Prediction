# ❤️ Heart Failure Prediction

**Прогнозирование сердечных заболеваний** по клиническим данным пациентов.

Цель проекта — построить модель машинного обучения, которая по результатам стандартного медицинского обследования может предсказать риск сердечного заболевания.

---

## 📊 Результаты (Performance)

🏆 **Лучшая модель: AdaBoost**

| Модель | F1-score | Accuracy | Recall | Precision |
| :--- | :---: | :---: | :---: | :---: |
| **AdaBoost** | **0.9091** | **0.8955** | 0.8824 | 0.8859 |
| CatBoost (tuned) | 0.9000 | 0.8911 | 0.8824 | 0.8804 |
| Logistic Regression | 0.8922 | 0.8922 | **0.8922** | 0.8804 |
| XGBoost (tuned) | 0.8900 | 0.8812 | 0.8725 | 0.8696 |
| Random Forest (tuned) | 0.8824 | 0.8824 | 0.8824 | 0.8696 |
| SVM (tuned) | 0.8750 | 0.8835 | 0.8922 | 0.8696 |
| Decision Tree | 0.8211 | 0.7919 | 0.7647 | 0.7772 |

> **Вывод:** Модель AdaBoost достигла F1-меры **0.9091**, что означает высокий баланс между точностью (Precision) и полнотой (Recall). Это особенно важно в медицинских задачах, где критично не пропустить больного пациента.

---

## 🛠️ Используемые технологии

| Инструмент | Назначение |
| :--- | :--- |
| **Python 3.14** | Основной язык |
| **pandas, numpy** | Обработка и анализ данных |
| **matplotlib, seaborn** | Визуализация (корреляции, распределения, boxplot'ы) |
| **scikit-learn** | Модели (LogisticRegression, SVM, RandomForest, AdaBoost, Decision Tree) |
| **XGBoost, CatBoost** | Градиентный бустинг |
| **Jupyter Notebook** | Интерактивная среда для EDA и экспериментов |
| **Git & GitHub** | Контроль версий и портфолио |

---

## 🔍 Ключевые выводы из EDA (Exploratory Data Analysis)

- В датасете 918 записей, пропуски **отсутствуют**.
- Наиболее сильные корреляции с целевой переменной (`HeartDisease`) показали:
  - `Oldpeak` (ST-депрессия) — корреляция **+0.40**
  - `MaxHR` (максимальное пульс) — корреляция **-0.40**
  - `ChestPainType_ASY` (асимптомная боль) — **79%** вероятности болезни
  - `ST_Slope_Flat` — **83%** вероятности болезни
  - `ExerciseAngina_Y` — **85%** вероятности болезни
- Обнаружены выбросы (отрицательные `Oldpeak`, нулевой `Cholesterol`), которые были обработаны на этапе Feature Engineering.

---

## ⚙️ Этапы работы

### 1. EDA (01_eda.ipynb)
- Загрузка и первичный осмотр данных
- Анализ пропусков, типов данных
- Корреляционный анализ (числовые признаки)
- Boxplot'ы для топ-признаков в разрезе целевой переменной
- Анализ категориальных признаков (`value_counts`, `crosstab`, stacked bar charts)

### 2. Feature Engineering (02_feature_engineering.ipynb)
- Удаление отрицательных `Oldpeak` (ошибки данных)
- Замена нулевого `Cholesterol` на медиану
- Создание новых признаков:
  - `age_oldpeak` (Age * Oldpeak)
  - `maxhr_age_ratio` (MaxHR / Age)
- One-Hot Encoding категориальных признаков
- Сохранение очищенного датасета (`heart_ready.csv`)

### 3. Обучение моделей (03_model_training.ipynb)
- Разделение на train/test (80/20) со стратификацией
- Кросс-валидация (5-fold) для оценки стабильности
- GridSearch для Random Forest, XGBoost, CatBoost, SVM
- Сравнение 7 моделей: Logistic Regression, SVM, Decision Tree, Random Forest, AdaBoost, XGBoost, CatBoost
- Сохранение лучшей модели (`models/best_model.pkl`)

---

## 🚀 Как запустить проект

1. **Клонировать репозиторий**
   ```bash
   git clone https://github.com/Liroykid11/Heart-Failure-Prediction.git
   cd Heart-Failure-Prediction