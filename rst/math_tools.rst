

DeLong: Teaching Economics 
----------------------------

Last edited: 2019-10-09

Introduction: Math Tools 
==========================

Due ???? via upload to ??? 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

J. Bradford DeLong 
~~~~~~~~~~~~~~~~~~~~

 

You should have gotten to this point vis this link:
http://datahub.berkeley.edu/user-redirect/interact?account=braddelong&repo=LS2019&branch=master&path=Introduction-Math-Tools-%26-Economics-delong.ipynb

 

This second introductory notebook will remind—well, at least
familiarize—you with some math tools useful in economics:

 

Table of Contents 
~~~~~~~~~~~~~~~~~~~

1. Math Review
2. Economics Review: Measuring the Economy
3. Economics Review: Economic Thought

 

There will be some questions for you in the notebook. For free response
questions, write your answers in the provided markdown cell that starts
with ANSWER:. Do not change the heading, and write your entire answer in
that one cell.

For questions that are to be answered numerically, there is a code cell
that starts with:

::

   __#ANSWER__ 

and has a line in which there is a variable (like “X”) currently set to
underscores so:

::

   X = ___

Replace those underscores with your final answer. It is okay to make
other computations in that cell and others, so long as you set the
variable to your answer.

 

Math as a Tool  
~~~~~~~~~~~~~~~~

Suppose a quantity grows at a steady proportional rate of 3% per year…
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

…How long will it take to double?

.. code-block:: python3

    #ANSWER
    import math
    n=math.log(2)/math.log(1.03)
    print(n)
    TIME_TO_DOUBLE = 23.45

Quadruple?

.. code-block:: python3

    #ANSWER
    import math
    n=math.log(4)/math.log(1.03)
    print(n)
    TIME_TO_QUADRUPLE = 46.90

Grow 1024-fold?

.. code-block:: python3

    #ANSWER
    import math
    n=math.log(1024)/math.log(1.03)
    print(n)
    TIME_TO_1024 = 234.50

Suppose we have a quantity x(t) that varies over time following the equation:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:math:`\frac{dx(t)}{dt} = -(0.06)x + 0.36`

:math:`\frac{dx(t)}{dt} -  \frac{d(6)}{dt} = -(0.06)(x - 6)`

:math:`\frac{dx(t)}{dt} = -(0.06)(x - 6)`

:math:`\frac{dy(t)}{dt} = -(0.06)y`

Without integrating the equation:

:math:`1.`\ Tell me what the long-run steady-state value of
:math:`x`–that is, the limit of :math:`x` as\ :math:`t` approaches in
infinity–is going to be.

.. code-block:: python3

    steady_state_val = 6

:math:`2.`\ Suppose that the value of :math:`x` at time
:math:`t=0`,\ :math:`x(0)` equals 12. Once again, without integrating
the equation, tell me how long it will take x to close half the distance
between its initial value of 12 and its steady-state value.

.. code-block:: python3

    half_dist_time = 12
    import math
    t=math.log(16)/0.06
    print(t)

:math:`3.` How long will it take to close 3/4 of the distance?

.. code-block:: python3

    three_fourth_time = 23

:math:`4.`\ :math:`7/8` of the distance?

.. code-block:: python3

    seven_eighth_time = 35

:math:`5.`\ :math:`15/16` of the distance?

.. code-block:: python3

    fifteen_sixteenth = 46

Now you are allowed to integrate
:math:`\frac{dx(t)}{dt} = -(0.06)x + 0.36`.

:math:`1.` Write down and solve the indefinite integral.

ANSWER:  :math:`\frac{dx(t)}{dt} -  \frac{d(6)}{dt} = -(0.06)(x - 6)`

:math:`\frac{dy(t)}{dt} = -(0.06)y`

:math:`\int \frac{dy(t)}{y} = \int -(0.06)dt`

:math:`\ln y = -0.06t + c`

:math:`y=c_{1}e^{-0.06t}`

:math:`x=c_{1}e^{-0.06t}+6`

:math:`2.`\ Write down and solve the definite integral for the initial
condition\ :math:`x(0) = 12`.

ANSWER: :math:`x=c_{1}e^{-0.06t}+6`

:math:`x(0)=12`

:math:`c_{1}=6`

:math:`x=6e^{-0.06t}+6`

