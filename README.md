# Developing a Neural Network Regression Model

## AIM

To develop a neural network regression model for the given dataset.

## THEORY

Neural networks consist of simple input/output units called neurons. These units are interconnected and each connection has a weight associated with it. Neural networks are flexible and can be used for both classification and regression. In this article, we will see how neural networks can be applied to regression problems.

Regression helps in establishing a relationship between a dependent variable and one or more independent variables. Regression models work well only when the regression equation is a good fit for the data. Although neural networks are complex and computationally expensive, they are flexible and can dynamically pick the best type of regression, and if that is not enough, hidden layers can be added to improve prediction.

Build your training and test set from the dataset, here we are making the neural network 3 hidden layer with activation layer as relu and with their nodes in them. Now we will fit our dataset and then predict the value.

## Neural Network Model

![261571337-ccc9e02d-c2a8-4425-bfff-ea12b49224c0](https://github.com/harshavardhini33/basic-nn-model/assets/93427208/9b4c37b6-ec63-438a-b53c-d37e5d16d171)


## DESIGN STEPS

### STEP 1:

Loading the dataset

### STEP 2:

Split the dataset into training and testing

### STEP 3:

Create MinMaxScalar objects ,fit the model and transform the data.

### STEP 4:

Build the Neural Network Model and compile the model.

### STEP 5:

Train the model with the training data.

### STEP 6:

Plot the performance plot

### STEP 7:

Evaluate the model with the testing data.

## PROGRAM

```
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler

from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

from google.colab import auth
import gspread
from google.auth import default

auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)

worksheet = gc.open('DLExp1').sheet1
data = worksheet.get_all_values()
df = pd.DataFrame(data[1:], columns=data[0])
df = df.astype({'Input':'float'})
df = df.astype({'Output':'float'})
df.head()

X = df[['Input']].values
y = df[['Output']].values
X

X_train,X_test,y_train,y_test = train_test_split(X,y,test_size = 0.33,random_state = 33)
Scaler = MinMaxScaler()
Scaler.fit(X_train)
X_train1 = Scaler.transform(X_train)
X_train1

ai=Sequential([
    Dense(21,activation='relu'),
    Dense(23,activation='relu'),
    Dense(1)
])
ai.compile(optimizer='rmsprop',loss='mse')
ai.fit(X_train1,y_train,epochs=2000)
ai.fit(X_train1,y_train,epochs=2000)

## Plot the loss
loss_df = pd.DataFrame(ai.history.history)
loss_df.plot()

## Evaluate the model
X_test1 = Scaler.transform(X_test)
ai.evaluate(X_test1,y_test)

# Prediction
X_n1 = [[30]]
X_n1_1 = Scaler.transform(X_n1)
ai.predict(X_n1_1)
```

## Dataset Information
![261504442-44710e33-4494-4480-917f-fc9bb50edebf](https://github.com/harshavardhini33/basic-nn-model/assets/93427208/e1a58fa2-86e1-4739-81ce-2052d33dcfeb)



## OUTPUT



### Training Loss Vs Iteration Plot

![261504468-9234d222-dbf5-4b45-bdac-cabcf0b10084](https://github.com/harshavardhini33/basic-nn-model/assets/93427208/055be79c-4a87-47e1-bd7e-78489f30480b)

### Test Data Root Mean Squared Error
![261504498-8441e9c6-13dc-469b-a665-45b637b906b2](https://github.com/harshavardhini33/basic-nn-model/assets/93427208/f63909ec-269b-4330-a2a8-8198266acb9f)



### New Sample Data Prediction

![261504510-77ff41ed-6a54-4aeb-ad3d-5ae647866b68](https://github.com/harshavardhini33/basic-nn-model/assets/93427208/238b88b3-f090-4829-90df-bea7c31e7a2f)


## RESULT
Thus a neural network regression model for the given dataset is written and executed successfully.
