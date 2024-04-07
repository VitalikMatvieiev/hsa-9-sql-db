# Indexes comparing
1. **B-tree index** | condition `WHERE DateOfBirth BETWEEN  '2018-03-27'  AND  '2018-04-29';` \
*Without index:* \
`37276  row(s) fetched - 12s (0.059s fetch), on  2024-04-05  at  17:47:57` \
*With index:* \
`37276  row(s) fetched - 6s (0.053s fetch), on  2024-04-05  at  17:47:03` \
2. **B-tree index** | condition `WHERE DateOfBirth = '2018-03-27';` \
*Without index:* \
`1171  row(s) fetched - 12s (0.001s fetch), on  2024-04-05  at  21:14:42` \
*With index:* \
`1171  row(s) fetched - 0.016s (0.001s fetch), on  2024-04-05  at  21:17:15` \
3. **Hash  index** | condition `WHERE DateOfBirth BETWEEN  '2018-03-27'  AND  '2018-04-29'`; \
*Without index:* \
`37276  row(s) fetched - 12s (0.059s fetch), on  2024-04-05  at  17:47:57` \
*With index:* \
`37276  row(s) fetched - 7s (0.041s fetch), on  2024-04-05  at  17:53:52` \
4. **Hash  index** | condition `WHERE DateOfBirth = '2018-03-27';`; \
*Without index:* \
`1171  row(s) fetched - 12s (0.001s fetch), on  2024-04-05  at  17:55:19` \
*With index:* \
`1171  row(s) fetched - 0.281s, on  2024-04-05  at  17:54:46` \

# innodb_flush_log_at_trx_commit comparing
## innodb_flush_log_at_trx_commit = 0;

### First test (ab -c  50  -t  3  http://localhost:5219/generate)
- Time: 3 seconds
- Number of Records: 5349, 4426

### Second Test (ab -c  50  -t  8  http://localhost:5219/generate)
- Time: 8 seconds
- Number of Records: 13863, 15068

## innodb_flush_log_at_trx_commit = 1;
### First test (ab -c  50  -t  3  http://localhost:5219/generate)
- Time: 3 seconds
- Number of Records: 3857, 3974

### Second Test (ab -c  50  -t  8  http://localhost:5219/generate)
- Time: 8 seconds
- Number of Records: 9981, 9582
## innodb_flush_log_at_trx_commit = 2;
### First test (ab -c  50  -t  3  http://localhost:5219/generate)
- Time: 3 seconds
- Number of Records: 4517, 4167

### Second Test (ab -c  50  -t  8  http://localhost:5219/generate)
- Time: 8 seconds
- Number of Records: 12942, 11553
