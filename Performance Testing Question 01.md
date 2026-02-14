Section 1 — Performance Testing, Testing Types & NFR (25 Q&A)
Q1. What is performance testing and why is it important?
A1. Performance testing measures a system's responsiveness, stability, scalability, and resource usage under expected workload. It's important because it verifies that applications meet SLA/NFRs, identifies bottlenecks before production, and ensures a good user experience. Example: Running a load test to validate that an e‑commerce checkout responds under 500 simultaneous users within 2 seconds.
Q2. Name and define the common types of performance testing.
A2. Load Testing (expected load), Stress Testing (beyond capacity), Spike Testing (sudden large increases), Endurance/Soak Testing (long-duration), Scalability Testing (behaviour as load grows), Volume Testing (large data volumes). Example: Spike test adding 1,000 users in 30 seconds to observe failure modes.
Q3. What is an NFR and give examples relevant to performance?
A3. Non-Functional Requirements specify system qualities, not functions. For performance: max response time (e.g., 95th percentile < 800ms), throughput (e.g., 500 requests/sec), concurrency (2,000 concurrent users), availability (99.95%), and resource utilization thresholds (CPU < 80%).
Q4. How do you convert business requirements into a workload model?
A4. Identify user journeys, peak/off-peak patterns, concurrency, think times, and transaction mix. Map business KPIs (orders/hour) to virtual users and pacing. Example: If peak is 3,600 orders/hour and each user performs 1 order per 2 minutes → ~120 concurrent ordering users; include browsing users too.
Q5. What's the difference between throughput, latency, and concurrency?
A5. Throughput = transactions/sec (system capacity). Latency = time to process a request (response time). Concurrency = number of simultaneous active users/requests. All three together describe system performance.
Q6. Define SLA, SLO, and KPI and how they relate.
A6. SLA (Service Level Agreement) is a contractual promise (e.g., 99.9% uptime). SLO (Service Level Objective) is an internal target (e.g., p95 latency < 500ms). KPI (Key Performance Indicator) measures health (e.g., error rate). Testing ensures SLOs are met to satisfy SLAs and KPIs.
Q7. Why percentiles (p90/p95/p99) matter more than averages?
A7. Averages hide outliers. Percentiles show the experience of the slowest X% of users. E.g., average = 200ms but p95 = 2,000ms means 5% of users had very poor experience; addressing p95 helps UX.
Q8. What is baseline testing and why do it?
A8. Baseline testing captures current performance metrics under a known configuration to compare against future changes. Use baseline before optimizations, deployments, or environment changes.
Q9. Describe capacity planning in performance testing.
A9. Capacity planning estimates resources required to meet forecasted loads. Steps: collect workload data, model growth, run tests at projected loads, and recommend infrastructure scaling (vertical/horizontal). Example: predicting DB read replicas needed for 2× expected traffic in holiday season.
Q10. How do you design a soak (endurance) test and what does it reveal?
A10. Run sustained load at expected or slightly higher than expected levels for many hours/days. Monitor memory, handles, connection pools, and performance degradation to detect leaks and resource exhaustion. Example: 72-hour test at 70% peak load to find memory leaks.
Q11. What are think-times and pacing; how to choose values?
A11. Think-time simulates user delays between actions. Pacing controls iterations per user to match throughput. Choose values from production logs or real-user monitoring. Example: average browsing think time = 12s; use sampling to model variety.
Q12. What is workload mix and why is it important?
A12. Workload mix defines the percentage of different transactions (search 40%, checkout 10%). It's critical because different transactions impose different load patterns on subsystems (DB vs CDN). Incorrect mix gives misleading results.
Q13. How do you handle third-party dependencies in tests?
A13. Options: use service virtualization/mocks, record and replay responses, or include real third-party endpoints with rate limiting. Example: mock payment gateway to simulate latency and error codes during stress tests.
Q14. What is spike testing and a typical scenario?
A14. Spike testing introduces sudden large increases in traffic to observe system behavior (auto-scaling, throttling). Example: flash-sale promotion driving 10× traffic for a minute — check autoscaler reaction and queuing/backpressure.
Q15. How do you validate test environment parity with production?
A15. Compare hardware specs, network bandwidth/latency, DB size, config/properties, and middleware versions. If exact parity isn't possible, document differences and adjust expectations (scale results mathematically where reasonable).
Q16. What is a performance test plan and its key components?
A16. Components: objectives, scope, test environment, workload model, test data, scripts, metrics, schedule, pass/fail criteria, risks, and test runbook. This ensures repeatable, auditable testing.
Q17. How to create reusable test data for performance tests?
A17. Use parameterization (CSV), data generators, and cleanup scripts. Ensure uniqueness for transactional tests (user IDs, order IDs). For DB-heavy tests, snapshot/clone production subsets.
Q18. What is negative performance testing?
A18. Testing how system behaves with invalid data, extreme inputs, or failing components (database down, high latency). Reveals graceful degradation, error rates, and recovery behavior.
Q19. How do you include security or auth flows in performance scripts?
A19. Parameterize user creds, handle token refresh (correlate JWT/session tokens), and simulate realistic auth patterns. Example: use OAuth token endpoints with proper caching to avoid token-server overload.
Q20. How to measure and report business-impacting metrics?
A20. Map tech metrics to business KPIs: failed checkouts → revenue loss, p95 latency → conversion rate drop. Include cost-of-downtime estimates and recommend mitigation steps in reports.
Q21. What is the role of APM tools during tests?
A21. APMs (New Relic, Dynatrace) provide code-level traces, DB calls, external calls, and latency breakdowns — essential for root-cause analysis during load tests.
Q22. How to test for scalability?
A22. Run tests with increasing load (linear, step) and observe throughput vs response time. Scalability is indicated by near-linear throughput increase and acceptable latency. Also test horizontal scaling (add nodes) to verify behavior.
Q23. How do you ensure tests are reproducible?
A23. Use infrastructure-as-code, version-controlled scripts, fixed datasets or snapshots, and document exact runtime settings. Tag results with environment, build, and config metadata.
Q24. What are common performance testing mistakes?
A24. Testing in GUI mode, not monitoring servers, unrealistic workloads, ignoring network constraints, lack of baseline, not validating results, and poor data setup. Avoid these by following best practices and run small smoke-load tests first.
Q25. How to present performance test findings to stakeholders?
A25. Summarize objectives, environment, key metrics (p50/p95/p99, throughput, errors), bottlenecks, business impact, prioritized recommendations, and action items. Use visuals — percentile charts, CPU/DB charts — and an executive summary.
