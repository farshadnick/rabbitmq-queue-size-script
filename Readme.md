# Queue Monitor Script
This script analyzes and displays information about various queues, focusing on key metrics like **queue name** , **body size** , and **number of occurrences**. The data can be used to monitor and troubleshoot different system queues effectively.
Key Features

- Queue Name Identification: Lists the names of all queues being tracked.
- Body Size Reporting: Shows the size of each queue's payload, enabling better optimization and management.
- Queue Count Tracking: Tracks the number of times each queue appears, helping identify high-traffic or problematic queues.

## Use Cases

- System Monitoring: Keep track of queue behavior and identify bottlenecks or errors quickly.
- Performance Optimization: Gain insights into queue sizes and usage patterns to optimize system performance.
- Debugging and Troubleshooting: Spot specific queues with large body sizes or frequent occurrences that may require attention

## Queue Monitor Script Output

| Body Size (MB) | Queue Name                          | Number of Occurrences |
|----------------|-------------------------------------|-----------------------|
| 0.00017        | flightAPI_error_handling            | 1                     |
| 0.00031        | customerData_fetch_failure          | 2                     |
| 0.00048        | reservationUpdate_error             | 3                     |
| 0.00064        | paymentReconciliation_timeout       | 4                     |
| 0.00111        | externalServiceAPI_timeout          | 7                     |
| 0.00175        | transferService_sync_issue          | 11                    |
| 0.00319        | scheduled-signal_Moghim_error       | 1781                  |
| 1.19097        | PaymentPartPaidEventHandler         | 4946                  |
| 3.12527        | agent-search-request_NiraVR_error   | 4594                  |
| 64.2401        | Alibaba.GL.Api.Error_Queue          | 13329                 |



## How to Use

  - give this repository a Start :)
  - change Rabbit-address and user & pass in script

```
curl -u USERNAME:PASSWORD http://YOUR_RABBIT_ADDR:15672/api/queues/%2f?columns=name,messages,message_bytes,consumers |  jq -r '.[] | select(.consumers == 0 and .message_bytes > 0) | { name: .name, messages: .messages, message_bytes_mb: (.message_bytes / 1048576) } | [.message_bytes_mb, .name, .messages] | @tsv'   | sort -n
```
