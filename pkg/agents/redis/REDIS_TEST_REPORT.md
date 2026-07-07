# Redis Agentic Copilot Test Report



## Application

E-commerce Dataset



## Key Schema



### user:* (hash)

Fields:

- name

- email

- age

- status



### cache:product:* (string)

Fields (JSON):

- id

- name

- price



### cart:user:* (set)

Members: product references



### wishlist:user:* (set)

Members: product references



### order_queue (list)

Items: order IDs



### high_score_buyers (zset)

Scores: user purchase totals



### purchase_stream (stream)

Fields: user_id, amount, timestamp



## Test Cases



### Test 1: Redis Connection

PASS



### Test 2: Data Seeding (9 keys, 6 data types)

PASS



### Test 3: MCP Server — Tool Registration (11 tools)

PASS



### Test 4: MCP Tool — discover_schema

Query: Scan keyspace and group by pattern

Output: 7 patterns discovered

PASS



### Test 5: MCP Tool — inspect_key

Query: Inspect hash key user:1

Output: type=hash, fields=[name, email, age, status]

PASS



### Test 6: MCP Tool — get (string key)

Query: Get cache:product:101

Output: Sleek Laptop, price=999.99

PASS



### Test 7: MCP Tool — hgetall (hash key)

Query: Get all fields of user:1

Output: name=Alice Smith, email=alice@example.com

PASS



### Test 8: MCP Tool — smembers (set key)

Query: Get cart:user:1 members

Output: cache:product:101, cache:product:102

PASS



### Test 9: MCP Tool — lrange (list key)

Query: Get order_queue items

Output: order:9001, order:9002

PASS



### Test 10: MCP Tool — zrange (sorted set)

Query: Get high_score_buyers with scores

Output: user:2(450), user:1(1500)

PASS



### Test 11: MCP Tool — xrange (stream)

Query: Get purchase_stream entries

Output: 2 stream entries

PASS



### Test 12: MCP Tool — scan_keys

Query: Scan keys matching user:*

Output: user:1, user:2

PASS



### Test 13: Read-Only Safety — SET blocked

PASS



### Test 14: Read-Only Safety — DEL blocked

PASS



### Test 15: Read-Only Safety — FLUSHDB blocked

PASS



### Test 16: MCP Client Integration (stdio protocol)

Query: hgetall user:2 via MCP client

Output: name=Bob Jones

PASS



### Test 17: File Structure Validation (17/17 files)

PASS



## Conclusion

All 49 tests passed.

Redis connection, data seeding, MCP server tools (11 tools), read-only safety guards, MCP client integration (stdio protocol round-trip), and file structure are all verified and working correctly.
