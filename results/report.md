# Assignment 2:

## Create a stacked bar chart decomposing total latency into: Network RTT, Init Duration, and Handler Duration — for zip cold start, container cold start, and warm invocations.

![Assignment 2 Bar Chart](assignment_2_bar_chart.png)

## Estimate Network RTT as the difference between client-side total latency (from oha) and server-side time (Init Duration + Handler Duration from CloudWatch).

| Metric | Zip Cold Start | Container Cold Start | Warm Invocation (Avg) |
| :--- | :--- | :--- | :--- |
| **Client-side Total Latency** | 2056.30 ms | 1775.60 ms | 224.30 ms |
| **CloudWatch Init Duration** | 625.12 ms | 610.03 ms | 0.00 ms |
| **CloudWatch Handler Duration**| 90.37 ms | 72.14 ms | 75.00 ms |
| **Calculated Network RTT** | 1340.81 ms | 1093.43 ms | 149.30 ms |

Network RTT = Total Latency - (Init Duration + Handler Duration)


## Comment on whether zip or container cold starts are faster, and explain why.
Container cold start performed faster than Zip deployment. First successful execution was ~280ms faster than the Zip deployment.

#### Why are Containers faster?
- Lambda doesn’t download the whole container image. It only loads the parts needed to start, which makes startup faster.
- Common parts of the image (like the OS or runtime) may already be stored on the server, so they don’t need to be downloaded again.