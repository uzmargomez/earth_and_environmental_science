# MISCADA – Earth & Environment specialisation 

## Assessment Uzmar Gomez (hgft79)

1. Describe how you would approach the analysis of a discrete time series (e.g. daily average air temperature) in such a way as to forecast for several time periods ahead.

    **Answer**

    In class we reviewed the ARIMA model, which is mainly used for time series forecasting. 

    I would start by defining if I am expecting to have a seasonality component in my time series. In the example provided, it can be the case that the average temperature decreases or rises depending on the time of the year, so it's important to take this into account. This would modify my approach a little bit, since I would require to use an extension of ARIMA that supports the direct modeling of a seasonal component called SARIMA.

    Let's suppose we do not have a seasonal component, ARIMA requires us to define 3 different variables, the autoregression order $p$, the difference order $d$ and the moving average order $q$. 

    In order to get a good approximation to my real values, I will try to use a grid search method. First of all, I would divide my dataset in training and testing, then I would define a way of calculating the error, like the Root Mean Squared Error, and basically I would introduce a range of values for my different parameters (p,d,q) for which the training and testing sets get the minimum error (comparing the true data with the prediction given by ARIMA) while checking if the method does not present overfitting using the test set. Once my model has a good enough error, I would use it to forecast for a range of months. I would also take care of not forecasting too ahead in time, since the prediction will surely be worse than for shorter periods.

    In the case of SARIMA, I would need to specify four other parameters that account for the seasonal component of the algorithm.


3.  * Explain what is meant by the terms "forward model", "linear forward model" and "non-linear forward model".  
    * Classify each of the following forward models as either linear or non-linear. Explain your reasoning in each case.  
        -  The pressure of a fixed volume of gas is modelled as a function of temperature, $P(T)=\alpha T$. You may assume $\alpha$ is a constant. 
        - The volume of a gas is modelled as a function of both pressure and temperature, $V(P,T)=\alpha\frac{T}{P}+\beta$. You may assume $\alpha$ and $\beta$ are constants. 
        - A data set is represented by two vectors $(\vec{x},\vec{y})$ respectively containing the $x$- and $y$- coordinates of the data points. It is modelled as a quadratic, $\vec{y}(a_0,a_1,a_2)=a_0 +a_1\vec{x}+a_2\vec{x}^2$. 
    * Why are non-linear inverse problems generally more challenging to solve than linear inverse problems? 

    **Answer**

    * A forward problem is one that gives you the complete specification of a system, all the properties, and one just has work out how it responds using a certain rule or given theory. A linear forward model has the following form

        $$\vec{g}\left(\alpha\vec{m}_1+\beta\vec{m}_2\right)=\alpha\vec{g}\left(\vec{m}_1\right)+\beta\vec{g}\left(\vec{m}_2\right)$$

        or equivalently  $\vec{g}\left(\vec{m}\right)=G\vec{m}$ where $G$ is a matrix.

        A non linear forward model cannot be represented by a linear operator or by a linear matrix.

    * - This is a linear forward model, since $\alpha$ is a constant we have 

        $$P(\gamma T_1+\beta T_2)=\alpha (\gamma T_1+\beta T_2)=\alpha\gamma T_1+\alpha\beta T_2=\gamma P(T_1) +\beta P(T_2)$$
    
      - This is a non linear problem, since 

        $$V(\gamma P_1+\eta P_2,T)=\alpha\frac{T}{\gamma P_1+\eta P_2}+\beta\neq\alpha\frac{T}{\gamma P_1}+\alpha\frac{T}{\eta P_2}+\beta$$
      
      - This is a linear problem, since the variables in this case are $a_0$, $a_1$ and $a_2$, and we can find a matrix that represents the transformation

        $$\vec{y}=[(1,x_1,\vec{x}^2),(1,x_2,\vec{x}^2),(1,x_3,\vec{x}^2)](a_0,a_1,a_2)$$

    * The difference between a non-linear and a linear inverse problem is that the operator that describes the relation for the non-linear problem is non-linear, and the linear inverse problem has a linear operator. The non-linear inverse problem would be an issue since it would require the solution of a partial differential equation. Also, it could cause the misfit function to be non-convex, or to have multiple minima, which would complicate finding the global minima resulting on falling on a local minima. There are ways of overcoming this difficulties, like using the Metropolis-Hasting's Algorithm to compare the performance of a "bag" of models and iteratively improve our selection.

