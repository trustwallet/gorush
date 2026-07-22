---
category: architecture
confidence: low
documentType: explanation
scope: repo
contentHash: 07b765addeac
tags: [architecture, service]
source: architecture/call-graph.md
verified: 2026-07-22
splitPartIndex: 1
splitPartTotal: 2
canonical: true
---

## Call Graph
<!-- sdd-knowledge-generated -->

> Deterministic call graph extracted via tree-sitter (no LLM). Direct calls are resolved by lexical scope + imports; **dynamic dispatch and ambiguous name matches are withheld** rather than guessed. The `## Calls` table is `EXTRACTED` (a single resolved target). Member calls (`obj.method()`) whose method name resolves to exactly one definition repo-wide are recovered separately under `## Inferred calls` (`INFERRED` — receiver type unverified, but a single plausible target).

## Calls

| Caller | Callee | Example args | Sites |
|--------|--------|--------------|-------|
| `GetLogPushEntry` | `hideToken(token: string, markLen: int): string` | `(input.Token, 10)` | 1 |
| `GetLogPushEntry` | `typeForPlatForm(platform: int): string` | `(input.Platform)` | 1 |
| `InitLog` | `SetLogLevel(log: *logrus.Logger, levelString: string): error` | `(LogAccess, accessLevel)` | 2 |
| `InitLog` | `SetLogOut(log: *logrus.Logger, outString: string): error` | `(LogAccess, accessLog)` | 2 |
| `LogPush` | `colorForPlatForm(platform: int): string` | `(input.Platform)` | 1 |
| `LogPush` | `GetLogPushEntry(input: *InputLog): LogPushEntry` | `(input)` | 1 |
| `main` | `createPIDFile(cfg: *config.ConfYaml): error` | `(cfg)` | 1 |
| `main` | `pinger(cfg: *config.ConfYaml): error` | `(cfg)` | 1 |
| `main` | `withContextFunc(ctx: context.Context, f: func()): context.Context` | `(…, func() { logx.LogAccess.Info("close th)` | 1 |
| `GetIOSNotification` | `iosAlertDictionary(payload: *payload.Payload, req: *PushNotification): *payload.Payload` | `(payload, req)` | 1 |
| `InitAPNSClient` | `configureHTTP2ConnHealthCheck(h2Transport: *http2.Transport)` | `(h2Transport)` | 1 |
| `InitAPNSClient` | `newApnsClient(cfg: *config.ConfYaml, certificate: tls.Certificate): (*apns2.Client, error)` | `(cfg, certificateKey)` | 1 |
| `InitAPNSClient` | `newApnsTokenClient(cfg: *config.ConfYaml, token: *token.Token): (*apns2.Client, error)` | `(cfg, token)` | 1 |
| `newApnsClient` | `configureHTTP2ConnHealthCheck(h2Transport: *http2.Transport)` | `(h2Transport)` | 1 |
| `newApnsTokenClient` | `configureHTTP2ConnHealthCheck(h2Transport: *http2.Transport)` | `(h2Transport)` | 1 |
| `PushToIOS` | `getApnsClient(cfg: *config.ConfYaml, req: *PushNotification): (client *apns2.Client)` | `(cfg, req)` | 1 |
| `PushToIOS` | `GetIOSNotification(req: *PushNotification): *apns2.Notification` | `(req)` | 1 |
| `PushToIOS` | `logPush(cfg: *config.ConfYaml, status: string, req: *PushNotification, err: error): logx.LogPushEntry` | `(cfg, core.FailedPush, token, req, err)` | 2 |
| `PushToAndroid` | `GetAndroidNotification(req: *PushNotification): *fcm.Message` | `(req)` | 1 |
| `PushToAndroid` | `InitFCMClient(cfg: *config.ConfYaml, key: string): (*fcm.Client, error)` | `(cfg, req.APIKey)` | 2 |
| `PushToAndroid` | `logPush(cfg: *config.ConfYaml, status: string, req: *PushNotification, err: error): logx.LogPushEntry` | `(cfg, core.FailedPush, req.To, req, err)` | 7 |
| `PushToAndroid` | `CheckMessage(req: *PushNotification): error` | `(req)` | 1 |
| `InitHMSClient` | `GetPushClient(conf: *c.Config): (*client.HMSClient, error)` | `(conf)` | 2 |
| `PushToHuawei` | `logPush(cfg: *config.ConfYaml, status: string, req: *PushNotification, err: error): logx.LogPushEntry` | `(cfg, core.FailedPush, req.To, req, err)` | 1 |
| `PushToHuawei` | `GetHuaweiNotification(req: *PushNotification): (*model.MessageRequest, error)` | `(req)` | 1 |
| `PushToHuawei` | `InitHMSClient(cfg: *config.ConfYaml, appSecret: string): (*client.HMSClient, error)` | `(cfg, cfg.Huawei.AppSecret, cfg.Huawei.AppID)` | 1 |
| `PushToHuawei` | `CheckMessage(req: *PushNotification): error` | `(req)` | 1 |
| `SendNotification` | `DispatchFeedback(log: logx.LogPushEntry, url: string, timeout: int64): error` | `(l, cfg.Core.FeedbackURL, cfg.Core.FeedbackTimeout)` | 1 |
| `SendNotification` | `PushToIOS(req: *PushNotification, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(v, cfg)` | 1 |
| `SendNotification` | `PushToAndroid(req: *PushNotification, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(v, cfg)` | 1 |
| `SendNotification` | `PushToHuawei(req: *PushNotification, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(v, cfg)` | 1 |
| `RunHTTPServer` | `routerEngine(cfg: *config.ConfYaml, q: *queue.Queue): *gin.Engine` | `(cfg, q)` | 1 |
| `RunHTTPServer` | `startServer(ctx: context.Context, s: *http.Server, cfg: *config.ConfYaml): error` | `(ctx, …, cfg)` | 2 |
| `RunHTTPServer` | `autoTLSServer(cfg: *config.ConfYaml, q: *queue.Queue): *http.Server` | `(cfg, q)` | 1 |
| `RunHTTPServer` | `routerEngine(cfg: *config.ConfYaml, q: *queue.Queue): *gin.Engine` | `(cfg, q)` | 1 |
| `startServer` | `listenAndServe(ctx: context.Context, s: *http.Server, cfg: *config.ConfYaml): error` | `(ctx, s, cfg)` | 1 |
| `startServer` | `listenAndServeTLS(ctx: context.Context, s: *http.Server, cfg: *config.ConfYaml): error` | `(ctx, s, cfg)` | 1 |
| `appStatusHandler` | `GetVersion(): string` | `()` | 1 |
| `autoTLSServer` | `routerEngine(cfg: *config.ConfYaml, q: *queue.Queue): *gin.Engine` | `(cfg, q)` | 1 |
| `handleNotification` | `markFailedNotification(cfg: *config.ConfYaml, notification: *notify.PushNotification, reason: string): []logx.LogPushEntry` | `(cfg, notification, "max capacity reached")` | 1 |
| `pushHandler` | `abortWithError(c: *gin.Context, code: int, message: string)` | `(c, http.StatusBadRequest, msg)` | 3 |
| `pushHandler` | `handleNotification(ctx: context.Context, cfg: *config.ConfYaml, req: notify.RequestPush, q: *queue.Queue): (int, []logx.LogPushEntry)` | `(ctx, cfg, form, q)` | 1 |
| `routerEngine` | `appStatusHandler(q: *queue.Queue): gin.HandlerFunc` | `(q)` | 1 |
| `routerEngine` | `configHandler(cfg: *config.ConfYaml): gin.HandlerFunc` | `(cfg)` | 1 |
| `routerEngine` | `pushHandler(cfg: *config.ConfYaml, q: *queue.Queue): gin.HandlerFunc` | `(cfg, q)` | 1 |
| `routerEngine` | `StatMiddleware(): gin.HandlerFunc` | `()` | 1 |
| `routerEngine` | `sysStatsHandler(): gin.HandlerFunc` | `()` | 1 |
| `routerEngine` | `VersionMiddleware(): gin.HandlerFunc` | `()` | 1 |
| `versionHandler` | `GetVersion(): string` | `()` | 1 |
| `RunGRPCServer` | `NewServer(cfg: *config.ConfYaml): *Server` | `(cfg)` | 1 |

