# Anomaly-Detection-for-Business-Metrics-with-R

The details of the codeset and plots are included in the attached Microsoft Word Document (.docx) file in this repository. 
You need to view the file in "Read Mode" to see the contents properly after downloading the same.

AnomalyDetection Package - A Brief Introduction
================================================

AnomalyDetection is an open-source R package to detect anomalies which is robust, from a statistical standpoint, in the presence of seasonality and an underlying trend. The AnomalyDetection package can be used in wide variety of contexts. For example, detecting anomalies in system metrics after a new software release, user engagement post an A/B test, or for problems in econometrics, financial engineering, political and social sciences.

How the package works:
=====================
The underlying algorithm – referred to as Seasonal Hybrid ESD (S-H-ESD) builds upon the Generalized ESD test for detecting anomalies. Note that S-H-ESD can be used to detect both global as well as local anomalies. This is achieved by employing time series decomposition and using robust statistical metrics, viz., median together with ESD. In addition, for long time series (say, 6 months of minutely data), the algorithm employs piecewise approximation - this is rooted to the fact that trend extraction in the presence of anomalies in non-trivial - for anomaly detection.Besides time series, the package can also be used to detect anomalies in a vector of numerical values. We have found this very useful as many times the corresponding timestamps are not available. The package provides rich visualization support. The user can specify the direction of anomalies, the window of interest (such as last day, last hour), enable/disable piecewise approximation; additionally, the x- and y-axis are annotated in a way to assist visual data analysis.
How to get started

Install the R package using the following commands on the R console:

    library(AnomalyDetection)

The function AnomalyDetectionTs is called to detect one or more statistically significant anomalies in the input time series. The documentation of the function AnomalyDetectionTs, which can be seen by using the following command, details the input arguments and the output of the function AnomalyDetectionTs.

    help(AnomalyDetectionTs)

The function AnomalyDetectionVec is called to detect one or more statistically significant anomalies in a vector of observations. The documentation of the function AnomalyDetectionVec, which can be seen by using the following command, details the input arguments and the output of the function AnomalyDetectionVec.

    help(AnomalyDetectionVec)

A simple example

To get started, the user is recommended to use the example dataset which comes with the packages. Execute the following commands:

    data(raw_data)
    res = AnomalyDetectionTs(raw_data, max_anoms=0.02, direction='both', plot=TRUE)
    res$plot

![image](https://user-images.githubusercontent.com/26252963/149072415-798d55f2-5121-42d1-8592-25934a9e825f.png)



From the plot, we observe that the input time series experiences both positive and negative anomalies. Furthermore, many of the anomalies in the time series are local anomalies within the bounds of the time series’ seasonality (hence, cannot be detected using the traditional approaches). The anomalies detected using the proposed technique are annotated on the plot. In case the timestamps for the plot above were not available, anomaly detection could then carried out using the AnomalyDetectionVec function; specifically, one can use the following command:

    AnomalyDetectionVec(raw_data[,2], max_anoms=0.02, period=1440, direction='both', only_last=FALSE, plot=TRUE)

Often, anomaly detection is carried out on a periodic basis. For instance, at times, one may be interested in determining whether there was any anomaly yesterday. To this end, we support a flag only_last whereby one can subset the anomalies that occurred during the last day or last hour. Execute the following command:

    res = AnomalyDetectionTs(raw_data, max_anoms=0.02, direction='both', only_last=”day”, plot=TRUE)
    res$plot

![image](https://user-images.githubusercontent.com/26252963/149072495-5b07f799-46c2-4012-90f0-edb63b011f40.png)


From the plot, we observe that only the anomalies that occurred during the last day have been annotated. Further, the prior six days are included to expose the seasonal nature of the time series but are put in the background as the window of prime interest is the last day.

Anomaly detection for long duration time series can be carried out by setting the longterm argument to T.
