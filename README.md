# Web-robot-detection-using-LSTM
Web robot detection based on Log access Pattern recognition using LSTM

# BackGroung
According to a recent survey, 37.2% of all internet users were robots in 2020. It consists of 13.1% of good bots and 24.1% of bad bots. And bad bots considered malicious usually threaten the security and privacy of web applications and users.<br>

In this project, the workflow pipeline which was proposed in the "DeepLog: Anomaly Detection and Diagnotics from System Logs" was applied to web robot detection by using the URL access pattern. The core assumption of the model in this project is that humans leave log records through URLs of similar related topics, but robots will repeat the standardized pattern regardless of the subject. For that reasons, we can determine the presence or absence of robots by capturing the uri access pattern which has been made by various web bots.
# Dataset
We used the web robot server log open data posted on ZENODE. This dataset includes server logs from search engines in libraries and information centers at the University of Aristotle of Thessaloniki in Greece (http://search.lib.auth.gr/).

# Methology
## Method1 : log key and parameter
All log entries were divided by key values and parameters. Key values are log bodies excluding specific values, and parameters are variable values that enter values. By parsing the log entries through the log parser, all logs are divided into log key and parameter value vector. In this step, value of the parameter vector is time difference between the current log and previous log. Two different models are trained with the order of log key values and the sequence of parameter values based on unique ip. When the new log entry generated, the log key is checked against pretrained log key anomaly detection model to see if there’s any anomaly. If not anomaly, it will further check this parameter value vector against parameter value anomaly detection model for that log key to see if there’s any anomaly happens. After checking through two different models, it will discern the ip's identity to access the website.<br>

To sum up, in our team project, we define the log entry as the combination of log key value whose column name is “request” and the parameter value for time difference between the current log and previous log.


## Method2 : Window size
In our model the window size is one of the most important hyperparameter. The above image is example of window size. In our project, we set window size 10.
After selecting the window size as 10, the encoded sequence of the log key and paramter whose length is 10 is generated. We use this sequence data sets with 10 length vector as input for LSTM model and predict the 11th log key and parameter value.

# result
model1 using LSTM<br>
loss: 0.3739 - accuracy: 0.8763 - val_loss: 0.3370 - val_accuracy: 0.8871<br><br>

model2 using LSTM<br>
loss: 0.0917 - accuracy: 0.9913 - val_loss: 0.1309 - val_accuracy: 0.9843<br><br>

Final accuracy in test set
2205it [1:22:03,  2.23s/it]<br>
elapsed_time: 4923.481s<br>
total : 72573<br>
accuracy : 90.975057<br>




