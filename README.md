# CheckFitment MCP server

Answers whether a wheel and tire will fit a vehicle. It looks up bolt pattern, center bore, thread size, lug nut torque and OEM wheel and tire sizes by make, model and year, each marked verified or unverified with its manufacturer sources, and reports vehicles that are not in the dataset as not found instead of guessing. Five calculators cover wheel offset and backspacing, tire size changes and speedometer error, wheel spacers and stud engagement, gear ratio after a tire change, and bolt pattern conversion.

- **Website:** [checkfitment.com](https://checkfitment.com)
- **Documentation:** [checkfitment.com/ai-assistants/](https://checkfitment.com/ai-assistants/)
- **Endpoint:** `https://checkfitment.com/mcp` (MCP Streamable HTTP, public, no authentication, no API key)

## Tools

- `bolt_pattern_lookup`: wheel specs by vehicle
- `wheel_fitment_check`: old vs new wheel and tire (poke, inner clearance, backspacing)
- `tire_size_compare`: diameter change and speedometer error
- `wheel_spacer_calculator`: spacer size and stud engagement
- `gear_ratio_calculator`: effective ratio and regear target
- `bolt_pattern_facts`: mm/inch conversion and look-alike patterns

All tools are read-only and stateless. The server stores nothing it receives.

## Connect

Any MCP client that supports remote servers:

```json
{
  "mcpServers": {
    "checkfitment": {
      "type": "streamable-http",
      "url": "https://checkfitment.com/mcp?src=mcp"
    }
  }
}
```

Quick test:

```bash
curl -s -X POST 'https://checkfitment.com/mcp?src=mcp' -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

This repository holds the listing metadata only. The server itself is a hosted service run by the CheckFitment website (https://checkfitment.com); see the documentation link above for privacy and terms.
