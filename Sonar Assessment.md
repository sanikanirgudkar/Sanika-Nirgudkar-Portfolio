# New parent page: SonarQube Server-hosted

Install and configure the SonarQube MCP Server extension on SonarQube Server.
{: shortdesc}

## Overview

The SonarQube MCP Server can be installed as an extension on SonarQube Server. Once installed, SonarQube Server acts as a proxy and exposes the MCP server's tools at <YourSonarQubeURL>/mcp. Your AI agent connects to that single endpoint. There is no separate MCP server URL to manage.
<!-- Rewrote this last line for clarity of the instruction -->

The SonarQube Server MCP extension is available on all commercial editions: Developer, Enterprise, and Data Center Edition.
{: note}

## Before you start

Sonar Vortex's agentic analysis and context augmentation features require file system access and don't work with the SonarQube Server-hosted MCP server. To set them up, the recommended methods are the SonarQube plugin or SonarQube CLI. See the *Make your agent verify its code* and *Add context to generate better code* pages.

<!-- Moved this limitation above the prerequisites list rather than below it, since it can change which install path a reader picks — someone who needs Vortex features shouldn't read three sections of setup steps before learning this path won't support them. -->
<!-- The links to *Make your agent verify its code* and *Add context to generate better code* pages seemed broken or I wont have access to, hence only identified them in Italics.They need to have working links to actual source pages.-->

## Prerequisites

- SonarQube Server 2026.3 or later
- A SonarQube Server user account with permission to generate a user token

<!-- This is now the one place where prerequisites are stated for the whole page group. Method-specific prerequisites (JDK 21 for the ZIP install; Docker/Docker Compose for the Docker install) move to their own pages, right next to the steps that need them, instead of being predicted here and repeated there.-->

## Compatibility

| SonarQube Server version | Compatible MCP Server version |
| ------------------------ | ----------------------------- |
| 2026.4 | 1.22.0.3040 |
| 2026.3 | 1.18.1.2664 |

Always set MCP_VERSION to the full 4-part version from this table (for example, use 1.18.1.2664 with SonarQube Server 2026.3). Only full 4-part tags are published to Docker Hub; 3-part tags like 1.18.1 don't exist.

## Choose your installation method

| Your setup | Installation guide |
| ------ | ----- |
| Run SonarQube Server from a downloaded ZIP/JAR and manage the process yourself (including as a systemd or Windows service) | Install from ZIP |
| Run SonarQube Server in Docker or Docker Compose, on any edition including Data Center | Install from Docker |
| Run SonarQube Server on Kubernetes or OpenShift, via Helm | Install on Kubernetes / OpenShift |

<!-- This table is something will make everything shorter and give a quick access. I have created a new table to fix the page structure. Instead of scrolling through every method to find yours, the reader picks their row and jumps straight there. It mirrors the “Three ways to use the CLI” table on the CLI page which reuses a pattern the docs already use successfully elsewhere. This also brings uniformity among the doc sets. -->

## Configuration reference

These properties configure the MCP proxy on SonarQube Server, regardless of which method you used to install it. Set them in conf/sonar.properties, or as environment variables on the SonarQube container.

| Property (sonar.properties / ENV variable) | Description |
| ---------------- | ----------- |
| sonar.mcp.enabled / SONAR_MCP_ENABLED | Enables or disables the MCP proxy. (default: true) |
| sonar.mcp.serverUrl / SONAR_MCP_SERVERURL | The URL where the MCP server will be running |
| sonar.mcp.healthCheckInterval / SONAR_MCP_HEALTHCHECKINTERVAL | Health check interval. (default: 30s, optional) |

## Connect your AI agent

Once the MCP server extension is running, configure your AI agent to connect to it.

**Generate a user token**
:   In SonarQube Server, go to My Account > Security and generate a user token.

**Configure your agent**
:   Use the official SonarQube MCP Server configuration generator to get a configuration snippet for your setup:

- Identify your target MCP client.
- Find your environment variables.
  - Select SonarQube Server as your instance.
  - Use environment variable substitution to pass your token, or enter your SonarQube Server user token directly in the User token (optional) field.
- Choose a hosting method:
  - Select Remote server (HTTP).
  - Fill the full server URL with https://<YourSonarQubeURL>/mcp. Don't add a trailing slash.
- Copy the configuration and paste it into your terminal.
  - Optional: To make the MCP server available globally and not only for the repo where the command has been run, append --scope user to your CLI command.
  - Optional: Verify that the SonarQube entry has been added to your agent configuration file with your user token and the new URL.
- Restart your agent after saving the configuration and run /mcp to verify it's working.

<!-- I wanted to reduce these steps in lesser steps, but somehow could not. I need a better understanding of the end user and if they really need the steps dummed down so much.-->

## Check the status

After installation, verify the extension is running correctly. In SonarQube Server, go to **Administration** > **System info** > **System** > **MCP** and check the **Enabled** and **Healthy** statuses.

<!-- I have made the UI buttons in BOLD format.-->

