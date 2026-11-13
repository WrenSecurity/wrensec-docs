This page describes the conventions shared by the documentation of all Wren Security projects (Wren:AM, Wren:DS, Wren:ICF, Wren:IDM, Wren:IG).
Each documentation project describes its own additional conventions, such as how its pages are organized and how it is built, in the `README.md` of its repository.

## Tooling

Documentation is written in [AsciiDoc](https://docs.antora.org/antora/latest/asciidoc/asciidoc/) and built with [Antora](https://antora.org/).
Each project has its own documentation repository (e.g. `wrenam-docs`) with an Antora component for the project.
The repository follows the standard [Antora directory structure](https://docs.antora.org/antora/latest/module-directory-names/).

## Types of documentation

Documentation is organized by its type and target audience.
Each type of documentation is a separate Antora module (or a separate section of the navigation) in the documentation project:

* **Reference Guide** – technical description of the architecture and components.
* **Deployment Guide** – how to deploy and configure the application: deployment strategies (HA, scaling), backup and restore, upgrades and migration, security hardening, performance tuning.
* **Administration Guide** – how to maintain the application and perform common administration tasks, including troubleshooting.
* **Integration Guide** – how other systems integrate with the application; written for developers and administrators of those systems.
* **Developer's Guide** – how to build, customize and extend the application.
* **User Guide** – how to use the user interface; written for end users.
* **Cookbook** – recipes for common use cases.
* **Knowledge Base** – articles that do not fit into any other type.

In addition, JavaDoc and OpenAPI documentation are generated from the source code.

The Reference Guide is the priority.
Other types of documentation are created when there is content for them, e.g. when a feature is implemented or a common use case comes up.
To place a topic, find the type of documentation whose audience and purpose it matches; for example, how a feature works and how it is configured belongs to the Reference Guide, while what a specific error in the debug log means belongs to the Administration Guide.

### Reference Guide

The Reference Guide describes what each component does, how it behaves and how it is configured.
It is organized by components and features and serves as the basis that other types of documentation refer to.

The Reference Guide does not contain step-by-step procedures, recipes or troubleshooting guides – these belong to the other types of documentation.
Facts that explain behavior, such as which situations make a server appear unavailable or where errors are logged, do belong to the reference.

Shared concepts, such as realms or the structure of the configuration, are described on their own pages and linked from other pages rather than repeated.

### Other guides

Other guides refer to the Reference Guide for details on components and settings instead of repeating them.

## Writing conventions

General [AsciiDoc recommended practices](https://asciidoctor.org/docs/asciidoc-recommended-practices/) apply, together with the conventions below.

### Formatting

* Write one sentence per line.
* Put two empty lines before section headings.
  If a heading has an anchor (`[[anchor]]`), the empty lines go before the anchor.
* Use a spaced en dash (` – `) for sentence breaks.

### AsciiDoc features

* Use [source blocks](https://docs.antora.org/antora/latest/asciidoc/source/) with the correct language for code, commands and configuration.
* Use [UI macros](https://docs.antora.org/antora/latest/asciidoc/ui-macros/) for user interface elements, e.g. `menu:Configure[Global Services > RADIUS Server]` for navigation and `btn:[Save Changes]` for buttons.
* Use [admonitions](https://docs.antora.org/antora/latest/asciidoc/admonitions/) for information that supports the main text, placed next to the text it relates to, e.g. a `NOTE` explaining the security background of a setting.
* Give examples a title starting with "Example of", placed above the source block, e.g. `.Example of mapping definitions in sync.json`.
* Use [example blocks](https://docs.antora.org/antora/latest/asciidoc/examples/) where applicable.

## Diagrams

* [Draw.io](https://www.drawio.com/) diagrams are stored as SVG with the embedded source diagram.
* [Mermaid](https://mermaid.js.org/) is preferred for simple diagrams embedded in the page; it requires an Antora extension in the documentation project.
