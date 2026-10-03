# Kiln — the project ladder

Settled in a grilling session on 2026-10-02/03. This file is the ladder. When something changes, change it here.

## The idea

One arc: 7 standalone public repos, each a real component of the flagship, **Crawl Toll**.

**The problem:** AI crawlers (GPTBot, ClaudeBot, PerplexityBot…) hit sites millions of times, and site owners can only block them or let them in for free. Crawl Toll is a toll booth in front of a site. It identifies each crawler, verifies it, applies a policy (allow, deny, rate-limit or pay per crawl), meters every request and bills it to a ledger.

**What the projects signal:** mostly high-load backend (Postgres, Kafka, gRPC, rate limiting, idempotency, observability, k8s), plus 2 rungs where I build the internals myself. AI is the problem domain, never the subject of the code.

**Stack:** standard library first. I add a library only once I've felt the pain of going without it.

## The rungs

| # | Repo | What it is (useful on its own) | Milestones | Ships as | Codebase to read |
|---|---|---|---|---|---|
| 1 | `botcheck` | CLI + HTTP API: is this request really GPTBot, ClaudeBot…? Checks the user-agent, then verifies the IP against published ranges or reverse DNS. Reports which AI bots hit a site. | M1, M3 | local | `benhoyt/goawk` |
| 2 | `tollgate` | Reverse proxy in front of any site. Per-bot policy file: allow, deny, or 402 Payment Required with a price header. | M1 | docker compose | Caddy `reverse_proxy` module |
| 3 | `ledger` | Double-entry billing ledger API, safe under retries. | M2 | **VPS (first public deploy)** | `formancehq/ledger` |
| 4 | `kvlite` *(internals)* | My own Redis-compatible KV server. Real `redis-cli` can talk to it. | M3, M4, M5 | VPS | `tidwall/redcon` + `tidwall/buntdb` |
| 5 | `ratekeeper` | Distributed rate limiter (token bucket / GCRA) over gRPC. Several replicas share state in kvlite or Redis. | M3, M4 | **k8s (kind): first cluster** | `envoyproxy/ratelimit` |
| 6 | `spool` *(internals)* | My own append-only log, a mini Kafka: segments, offsets, consumer groups. | M3, M5 | k8s StatefulSet + persistent volume | `travisjeffery/proglog` (book: *Distributed Services with Go*) |
| 7 | `meter` | tollgate events → Kafka (Redpanda) → aggregator → ledger, with exactly-once-ish billing through the outbox pattern, plus OpenTelemetry. | M3 | k8s + Helm | `ThreeDotsLabs/watermill` |
| ★ | `crawltoll` | The whole system as one product, in front of a real site taking real crawler traffic, with a Grafana dashboard. k6 load test, HPA autoscaling, alerting, 10× write-up. | all | **k3s on a VPS (k8s in production)** | `traefik/traefik` |

**How Kubernetes comes in:** rung 2 is containers only, rung 5 is a first cluster with stateless replicas, rung 6 adds state (StatefulSet and volumes), rung 7 installs third-party software with Helm, and the flagship runs a production cluster with autoscaling. Each new k8s idea arrives only when the project forces it.

## Rules for every rung

1. **10 lines first.** I write what the rung does before any code. Only then does it get sliced.
2. **Slice only on the day I start.** Later rungs stay at table level until then.
3. **6-week cap.** At the cap I ship what works, write a "what's missing" section and move on. The resume card says so once.
4. **Definition of done:**
   - README with the problem, a design diagram, and the decisions with their trade-offs
   - tests, with `go test -race` passing in CI
   - **one measured number** (p99, req/s, or before/after `pprof`)
   - a "what I'd do at 10× load" section
5. **I type** all the Go, plus the Dockerfiles, compose files, k8s manifests and Helm values. AI writes only CI workflow files, Grafana dashboard JSON and the bait site.
6. **Mentor fade:** rungs 1–2 walked step by step, 3–5 reviewed, 6, 7 and ★ reviewed afterwards.
7. **Read one codebase** (column above, 30 min, guided). The mentor picks the exact files when the rung starts.

## Apply trigger

When **Go milestones 1–3 + ~60 LeetCode + 3 public ladder repos with READMEs** are all true, the resume card says "apply now" once. I start with internships and junior roles (Yandex, Ozon, Avito), and I keep building while I apply.

## Real traffic

A static portfolio/blog site (AI builds it, the only non-Go thing it builds) goes live **during rung 1**, served by nginx on my VPS with a cheap domain and access logs on from day 1. It feeds botcheck real data and builds months of crawler history for the flagship. Public log datasets are a fallback, for load tests only.

---

## Rung 1 — `botcheck` (status: not started)

**10 lines:** *(I write these at the first sitting, before slice 1.)*

**Slices:**
- [ ] 1. **Walking skeleton:** an empty folder, then `go mod init`, then a `main.go` that reads log lines from stdin and prints them.
- [ ] 2. **Parse:** turn an nginx combined-log line into a struct (IP, time, method, path, status, user-agent), with table tests.
- [ ] 3. **Identify:** match known AI-crawler user-agents (GPTBot, ClaudeBot, PerplexityBot, CCBot, Bytespider…) and print a count per bot.
- [ ] 4. **Verify:** check the IP against the bot's published IP ranges where they exist, otherwise reverse DNS. Mark each request verified or spoofed, and handle timeouts and errors properly.
- [ ] 5. **Go concurrent:** a worker pool with `errgroup` and `context` cancellation over a big log. `-race` passes, plus one benchmark number.
- [ ] 6. **API:** `net/http` with `GET /verify?ip=&ua=` and `POST /report`, tested with `httptest`.
- [ ] 7. **Ship:** run it on my real site's log, write the README to the definition of done, and push the public repo.
