# Model Context Protocol

{% hint style="warning" %}
The MCP is under active development and experimentation. All feedback is welcome in [https://community.opentargets.org](https://community.opentargets.org)
{% endhint %}

The Open Targets Platform Model Context Protocol (MCP) server provides a purpose-built interface and instructions to access and interpret the data and analyses in the Open Targets Platform using AI.

MCP Servers are part of a standardised interface for AI agents to interact with data sources using the [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro).

### Ways to connect

* **Remote Server**: Connect directly to Open Targets hosted endpoint available in `https://mcp.platform.opentargets.org/mcp`
* **Local Server:** Run a local MCP server using uvx or Docker

More detailed information can be found in the [MCP server github repository](https://github.com/opentargets/open-targets-platform-mcp).

Claude provides [a detailed tutorial](https://claude.com/resources/tutorials/using-the-open-targets-connector-in-claude) on how to add the MCP as a connector.

<figure><img src="../.gitbook/assets/Screenshot 2026-01-09 at 11.51.05.png" alt=""><figcaption><p>Remote Server + Sonnet 4.5 + Open Targets Platform 25.12 data</p></figcaption></figure>

{% hint style="info" %}
The Platform documentation you are reading here is also available as an MCP in `https://platform-docs.opentargets.org/~gitbook/mcp`
{% endhint %}
