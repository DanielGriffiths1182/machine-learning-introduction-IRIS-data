**MACHINE LEARNING WITH PYTHON**

**COMMAND LINE PROMPTS**

**IRIS DATASET**

*Thanks to Jason Brownlee's blog! (this was a great, and simple introduction) - Daniel Griffiths*

1. > `Python`

Check the versions of libraries
2. >	`import sys
  	print('Python: {}'.format(sys.version))`

  	`import scipy
  	print('scipy: {}'.format(scipy.__version__))`

  	`import numpy
  	print('numpy: {}'.format(numpy.__version__))`

	`import matplotlib
  	print('matplotlib: {}'.format(matplotlib.__version__))`

	`import pandas
  	print('pandas: {}'.format(pandas.__version__))`

	`import sklearn
  	print('sklearn: {}'.format(sklearn.__version__))`

3. > `# Load libraries
  import pandas from pandas.tools.plotting import scatter_matrix
  import matplotlib.pyplot as plt
  from sklearn import model_selection
  from sklearn.metrics import classification_report
  from sklearn.metrics import confusion_matrix
  from sklearn.metrics import accuracy_score
  from sklearn.linear_model import LogisticRegression
  from sklearn.tree import DecisionTreeClassifier
  from sklearn.neighbors import KNeighborsClassifier
  from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
  from sklearn.naive_bayes import GaussianNB
  from sklearn.svm import SVC`

4. > `# Load dataset
  url = "https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data"
  names = ['sepal-length', 'sepal-width', 'petal-length', 'petal-width', 'class']
  dataset = pandas.read_csv(url, names=names)`

5. > `# shape
  print(dataset.shape)`

6. > `# head
  print(dataset.head(20))`

7. > `# descriptions
  print(dataset.describe())`

8. > `# class distribution
  print(dataset.groupby('class').size())`

9. > `# box and whisker plots
  dataset.plot(kind='box', subplots=True, layout=(2,2), sharex=False, sharey=False)
  plt.show()`

10. > `# histograms
  dataset.hist()
  plt.show()`

11. > `# scatter plot matrix
  scatter_matrix(dataset)
  plt.show()`

12. > `# Split-out validation dataset
  array = dataset.values
  X = array[:,0:4]
  Y = array[:,4]
  validation_size = 0.20
  seed = 7
  X_train, X_validation, Y_train, Y_validation = model_selection.train_test_split(X, Y, test_size=validation_size, random_state=seed)`

13. > `# Test options and evaluation metric
  seed = 7
  scoring = 'accuracy'`

14. > `# Spot Check Algorithms
  models = []
  models.append(('LR', LogisticRegression()))
  models.append(('LDA', LinearDiscriminantAnalysis()))
  models.append(('KNN', KNeighborsClassifier()))
  models.append(('CART', DecisionTreeClassifier()))
  models.append(('NB', GaussianNB()))
  models.append(('SVM', SVC()))
  # evaluate each model in turn
  results = []
  names = []
  for name, model in models:
	kfold = model_selection.KFold(n_splits=10, random_state=seed)
  cv_results = model_selection.cross_val_score(model, X_train, Y_train, cv=kfold, scoring=scoring)
  results.append(cv_results)
	names.append(name)
  msg = "%s: %f (%f)" % (name, cv_results.mean(), cv_results.std())
	print(msg)`

15. > `# Compare Algorithms
  fig = plt.figure()
  fig.suptitle('Algorithm Comparison')
  ax = fig.add_subplot(111)
  plt.boxplot(results)
  ax.set_xticklabels(names)
  plt.show()`

16. > `# Make predictions on validation dataset
  knn = KNeighborsClassifier()
  knn.fit(X_train, Y_train)
  predictions = knn.predict(X_validation)
  print(accuracy_score(Y_validation, predictions))
  print(confusion_matrix(Y_validation, predictions))
  print(classification_report(Y_validation, predictions))`

  **TADA!**