:math:`3.`\ Write down and solve the definite integral for the initial
condition\ :math:`x(0) = 6`.

ANSWER: :math:`x=c_{1}e^{-0.06t}+6`

:math:`x(0)=6`

:math:`c_{1}=0`

:math:`x=6`

Suppose we have a quantity :math:`z = (\frac{x}{y})^\beta`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Suppose :math:`x`\ is growing at 4% per year and
that\ :math:`\beta=1/4`:

:math:`1.`\ How fast is :math:`z` growing if\ :math:`y` is growing at 0%
per year?

.. code-block:: python3

    zero_per_growth = 1%

:math:`2.`\ If\ :math:`y` is growing at 2% per year?

.. code-block:: python3

    two_per_growth = 0.5%

:math:`3.`\ If\ :math:`y` is growing at 4% per year?

.. code-block:: python3

    four_per_growth = 0%

Rule of 72 (Use it for the next four questions)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. If a quantity grows at about 3% per year, how long will it take to
   double?

.. code-block:: python3

    time_to_double = 24

:math:`2.` If a quantity shrinks at about 4% per year, how long will it
take it to halve itself?

.. code-block:: python3

    time_to_half = 18

:math:`3.` If a quantity doubles five times, how large is it relative to
its original value?

.. code-block:: python3

    doubled_five_times_ratio = 32

:math:`4.` If a quantity halves itself three times, how large is it
relative to its original value?

.. code-block:: python3

    halved_three_times_ratio = 0.125

Interactive Model for Rule of 72
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In future problem sets, you will build models of your own, but for now,
look over this code. Its a simple model that shows what happens as you
adjust a single parameter (the interest rate) and its effect on the
outcome (the time to double). First we need to make sure all of our
packages are imported.

.. code-block:: python3

    import matplotlib.pyplot as plt
    import numpy as np
    from ipywidgets import interact, IntSlider
    %matplotlib inline

Our model is going to be graph that shows what happens as the interest
rate varies.

.. code-block:: python3

    def graph_rule_of_72(interest_rate):
        # np.linspace takes values evenly spaced between a stop and end point. In this case,
        # will take 30 values between 1 and 10. These will be our x values in the graph.
        x = np.linspace(1,10,30)
        
        # Here we create are corresponding y values
        y = 72 / x
        
        print('Time to double:', 72 / interest_rate, 'years')
        
        # graphing our lines
        plt.plot(x,y)
        # graphing the specific point for our interest_rate
        plt.scatter(interest_rate, 72 / interest_rate, c='r')
        
        plt.xlabel('interest rate (%)')
        plt.ylabel('time (years)')
        plt.show()

When we call ``interact``, select the function that we want to interact
with (``graph_rule_of_72``) and tell it what the value we want its
parameters to take on. In this case, ``graph_rule_of_72`` only takes one
parameter, ``interest_rate``, and we choose to put an adjustable slider
there. You can check out the `ipywidget
examples <https://github.com/jupyter-widgets/ipywidgets/blob/master/docs/source/examples/Index.ipynb>`__
for more uses.

.. code-block:: python3

    interact(graph_rule_of_72, interest_rate=IntSlider(min=1,max=10,step=1))

Why do DeLong and Olney think that the interest rate and the level of the stock market are important macroeconomic variables?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ANSWER:

What are the principal flaws in using national product per worker as a measure of material welfare? Given these flaws, why do we use it anyway?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ANSWER:

What is the difference between the nominal interest rate and the real interest rate? Why do DeLong and Olney think that the real interest rate is more important?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ANSWER:

Review: Measuring the Economy Concepts and Quantities 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

National Income and Product Accounting
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Explain whether or not, why, and how the following items are included in
the calculations of national product:

:math:`1.` Increases in business inventories.

ANSWER: yes, so that New goods that are produced but go unsold will
still be counted in the year in which they are produced.

:math:`2.` Fees earned by real estate agents on selling existing homes.

ANSWER: yes. The service of real estate agents needs to be counted.

:math:`3.` Social Security checks written by the government.

ANSWER: no. they do not involve the production of any good or service

:math:`4.` Building of a new dam by the Army Corps of Engineers.

ANSWER: yes. The goods and services purchased by the government to
build the dam will count in GDP.

:math:`5.` Interest that your parents pay on the mortgage they have on
their house.

ANSWER: no. It is not assumed to flow from the production of goods and
services.

