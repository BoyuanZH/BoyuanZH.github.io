---
layout:     post
title:      "Kaggle: NY Taxi Trip Duration Prediction"
subtitle:   "Feature engineering and Hyperparameter tunning."
date:       2017-09-02
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - Machine Learning
    - Cloud Computing
    - Kaggle
    - Study Notes
---


NY Taxi Trip Duration is the FIRST kaggle competition I have been diving into. With nearly no prior knowledge with pandas and xgboost, it took me fairly a long time even to understand other's code. But for now I am more confident to write my own cods and build my own model.

The following post is for recording my thoughts about this project.


### Hyperparameter Tunning

After feature engineering, the model performance can be improved efficiently through hyperparameter tunning.

##### Hyperparameters

[Full list of parameters for Xgboost](https://github.com/dmlc/xgboost/blob/master/doc/parameter.md)

1. **eta:** smaller `eta` is paired with larger ` num_boost_round`. I prefer first fix `num_boost_round = 2000`, using `early_stopping_rounds = 10` to grid search for the optimal `eta`. 
2. min\_child\_weight
2. max_depth
3. subsample
4. colsample_bytree
5. lambda

##### Method: Grid Search Cross Validation

###### Option 1. sklearn.model_selection.GridSearchCV

Since Xgboost provide a sklearn wrapper class `xgboost.XGBRegressor` and `xgboost.XGBClassifier`, we can use sklearn rendered `sklearn.model_selection.GridSearchCV()` to do the heavy lifting.

However, in this project, I encountered several issue using this `GridSearchCV()` method:

1. dataset with 4 Million data points makes the cross validation (even 3 folds) super slow.
2. evaluation metrics turns out to be not what I want. In this project, score I want is `RMSE`, however, the `GridSearchCV()` provided me with some negative number.

Since our dataset is pretty large, it won't be a big problem to split out a seperate evaluation set. I.E., not using cross validation but just validation.

###### Option 2. hand-made grid search method

After reading others' posts I turned to write my own grid search method.

Here are main goals I want my grid search function to achieve:

1. Fast:

    Seen other posts using nested for loop for executing diffent parameter choices, which should be rather slow, I want the function to be able to doing parallel processing, making use of all the cpus on my machine.
    
    This is feasible, because the tasks are so called [Embarrassingly parallel](https://en.wikipedia.org/wiki/Embarrassingly_parallel).
    
2. Real-time Insepction:
    
    Be able to see evaluation result per iteration and such.
    
3. Store tested model real-time:

   Finally, I want my tested-model be accessible after, not only getting just the evaluation values.
   
   
Following are my code for the function, **not neat but works** for me:

```
def train_unit(comb, xgb_param = xgb_param, dtrain = dtrain, watchlist=watchlist, early_stopping_rounds=10, num_boost_round=2000, verbose_eval=20):
  print("Testing ...{}".format(comb))
  t0 = dt.datetime.now()

  xgb_param.update(comb)
  xgb_model = xgb.train(xgb_param, 
                        dtrain, 
                        evals = watchlist,
                        early_stopping_rounds = early_stopping_rounds,
                        num_boost_round = num_boost_round,
                        verbose_eval = verbose_eval)
  t1 = dt.datetime.now(); 
  xgb_model.save_model(os.path.join("models", str(comb) + ".model"))
  print("Done Test: {0}. \n     Time: {1:.1f} min".format(comb, (t1-t0).seconds/60))
  return [str(comb), xgb_model.best_score]


def xgb_gridsearch(param_grid, xgb_param, dtrain, watchlist, random_sample = False):

    def translate(param_grid):
        '''
        type: dict: {'f1': [v1, v2, v3], 'f2': [v4, v5]}
        rtype: list: [{'f1': v1, 'f2': v4}, {'f1': v1, 'f2': v5}, ...]
        '''
        from itertools import product
        features = list(param_grid.keys())
        values = list(param_grid.values())
        comb_list = [dict(zip(features, i)) for i in list(product(*values))]
        return comb_list

  
    comb_list = translate(param_grid)
    if random_sample:
        comb_list = random.sample(comb_list, len(comb_list)//3)
    random.shuffle(comb_list)

    print("GridSearch Required Tests: {}. ".format(len(comb_list)), "\nStart......")
    T0 = dt.datetime.now()

    pool = mp.Pool(mp.cpu_count())
    result = pool.map(train_unit, comb_list)

    T1 = dt.datetime.now(); print("Complete teseting. Time: {0:.1f} min".format((T1-T0).seconds/60))
    return result

##### Carry out the tests
param_grid = {"eta": [0.05],
              "min_child_weight": [10, 15], 
              "max_depth": [15],
              "lambda": [1, 2],
              "gamma": [0],
              "subsample": [0.8, 1],
              "colsample_bytree": [0.8, 1]}
scores = xgb_gridsearch(param_grid, xgb_param, dtrain, watchlist, random_sample = False)

```

> The helper function takes in a whole lot of default arguments as one may notice. I did this because the `multiprocessing.Pool.map()` function require the function argement it takes in to be picklable. By doing what I did, just pass in the `comb_list` as the parameter list is enough, no need to pickle `dtrain`, `watchlist`, etc..

The function works the way I expected at last. I build a 24-cpu machine on GCP and saved me nearlly 24 times of time in searching through 24 parameter combinations. This is good.

