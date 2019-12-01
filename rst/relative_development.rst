
DeLong: Teaching Economics 
----------------------------

Last edited: 2019-10-12

Deep Roots of Relative Development 
====================================

Due ???? via upload to ??? 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

J. Bradford DeLong 
~~~~~~~~~~~~~~~~~~~~

Derived from QuantEcon: Linear Regression in Python: https://python.quantecon.org/ols.html
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 

You should have gotten to this point vis this link:

 

Table of Contents 
~~~~~~~~~~~~~~~~~~~

1.
2.
3. 

 

.. code-block:: ipython
  :class: hide-output

    #libraries:
    
    !pip install linearmodels
    
    import numpy as np
    import matplotlib.pyplot as plt
    import pandas as pd
    import statsmodels.api as sm
    from statsmodels.iolib.summary2 import summary_col
    from linearmodels.iv import IV2SLS
    
    
    # inline graphics
    
    %matplotlib inline


.. code-block:: python3

    ajr_df = pd.read_csv('https://delong.typepad.com/files/ajr.csv')
    ajr_df.head()




Let’s use a scatterplot to see whether any obvious relationship exists
between GDP per capita and the protection against expropriation index:

.. code-block:: python3

    plt.style.use('seaborn')
    
    ajr_df.plot.scatter(x='avexpr', y='logpgp95')
    plt.show()


Let’s add three-letter country labels to the points:

.. code-block:: python3

    x = ajr_df['avexpr'].tolist()
    y = ajr_df['logpgp95'].tolist()
    labels = ajr_df['shortnam'].tolist()
    
    fig, ax = plt.subplots()
    ax.scatter(x, y, marker='.')
    
    for i, txt in enumerate(labels):
        ax.annotate(txt, (x[i], y[i]))
        
    plt.show()
    
    # no, I do not understand why the data and labels need to be
    # coerced into a list before ax.annotate will do its thing...



Let’s fit a linear model to this scatter:

   (1) :math:`\ln(pgp_95)_i= β_0 + β_1(avexpr_i) + u_i`

-  :math:`β_0` is the intercept of the linear trend line on the y-axis
-  :math:`β_1` is the slope of the linear trend line, representing the
   marginal association of protection against against expropriation risk
   with log GDP per capita
-  :math:`u_i` is an error term.

Fitting this linear model chooses a straight line that best fits the
data in a least-squares, as in the following plot (Figure 2 in AJR):

.. code-block:: python3

    # dropping NA's is required to use numpy's polyfit...
    # using only 'base sample' for plotting purposes...
    
    
    ajr_df = ajr_df.dropna(subset=['logpgp95', 'avexpr'])
    ajr_df = ajr_df[ajr_df['baseco'] == 1]
    
    x = ajr_df['avexpr'].tolist()
    y = ajr_df['logpgp95'].tolist()
    labels = ajr_df['shortnam'].tolist()
    
    fig, ax = plt.subplots()
    ax.scatter(x, y, marker='.')
    
    for i, txt in enumerate(labels):
        ax.annotate(txt, (x[i], y[i]))
        
    ax.plot(np.unique(x),
             np.poly1d(np.polyfit(x, y, 1))(np.unique(x)),
             color='black')
    
    ax.set_xlabel('Inverse Expropriation Risk Classification, 1985-95')
    ax.set_ylabel('Log GDP per capita 1995 (PPP)')
    ax.set_title('Figure 2: OLS Relationship: Prosperity and "Property Security Institutions"')
    
    plt.show()



To estimate the constant term :math:`β_0`, we need to add a column of
1’s to our dataframe so that we can use statsmodels’s OLS routines:

.. code-block:: python3

    ajr_df['constant'] = 1
    
    regression_1 = sm.OLS(endog=ajr_df['logpgp95'], 
                    exog=ajr_df[['constant', 'avexpr']], 
                    missing='drop')
    results_1 = regression_1.fit()
    print(results_1.summary())


We extend our bivariate regression model to a multivariate regression
model by adding in other factors correlated with :math:`\ln(pgp_95)_i`:

