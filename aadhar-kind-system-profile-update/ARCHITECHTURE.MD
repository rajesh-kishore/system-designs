### High Level Estimations

| Metric                        | Calculation                                                                 | Result                  |
|-------------------------------|-----------------------------------------------------------------------------|-------------------------|
| Profile Update Requests       | 10 million requests per day                                                 | ~100 requests/sec       |
| Direct Update Requests        | 20% of total requests                                                       | 20 requests/sec         |
| Approval Requests             | 80% of total requests                                                       | 80 requests/sec         |
| Storage for Attachments       | 8 million requests * 25 MB * 2 uploads                                      | 400,000 GB/day          |
| Storage with Replication      | 400,000 GB/day * replication factor of 3                                     | 1,200,000 GB/day        |
| Request Metadata Storage      | 10 million requests * 1 KB                                                  | 10,000 GB/day           |
| Metadata Storage with Replication | 10,000 GB/day * replication factor                                        | 10,000 GB/day * replication factor |

### High Level Profile Update Flow
![Profile Update Flow](./flow-profile-update.svg)