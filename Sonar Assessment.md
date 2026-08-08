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