:math:`6.` Purchases of foreign-made trucks by American residents

ANSWER: Purchases of foreign-made trucks by American residents are
counted in the calculation of GDP. They enter GDP negatively through the
category IM and positively through C. In reality, C may be slightly
greater than IM in magnitude. The net contribution to GDP would be
positive due to the production of these American services.

In or Out of National Product? And Why
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Explain whether or not, why, and how the following items are included in
the calculation of national product:

:math:`1.`\ The sale for :math:`\$25,000` of an automobile that
cost\ :math:`\$20,000` to manufacture that had been produced here at
home last year and carried over in inventory.

ANSWER:

:math:`2.`\ The sale for :math:`\$35,000` of an automobile that
cost\ :math:`\$25,000` to manufacture newly- made at home this year.

ANSWER:

:math:`3.`\ The sale for :math:`\$45,000` of an automobile that
cost\ :math:`\$30,000` to manufacture that was newly-made abroad this
year and imported.

ANSWER:

:math:`4.`\ The sale for :math:`\$25,000` of an automobile that
cost\ :math:`\$20,000` to manufacture that was made abroad and imported
last year.

ANSWER:

In or Out of National Product? And Why II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Explain whether or not, why, and how the following items are included in
the calculation of GDP:

:math:`1.`\ The purchase for $500 of a dishwasher produced here at home
this year.

ANSWER:

:math:`2.`\ The purchase for$500 of a dishwasher made abroad this year.

ANSWER:

:math:`3.`\ The purchase for$500 of a used dishwasher.

ANSWER: n GNP.

:math:`4.`\ The manufacture of a new dishwasher here at home for$500 of
a dishwasher that then nobody wants to buy.

ANSWER:

Components of National Income and Product
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Suppose that the appliance store buys a refrigerator from the
manufacturer on December 15, 2018 for :math:`\$600`, and that you then
buy that refrigerator on January 15, 2019 for\ :math:`\$1000`:

:math:`1.` What is the contribution to GDP in 2018?

.. code-block:: python3

    contribution_2018 = 

:math:`2.` How is the refrigerator accounted for in the NIPA in 2019?

ANSWER:

:math:`3.` What is the contribution to GDP in 2019?

.. code-block:: python3

    contribution_2019 =

:math:`4.` How is the refrigerator accounted for in the NIPA in 2019?

ANSWER:

.. code-block:: python3

    """
    These lines are reading in CSV files and creating dataframes from then,
    you don't have to change about them! 
    """
    
    import pandas as pd
    import numpy as np
    
    unemployment = pd.read_csv("data/Unemployment.csv")
    quarterly_acc = pd.read_csv("data/Quarterly_Accounts.csv")
    from_2007 = quarterly_acc.loc[(quarterly_acc["Year"].isin(np.arange(2007, 2018)))]

Estimating National Product
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Bureau of Economic Analysis measures national product in two
different ways: as total expenditure on the economy’s output of goods
and services and as the total income of everyone in the economy. Since –
as you learned in earlier courses – these two things are the same, the
two approaches should give the same answer. But in practice they do not.

We have provided a data table ``quarterly_gdp`` that contains quarterly
data on real GDP measured on the expenditure side (referred to in the
National Income and Product Accounts as “Real Gross Domestic Product,
chained dollars”) and real GDP measured on the income side (referred to
as “Real Gross Domestic Income, chained dollars”). The table refers to
Real Gross Dometic Product as “Real GDP” and to Real Gross Dometic
Income as “Real GDI”, and they are measured in billions of dollars.
(Note: You will not have to use Nominal GDP)

Another table, ``from_2007``, has been created from ``quarterly_gdp``,
and includes information from 2007 to 2017. Below is a snippet from
``from_2007``:

.. code-block:: python3

    from_2007.head(10)

:math:`1.` Compute the growth rate at an annual rate of each of the two
series by quarter for 2007:Q1–2012:Q4.

.. code-block:: python3

    gdi_rate = ___
    gdp_rate = ___
    from_2007

:math:`2.` Describe any two things you see when you compare the two
series that you find interesting, and explain why you find them
interesting.

ANSWER:

Calculating Real Magnitudes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:math:`1.` When you calculate real national product, do you do so by
dividing nominal national product by the price level or by subtracting
the price level from nominal national product?

ANSWER: dividing nominal national product by the price level

