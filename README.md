# AntelopeJS interface registry

<div align="center">
<a href="./LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache_2.0-000000?style=for-the-badge&labelColor=000000"></a>
<a href="https://discord.gg/g4pFt6eXqu"><img alt="Discord" src="https://img.shields.io/badge/Discord-18181B?logo=discord&style=for-the-badge&color=000000"></a>
<a href="https://framework.antelopejs.com/docs/module-development/interface-registry"><img alt="Docs" src="https://img.shields.io/badge/Docs-18181B?style=for-the-badge&color=000000"></a>
</div>

The catalog the `ajs` CLI reads to find which modules implement an interface. It holds metadata only: the interface packages and their implementations live on npm.

## What it does

- `ajs project modules install` finds the interfaces a project imports without an implementation, and offers the modules this registry lists for them.
- `ajs module init` offers the starred interfaces of this registry when it scaffolds a module, and the templates listed here.
- `ajs project init` also offers complete project templates, including **DMS Starter**, **DMS Demo**, and **DMS Adonis**.
- Each interface has a folder under `interfaces/` with a `manifest.json`: a description, the interface package and the modules that implement it.
- The root `manifest.json` maps each interface package to its folder and lists the starred interfaces and the project templates.

## Interfaces

| Interface                                                                                   | Package                                     | Modules listed                                                  |
| ------------------------------------------------------------------------------------------- | ------------------------------------------- | --------------------------------------------------------------- |
| [API](https://interfaces.antelopejs.com/docs/api)                                           | `@antelopejs/interface-api`                 | `@antelopejs/api`                                               |
| [API Util](https://interfaces.antelopejs.com/docs/api-util)                                 | `@antelopejs/interface-api-util`            | `@antelopejs/api`                                               |
| [Auth](https://interfaces.antelopejs.com/docs/auth)                                         | `@antelopejs/interface-auth`                | `@antelopejs/auth-jwt`                                          |
| [Core](https://interfaces.antelopejs.com/docs/core)                                         | `@antelopejs/interface-core`                | none: `@antelopejs/core` provides it                            |
| [Data API](https://interfaces.antelopejs.com/docs/data-api)                                 | `@antelopejs/interface-data-api`            | `@antelopejs/data-api`                                          |
| [Database](https://interfaces.antelopejs.com/docs/database)                                 | `@antelopejs/interface-database`            | `@antelopejs/mongodb`, `@antelopejs/rethinkdb`                  |
| [Database Catalog](https://github.com/AntelopeJS/interface-database-catalog/tree/main/docs) | `@antelopejs/interface-database-catalog`    | none: no public implementation yet                              |
| [Database Decorators](https://interfaces.antelopejs.com/docs/database-decorators)           | `@antelopejs/interface-database-decorators` | `@antelopejs/database-decorators`                               |
| [Email](https://github.com/AntelopeJS/interface-email/tree/main/docs)                       | `@antelopejs/interface-email`               | `@antelopejs/nodemailer`, `@antelopejs/brevo`                     |
| [File Storage](https://github.com/AntelopeJS/interface-file-storage/tree/main/docs)         | `@antelopejs/interface-file-storage`        | `@antelopejs/file-storage-s3`, `@antelopejs/file-storage-local` |
| [Logging](https://interfaces.antelopejs.com/docs/core/logging)                              | `@antelopejs/interface-core`                | none: `@antelopejs/core` provides it                            |
| [MongoDB](https://interfaces.antelopejs.com/docs/mongodb)                                   | `@antelopejs/interface-mongodb`             | `@antelopejs/mongodb`                                           |
| [Redis](https://interfaces.antelopejs.com/docs/redis)                                       | `@antelopejs/interface-redis`               | `@antelopejs/redis`                                             |
| [Redis Scheduler](https://interfaces.antelopejs.com/docs/redis-scheduler)                   | `@antelopejs/interface-redis-scheduler`     | `@antelopejs/redis`                                             |
| [RethinkDB](https://interfaces.antelopejs.com/docs/rethinkdb)                               | `@antelopejs/interface-rethinkdb`           | `@antelopejs/rethinkdb`                                         |
| [Stripe](https://interfaces.antelopejs.com/docs/stripe)                                     | `@antelopejs/interface-stripe`              | `@antelopejs/stripe`                                            |

Registration does not publish an npm package or deploy its documentation.
Database Catalog is not yet published to npm. The public documentation site has
its own source registry in `AntelopeJS/antelope-web`; add a source there when a
public interface is ready to appear on the site. Private interfaces are not
listed in this public registry.

Each interface owns its reference in its package's `docs/` directory. For DMS
monorepos this is `packages/interface-dms-*/docs/`; the
[DMS documentation](https://dms.antelopejs.com/docs/interfaces) links those
contracts separately from the runtime guides. This registry is not an inventory
of every package that can participate in AntelopeJS.

The catalog also includes these contracts:

| Interface | Package | Modules listed |
| --- | --- | --- |
| DMS | `@antelopejs/interface-dms` | `@antelopejs/dms` |
| DMS Automation | `@antelopejs/interface-dms-automation` | `@antelopejs/dms-automation` |
| DMS Builder | `@antelopejs/interface-dms-builder` | `@antelopejs/dms-builder` |
| DMS Mailing | `@antelopejs/interface-dms-mailing` | `@antelopejs/dms-mailing` |
| DMS Marketing | `@antelopejs/interface-dms-marketing` | `@antelopejs/dms-marketing` |
| DMS Media | `@antelopejs/interface-dms-media` | `@antelopejs/dms-media` |
| DMS SaaS | `@antelopejs/interface-dms-saas` | `@antelopejs/dms-saas` |

## Use it

The CLI reads this repository by default. Resolve the missing implementations of a project from its folder:

```bash
ajs project modules install
```

### Start a DMS project with Docker

Select **DMS Starter** in `ajs project init`, or pass it explicitly:

```bash
ajs project init my-app --template "DMS Starter" --yes
cd my-app
docker compose up
```

This template runs the DMS, the Builder, and the AI assistant with no sample data. Docker Compose also starts the MongoDB that the DMS needs. Open <http://localhost:3001> to create the first administrator. See the [template README](https://github.com/AntelopeJS/template-dms#readme).

### Start a DMS project with the demo application

Use a CLI release with project-template support to select **DMS Demo** in
`ajs project init`, or pass the template explicitly:

```bash
ajs project init my-app --template "DMS Demo" --yes
cd my-app
pnpm dev
```

The demo requires Node.js 24, pnpm and a running MongoDB instance. Run
`pnpm frontend:dev` in a second terminal, then open the printed dashboard URL
to create the first administrator. See the [template README](https://github.com/AntelopeJS/template-dms-demo#readme)
for configuration and direct-clone instructions for older CLIs.

`modules install` resolves missing contracts; it is not a menu of every DMS
feature. Modules such as `dms-ai`, `dms-api`, `dms-database` and `dms-lang`
do not declare an interface implementation. The demo already configures them.
Installing an interface package alone does not configure a working dashboard.

### Start a DMS project inside AdonisJS

Select **DMS Adonis** in `ajs project init` (CLI 1.16 or later), or pass it
explicitly:

```bash
ajs project init my-app --template "DMS Adonis" --pm pnpm
cd my-app
cp .env.example .env
node ace generate:key
pnpm dev
```

This template runs the DMS embedded in an AdonisJS 6 application. See the
[template README](https://github.com/AntelopeJS/template-dms-adonis#readme).

### Start a reusable DMS module

Select **DMS Module Typescript** in `ajs module init`, or pass it explicitly:

```bash
ajs module init my-module --template "DMS Module Typescript" --pm pnpm --yes
cd my-module
pnpm services:up
pnpm dev
```

Run `pnpm frontend:dev` in a second terminal. This template contains a reusable
module, one Vue component and a `playground/` project. Docker Compose supplies
MongoDB and Mailpit; existing local services also work. See the
[module template README](https://github.com/AntelopeJS/template-module-dms#readme).
It belongs in `templates`, not `projectTemplates`: it is a module with a
development host, not a complete application.

### Project template metadata

The root `projectTemplates` array holds complete projects. The CLI offers
them only in `project init`, alongside the module templates in `templates`.
Older CLIs ignore `projectTemplates`, so they cannot offer a project they
would incorrectly overwrite. Keep complete projects out of `templates`.

Both arrays use the required `name`, `repository` and `branch` fields and
these optional fields:

- `description`: a hint in the template selector, including prerequisites.
- `packageManager`: require this package manager and skip its prompt.
- `nextSteps`: commands and optional descriptions displayed after creation;
  the CLI does not execute these commands automatically.

Project creation requires the CLI release with project-template support.
CLI releases through 1.15.2 do not list
complete project templates; use the direct-clone instructions with those releases.

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
