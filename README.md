# Fraud-Detection-ml

## [IEEE-CIS Fraud Detection](https://www.kaggle.com/c/ieee-fraud-detection/overview)
- მიმოხილვა
  - მოცემული გვაქვს transaction.csv და identity.csv ფაილები, რომზებზეც ვიცით იყო თუ არა თაღლითური ტრანზაქცია. ამ მონაცემებზე დაყრდნობით უნდა გამოვიცნოთ ახალი ტრანზაქცია იყო თუ არა თაღლითობა.
  - მოცემული დატასეტის აღწერა იხილეთ [ლინკზე](https://www.kaggle.com/c/ieee-fraud-detection/discussion/101203#610146)
- პრობლემის გადაჭრა
  - დატასეტის დაყოფა: ტრანზაქციების დატასეტში, card1 მახასიათებელი არ შეიცავს nan მნიშვნელობებს. ამოტომ მისი შინაარსიდან გამომდინარე ვფიქრობ რომ ამ სვეტის მიხედვით უნდა გავყო მთლიანი დატა სატესტო და სატრენინგო ნაწილებად.
  - ამოვიღე უნიკალური card1 მნიშვნელობები.
  - card1 ის უნიკალური მნიშვნელობები დავყავი 60% 20% 20% ნაწილებად (ტრენინგი, ვალიდაცია, ტესტი) (მომავალში თუ დამჭირდა ვალიდაციის ნაწილი, ბარემ წინასწარ მექნება გამოყოფილი)
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
  - ამის შემდეგ დავიწყე model tuning.
  - ხის მოდელების ტრენინგისას, დეფოლტ პარამეტრებზე ეგრევე overfit ში წავიდა მოდელი, ტრენინგ სეტზე მაღალი AUC ქულა (დაახლოებით 0.97 - 0.99), ხოლო ვალიდაციაზე შედარებით დაბალი ქულა ჰქონდა (0.83 - 0.87). ჰიპერ პარამეტრების შერჩევის შემდეგ უკეთესი შედეგი მივიღე, ვიდრე logistic regression იძლეოდა. 

## რეპოზიტორიის სტრუქტურა
```
Fraud-Detection-ml/
│
├── model_experiment_fraud_detection.ipynb      # ამ ფაილში ვაკვირდებოდი დატასეტს და გადავწყვიტე როგორ დამეყო სატესტო და სატრენინგო ნაწილებად
├── model_experiment_LogisticRegression.ipynb   # Logistic Regression მოდელი
├── model-experiment-randomforest.ipynb         # Random Forest მოდელი
├── README.md                                   # პროექტის აღწერა
└── model_inference.ipynb                       # გაწვრთნილი მოდელის ჩამოტვირთვა mlflow დან და prediction ის დაგენერირება
```

## Feature Engineering
- LogisticRegression
  - პირველი ეტაპისთვის ყველა ის უჯრა სადაც მნიშვნელობა არ ეწერა შევავსე 0 ით
  - კატეგორიულებისთვის გავაკეთე woe encoding
- RandomForest
  - აქაც იგივეა ყველაფერი, რაც წინაზე
- XGBoost
  - აქაც იგივეა ყველაფერი, რაც წინაზე

## Feature Selection
- LogisticRegression
  - საწყის ეტაპზე მხოლოდ 'TransactionID' გადავაგდე
  - დავთვალე სვეტები, სადაც მაღალი პროცენტი იყო nan ების
  - კორელაციური ფილტრით გამოვთვალე მაღალი კორელაციის მქონე სვეტები (>0,95)
  - ორივენაირად ვცადე და მაღალკორელირებული სვეტების წაშლამ უკეთესი შედეგი აჩვენა, ამიტომ დატასეტიდან ამოვაკელი ყველა ასეთი სვეტი.
- RandomForest
  - აქაც მაღალი კორელაციის მქონე სვეტები და 'TransactionID' წავშალე.
- XGBoost
  - აქაც მაღალი კორელაციის მქონე სვეტები და 'TransactionID' წავშალე.

## Training
- LogisticRegression
  - 

## MLflow Tracking
- [LogisticRegression](https://dagshub.com/nmach22/Fraud-Detection-ml.mlflow/#/experiments/0?searchFilter=&orderByKey=attributes.start_time&orderByAsc=false&startTime=ALL&lifecycleFilter=Active&modelVersionFilter=All+Runs&datasetsFilter=W10%3D)
  - [BaseModel](https://dagshub.com/nmach22/Fraud-Detection-ml.mlflow/#/experiments/0/runs/7d17ecf36b114b91b05690ef91971023)
  - [BestLogisticModel](https://dagshub.com/nmach22/Fraud-Detection-ml.mlflow/#/experiments/0/runs/2b3e473227ce4688882ad25503aa9aa5)
- [RandomForest](https://dagshub.com/nmach22/Fraud-Detection-ml.mlflow/#/experiments/1?searchFilter=&orderByKey=attributes.start_time&orderByAsc=false&startTime=ALL&lifecycleFilter=Active&modelVersionFilter=All+Runs&datasetsFilter=W10%3D)
  - [BaseModel](https://dagshub.com/nmach22/Fraud-Detection-ml.mlflow/#/experiments/1/runs/a1fccdb046f840a7b00b4f5adb890585)
  - [BestRandomForestModel]()

  
