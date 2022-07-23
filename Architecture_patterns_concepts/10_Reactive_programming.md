# Reactive programming

1. Flexible, loosely-coupled, scalable
2. Responsive - rapid and consistent response and quality
3. Resilient - system should remain responsive in case of random failures (replication, isolation)
4. Elastic - remain responsive under unpredictable workloads (cost-efective stability)
5. Message-driven - rely on asynchronous message passing between components
6. Reactive system is a result of specific architectural style
7. Reactive programming is a programming paradigm where the focus is on developing asynchronous and
non-blocking components. Data stream, that we observe and react to, even apply back pressure.
This leads to non-blocking execution and better scalability with fewer threads.
8. Reactive streams - server does not send the complete stream at once - as soon as element is ready 
for processing it pushes it to client - client waits less time to receive and process events.
9. Blocking calls - database calls, calls to web services, file system calls.