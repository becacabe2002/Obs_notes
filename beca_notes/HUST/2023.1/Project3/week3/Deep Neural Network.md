> [!info] Neural Network/Artificial Neural Network
> loosely connected  models with flexible structures and large parameter space.

* NN are composed of three types of layer:
	* **Input Layer**: direct data, which will be processed by the network
	* **Hidden Layers**: their inputs and outputs are not directly visible. In these layers, the model gains the ability to recognize patterns in the data, updating its parameters (weights) during training based on the input data.
	* **Output Layer**: return the final result of the network's operation.

* ==-> Learn which aspects of the input data affect the final processing result without manually extracting features from the data. (Better feature extraction)==

![[Pasted image 20231010094545.png]]

## Key Concepts and Terminology

* An input is received by input neurons in the input layer, and the information then goes through the synapse connection to the hidden layers.
* Each neuron inside a hidden layer has a connection to another node in another layer.
	* When neuron receive data -> Send with additional information to the connected neuron. (which is dissected within node)
	* The amount of information (**weight**) sent is determined by [**Mathematical activation function**]([Activation functions in Neural Networks - GeeksforGeeks](https://www.geeksforgeeks.org/activation-functions-neural-networks/)) of that neuron (0<= ... <= 1).
	* Each layer has a bias, also calculated as part of activation function.
	* The output of activation function is input of the next hidden layer, util go to the output layer.
* The output in the output layer will be 0 or 1 to answer the question or make the prediction.

> [!info] Deep Neural Network (DNN)
> A type of neural network with **multiple** layers .
> A fundamental component of **deep learning**.

* Each of hidden layers performs different types of specific sorting and categorization called "***feature hierarchy***"
	* Each layer captures increasingly abstract and complex features from the raw input data.

## How can DNNs be used in transportation risk assessment?

* **Predict Risks of Late Delivery**: [Machine Learning Techniques for Predicting Risks of Late Delivery](https://doi.org/10.1007/978-981-99-0741-0_25) 
	* Analyze historical data using hybrid technique: Logistic Regression, XGBoost, Light GBM, and Random Forest
	-> Accuracy, specificity, precision, and F1-score

* **Build predictive models for proactively respond to delivery risk in supply chain**: [Development of Predictive Models for Order Delivery Risk in a Supply Chain: A Machine Learning Approach](http://dx.doi.org/10.1007/978-981-19-6945-4_43)
	* Apply machine learning algorithms to build a predictive model for identifying late delivery risks.
	* Analyze comparatively with specific performance metrics (receiver operator characteristics, precision, recall, and F1-score) to identify the best predictive model for the delivery risk prediction problem.

* **Propose directions for future confluence of SCRM (supply chain risk management) and AI**: [Supply Chain Risk Management and Artificial Intelligence: State of the Art and Future Research Directions](http://dx.doi.org/10.1080/00207543.2018.1530476)
	* Investigate on various definitions and classifications of supply chain risk and related notions.
	* Categorise existing literature according to the used AI methodology (ML, Big Data Analytics) and the specific SCRM task they address (indentification, assessment or response)

* **Minimized delivery time by shipping products in advance**: [Shortening Delivery Times by Predicting Customer's Online Purchases](http://dx.doi.org/10.24251/HICSS.2020.159)
	* Develop a prediction model for predicting customer's online purchase so that retailers can shipping products in advance.
	* Combination of different forecasting methods and K-means clustering to test if (and how early) it is possible to predict online purchases.

* **Route Selection**: [A Multi Parametric Route Selection Algorithm For Delay Minimization Using Machine Learning in VANET](https://doi.org/10.21203/rs.3.rs-2027736/v1)
	* Most of the VANET's make use of fixed schedule vehicles for reliable data delivery.
		* Public vehicles with multiple stoppages -> add significant delay
	* To obtaine less data delivery delay, higher route's reliability: 
		* **heterogeneous vehicle nodes** (không đồng nhất): Vehicles either has fixed route or dynamic routes
		* Storage buffers in major traffic junctions: keep the data for shorter time duration.
		* Discover optimal routes