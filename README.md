# Dash
Databricks Notebook Rendering Issue: IPython.lib.display.IFram

Step 1 
------
Set the Environment variables in Databricks cluster 

For example : 

DASH_REQUEST_PATHNAME_PREFIX=/driver-proxy/o/4080082044612008/1004-091920-cpkidhkx/8888

Workspace ID : 4080082044612008 
Cluster ID : 1004-091920-cpkidhkx
Port number : 8888 

Step 2 
------
Via Databricks notebook install the explainerdashboard

%pip install explainerdashboard

Step 3
------
Via databricks notebook run the below sample code 

from sklearn.ensemble import RandomForestClassifier
from explainerdashboard import ClassifierExplainer, ExplainerDashboard
from explainerdashboard.datasets import titanic_survive, feature_descriptions

X_train, y_train, X_test, y_test = titanic_survive()

model = RandomForestClassifier(n_estimators=50, max_depth=10).fit(X_train, y_train)

explainer = ClassifierExplainer(model, X_test, y_test,
          cats=['Deck', 'Embarked'],
          descriptions=feature_descriptions,
          labels=['Not survived', 'Survived'])

ExplainerDashboard(explainer, mode = 'dash',

          importances=False,
          model_summary=False,
          contributions=True,
          whatif=False,
          shap_dependence=False,
          shap_interaction=False,
          decision_trees=False).run(8888)
          
Step 4
------

Access the dashboard via web url 

For example : https://xxxxxx.azuredatabricks.net/driver-proxy/o/4080082044612008/1004-091920-cpkidhkx/8888

Workspace URL : https://xxxxxx.azuredatabricks.net
Workspace ID : 4080082044612008 
Cluster ID : 1004-091920-cpkidhkx