## Callers (reverse)

| Symbol | Called by |
|--------|-----------|
| `abortWithError` | `pushHandler` |
| `appStatusHandler` | `routerEngine` |
| `autoTLSServer` | `RunHTTPServer` |
| `CheckMessage` | `PushToAndroid`, `PushToHuawei` |
| `colorForPlatForm` | `LogPush` |
| `configHandler` | `routerEngine` |
| `configureHTTP2ConnHealthCheck` | `InitAPNSClient`, `newApnsClient`, `newApnsTokenClient` |
| `createPIDFile` | `main` |
| `DispatchFeedback` | `SendNotification` |
| `GetAndroidNotification` | `PushToAndroid` |
| `getApnsClient` | `PushToIOS` |
| `GetHuaweiNotification` | `PushToHuawei` |
| `GetIOSNotification` | `PushToIOS` |
| `GetLogPushEntry` | `LogPush` |
| `GetPushClient` | `InitHMSClient` |
| `GetVersion` | `appStatusHandler`, `versionHandler` |
| `handleNotification` | `pushHandler` |
| `hideToken` | `GetLogPushEntry` |
| `InitFCMClient` | `PushToAndroid` |
| `InitHMSClient` | `PushToHuawei` |
| `iosAlertDictionary` | `GetIOSNotification` |
| `listenAndServe` | `startServer` |
| `listenAndServeTLS` | `startServer` |
| `logPush` | `PushToAndroid`, `PushToHuawei`, `PushToIOS` |
| `markFailedNotification` | `handleNotification` |
| `newApnsClient` | `InitAPNSClient` |
| `newApnsTokenClient` | `InitAPNSClient` |
| `NewServer` | `RunGRPCServer` |
| `pinger` | `main` |
| `pushHandler` | `routerEngine` |
| `PushToAndroid` | `SendNotification` |
| `PushToHuawei` | `SendNotification` |
| `PushToIOS` | `SendNotification` |
| `routerEngine` | `RunHTTPServer`, `autoTLSServer` |
| `SetLogLevel` | `InitLog` |
| `SetLogOut` | `InitLog` |
| `startServer` | `RunHTTPServer` |
| `StatMiddleware` | `routerEngine` |
| `sysStatsHandler` | `routerEngine` |
| `typeForPlatForm` | `GetLogPushEntry` |
| `VersionMiddleware` | `routerEngine` |
| `withContextFunc` | `main` |

