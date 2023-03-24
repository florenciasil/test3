# Jupyter Workspaces - Python


## Intro

Jupyter Workspaces in Domo are a web-based interactive development environment for Jupyter notebooks, code, and data. Workspaces are tightly integrated with Domo to allow users to easily explore their Domo DataSets, leverage instantaneous code execution to develop pipelines for data science and machine learning, document their processes, create custom visualizations, and write transformed data back into Domo.

See the Domo [Knowledge Base](https://domohelp.domo.com/hc/en-us/articles/360047400753-Jupyter-Workspaces)
for more information on using Jupyter Workspaces: 

Having issues with your workspace? Check out our [troubleshooting guide](https://domohelp.domo.com/hc/en-us/articles/7440921035671-Jupyter-Troubleshooting-Guide-)!

---

## Exploring Your Data in Jupyter

Any dataset that has been configured as an *Input* to your Jupyter Workspace in Domo can be read into a dataframe in Jupyter. In order to do this, import the domojupyter library and call the `read_dataframe()` function with the alias you've configured for your input dataset.

```python
    import domojupyter as domo
    # Read the dataset configured with alias 'BMX I' as a pandas dataframe
    bmx = domo.read_dataframe('BMX I')
    bmx.head()
```

domo.read_dataframe will cast the column's dtypes based on the provided schema. However, the user can override the default dtypes. 
When using the domo.read_dataframe function you are able to use any parameter that is included in [pandas.read_csv](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html):

Here's an example utilizing multiple args, overriding a few of the column's dypes and changing the "date" column into a datetime64 dtype:  
```python
read_dataframe('Test_DataSource', query='SELECT * FROM table', dtype={'P': 'int64', 'D': 'object', 'price': 'float64'}, parse_dates=['date'], na_filter=False)
```


---

## Query Data Using SQL

Datasets can be queried with SQL-like syntax. This can be used to limit the size of the data returned for large datasets or to leverage the power of Domo to perform aggregations on the fly.

```python
    import domojupyter as domo
    demo = domo.read_dataframe('DEMO I', query='SELECT SEQN, RIAGENDR AS Gender, RIDAGEYR AS Age FROM table WHERE RIDAGEYR > 20')
    demo.head()
```
---

## Write Data Back to Domo

If you've made some transformations that you'd like to preserve as a separate dataset in Domo, configure your workspace to include an *Output* dataset. Then use the `write_dataframe()` function with your dataframe and the alias you've configured for your output dataset as parameters.


```python
    import domojupyter as domo
    # Write dataframe to Domo dataset configured with alias 'Jupyter Data'
    domo.write_dataframe(df, 'Jupyter Data')
```
---

## Installing Additional Libraries

3rd party libraries not already included in the workspace can be installed using pip for Python, CRAN for R or Conda for both.

```bash
    pip install requests-toolbelt
    
    OR

    conda install requests-toolbelt
```