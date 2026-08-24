<!-- pam:product-page:start -->
<div align="center">

# PAM Socket

**Rooms, broadcasts, acknowledgements, and scale-out over native WebSockets.**

An event-oriented API over PAM's RFC 6455 transport with authentication, bounded events, rooms, resume behavior, and Redis Streams/NATS adapters.

[![Release](https://img.shields.io/github/v/release/push-in/pam-socket?style=flat-square&label=stable)](https://github.com/push-in/pam-socket/releases)
![PHP](https://img.shields.io/badge/PHP-8.5-777BB4?style=flat-square&logo=php&logoColor=white)
![License](https://img.shields.io/github/license/push-in/pam-socket?style=flat-square)

**[Documentation](https://push-in.github.io/pam-docs/packages/socket/) · [Why this exists](#why-this-exists) · [What you can build](#what-you-can-build) · [Quick start](#quick-start) · [Issues](https://github.com/push-in/pam-socket/issues)**

</div>

---

## Why this exists

An event-oriented API over PAM's RFC 6455 transport with authentication, bounded events, rooms, resume behavior, and Redis Streams/NATS adapters.

| | |
| --- | --- |
| **Role** | Realtime framework |
| **Execution path** | PAM WebSocket transport · PHP event API |
| **This repository owns** | Application events, rooms, acknowledgements, and broadcast adapters |
| **Boundary** | Not wire-compatible with Socket.IO or Engine.IO clients |

## What you can build

- Chat, presence, and collaboration
- Realtime dashboards and notifications
- Multi-worker broadcasts coordinated through Redis Streams or NATS

## Quick start

```bash
pam composer require pushinbr/pam-socket
```

The **[PAM documentation](https://push-in.github.io/pam-docs/packages/socket/)** covers prerequisites, production setup, and the complete workflow. PAM projects keep normal manifests and lockfiles; product features stay in the package that owns them.
<!-- pam:product-page:end -->

Event-oriented socket APIs for Pam's native WebSocket transport, including
authentication, rooms, broadcasts, acknowledgements and Redis Streams/NATS
adapters.

## See it in action

```php
use Pam\Socket\Server;

$io = Server::create();
$io->on('connection', static fn ($socket) => $socket->emit('ready'));
```

## License

Free and open-source under the [Apache License 2.0](LICENSE). You may use,
modify, and distribute this package for any purpose, including commercially.


## Recommended PAM workflow

Create a realtime application with `pam init realtime-api --template api --socket` or `pam init realtime-laravel --template laravel --socket`. In an existing project, use `pam composer require pushinbr/pam-socket`.

Run `pam doctor` after dependency changes and before creating a release. The project remains a normal Composer project with a standard manifest, lockfile, PSR-4 autoloading, and `vendor/autoload.php`.

## API guide

| Surface | Use it for |
| --- | --- |
| `Server::create()` | Create the event layer over PAM's native WebSocket server. |
| `on()` | Handle connection and application events. |
| `auth()` | Authenticate the connection before application events are accepted. |
| `emit()` | Broadcast an event to connected clients. |
| `to()` | Target a room through a `RoomEmitter`. |
| Adapters | Coordinate broadcasts across workers through supported Redis Streams or NATS adapters. |

PAM Socket uses standard RFC 6455 frames and its own event envelope. It is not an Engine.IO or Socket.IO server. Clients must implement the documented PAM event contract, acknowledgement identifiers, reconnect policy, and resume behavior.

## Production checklist

- Keep request data and mutable state scoped to the current request.
- Test success, validation failure, exception, cancellation, and timeout paths.
- Configure explicit limits and avoid unbounded payloads, queues, or retained collections.
- Run `pam doctor`, `pam test`, and the relevant integration suite before release.
- Validate real dependencies and workload behavior; compatibility is not inferred from package installation alone.

## Troubleshooting

- **Class not found:** run `pam composer install`, verify PSR-4 configuration, and rerun `pam doctor`.
- **Behavior differs over the network:** reproduce with PAM's transport integration tests; in-memory execution does not model the socket boundary.
- **A dependency blocks a worker:** use PAM-native I/O, a compatible event loop, a process pool, or additional isolated workers.

## Documentation and support

- [PAM introduction](https://push-in.github.io/pam-docs/introduction/)
- [Package ecosystem](https://push-in.github.io/pam-docs/packages/overview/)
- [Runtime compatibility](https://push-in.github.io/pam-docs/runtime/compatibility/)
- [Report an issue](https://github.com/push-in/pam-socket/issues)

Report security vulnerabilities through GitHub private vulnerability reporting or the PAM security policy, not a public issue.