4. A particular forward model has the form $\vec{g}(\vec{m})=G\vec{m}$, where $G$ is a matrix and $m$ is a vector. The agreement between model predictions and a vector of observations, $d$, is measured using an L2 misfit, $\phi(\vec{m})=||\vec{d}-\vec{G}\vec{m}||_2^2$.  
    * By differentiating this misfit with respect to an arbitrary model parameter, show that the optimal (best-fitting) model is given by $\vec{m}=(G^TG)^{-1}G^T \vec{d}$.  
    * Explain what is meant by ‘regularisation’, and why it may be necessary.

    **Answer**

    * Having 

        $$\phi(\vec{m})=||\vec{d}-\vec{G}\vec{m}||_2^2=\sum_i\left(d_i-G_{ij}m_j\right)^2$$

        $$\Rightarrow\frac{\partial\phi}{\partial m_k}=\sum_i 2\left(d_i-G_{ij}m_j\right)\frac{\partial\left(G_{ij}m_j\right)}{\partial m_k}$$

        $$\Rightarrow\frac{\partial\phi}{\partial m_k}=\sum_i 2\left(d_i-G_{ij}m_j\right)G_{ij}\frac{\partial m_j}{\partial m_k} = \sum_i 2\left(d_i-G_{ij}m_j\right)G_{ij}\delta_{jk} $$

        $$\Rightarrow \frac{\partial\phi}{\partial m_k} =2\left(d_i-G_{ij}m_j\right)G_{ik}$$

        In the last equation and in what follows I'm using the Einstein notation for indexes to avoid issues with notation

        $$\Rightarrow \frac{\partial\phi}{\partial m_k} =2d_iG_{ik}-2G_{ij}G_{ik}m_j$$

        In the minimum $\frac{\partial\phi}{\partial m_k}=0, \forall k$, so

        $$d_iG_{ik}=G_{ij}G_{ik}m_j\Rightarrow G_{ik}d_i=G^T_{ji}G_{ik}m_j\Rightarrow m_j =\left(G^T_{ji}G_{ik}\right)^{-1} G^T_{ki}d_i$$

        which in vector notation gives $\vec{m}=(G^TG)^{-1}G^T \vec{d}$

    * The regularization is a penalization for a model that gives some information for the model.

        Usually we add it to the misfit $\phi$ as a term $J(\vec{m})=\epsilon^2\vec{m}^T\vec{m}$. It is a tradeoff parameter that balances fitting the data against keeping the model small enough. 
 
8. Discuss, giving examples, methods of image classification that can be applied to remote sensed data.

    **Answer**

    The remote sense images are obtained using a range of spectral bands that map a certain spectrum to a given element (rocks, water, etc.). For a given raster image, if we want to classify the elements that are present in  it, we need to classify these different elements and there are different methods: the unsupervised classification based on pixels (which analizes each pixel of a certain image), the supervised classification based on pixels (which takes more time than the unsupervised method, but may be more precise), the deep learning approximation (that allows us to extract features out of the images) and the supervised classification based on objects (which analyzes a set of pixels and the relations between them that create an object).

    There are many benefits and drawbacks for each one of this methods, and we need to consider why are we using them and what do we expect from them when choosing a given method. First of all, we need to consider which kind of image we have, if the resolution is appropiate for the model we want to use, if we have time to train a deep learning classifier or if we need to use a different approach that doesn't consume too much time, like the supervised classification based on pixels.