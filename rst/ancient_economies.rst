
A Solow-Malthus Approach to Modeling the Pre-Industrial Economy
----------------------------------------------------------------

The Solow Model 
~~~~~~~~~~~~~~~~~

In the standard Solow growth model, total output and income Y is:

   (1) :math:`Y = (\kappa)^\theta E L`

where :math:`E` is the efficiency of labor, :math:`L` is the labor force,
:math:`\kappa`  is the capital-output ratio
:math:`\kappa = K/L`, and the parameter :math:`\theta` 
is a transform of the more usual Cobb-Douglas constant-returns-to-scale
:math:`\alpha` , with :math:`\theta =
\alpha / (1 - \alpha )`. Along this model’s
steady-state growth path:

   (2) :math:`Y^* = \left(\kappa^* \right)^\theta E L`

with :math:`\kappa^\*` equal to the quotient of the
savings-investment share :math:`s` and the investment requirements :math:`n + g +
\delta` , which are the sum of the labor-force growth rate
:math:`n`, the efficiency-of-labor growth rate :math:`g`, and the depreciation
rate :math:`\delta` : :math:`\kappa`^\* = s/(n + g +
\delta )`. With :math:`\kappa`  taken as the state
variable, for constant :math:`s, n, g` and :math:`\delta`, this
model economy converges exponentially to its steady state according to:

   (3) :math:`\frac{d\kappa}{dt} = - (1-\alpha)(n+g+\delta)(\kappa - \kappa^*)`

Malthusianism: Resource Scarcity, Population, and the Efficiency of Labor 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now let’s make the model Malthusian:

(a) Let’s make efficiency-of-labor growth :math:`g` a function of the rate
    :math:`h` at which economically useful ideas are generated, but also of
    the rate of population and labor force growth :math:`n`, because a
    higher population makes resources per capita scarce, as determined
    by an effect-of-resource scarcity parameter :math:`\gamma`:

..

   (4) :math:`\frac{1}{E} \frac{dE}{dt} = \frac{d\ln(E)}{dt} = g = h - \frac{n}{\gamma}`

(b) Let’s make the rate of growth of the population and labor force
    depend on the level of prosperity :math:`y = Y/L`; on the “subsistence”
    standard of living for necessities :math:`y^{sub}`; and also on the
    fraction :math:`1/\phi` of production that is devoted to
    necessities, not conveniences and luxuries, and thus enters into
    reproductive and survival fitness:

..

   (5) :math:`\frac{1}{L} \frac{dL}{dt} = \frac{d\ln(L)}{dt} = n = \beta \left( \frac{y}{\phi y^{sub}}-1 \right)`

At high levels of income per worker, we get the “demographic
transition”: population growth then does not speed up but slows down as
prsoperity increases, because women learn to read, acquire social power,
and begin to use artificial means of birth control for family planning.
But neglect that for now.

 

Malthusian Equilibrium 
~~~~~~~~~~~~~~~~~~~~~~~~

We search for a *Malthusian* equilibrium in which the
efficiency-of-labor growth rate :math:`g = g^{*mal} = 0`. That then
requires that:

   (6) :math:`n^{*mal} = \gamma h`

which in its turn requires that:

   (7) :math:`y^{*mal} = \phi y^{sub} \left( 1 + \frac{ \gamma h}{\beta}\right)`

Since it is also the case that:

   (8) :math:`y^{*mal} = \left( \frac{s}{n + g +\delta} \right)^\theta E^{*mal} = \left( \frac{s}{\gamma h +\delta} \right)^\theta E^{*mal}`

and:

   (9) :math:`E = \frac{H}{L^\gamma}`

We can solve for the labor force :math:`L` as a function of the ideas stock
:math:`H` and the parameters of the model:

   (10) :math:`\ln(\phi) + \ln\left( y^{sub} \right) + \ln\left(1 + \frac{\gamma h}{\beta} \right) = \theta \ln(s) - \theta \ln(\gamma h +\delta) + \ln(E^{*mal})`

..

   (11) :math:`\ln(y^{sub}) =
        \theta \ln(s) -
        \theta \ln(\gamma h
        +\delta) + \ln(H) -
        \frac{\ln(L)}{\gamma} -
        \ln(\phi) -
        \ln\left(1 +
        \frac{\gamma h}{\beta} \right)`

   (12) :math:`\frac{\ln(L)}{\gamma} = \theta \ln(s) - \theta \ln(\gamma h +\delta) + \ln(H) - \ln(\phi) - \ln( y^{sub}) -ln\left(1 + \frac{\gamma h}{\beta} \right)`

Thus the population and labor force in the full Malthusian equilibrium
will be:

   (13) :math:`\ln(L^{*mal}) = \gamma \left[ \theta \ln(s) - \theta \ln(\gamma h +\delta) + \ln(H) - \ln(\phi) - \ln( y^{sub}) -ln\left(1 + \frac{\gamma h}{\beta} \right) \right]`

It might be worthwhile decomposing this into terms depending on: (1) the
level and rate of growth of the stock of *ideas*; (2) the rule of law,
which creates social peace, induces thrift, and thus drives up
investment; (3) luxuries, including urbanization, elite consumption, and
destruction to maintain order; and (4) demography, in the form of
sociological (and law-and-order) determinants of “subsistence”:

   (38) :math:`\ln(L^{*mal}) = \gamma \left[ \ln(H) - \theta \ln(\gamma h +\delta) -ln\left(1 + \frac{\gamma h}{\beta} \right) \right] + \gamma \left[ \theta \ln(s) \right] - \gamma \left[ \ln(\phi) \right] - \gamma \left[ \ln( y^{sub}) \right]`

As time passes and knowledge increases, the population and labor would
will grow in proportion. And other changes in society that shifted the
parameters would raise or lower the Malthusian equilibrium path of the
economy.

The Malthusian equilibrium level of population is:

-  raised by increases in the level of economically-useful knowledge
   :math:`H_t`
-  raised by increases in the importance :math:`\theta` of capital
   accumulation for production
-  raised by increases in the share of production saved and invested
   :math:`s`
-  lowered by increases in the rate of depreciation
   :math:`\delta` , in the rate of increase of knowledge :math:`h`,
   and in the parameter :math:`\gamma`  capturing how much
   resource scarcity reduces the efficiency of labor :math:`E`
-  lowered by an increase in the wedge :math:`\phi` between prosperity
   and subsistence created by spending on luxuries and conveniences
   (middle-class luxuries that do not affect reproduction, but also the
   “luxury” of having an upper class, and the additional luxuries of
   living in cities and having trade networks that can spread plagues).
-  lowered by an increase in basic biological subsistence requirements
   :math:`y^{sub}` (produced by, say, Western European marriage patterns
   or lineage-family control of reproduction by clan heads).
-  lowered by an increase in the wedge :math:`\gamma h / \beta` between
   basic subsistence and spending on necessities needed to generate
   population growth consonant with the advance of knowledge and
   population pressure’s generation of resource scarcity.

In response to shocks that were to change the Malthusian equilibrium
path, the economy would then converge to the new, changed equilibrium.

There are no easy formulas for the speed with which it would converge,
however…

 

A Python Jupyter Notebook file for simulations of this Malthusian model
is available on Github at:
https://github.com/braddelong/LS2019/blob/master/2019-08-17-Ancient_Economies.ipynb

 

--------------

Modeling a Pre-Industrial Economy 
-----------------------------------

Catch Our Breath—Further Notes:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. figure:: /_static/skitch.png


-  Weblog Support
   https://github.com/braddelong/LS2019/blob/master/2019-09-06-210a-ancient-intro.ipynb
-  nbViewer
   https://nbviewer.jupyter.org/github/braddelong/LS2019/blob/master/2019-09-06-210a-ancient-intro.ipynb

 