-  climate, as proxied by latitude
-  the different culture and history of different continents

latitude is used to proxy this differences that affect both economic
performance and institutions, eg. cultural, historical, etc.; controlled
for with the use of continent dummies Let’s estimate some of the
extended models considered in the paper (Table 2) using data from

.. code-block:: python3

    ajr2_df = pd.read_csv('https://delong.typepad.com/files/ajr2.csv')
    ajr2_df['constant'] = 1
    
    X1 = ['constant', 'avexpr']
    X2 = ['constant', 'avexpr', 'lat_abst']
    X3 = ['constant', 'avexpr', 'lat_abst', 'asia', 'africa', 'other']
    
    regression_2 = sm.OLS(ajr2_df['logpgp95'], ajr2_df[X1], missing='drop').fit()
    regression_3 = sm.OLS(ajr2_df['logpgp95'], ajr2_df[X2], missing='drop').fit()
    regression_4 = sm.OLS(ajr2_df['logpgp95'], ajr2_df[X3], missing='drop').fit()
    
    info_dict={'R-squared' : lambda x: f"{x.rsquared:.2f}",
               'No. observations' : lambda x: f"{int(x.nobs):d}"}
    
    results_table = summary_col(results=[regression_2, regression_3, regression_4],
                                float_format='%0.2f',
                                stars = True,
                                model_names=['Model 1',
                                             'Model 3',
                                             'Model 4'],
                                info_dict=info_dict,
                                regressor_order=['constant',
                                                 'avexpr',
                                                 'lat_abst',
                                                 'asia',
                                                 'africa'])
    
    results_table.add_title('Table 2 - OLS Regressions')
    
    print(results_table)



.. code-block:: python3

    # Dropping NA's is required to use numpy's polyfit
    df1_subset2 = ajr_df.dropna(subset=['logem4', 'avexpr'])
    
    X = df1_subset2['logem4']
    y = df1_subset2['avexpr']
    labels = df1_subset2['shortnam']
    
    # Replace markers with country labels
    fig, ax = plt.subplots()
    ax.scatter(X, y, marker='')
    
    for i, label in enumerate(labels):
        ax.annotate(label, (X.iloc[i], y.iloc[i]))
    
    # Fit a linear trend line
    ax.plot(np.unique(X),
             np.poly1d(np.polyfit(X, y, 1))(np.unique(X)),
             color='black')
    
    ax.set_xlim([1.8,8.4])
    ax.set_ylim([3.3,10.4])
    ax.set_xlabel('Log of Settler Mortality')
    ax.set_ylabel('Average Expropriation Risk 1985-95')
    ax.set_title('Figure 3: First-stage relationship between settler mortality \
        and expropriation risk')
    plt.show()



.. code-block:: python3

    df4 = pd.read_stata('https://github.com/QuantEcon/QuantEcon.lectures.code/raw/master/ols/maketable4.dta')
    df4 = df4[df4['baseco'] == 1]
    df4['const'] = 1
    
    iv = IV2SLS(dependent=df4['logpgp95'],
                exog=df4['const'],
                endog=df4['avexpr'],
                instruments=df4['logem4']).fit(cov_type='unadjusted')
    
    print(iv.summary)

 

Deep Roots of Relative Development 
------------------------------------

Catch Our Breath—Further Notes:
===============================


.. figure:: /_static/skitch.png


-  weblog support:
   https://github.com/braddelong/LS2019/blob/master/Deep-Roots-of-Relative-Development.ipynb
-  nbViewer:
   https://nbviewer.jupyter.org/github/braddelong/LS2019/blob/master/Deep-Roots-of-Relative-Development.ipynb
-  datahub:
   http://datahub.berkeley.edu/user-redirect/interact?account=braddelong&repo=LS2019&branch=master&path=Deep-Roots-of-Relative-Development.ipynb

 

--------------

.. code-block:: python3

    pwt91_df = pd.read_csv('https://delong.typepad.com/files/pwt91-data.csv')

.. code-block:: python3

    pwt91_df.head()



