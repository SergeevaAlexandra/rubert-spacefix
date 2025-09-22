# RuBERT Space Restoration

Fine-tuning [DeepPavlov/rubert-base-cased](https://huggingface.co/DeepPavlov/rubert-base-cased) 
for **restoring spaces in Russian text** (sequence labeling at the character level).

## 📌 Задача
Восстановление пропусков между словами в тексте без пробелов.  
Формулировка: бинарная классификация для каждого символа (0 = нет пробела после символа, 1 = пробел после символа).

## 🛠️ Стек
- HuggingFace Transformers
- PyTorch
- Datasets
- RuBERT 

## 🔧 Подготовка данных
1. Подготовить `train_dataset.csv` со следующими колонками:
   - `text_no_space` — строка без пробелов  
   - `labels` — список меток (0/1) для каждого символа  

Пример строки:
```csv
text_no_space,labels
приветкакдела,"[0,1,0,0,1,0,0,1,0,0,1,0]"
```

Для подготовки тренировочного набора использовался датасет парафраз [merionum/ru_paraphraser](https://huggingface.co/datasets/merionum/ru_paraphraser)

## 🚀 Запуск обучения

## ⚖️ Балансировка классов

- Используется CrossEntropyLoss с весами классов.
- Автоматически вычисляется на основе распределения 0/1.

## 📊 Метрика

Качество оценивается по F1-score для позиций пропущенных пробелов.

Для каждой строки мы сравниваем множество позиций, где вы поставили пробелы, с истинным множеством.

Формула:

$F_1 = \frac{2 \cdot (precision \cdot recall)}{precision + recall}$

## 💡 Идеи для улучшения

- Донастройка весов классов или focal loss
- Downsampling отрицательных примеров 
- Использование character-level моделей без WordPiece

## 📂 Структура репозитория

Автоматически вычисляется на основе распределения 0/1.

Поддерживается multi-GPU (Kaggle / Colab).
