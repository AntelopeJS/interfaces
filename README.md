# AntelopeJS interface registry

<div align="center">
<a href="./LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache_2.0-000000?style=for-the-badge&labelColor=000000"></a>
<a href="https://discord.gg/sjK28QHrA7"><img alt="Discord" src="https://img.shields.io/badge/Discord-18181B?logo=discord&style=for-the-badge&color=000000"></a>
<a href="https://framework.antelopejs.com/docs/module-development/interface-registry"><img alt="Docs" src="https://img.shields.io/badge/Docs-18181B?style=for-the-badge&color=000000"></a>
</div>

The catalog the `ajs` CLI reads to find which modules implement an interface. It holds metadata only: the interface packages and their implementations live on npm.

## What it does

- `ajs project modules install` finds the interfaces a project imports without an implementation, and offers the modules this registry lists for them.
- `ajs module init` offers the starred interfaces of this registry when it scaffolds a module, and the templates listed here.
- Each interface has a folder under `interfaces/` with a `manifest.json`: a description, the interface package and the modules that implement it.
- The root `manifest.json` maps each interface package to its folder and lists the starred interfaces and the project templates.

## Interfaces

| Interface                                                                         | Package                                     | Modules listed                                 |
| --------------------------------------------------------------------------------- | ------------------------------------------- | ---------------------------------------------- |
| [API](https://interfaces.antelopejs.com/docs/api)                                 | `@antelopejs/interface-api`                 | `@antelopejs/api`                              |
| [API Util](https://interfaces.antelopejs.com/docs/api-util)                       | `@antelopejs/interface-api-util`            | `@antelopejs/api`                              |
| [Auth](https://interfaces.antelopejs.com/docs/auth)                               | `@antelopejs/interface-auth`                | `@antelopejs/auth-jwt`                         |
| [Core](https://interfaces.antelopejs.com/docs/core)                               | `@antelopejs/interface-core`                | none: `@antelopejs/core` provides it           |
| [Data API](https://interfaces.antelopejs.com/docs/data-api)                       | `@antelopejs/interface-data-api`            | `@antelopejs/data-api`                         |
| [Database](https://interfaces.antelopejs.com/docs/database)                       | `@antelopejs/interface-database`            | `@antelopejs/mongodb`, `@antelopejs/rethinkdb` |
| [Database Decorators](https://interfaces.antelopejs.com/docs/database-decorators) | `@antelopejs/interface-database-decorators` | `@antelopejs/database-decorators`              |
| [Logging](https://interfaces.antelopejs.com/docs/core/logging)                    | `@antelopejs/interface-core`                | none: `@antelopejs/core` provides it           |
| [MongoDB](https://interfaces.antelopejs.com/docs/mongodb)                         | `@antelopejs/interface-mongodb`             | `@antelopejs/mongodb`                          |
| [Redis](https://interfaces.antelopejs.com/docs/redis)                             | `@antelopejs/interface-redis`               | `@antelopejs/redis`                            |
| [Redis Scheduler](https://interfaces.antelopejs.com/docs/redis-scheduler)         | `@antelopejs/interface-redis-scheduler`     | `@antelopejs/redis`                            |
| [RethinkDB](https://interfaces.antelopejs.com/docs/rethinkdb)                     | `@antelopejs/interface-rethinkdb`           | `@antelopejs/rethinkdb`                        |
| [Stripe](https://interfaces.antelopejs.com/docs/stripe)                           | `@antelopejs/interface-stripe`              | `@antelopejs/stripe`                           |

## Use it

The CLI reads this repository by default. Resolve the missing implementations of a project from its folder:

```bash
ajs project modules install
```

## Add an interface or an implementation

Create `interfaces/<name>/manifest.json`, or add your module to the `modules` array of an existing one:

```json
{
  "description": "Payment processing interface",
  "package": "@antelopejs/interface-payment",
  "modules": [
    {
      "name": "payment-stripe",
      "source": {
        "type": "package",
        "package": "@acme/payment-stripe",
        "version": "latest"
      }
    }
  ]
}
```

For a new interface, also map its package to the folder in the `interfaces` object of the root `manifest.json`. The [interface registry guide](https://framework.antelopejs.com/docs/module-development/interface-registry) describes every field.

## Contributing

Read [CONTRIBUTING.md](./CONTRIBUTING.md), then open a pull request with your manifest change.

## License

[Apache-2.0](./LICENSE)
