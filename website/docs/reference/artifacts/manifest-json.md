---
title: Manifest
---
**Current schema**: [`v8`](https://schemas.getdbt.com/dbt/manifest/v8/index.html)

**Produced by:** [`build`](commands/build) [`compile`](commands/compile) [`docs generate`](commands/cmd-docs) [`list`](commands/list) [`seed`](commands/seed) [`snapshot`](commands/snapshot) [`source freshness`](commands/source) [`test`](commands/test) [`run`](commands/run) [`run-operation`](commands/run-operation)


This single file contains a full representation of your dbt project's resources (models, tests, macros, etc), including all node configurations and resource properties. Even if you're only running some models or tests, all resources will appear in the manifest (unless they are disabled) with most of their properties. (A few node properties, such as `compiled_sql`, only appear for executed nodes.)

Today, dbt uses this file to populate the [docs site](documentation), and to perform [state comparison](/docs/deploy/about-state). Members of the community have used this file to run checks on how many models have descriptions and tests.

### Top-level keys

- [`metadata`](dbt-artifacts#common-metadata)
- `nodes`: Dictionary of all analyses, models, seeds, snapshots, and tests.
- `sources`: Dictionary of sources.
- `metrics`: Dictionary of metrics.
- `exposures`: Dictionary of exposures.
- `macros`: Dictionary of macros.
- `docs`: Dictionary of `docs` blocks.
- `parent_map`: Dictionary that contains the first-order parents of each resource.
- `child_map`: Dictionary that contains the first-order children of each resource.
- `selectors`: Expanded dictionary representation of [YAML `selectors`](yaml-selectors).
- `disabled`: Array of resources with `enabled: false`.

### Resource details

All resources nested within `nodes`, `sources`, `metrics`, `exposures`, `macros`, and `docs` have the following base properties:

- `name`: Resource name.
- `unique_id`: `<resource_type>.<package>.<resource_name>`, same as dictionary key
- `package_name`: Name of package that defines this resource.
- `root_path`: Absolute file path of this resource's package. This is removed in dbt Core v1.4 / manifest v8 to reduce duplicative information across nodes.
- `path`: Relative file path of this resource's definition within its "resource path" (`model-paths`, `seed-paths`, etc.).
- `original_file_path`: Relative file path of this resource's definition, including its resource path.

Each has several additional properties related to its resource type.