:math:`2.` When you calculate the real interest rate, do you do so by
dividing the nominal interest rate by the price level or by subtracting
the inflation rate from the nominal interest rate?

ANSWER: subtracting the inflation rate from the nominal interest rate

:math:`3.` Are your answers to (a) and (b) the same? Why or why not?

ANSWER: no. The interest rate is a ratio.

Unemployment Rate
~~~~~~~~~~~~~~~~~

Use the ``unemployment`` table provided to answer the following
questions. **All numbers (other than percents) are in the thousands.**

Here are the first five entries of the table.

.. code-block:: python3

    unemployment.head()

What, roughly, was the highest level the U.S. unemployment rate (measured as Percent Unemployed of Labor Force in the table) reached in:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:math:`1.` The 20th century?

.. code-block:: python3

    unemployment.sort_values('Percent Unemployed\nof\nlabor\nforce', ascending=False)
    1982

:math:`2.` The past fifty years?

.. code-block:: python3

    1982
    un2=unemployment[unemployment["Year"]>=1964]
    un2.sort_values('Percent Unemployed\nof\nlabor\nforce', ascending=False)

:math:`3.` The twenty years before 2006?

.. code-block:: python3

    1992
    un3=unemployment[39:59]
    un3.sort_values("Percent Unemployed\nof\nlabor\nforce", ascending=False)

:math:`4.` Given your answers to (1) through (3), Do you think there is
a connection between your answer to the question above and the fact that
Federal Reserve Chair Alan Greenspan received a five-minute standing
ovation at the end of the first of many events marking his retirement in
2005?

ANSWER:

The State of the Labor Market
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:math:`1.` About how many people lose or quit their jobs in an average
year?

.. code-block:: python3

    unemployment

:math:`2.` About how many people get jobs in an average year?

.. code-block:: python3

    average_getters = ___

:math:`3.` About how many people are unemployed in an average year?

.. code-block:: python3

    average_unemployed = ___

:math:`4.` About how many people are at work in an average year?

.. code-block:: python3

    average_workers = ___

:math:`5.` About how many people are unemployed now?

.. code-block:: python3

    unemployed_now = ___

National Income Accounting:
^^^^^^^^^^^^^^^^^^^^^^^^^^^

:math:`1.` What was the level of real GDP in 2005 dollars in 1970?

.. code-block:: python3

    quarterly_acc.loc[90:98]


:math:`2.` What was the rate of inflation in the United States in 2000?

.. code-block:: python3

    quarterly_acc.loc[211:215]

:math:`3.` Explain whether or not, how, and why the following items are
included in the calculation of GDP: (i) rent you pay on an apartment,
(ii) purchase of a used textbook, (iii) purchase of a new tank by the
Department of Defense, (iv) watching an advertisement on youtube.

ANSWER:

Congratulations, you have finished your first assignment for Econ 101B!
Run the cell below to submit all of your work. Make sure to check on OK
to make sure that it has uploaded.

Some materials this notebook were taken from `Data
8 <http://data8.org/>`__, `CS 61A <http://cs61a.org/>`__, and `DS
Modules <http://data.berkeley.edu/education/modules>`__ lessons.

--------------

 

Introduction: Python and Economics 
------------------------------------

Catch Our Breath—Further Notes:
===============================


.. figure:: /_static/skitch.png


-  weblog support:
   https://github.com/braddelong/LS2019/blob/master/Introduction-Math-Tools-%26-Economics-delong.ipynb
-  nbViewer:
   https://nbviewer.jupyter.org/github/braddelong/LS2019/blob/master/Introduction-Math-Tools-%26-Economics-delong.ipynb
-  datahub:
   http://datahub.berkeley.edu/user-redirect/interact?account=braddelong&repo=LS2019&branch=master&path=Introduction-Math-Tools-%26-Economics-delong.ipynb

 

--------------

https://www.icloud.com/keynote/0yKJfOMN5SvDtK_K7tjWAstcA

https://www.typepad.com/site/blogs/6a00e551f08003883400e551f080068834/post/6a00e551f0800388340240a4a488c4200d/edit

https://nbviewer.jupyter.org/github/braddelong/weblog-support/blob/master/2017-08-30%20%28More%20than%20a%29%20Few%20Words%20About%20%22Computer%20Literacy%22%20in%20the%20Twenty-First%20Century....ipynb
