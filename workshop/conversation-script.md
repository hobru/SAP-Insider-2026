# 💬 Guided conversation: Sales Orders with MCP, then master data with A2A

[🏠 Welcome](../README.md) · [🗺️ Workshop map](tutorial.md) · [🎤 Presentation outline](presentation.md)

**Your route:** [1 · Getting started](module-1-getting-started.md) → [2 · Work IQ](module-2-work-iq.md) → [3 · MCP](module-3-mcp.md) → [4 · A2A](module-4-a2a.md) → **Guided conversation**

Use these prompts in one continuous Copilot Studio conversation. Do not start a new
conversation between turns: later prompts deliberately refer to results from earlier
turns.

The exact records depend on the GWSAMPLE data in the connected SAP system. When a
prompt says "the selected order," "that customer," or "that product," Copilot should
reuse the identifier from the preceding answers instead of asking the participant to
copy it manually.

## Part 1: Explore a Sales Order through MCP

### Turn 1

> Show me five sales orders. Include the sales order ID, customer or business partner
> ID, customer name, order date, net amount, gross amount, and currency where
> available.

**Purpose:** Establish a small result set and the identifiers used by later turns.

### Turn 2

> From those five orders, which order has the highest gross amount? Keep that as our
> selected order and explain briefly how you chose it.

**Purpose:** Test whether the agent can reason over the previous tool result without
fetching an unrelated order.

### Turn 3

> Get the full header details for the selected order. Do not ask me for its ID; reuse
> it from the previous answer.

**Purpose:** Demonstrate conversational context and a second MCP operation.

### Turn 4

> Now list all line items for the selected order. Include item number, product ID,
> quantity, unit, net amount, gross amount, and currency where available.

**Purpose:** Navigate from the Sales Order header to its items.

### Turn 5

> Which line item has the highest gross amount? Remember its product ID as the selected
> product and show the calculation.

**Purpose:** Reason over the returned line items and retain a Product identifier for
the A2A section.

## Part 2: Delegate customer questions to the A2A agent

### Turn 6

> Using the customer or business partner ID from the selected sales order, retrieve
> the full Business Partner details.

**Purpose:** Make the transition from an MCP tool to an A2A agent explicit while
carrying forward an identifier discovered through MCP.

### Turn 7

> For that same Business Partner, list its contact people with their names, titles,
> email addresses, and phone numbers.

**Purpose:** Test A2A context retention and the Business Partner contact skill.

### Turn 8

> Based on the available contact information, identify the best contact for a question
> about the selected order. If the data does not indicate responsibilities, say so and
> choose the first usable contact rather than inventing a role.

**Purpose:** Encourage grounded reasoning and discourage fabricated responsibilities.

## Part 3: Delegate product and supplier questions to the A2A agent

### Turn 9

> Retrieve the full details for the selected product from the highest-value line item.
> Reuse its product ID from earlier.

**Purpose:** Use the Product details skill with an identifier originally returned by
the Sales Order MCP tools.

### Turn 10

> What is the supplier ID for that product? Use it to retrieve the supplier's full
> Business Partner details.

**Purpose:** Follow the relationship from Product master data to Business Partner
master data.

### Turn 11

> List up to ten other products supplied by that same supplier. Include product ID,
> name, category, price, currency, and unit.

**Purpose:** Exercise the supplier-filtered Product catalog skill while retaining the
supplier ID from the previous answer.

### Turn 12

> Compare the selected product with the other products from that supplier. Is it the
> most expensive product in the returned list, and which products share its category?

**Purpose:** Reason over the A2A result without losing the selected Product context.

## Part 4: Combine the MCP and A2A context

### Turn 13

> Create a concise relationship summary for the selected sales order: order, customer,
> customer contact, highest-value line item, product, and supplier.

**Purpose:** Show how MCP tools and an A2A agent complement one another in one
conversation.

### Turn 14

> Finish with a short account briefing for a sales representative. Include the selected
> order value, the customer contact, the key product and supplier, and two sensible
> follow-up actions. Base the facts only on information already retrieved and clearly
> label any suggested action as a recommendation.

**Purpose:** Produce a useful business outcome while keeping retrieved facts separate
from generated recommendations.

## Facilitator notes

- If the MCP response omits a requested field, continue with the fields that are
  available rather than inserting a fixed identifier.
- If the chosen Sales Order has no line items or lacks a Business Partner ID, repeat
  Turn 1 with a larger result set and select a complete order.
- The transition at Turn 6 is intentional: Sales Orders remain MCP tools, while
  Business Partners and Products are delegated to the A2A agent.
- Watch whether Copilot passes identifiers between tools and the agent correctly. This
  is the main learning objective of the exercise.
- Do not paste credentials, access tokens, or destination details into the
  conversation.

---

## 🧭 Where to next?

**Revisit the lab:** [← Module 4 · A2A](module-4-a2a.md)

[🏠 Welcome](../README.md) · [🗺️ All modules](tutorial.md) · [⬆️ Back to top](#)
