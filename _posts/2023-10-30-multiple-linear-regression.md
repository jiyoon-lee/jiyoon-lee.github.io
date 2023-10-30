Linear Regression은 독립변수가 1개 종속변수가 1개였는데

Multiple Linear Regression은 독립변수가 여러개 종속변수가 1개가 됩니다.

Linear Regression을 통해 얻게되는 모델의 예측값은 연속적인 숫자값이 나옵니다.

만약 연속적인 숫자를 예측하는 것이 아니라 분류를 예측하려면 어떻게 해야할까요? 기존의 linear regression이 아닌 다른 방식을 사용하여야 합니다.

예를 들어 시험을 쳤을 경우 시험 결과로 Fail과 Pass로 분류될 수 있습니다.

결과가 Fail또는 Pass가 나오기 때문에 이진 분류(binary classification)라고 합니다.

이것을 구현하기 위해서는 linear regression을 변형하여 logistic regression으로 구현할 수 있습니다.

logistic regression model은 확률값이 나옵니다.

둘다 직선이 나오는데 linear regression으로는 불가능할까요?

불가능한 이유는 linear regression은 linear하게 값이 증가하는 모델이기 때문입니다.

그러면 1.2, 1.5 이렇게 0과 1사이를 넘어가게 되어버리는데요.

이를 해결하기 위해 직선을 S모양의 곡선으로 model을 변경해야 합니다.

그래프를 보면 sigmoid공식이 떠오르는데요.

sigmoid 공식을 통해 model이 구현되면 이제 loss함수를 사용하여 오차를 구해야합니다.

이 또한 linear regression에서 사용했던 mse를 사용할 수 는 없습니다. 

왜냐하면 logistic regression model은 꼬불꼬불한 그래프가 그려지기 때문입니다.

이를 해결하기 위해서는 MSE대신 Cross Entropy를 사용할 수 있습니다.

이 것은 기존의 linear regression에서 activation 과정을 추가하면 됩니다.

이제 저희는 모델을 만들어보았으니 평가(Evaluation)을 해보아야 합니다.

Linear Regression에서는 평가를 할때 skit-learn을 사용했었는데요. Logistic Regression에서는 다른 방법을 사용해야 합니다.

Linear Regression과 같이 Training Data Set을 이용해서 평가를 진행하면 안됩니다.

데이터는 아래와 같이 Original Data Set을 Training Data, Validation Data, Test Data로 나눌 수 있습니다.

Test data는 마지막에 우리 모델의 성능을 확장시키기 위해 딱 1번 사용하는 데이터 입니다.
