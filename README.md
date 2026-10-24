# DotaNet Advertising Platform

A Go advertising-platform project with ad selection, click and impression tracking, advertiser and publisher management, and reporting.

## Services

| Directory | Responsibility |
| --- | --- |
| `adserver/` | Ad retrieval, selection, and auctions |
| `eventservice/` | Click and impression ingestion |
| `panel/` | Advertiser/publisher management and browser pages |
| `reporter/` | Event-driven reporting |
| `publisherwebsite/` | Example publisher pages |
| `common/` | Shared data structures |
| `screper/` | Additional scraping utility |

The root `go.work` joins the service modules. Their declared Go version is 1.22.5.

## Local setup

Use Docker with Compose support for the multi-service stack. It includes PostgreSQL, Kafka, and ZooKeeper.

1. Review `docker-compose.yml`, its environment-variable references, and the historical `.envLocal`/`.envProduct` settings.
2. Prepare your own local environment file with appropriate credentials and hostnames.
3. Start the stack:

```sh
docker compose --env-file .env up --build
```

The configured host ports include 8081 for ad serving, 8082 for events, and 8085 for the management panel. Confirm the actual addresses in Compose and service startup output.

For native development, use the individual module directories with Go 1.22.5 or newer. The Kafka client may require a compatible native toolchain; Docker is the existing integrated deployment path.

## Existing checks

```sh
cd adserver
go test ./...
```

The panel also contains tests; run them from its module directory with its dependencies available. A full Kafka/PostgreSQL integration run has not been verified during this documentation update.

Committed example secrets and default signing keys must be replaced before exposing a deployment.

## License

See [LICENSE](LICENSE).

## Project credits

This is Sobhan Alaeddini's portfolio fork of [nobletooth/dotanet](https://github.com/nobletooth/dotanet). The project was developed collaboratively; the upstream repository and Git history retain the original contributor credits. Documentation in this fork is maintained independently.
