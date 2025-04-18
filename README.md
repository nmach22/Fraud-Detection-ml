# Fraud-Detection-ml

## [IEEE-CIS Fraud Detection](https://www.kaggle.com/c/ieee-fraud-detection/overview)
- მიმოხილვა
- პრობლემის გადაჭრა
  - დატასეტის დაყოფა: ტრანზაქციების დატასეტში, card1 მახასიათებელი არ შეიცავს nan მნიშვნელობებს. ამოტომ მისი შინაარსიდან გამომდინარე ვფიქრობ რომ ამ სვეტის მიხედვით უნდა გავყო მთლიანი დატა სატესტო და სატრენინგო ნაწილებად.
  - ამოვიღე უნიკალური card1 მნიშვნელობები.
  - მასივი დავყავი 60% 20% 20% (ტრენინგი, ვალიდაცია, ტესტი)
  - შევამოწმე განაწილებები მიღებულ დატასეტებში და მივიღე შემდეგი შედეგები, რაზეც ვფიქრობ რომ დამაკმაყოფილებელია:
```
📊 Train set:
Fraud distribution:
isFraud
0    0.964869
1    0.035131
Name: proportion, dtype: float64
isFraud
0    362261
1     13190
Name: count, dtype: int64
Total rows: 375451
Number of features: 393
----------------------------------------
📊 Validation set:
Fraud distribution:
isFraud
0    0.961098
1    0.038902
Name: proportion, dtype: float64
isFraud
0    94820
1     3838
Name: count, dtype: int64
Total rows: 98658
Number of features: 393
----------------------------------------
📊 Test set:
Fraud distribution:
isFraud
0    0.96878
1    0.03122
Name: proportion, dtype: float64
isFraud
0    112796
1      3635
Name: count, dtype: int64
Total rows: 116431
Number of features: 393
----------------------------------------
```
  - 

## რეპოზიტორიის სტრუქტურა
```
Fraud-Detection-ml/
│
├── model_experiment_Linear_Regression.ipynb    # რაღაც მოდელი
├── README.md                                   # პროექტის აღწერა
└── model_inference.ipynb                       # გაწვრთნილი მოდელის ჩამოტვირთვა mlflow დან და prediction ის დაგენერირება
```

## Feature Engineering

## Feature Selection

## Training

## MLflow Tracking
