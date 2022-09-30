# 

> **Note:**
> Python development, the Anaconda Python distributions 3.5 and 2.7 are installed on the DSVM. 

> **Note:**
> The Anaconda distribution includes Conda. You can use Conda to create custom Python environments that have different versions or packages installed in them. 

Let's read in some of the spambase dataset and classify the emails with support vector machines in Scikit-learn: 

```Python
import pandas 
from sklearn import svm 
data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*') 
X = data.ix[:, 0:57] 
y = data.ix[:, 57] 
clf = svm.SVC() 
clf.fit(X, y) 
```

To make predictions: 

```Python
clf.predict(X.ix[0:20, :]) 
```

To demonstrate how to publish an Azure Machine Learning endpoint, let's make a more basic model. We'll use the three variables that we used when we published the R model earlier: 

```Python
X = data[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]] 
y = data.ix[:, 57] 
clf = svm.SVC() 
clf.fit(X, y) 
```

Try these code blocks in your VM. 

<!--- other langs --->