## Inferred calls (member, unique name)

> `INFERRED` (confidence 0.9): `obj.method()` where `method` resolves to exactly one definition repo-wide. Receiver type is not resolved; common method names (init/update/onCreate) remain withheld as ambiguous. Use SCIP (`--scip`) for type-resolved member calls at full certainty.

| Caller | Callee | Example args | Sites |
|--------|--------|--------------|-------|
| `GetLogPushEntry` | `Error(args: interface{})` | `()` | 1 |
| `InitLog` | `Error(args: interface{})` | `()` | 4 |
| `LogPush` | `Error(args: interface{})` | `(output)` | 1 |
| `LogPush` | `Info(args: interface{})` | `(output)` | 1 |
| `createPIDFile` | `Errorf(format: string, args: interface{})` | `("can't create PID folder on %v", err)` | 4 |
| `main` | `LoadConf(confPath: string): (*ConfYaml, error)` | `(configFile)` | 1 |
| `main` | `Queue` | `(cfg.Queue.Engine)` | 1 |
| `main` | `Error(args: interface{})` | `()` | 1 |
| `main` | `Fatal(args: interface{})` | `(err)` | 11 |
| `main` | `Fatalf(format: string, args: interface{})` | `("can't load log module, error: %v", err)` | 3 |
| `main` | `Info(args: interface{})` | `("close the queue system, current queue u, …)` | 2 |
| `main` | `QueueLogger(): DefaultQueueLogger` | `()` | 4 |
| `main` | `InitLog(accessLevel: string): error` | `(cfg.Log.AccessLevel, cfg.Log.AccessLog, cfg.Log.ErrorLevel, cfg.Log.ErrorLog)` | 1 |
| `main` | `InitAPNSClient(cfg: *config.ConfYaml): error` | `(cfg)` | 2 |
| `main` | `PushToIOS(req: *PushNotification, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(req, cfg)` | 1 |
| `main` | `InitFCMClient(cfg: *config.ConfYaml, key: string): (*fcm.Client, error)` | `(cfg, cfg.Android.APIKey)` | 1 |
| `main` | `PushToAndroid(req: *PushNotification, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(req, cfg)` | 1 |
| `main` | `InitHMSClient(cfg: *config.ConfYaml, appSecret: string): (*client.HMSClient, error)` | `(cfg, cfg.Huawei.AppSecret, cfg.Huawei.AppID)` | 1 |
| `main` | `PushToHuawei(req: *PushNotification, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(req, cfg)` | 1 |
| `main` | `CheckMessage(req: *PushNotification): error` | `(req)` | 3 |
| `main` | `CheckPushConf(cfg: *config.ConfYaml): error` | `(cfg)` | 1 |
| `main` | `SetProxy(proxy: string): error` | `(cfg.Core.HTTPProxy)` | 1 |
| `main` | `PrintGoRushVersion()` | `()` | 1 |
| `main` | `SetVersion(ver: string)` | `(Version)` | 1 |
| `main` | `RunGRPCServer(ctx: context.Context, cfg: *config.ConfYaml): error` | `(ctx, cfg)` | 1 |
| `main` | `InitAppStatus(conf: *config.ConfYaml): error` | `(cfg)` | 4 |
| `pinger` | `Errorf(format: string, args: interface{})` | `("server returned non-200 status code")` | 1 |
| `GetIOSNotification` | `Sound` | `(result)` | 3 |
| `GetIOSNotification` | `Alert` | `(req.Message)` | 1 |
| `InitAPNSClient` | `Error(args: interface{})` | `()` | 9 |
| `logPush` | `LogPush(input: *InputLog): LogPushEntry` | `(…)` | 1 |
| `PushToAndroid` | `Error(args: interface{})` | `()` | 6 |
| `PushToAndroid` | `IsTopic(): bool` | `()` | 3 |
| `PushToAndroid` | `Send(ctx: context.Context, in: *proto.NotificationRequest): (*proto.NotificationReply, error)` | `(notification)` | 1 |
| `GetHuaweiNotification` | `Error(args: interface{})` | `()` | 2 |
| `PushToHuawei` | `Error(args: interface{})` | `()` | 6 |
| `CheckMessage` | `IsTopic(): bool` | `()` | 1 |
| `SendNotification` | `Error(args: interface{})` | `(err)` | 1 |
| `SendNotification` | `Bytes(): []byte` | `()` | 1 |
| `RunHTTPServer` | `Info(args: interface{})` | `(…)` | 1 |
| `RunHTTPServer` | `Error(args: interface{})` | `("Failed to load https cert file: ", err)` | 7 |
| `RunHTTPServer` | `Info(args: interface{})` | `("httpd server is disabled.")` | 2 |
| `handleNotification` | `IsLocalQueue(q: Queue): bool` | `(…)` | 2 |
| `handleNotification` | `Queue` | `(cfg.Queue.Engine)` | 3 |
| `handleNotification` | `Error(args: interface{})` | `(err)` | 1 |
| `handleNotification` | `SendNotification(req: queue.QueuedMessage, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(msg, cfg)` | 1 |
| `markFailedNotification` | `Error(args: interface{})` | `(reason)` | 1 |
| `markFailedNotification` | `GetLogPushEntry(input: *InputLog): LogPushEntry` | `(…)` | 1 |
| `routerEngine` | `NewMetrics(c: func() int): Metrics` | `(func() int { return q.Usage() })` | 1 |
| `main` | `Fatalf(format: string, args: interface{})` | `("did not connect: %v", err)` | 1 |
| `main` | `NewGrpcHealthClient(conn: *grpc.ClientConn): Health` | `(conn)` | 1 |
| `main` | `Fatalf(format: string, args: interface{})` | `("did not connect: %v", err)` | 1 |
| `main` | `Send(ctx: context.Context, in: *proto.NotificationRequest): (*proto.NotificationReply, error)` | `(…, …)` | 1 |
| `main` | `Alert` | `()` | 1 |
| `Check` | `Error(args: interface{})` | `(codes.NotFound, "unknown service")` | 1 |
| `RunGRPCServer` | `Info(args: interface{})` | `("gRPC server is disabled.")` | 3 |
| `Send` | `Error(args: interface{})` | `(err)` | 1 |
| `Send` | `SendNotification(req: queue.QueuedMessage, cfg: *config.ConfYaml): (resp *ResponsePush, err error)` | `(…, s.cfg)` | 1 |
| `InitAppStatus` | `Error(args: interface{})` | `("storage error: can't find storage drive)` | 3 |
| `InitAppStatus` | `Info(args: interface{})` | `("Init App Status Engine as ", conf.Stat.Engine)` | 1 |
| `AddAndroidError` | `setBadger(key: string, count: int64)` | `(storage.AndroidErrorKey, total)` | 1 |
| `AddAndroidSuccess` | `setBadger(key: string, count: int64)` | `(storage.AndroidSuccessKey, total)` | 1 |
| `AddHuaweiError` | `setBadger(key: string, count: int64)` | `(storage.HuaweiErrorKey, total)` | 1 |
| `AddHuaweiSuccess` | `setBadger(key: string, count: int64)` | `(storage.HuaweiSuccessKey, total)` | 1 |
| `AddIosError` | `setBadger(key: string, count: int64)` | `(storage.IosErrorKey, total)` | 1 |
| `AddIosSuccess` | `setBadger(key: string, count: int64)` | `(storage.IosSuccessKey, total)` | 1 |
| `AddTotalCount` | `setBadger(key: string, count: int64)` | `(storage.TotalCountKey, total)` | 1 |
| `GetAndroidError` | `getBadger(key: string, count: *int64)` | `(storage.AndroidErrorKey, …)` | 1 |
| `GetAndroidSuccess` | `getBadger(key: string, count: *int64)` | `(storage.AndroidSuccessKey, …)` | 1 |
| `getBadger` | `Error(args: interface{})` | `()` | 1 |
| `GetHuaweiError` | `getBadger(key: string, count: *int64)` | `(storage.HuaweiErrorKey, …)` | 1 |
| `GetHuaweiSuccess` | `getBadger(key: string, count: *int64)` | `(storage.HuaweiSuccessKey, …)` | 1 |
| `GetIosError` | `getBadger(key: string, count: *int64)` | `(storage.IosErrorKey, …)` | 1 |
| `GetIosSuccess` | `getBadger(key: string, count: *int64)` | `(storage.IosSuccessKey, …)` | 1 |
| `GetTotalCount` | `getBadger(key: string, count: *int64)` | `(storage.TotalCountKey, …)` | 1 |
| `Reset` | `setBadger(key: string, count: int64)` | `(storage.TotalCountKey, 0)` | 7 |
| `setBadger` | `Error(args: interface{})` | `()` | 1 |
| `AddAndroidError` | `setBoltDB(key: string, count: int64)` | `(storage.AndroidErrorKey, total)` | 1 |
| `AddAndroidSuccess` | `setBoltDB(key: string, count: int64)` | `(storage.AndroidSuccessKey, total)` | 1 |
| `AddHuaweiError` | `setBoltDB(key: string, count: int64)` | `(storage.HuaweiErrorKey, total)` | 1 |
| `AddHuaweiSuccess` | `setBoltDB(key: string, count: int64)` | `(storage.HuaweiSuccessKey, total)` | 1 |
| `AddIosError` | `setBoltDB(key: string, count: int64)` | `(storage.IosErrorKey, total)` | 1 |
| `AddIosSuccess` | `setBoltDB(key: string, count: int64)` | `(storage.IosSuccessKey, total)` | 1 |
| `AddTotalCount` | `setBoltDB(key: string, count: int64)` | `(storage.TotalCountKey, total)` | 1 |
| `GetAndroidError` | `getBoltDB(key: string, count: *int64)` | `(storage.AndroidErrorKey, …)` | 1 |
| `GetAndroidSuccess` | `getBoltDB(key: string, count: *int64)` | `(storage.AndroidSuccessKey, …)` | 1 |
| `getBoltDB` | `Error(args: interface{})` | `()` | 1 |
| `GetHuaweiError` | `getBoltDB(key: string, count: *int64)` | `(storage.HuaweiErrorKey, …)` | 1 |
| `GetHuaweiSuccess` | `getBoltDB(key: string, count: *int64)` | `(storage.HuaweiSuccessKey, …)` | 1 |
| `GetIosError` | `getBoltDB(key: string, count: *int64)` | `(storage.IosErrorKey, …)` | 1 |
| `GetIosSuccess` | `getBoltDB(key: string, count: *int64)` | `(storage.IosSuccessKey, …)` | 1 |
| `GetTotalCount` | `getBoltDB(key: string, count: *int64)` | `(storage.TotalCountKey, …)` | 1 |
| `Reset` | `setBoltDB(key: string, count: int64)` | `(storage.TotalCountKey, 0)` | 7 |
| `setBoltDB` | `Error(args: interface{})` | `()` | 1 |
| `AddAndroidError` | `setBuntDB(key: string, count: int64)` | `(storage.AndroidErrorKey, total)` | 1 |
| `AddAndroidSuccess` | `setBuntDB(key: string, count: int64)` | `(storage.AndroidSuccessKey, total)` | 1 |
| `AddHuaweiError` | `setBuntDB(key: string, count: int64)` | `(storage.HuaweiErrorKey, total)` | 1 |
| `AddHuaweiSuccess` | `setBuntDB(key: string, count: int64)` | `(storage.HuaweiSuccessKey, total)` | 1 |
| `AddIosError` | `setBuntDB(key: string, count: int64)` | `(storage.IosErrorKey, total)` | 1 |
| `AddIosSuccess` | `setBuntDB(key: string, count: int64)` | `(storage.IosSuccessKey, total)` | 1 |
| `AddTotalCount` | `setBuntDB(key: string, count: int64)` | `(storage.TotalCountKey, total)` | 1 |
| `GetAndroidError` | `getBuntDB(key: string, count: *int64)` | `(storage.AndroidErrorKey, …)` | 1 |
| `GetAndroidSuccess` | `getBuntDB(key: string, count: *int64)` | `(storage.AndroidSuccessKey, …)` | 1 |
| `getBuntDB` | `Error(args: interface{})` | `()` | 1 |
| `GetHuaweiError` | `getBuntDB(key: string, count: *int64)` | `(storage.HuaweiErrorKey, …)` | 1 |
| `GetHuaweiSuccess` | `getBuntDB(key: string, count: *int64)` | `(storage.HuaweiSuccessKey, …)` | 1 |
| `GetIosError` | `getBuntDB(key: string, count: *int64)` | `(storage.IosErrorKey, …)` | 1 |
| `GetIosSuccess` | `getBuntDB(key: string, count: *int64)` | `(storage.IosSuccessKey, …)` | 1 |
| `GetTotalCount` | `getBuntDB(key: string, count: *int64)` | `(storage.TotalCountKey, …)` | 1 |
| `Reset` | `setBuntDB(key: string, count: int64)` | `(storage.TotalCountKey, 0)` | 7 |
| `setBuntDB` | `Error(args: interface{})` | `()` | 1 |
| `AddAndroidError` | `setLevelDB(key: string, count: int64)` | `(storage.AndroidErrorKey, total)` | 1 |
| `AddAndroidSuccess` | `setLevelDB(key: string, count: int64)` | `(storage.AndroidSuccessKey, total)` | 1 |
| `AddHuaweiError` | `setLevelDB(key: string, count: int64)` | `(storage.HuaweiErrorKey, total)` | 1 |
| `AddHuaweiSuccess` | `setLevelDB(key: string, count: int64)` | `(storage.HuaweiSuccessKey, total)` | 1 |
| `AddIosError` | `setLevelDB(key: string, count: int64)` | `(storage.IosErrorKey, total)` | 1 |
| `AddIosSuccess` | `setLevelDB(key: string, count: int64)` | `(storage.IosSuccessKey, total)` | 1 |
| `AddTotalCount` | `setLevelDB(key: string, count: int64)` | `(storage.TotalCountKey, total)` | 1 |
| `GetAndroidError` | `getLevelDB(key: string, count: *int64)` | `(storage.AndroidErrorKey, …)` | 1 |
| `GetAndroidSuccess` | `getLevelDB(key: string, count: *int64)` | `(storage.AndroidSuccessKey, …)` | 1 |
| `GetHuaweiError` | `getLevelDB(key: string, count: *int64)` | `(storage.HuaweiErrorKey, …)` | 1 |
| `GetHuaweiSuccess` | `getLevelDB(key: string, count: *int64)` | `(storage.HuaweiSuccessKey, …)` | 1 |
| `GetIosError` | `getLevelDB(key: string, count: *int64)` | `(storage.IosErrorKey, …)` | 1 |
| `GetIosSuccess` | `getLevelDB(key: string, count: *int64)` | `(storage.IosSuccessKey, …)` | 1 |
| `GetTotalCount` | `getLevelDB(key: string, count: *int64)` | `(storage.TotalCountKey, …)` | 1 |
| `Reset` | `setLevelDB(key: string, count: int64)` | `(storage.TotalCountKey, 0)` | 7 |
| `GetAndroidError` | `getInt64(key: string, count: *int64)` | `(storage.AndroidErrorKey, …)` | 1 |
| `GetAndroidSuccess` | `getInt64(key: string, count: *int64)` | `(storage.AndroidSuccessKey, …)` | 1 |
| `GetHuaweiError` | `getInt64(key: string, count: *int64)` | `(storage.HuaweiErrorKey, …)` | 1 |
| `GetHuaweiSuccess` | `getInt64(key: string, count: *int64)` | `(storage.HuaweiSuccessKey, …)` | 1 |
| `GetIosError` | `getInt64(key: string, count: *int64)` | `(storage.IosErrorKey, …)` | 1 |
| `GetIosSuccess` | `getInt64(key: string, count: *int64)` | `(storage.IosSuccessKey, …)` | 1 |
| `GetTotalCount` | `getInt64(key: string, count: *int64)` | `(storage.TotalCountKey, …)` | 1 |
