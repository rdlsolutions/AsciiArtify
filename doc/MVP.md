#  Demo ArgoCD 
Logs AMBASSADOR


2024-04-25 20:15:16 kubewatch [24 TMainThread] 0.51.2 INFO: kubewatch starting: mode 'cluster-id' ambassador_config_dir '/no/such/path' envoy_config_file '/dev/null' debug 'False' delay '1.0' pid 'None'
2024-04-25 20:15:16 kubewatch [24 TMainThread] 0.51.2 INFO: namespace demo, watching just this namespace
2024-04-25 20:15:16 kubewatch [24 TMainThread] 0.51.2 ERROR: couldn't read namespace demo? (403)
Reason: Forbidden
HTTP response headers: HTTPHeaderDict({'Audit-Id': '0d438288-69af-495e-a906-d132884f0b60', 'Cache-Control': 'no-cache, private', 'Content-Type': 'application/json', 'X-Content-Type-Options': 'nosniff', 'X-Kubernetes-Pf-Flowschema-Uid': 'c9874009-dc33-43a5-be1e-4f95df79c80c', 'X-Kubernetes-Pf-Prioritylevel-Uid': 'dc45cbae-f922-487b-809b-a593eeb32037', 'Date': 'Thu, 25 Apr 2024 20:15:16 GMT', 'Content-Length': '319'})
HTTP response body: {"kind":"Status","apiVersion":"v1","metadata":{},"status":"Failure","message":"namespaces \"demo\" is forbidden: User \"system:serviceaccount:demo:ambassador\" cannot get resource \"namespaces\" in API group \"\" in the namespace \"demo\"","reason":"Forbidden","details":{"name":"demo","kind":"namespaces"},"code":403}
2024-04-25 20:15:16 kubewatch [24 TMainThread] 0.51.2 INFO: cluster ID is 07eb43c8-1166-5145-a060-45e4dd907e10 (from hardcoded ID)
AMBASSADOR: using cluster ID 07eb43c8-1166-5145-a060-45e4dd907e10
AMBASSADOR: starting ads
AMBASSADOR: starting diagd
AMBASSADOR: pinging diagd (10)...
time="2024-04-25T20:15:16Z" level=info msg="Ambex 0.1.1 starting..."
time="2024-04-25T20:15:16Z" level=info msg=Listening port=18000
time="2024-04-25T20:15:16Z" level=info msg="Wrote PID" file=ambex.pid pid=41
time="2024-04-25T20:15:16Z" level=info msg="Pushing snapshot v0"
AMBASSADOR: pinging diagd (9)...
AMBASSADOR: pinging diagd (8)...
2024-04-25 20:15:22 diagd 0.51.2 [P42TMainThread] INFO: thread count 25, listening on 0.0.0.0:8877
[2024-04-25 20:15:22 +0000] [42] [INFO] Starting gunicorn 19.9.0
[2024-04-25 20:15:22 +0000] [42] [INFO] Listening at: http://0.0.0.0:8877 (42)
[2024-04-25 20:15:22 +0000] [42] [INFO] Using worker: threads
[2024-04-25 20:15:22 +0000] [61] [INFO] Booting worker with pid: 61
2024-04-25 20:15:22 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: starting event watcher
AMBASSADOR: pinging diagd (7)...
AMBASSADOR: diagd running
+ set +x
+ kubewatch --namespace demo --sync 'python3 /ambassador/post_update.py' --warmup-delay 10s secrets services
AMBASSADOR: waiting
PIDS: 41:ambex 42:diagd 66:kubewatch
2024/04/25 20:15:34 SYNC: python3 /ambassador/post_update.py http://localhost:38981/api/snapshot/1
2024-04-25 20:15:35 diagd 0.51.2 [P61TThreadPoolExecutor-0_0] INFO: Update requested from http://localhost:38981/api/snapshot/1
2024-04-25 20:15:35 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: copying configuration from http://localhost:38981/api/snapshot/1 to /ambassador/snapshots/snapshot-tmp.yaml
2024-04-25 20:15:36 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: successfully validated the resulting envoy configuration, continuing...
2024-04-25 20:15:36 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: rotating snapshots for snapshot 1
2024-04-25 20:15:36 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: saving Envoy configuration for snapshot 1
2024-04-25 20:15:36 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: running 'sh /ambassador/kick_ads.sh 41'
KICK: started Envoy as PID 99
KICK: kicking ambex
2024-04-25 20:15:36 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: configuration updated
2024-04-25 20:15:36 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: starting Envoy status updater
time="2024-04-25T20:15:36Z" level=info msg="Loaded file /ambassador/envoy/envoy.json"
time="2024-04-25T20:15:36Z" level=info msg="Pushing snapshot v1"
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:203] initializing epoch 0 (hot restart version=10.200.16384.127.options=capacity=16384, num_slots=8209 hash=228984379728933363 size=2654312)
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:205] statically linked extensions:
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:207]   access_loggers: envoy.file_access_log,envoy.http_grpc_access_log
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:210]   filters.http: envoy.buffer,envoy.cors,envoy.ext_authz,envoy.fault,envoy.filters.http.header_to_metadata,envoy.filters.http.jwt_authn,envoy.filters.http.rbac,envoy.grpc_http1_bridge,envoy.grpc_json_transcoder,envoy.grpc_web,envoy.gzip,envoy.health_check,envoy.http_dynamo_filter,envoy.ip_tagging,envoy.lua,envoy.rate_limit,envoy.router,envoy.squash
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:213]   filters.listener: envoy.listener.original_dst,envoy.listener.proxy_protocol,envoy.listener.tls_inspector
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:216]   filters.network: envoy.client_ssl_auth,envoy.echo,envoy.ext_authz,envoy.filters.network.dubbo_proxy,envoy.filters.network.rbac,envoy.filters.network.sni_cluster,envoy.filters.network.thrift_proxy,envoy.http_connection_manager,envoy.mongo_proxy,envoy.ratelimit,envoy.redis_proxy,envoy.tcp_proxy
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:218]   stat_sinks: envoy.dog_statsd,envoy.metrics_service,envoy.stat_sinks.hystrix,envoy.statsd
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:220]   tracers: envoy.dynamic.ot,envoy.lightstep,envoy.tracers.datadog,envoy.zipkin
[2024-04-25 20:15:37.022][000099][info][main] [source/server/server.cc:223]   transport_sockets.downstream: envoy.transport_sockets.alts,envoy.transport_sockets.capture,raw_buffer,tls
[2024-04-25 20:15:37.023][000099][info][main] [source/server/server.cc:226]   transport_sockets.upstream: envoy.transport_sockets.alts,envoy.transport_sockets.capture,raw_buffer,tls
[2024-04-25 20:15:37.035][000099][info][main] [source/server/server.cc:268] admin address: 127.0.0.1:8001
[2024-04-25 20:15:37.102][000099][info][config] [source/server/configuration_impl.cc:50] loading 0 static secret(s)
[2024-04-25 20:15:37.102][000099][info][config] [source/server/configuration_impl.cc:56] loading 1 cluster(s)
[2024-04-25 20:15:37.117][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:132] cm init: initializing cds
[2024-04-25 20:15:37.120][000099][info][config] [source/server/configuration_impl.cc:61] loading 0 listener(s)
[2024-04-25 20:15:37.120][000099][info][config] [source/server/configuration_impl.cc:94] loading tracing configuration
[2024-04-25 20:15:37.120][000099][info][config] [source/server/configuration_impl.cc:112] loading stats sink configuration
[2024-04-25 20:15:37.121][000099][info][main] [source/server/server.cc:456] starting main dispatch loop
[2024-04-25 20:15:37.193][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:496] add/update cluster cluster_127_0_0_1_8877 during init
[2024-04-25 20:15:37.210][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:496] add/update cluster cluster_go_demo_app_api during init
[2024-04-25 20:15:37.222][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:496] add/update cluster cluster_go_demo_app_ascii during init
[2024-04-25 20:15:37.234][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:496] add/update cluster cluster_go_demo_app_front during init
[2024-04-25 20:15:37.267][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:496] add/update cluster cluster_go_demo_app_img during init
[2024-04-25 20:15:37.269][000099][info][upstream] [source/common/upstream/cluster_manager_impl.cc:136] cm init: all clusters initialized
[2024-04-25 20:15:37.269][000099][info][main] [source/server/server.cc:428] all clusters initialized. initializing init manager
[2024-04-25 20:15:37.397][000099][info][upstream] [source/server/lds_api.cc:80] lds: add/update listener 'ambassador-listener-80'
[2024-04-25 20:15:37.398][000099][info][config] [source/server/listener_manager_impl.cc:908] all dependencies initialized. starting workers
2024-04-25 20:15:37 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: Scout reports {"latest_version": "1.14.4", "application": "ambassador", "cached": false, "timestamp": 1714076137.955351}
2024-04-25 20:15:37 diagd 0.51.2 [P61TAmbassadorEventWatcher] INFO: Scout notices: [{"level": "INFO", "message": "Upgrade available! to Ambassador version 1.14.4"}]
ACCESS [2024-04-25T20:16:23.362Z] "GET / HTTP/1.1" 200 - 0 18 4 1 "10.244.0.238" "curl/7.81.0" "260421b3-3073-4299-ab44-bffc5d08c42f" "localhost:8877" "10.109.184.171:80"
ACCESS [2024-04-25T20:18:41.154Z] "POST /img/ HTTP/1.1" 503 UC 915 57 6 - "10.244.0.238" "curl/7.81.0" "cc72131d-83f9-42ef-9a1f-816c79da5144" "localhost:8877" "10.108.17.29:80"
ACCESS [2024-04-25T20:22:29.090Z] "POST /img/ HTTP/1.1" 503 UC 915 57 7 - "10.244.0.238" "curl/7.81.0" "63e92076-2699-4e9a-b10a-7a33f214836b" "localhost:8877" "10.108.17.29:80"
ACCESS [2024-04-25T20:26:10.658Z] "POST /img/ HTTP/1.1" 503 UC 916 57 9 - "10.244.0.238" "curl/7.81.0" "d5987daa-2758-4024-84ce-7e533554ff5c" "localhost:8877" "10.108.17.29:80"
ACCESS [2024-04-25T20:27:40.904Z] "POST /img/ HTTP/1.1" 503 UC 916 57 7 - "10.244.0.238" "curl/7.81.0" "f5bcaba6-eb21-4628-8659-2cfc7eeb92c7" "localhost:8877" "10.108.17.29:80"
ACCESS [2024-04-25T20:28:07.469Z] "POST /img/ HTTP/1.1" 503 UF 916 57 1 - "10.244.0.238" "curl/7.81.0" "f080771f-2050-4f17-87e5-dfed9e6f021c" "localhost:8877" "10.108.17.29:80"
ACCESS [2024-04-25T20:29:45.668Z] "POST /img/ HTTP/1.1" 503 UC 916 57 7 - "10.244.0.238" "curl/7.81.0" "705d21be-31e5-4fbc-ba7f-c0a5c3926851" "127.0.0.1:8877" "10.108.17.29:80"
[2024-04-25 20:30:37.298][000099][info][main] [source/server/drain_manager_impl.cc:63] shutting down parent after drain



![alt text](656415.gif)

